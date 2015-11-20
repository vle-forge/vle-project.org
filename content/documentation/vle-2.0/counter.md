+++
categories = ["vle-2.0", "documentation", "c++", "atomic-model"]
date = "2015-11-20T13:04:38+01:00"
description = ""
keywords = []
title = "VLE-2.0: Counter-Generator model"
+++

```c++
#include <vle/dsde/generic.hpp>
#include <vle/dsde/dsde-debug.hpp>

typedef vle::DoubleTime MyTime;
typedef vle::PortList <std::string> MyPort;
typedef vle::dsde::Engine <MyTime> MyDSDE;

using AtomicModel = vle::dsde::AtomicModel <MyTime, MyPort, MyPort>;
using GenericCoupledModel = vle::dsde::GenericCoupledModel <MyTime,
      vle::dsde::TransitionPolicyThread <MyTime>>;
using CoupledModelThread = vle::dsde::CoupledModel <MyTime, MyPort, MyPort,
      MyPort, MyPort,
      vle::dsde::TransitionPolicyThread <MyTime>>;
using CoupledModelMono = vle::dsde::CoupledModel <MyTime, MyPort, MyPort,
      MyPort, MyPort,
      vle::dsde::TransitionPolicyDefault <MyTime>>;

struct Counter : AtomicModel {
    int i;

    Counter(const vle::Context &ctx)
        : AtomicModel(ctx, 1u, 0u), i(0)
    {}

    Counter(const Counter &other)
        : AtomicModel(other), i(other.i)
    {}

    virtual ~Counter()
    {}

    virtual double init(const vle::Common &, const double &) override final
    {
        i = 0;
        return MyTime::infinity();
    }

    virtual double delta(const double &, const double &,
                         const double &) override final
    {
        ctx->dbg() << "Counter make a delta with " << x[0].size()
                   << " message(s) so, number of received message is "
                   << i << "\n";
        i += x[0].size();
        return MyTime::infinity();
    }

    virtual void lambda() const override final
    {}

    virtual std::string observation() const
    {
        return std::to_string(i);
    }
};

struct Generator : AtomicModel {
    unsigned int timestep;
    int i;
    std::mt19937 prng;
    std::normal_distribution < double > dist;

    Generator(const vle::Context &ctx)
        : AtomicModel(ctx, 0u, 1u)
        , timestep(1), i(0), prng(1234), dist(0., 5.)
    {}

    Generator(const vle::Context &ctx, unsigned int timestep)
        : AtomicModel(ctx, 0u, 1u)
        , timestep(timestep), i(0), prng(1234), dist(0., 5.)
    {}

    Generator(const Generator &other)
        : AtomicModel(other)
        , timestep(other.timestep), i(other.i)
        , prng(other.prng), dist(other.dist)
    {}

    virtual ~Generator()
    {}

    virtual double init(const vle::Common &, const double &) override final
    {
        return timestep; // return std::abs(dist(prng));
    }

    virtual double delta(const double &, const double &,
                         const double &) override final
    {
        ctx->dbg() << "Generator " << this << " delta\n";
        i++;
        return timestep; // return std::abs(dist(prng));
    }

    virtual void lambda() const override final
    {
        ctx->dbg() << "Generator lambda " << this
                   << " sends two messages\n";
        y[0] = { std::string("msg"), std::string("msg2") };
    }

    virtual std::string observation() const
    {
        return std::to_string(i);
    }
};

template <typename Parent>
struct MyNetwork : Parent {
    Generator gen1, gen2;
    Counter cpt;

    MyNetwork(const vle::Context &ctx) :
        Parent(ctx), gen1(ctx), gen2(ctx), cpt(ctx)
    {}

    MyNetwork(const vle::Context &ctx, unsigned int timestep1,
              unsigned int timestep2)
        : Parent(ctx), gen1(ctx, timestep1), gen2(ctx, timestep2), cpt(ctx)
    {}

    virtual typename Parent::children_t children(const vle::Common &) override final
    {
        return {&gen1, &gen2, &cpt};
    }

    virtual std::string observation() const
    {
        std::string ret = cpt.observation() + " " + gen1.observation() + " " +
                          gen2.observation();
        return ret;
    }

    virtual void post(const typename Parent::UpdatedPort &out,
                      typename Parent::UpdatedPort &in) const override final
    {
        assert(Parent::heap.size() == 3);

        if (out.count(&gen1) + out.count(&gen2) > 0) {
            in.emplace(&cpt);
            cpt.x[0].insert(cpt.x[0].begin(),
                            gen1.y[0].begin(),
                            gen1.y[0].end());
            cpt.x[0].insert(cpt.x[0].end(),
                            gen2.y[0].begin(),
                            gen2.y[0].end());
        }
    }
};

int main(int argc, char **argv)
{
    (void)argc;
    (void)argv;

    vle::Context ctx = std::make_shared <vle::ContextImpl>();
    MyDSDE dsde_engine;
    MyNetwork <CoupledModelMono> model(ctx);
    vle::SimulationDbg <MyDSDE> sim(ctx, dsde_engine);
    double final_date = sim.run(model, 0.0, 10);
    std::string result = model.observation();
}
```
