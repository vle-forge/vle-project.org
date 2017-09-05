+++
date = "2016-12-16T12:32:04+01:00"
topics = ["exmaple"]
tags = ["vle-2.0", "examples", "atomic-model", "counter"]
title = "counter"
+++

A simple model that counts events received in any input port.

First, we create a new package with the following command:

```bash
mkdir -p cd $HOME/vle/tutorial
cd $HOME/vle/tutorial
vle-2.0 -P examples create
```

We add the file `counter.cpp` and update the `CMakeLists.txt` file in the `src`
directory.

```C++
#include <vle/devs/Dynamics.hpp>
#include <vle/value/Double.hpp>

namespace example {

class Counter : public vle::devs::Dynamics
{
public:
    Counter(const vle::devs::DynamicsInit& model,
            const vle::devs::InitEventList& events)
        : vle::devs::Dynamics(model, events)
        , m_counter(0),
    {}

    ~Counter() = default;

    vle::devs::Time init(vle::devs::Time& time) override
    {
        return 0;
    }

    vle::devs::Time
    timeAdvance() const override
    {
        return vle::devs::infinity;
    }

    void
    externalTransition(const vle::devs::ExternalEventList& events,
                       vle::devs::Time time) override
    {
        m_counter += events.size();
    }

    std::unique_ptr<vle::value::Value>
    observation(const vle::devs::ObservationEvent& event) const override
    {
        return new vle::value::Double(m_counter);
    }

private:
    std::size_t m_counter;
};

} // namespace vle examples counter

DECLARE_DYNAMICS(vle::example::Counter)
```

Then build the package:

```bash
vle-2.0 -P example configure build
```
