+++
categories = ["tutorials", "c++"]
date = "2015-09-28T12:03:41+02:00"
description = ""
keywords = ["devs", "atomic", "model", "counter", "generator"]
title = "tuto 01"
+++

In this first example, we will create simulation of two models: an event
generator and a event counter. First, we need to create a new empty package in
the user home directory.

````bash
cd $HOME/examples
vle-1.1 -P generator-counter create
vle-1.1 -P generator-counter configure build
````
The binary package is now installed into the VLE's home (`$VLE_HOME/pkgs-1.1` or
`$HOME/.vle/pkgs-1.1`).

Now, we need to add two DEVS models, the *counter* and the *generator*. Copy the
file *Simple.cpp* in the `$HOME/examples/generator-counter` into new files
*Counter.cpp* and *Generator.cpp*:

````bash
cd $HOME/examples/generator-counter/src
cp Simple.cpp Counter.cpp
cp Simple.cpp Generator.cpp
````

Update the content of these files with the following content. First, the
*Counter*" model:

````c++
#include <vle/value/Value.hpp>
#include <vle/devs/Dynamics.hpp>

namespace vd = vle::devs;
namespace vv = vle::value;

namespace examples {

class Counter : public vd::Dynamics
{
    int m_number;

public:
    Counter(const vd::DynamicsInit& init, const vd::InitEventList& events)
        : vd::Dynamics(init, events)
    {}

    virtual ~Counter()
    {}

    virtual vd::Time init(const vd::Time& /*time*/)
    {
        m_number = 0;
        return vd::infinity;
    }

    virtual void output(const vd::Time& /*time*/,
    vd::ExternalEventList& /*output*/) const
    {}

    virtual vd::Time timeAdvance() const
    {
        return vd::infinity;
    }

    virtual void internalTransition(const vd::Time& /*time*/)
    {}

    virtual void externalTransition(
        const vd::ExternalEventList& /*event*/,
        const vd::Time& /*time*/)
    {
        m_number++;
    }

    virtual void confluentTransitions(const vd::Time& time,
        const vd::ExternalEventList& events)
    {
        internalTransition(time);
        externalTransition(events, time);
    }

    virtual vv::Value* observation(
        const vd::ObservationEvent& /*event*/) const
    {
        return new vle::value::Integer(m_number);
    }

    virtual void finish()
    {}
};

} // namespace vle examples

DECLARE_DYNAMICS(examples::Counter)
````

And for the *Generator* model:

````c++
#include <vle/value/Value.hpp>
#include <vle/devs/Dynamics.hpp>

namespace vd = vle::devs;
namespace vv = vle::value;

namespace examples {

class Generator : public vd::Dynamics
{
    public:
    Generator(const vd::DynamicsInit& init,
        const vd::InitEventList& events)
    : vd::Dynamics(init, events)
    {}

    virtual ~Generator()
    {}

    virtual vd::Time init(const vd::Time& /*time*/)
    {
        return 0.1;
    }

    virtual void output(const vd::Time& /*time*/,
    vd::ExternalEventList& output) const
    {
        output.push_back(new vle::devs::ExternalEvent("out"));
    }

    virtual vd::Time timeAdvance() const
    {
        return 0.1;
    }

    virtual void internalTransition(const vd::Time& /*time*/)
    {}

    virtual void externalTransition(
        const vd::ExternalEventList& /*event*/,
        const vd::Time& /*time*/)
    {}

    virtual void confluentTransitions(const vd::Time& time,
        const vd::ExternalEventList& events)
    {
        internalTransition(time);
        externalTransition(events, time);
    }

    virtual vv::Value* observation(
        const vd::ObservationEvent& /*event*/) const
    {
        return 0;
    }

    virtual void finish()
    {}
};

} // namespace vle examples

DECLARE_DYNAMICS(examples::Generator)
````

We also need to update the `CMakeLists.txt` file and adding the new to compile
our new model. So update the `src/CMakeLists.txt` file and add the lines:

````
DeclareDevsDynamics(Counter "Counter.cpp")
DeclareDevsDynamics(Generator "Generator.cpp")
````

Check the compilation of your model:

````bash
cd $HOME/examples
vle-1.1 -P generator-counter configure build
````

Now we need to add a new simulation file to assign the structure of the model
(*counter* coupled with *generator*) and observation of the *counter*. First,
start GVLE and open the *counter-generator* package.

{{< figure src="/tutorials/images/tuto-00.png" caption="This is the default GVLE window at startup" >}}

{{< figure src="/tutorials/images/tuto-01.png" caption="Use the `file/open project` menu to open the select package dialog box" >}}

{{< figure src="/tutorials/images/tuto-02.png" caption="Open the empty.vpz file from the exp directory" >}}

{{< figure src="/tutorials/images/tuto-03.png" caption="Select the add model button and adds two models" >}}

{{< figure src="/tutorials/images/tuto-04.png" caption="Assign a name to the output (out) and input (in) ports and make the connection" >}}

{{< figure src="/tutorials/images/tuto-05.png" caption="Coupling between A and B must be draw" >}}

{{< figure src="/tutorials/images/tuto-06.png" caption="Add a new dynamics to the atomic dialog box with the right button." >}}

{{< figure src="/tutorials/images/tuto-07.png" caption="In the dynamics dialog box, select the Counter library (generated from the Counter.cpp file)" >}}

{{< figure src="/tutorials/images/tuto-08.png" caption="Finally select the Generator dynamics to the model A and do the same for the second model but with the Counter library" >}}

{{< figure src="/tutorials/images/tuto-09.png" caption="Add a new view into the view dialog box. Set the view type to time-step 1.0. Each time-step, the view call the observation function of all observable (all atomic model with the specified observable" >}}

{{< figure src="/tutorials/images/tuto-10.png" caption="Add an observable to the model B and edit it with the right click" >}}

{{< figure src="/tutorials/images/tuto-11.png" caption="Append the default view to the current observable" >}}

{{< figure src="/tutorials/images/tuto-12.png" caption="Start the experiment dialog box from the menu" >}}

{{< figure src="/tutorials/images/tuto-13.png" caption="In the experiment dialog box, increase the simulation's duration to 100.0" >}}

{{< figure src="/tutorials/images/tuto-14.png" caption="Finally, run the simulation into the simulation dialog box." >}}

Finally, to get results, show the directory `test_default.dat` in the `output`
directory under GVLE. If you launch the simulation from GVLE, output are stored
into the `output` directory in the source directory. If you run the simulation
from the command line, the output directory is the current path. To run in
command line:

````bash
vle-1.1 -P generator-counter empty.vpz
````
