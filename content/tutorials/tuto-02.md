+++
categories = ["tutorials", "c++"]
date = "2015-11-11T21:13:05+01:00"
description = ""
keywords = ["devs", "atomic", "model", "lotka-volterra", "conditions"]
title = "tuto 02"
+++

In this tutorial, we create a Lotka-Volterra system solved with Euler. The first
part shows you how to develop a such model then we use the experimental
conditions to assign value from the VPZ and use it directly from R.

### First, we develop the model

```
vle -P lotka-volterra create
```

Rename the `lotka-volterra/src/Simple.cpp` into `SystemLotkaVolterra.cpp` for
example and edit the source code like this:

```c++
#include <vle/value/Value.hpp>
#include <vle/devs/Dynamics.hpp>

namespace vd = vle::devs;
namespace vv = vle::value;

namespace examples {

class SystemLotkaVolterra : public vd::Dynamics
{
    double X, Y;
    double alpha, beta, gamma, delta;
    double step;

public:
    SystemLotkaVolterra(const vd::DynamicsInit& init,
            const vd::InitEventList& events)
        : vd::Dynamics(init, events)
    {
        X = 1.;
        Y = 1.;

        alpha = 5.2;   // Reproduction rate of prey
        beta = 3.4;    // Mortality rate of predator per prey
        gamma = 2.1;   // Mortality rate of predator
        delta = 1.4;   // Reproduction rate of predator per prey
        step = 0.00001;// Euler integration
    }

    virtual ~SystemLotkaVolterra()
    {}

    virtual vd::Time init(const vd::Time& /*time*/)
    {
        return 0.0;
    }

    virtual vd::Time timeAdvance() const
    {
        return step;
    }

    virtual void internalTransition(const vd::Time& /*time*/)
    {
        double dxdt = ((X * alpha) - (beta * X * Y));
        double dydt = (- (gamma * Y) + (delta * X * Y));
    
        X += step * dxdt;
        Y += step * dydt;
    }

    virtual vv::Value* observation(
            const vd::ObservationEvent& event) const
    {
        if (event.onPort("X"))
            return new vle::value::Double(X);
        else if (event.onPort("Y"))
            return new vle::value::Double(Y);
        else
            return vle::devs::Dynamics::observation(event);
    }
};

} // namespace vle example

DECLARE_DYNAMICS(examples::SystemLotkaVolterra)
```

Do not forget to update the `CMakeLists.txt` in the source directory. Replace
the `Simple.cpp` with `SystemLotkaVolterra.cpp`:

```
DeclareDevsDynamics(SystemLotkaVolterra "SystemLotkaVolterra.cpp")
```

Finally, try to compile the package with the command line interface:

```
vle -P lotka-volterra configure build
```

As in the first tutorial, we need to add a new simulation file to assign the
structure of the model and observation of the *X* and *Y* variables in the
model. First, start GVLE and open the *LotkaVolterra* package.

{{< figure src="/tutorials/images/tuto-02-00.png" caption="This is the default GVLE window at start-up." >}}

{{< figure src="/tutorials/images/tuto-02-01.png" caption="Open the VoltaVolterra package in menu file/open project." >}}

{{< figure src="/tutorials/images/tuto-02-02.png" caption="Open the exp/Empty.vpz file and add a atomic model with the add model button." >}}

{{< figure src="/tutorials/images/tuto-02-03.png" caption="Normally, the structure of the model have only one model with no input/output port." >}}

{{< figure src="/tutorials/images/tuto-02-04.png" caption="Attach a the dynamics to the model. Use the select tool, double-click on the atomic model you have created previously, go to the Dynamics tab and right click to add a new Dynamics." >}}

{{< figure src="/tutorials/images/tuto-02-05.png" caption="Do not forget to attach the Dynamics to the model." >}}

{{< figure src="/tutorials/images/tuto-02-06.png" caption="To get result of the simulation, we need to attach a View to the observation function on the observable X and Y (see the observation function in the model. So, select the View menu and create the view with a right button click and the add menu, then select a time step and use the File plug-in." >}}

{{< figure src="/tutorials/images/tuto-02-07.png" caption="The use the select button to select the model, double click, select the observable menu, add a new observables, edit this observable (right click), add two observable X and Y, then attach the view to this observable." >}}

{{< figure src="/tutorials/images/tuto-02-08.png" caption="Select the Experiment menu to change the simulation duration." >}}

{{< figure src="/tutorials/images/tuto-02-09.png" caption="Start the simulation with the Launch Simulation menu." >}}

{{< figure src="/tutorials/images/tuto-02-10.png" caption="The result of the simulation is a file in the output directory of the package." >}}

### Experimental condition

Now, we update the source code to use the experimental conditions to easily
update the parameter *alpĥa*, *beta*, *gamma* and *delta* and the initial states
of the variables *X* and *Y*.

We use the `vle::devs::InitEventLists` in the constructor of the model to get a
list of initialization list.

First, edit the source code of the model. See the constructor:

```c++
#include <vle/value/Value.hpp>
#include <vle/devs/Dynamics.hpp>

namespace vd = vle::devs;
namespace vv = vle::value;

namespace examples {

class SystemLotkaVolterra : public vd::Dynamics
{
    double X, Y;
    double alpha, beta, gamma, delta;
    double step;

public:
    SystemLotkaVolterra(const vd::DynamicsInit& init,
            const vd::InitEventList& events)
        : vd::Dynamics(init, events)
    {
        // If an experimental condition called X0 exist,
        // we transform the value into a double and
        // we assign this value to X. Otherwise we
        // use a default value equal to 10.
        if (events.exist("X0"))
            X = events.getDouble("X0");
        else
            X = 10.;

        // The same behaviour for Y0.
        if (events.exist("Y0"))
            Y = events.getDouble("Y0");
        else
            Y = 10.;

        // The experimental condition alpha, beta, gamma
        // and delta must exist in the experimental
        // conditions.
        alpha = events.getDouble("alpha");
        beta = events.getDouble("beta");
        gamma = events.getDouble("gamma");
        delta = events.getDouble("delta");

        step = 0.00001;
    }

    virtual ~SystemLotkaVolterra()
    {}

    virtual vd::Time init(const vd::Time& /*time*/)
    {
        return 0.0;
    }

    virtual vd::Time timeAdvance() const
    {
        return step;
    }

    virtual void internalTransition(const vd::Time& /*time*/)
    {
        double dxdt = ((X * alpha) - (beta * X * Y));
        double dydt = (- (gamma * Y) + (delta * X * Y));
    
        X += step * dxdt;
        Y += step * dydt;
    }

    virtual vv::Value* observation(const vd::ObservationEvent& event) const
    {
        if (event.onPort("X"))
            return new vle::value::Double(X);
        else if (event.onPort("Y"))
            return new vle::value::Double(Y);
        else
            return vle::devs::Dynamics::observation(event);
    }
};

} // namespace vle example

DECLARE_DYNAMICS(examples::SystemLotkaVolterra)
```

In GVLE, use the *Conditions* sub-menu in the *Simulation* menu.

{{< figure src="/tutorials/images/tuto-02-11.png" caption="The conditions dialogue box." >}}

{{< figure src="/tutorials/images/tuto-02-12.png" caption="Add a new condition and fill it with value. Use the right click to create condition, parameter and value." >}}

{{< figure src="/tutorials/images/tuto-02-13.png" caption="Select the atomic model, switch to the conditions tabulation and select the previous created conditions and attach is to the atomic model." >}}

{{< figure src="/tutorials/images/tuto-02-14.png" caption="You can rerun the simulation." >}}

### RVLE

First change the View plug-in into the View dialogue box and select the plug-in
called *storage*. This plug-in allows simulation results to be send to R or
Python.

{{< figure src="/tutorials/images/tuto-02-15.png" caption="Here, update the output plug-in from File to Storage." >}}

Install RVLE and run the following commands:

```R
# import the rvle package
library(rvle)

# open the file 'empty.vpz' from the 'lokta-volterra' package
f = rvle.open("empty.vpz", "lotka-volterra")

# show the conditions available
rvle.listConditions(f)

# show the parameters from the previous conditions
rvle.listConditionPorts(f, "GeneralConditions")

# update the value of the parameter 'X0' in the GeneralConditions
rvle.setRealCondition(f, "GeneralConditions", "X0", 2.0)

# run the simulation and get results into the result variables
result = rvle.run(f)

# some process on result

result = rvle.setRealCondition(f, "GeneralConditions", "X0", 3.0)
result = rvle.run(f)
```

The `help(rvle)` command give you some informations. Type the tabulation key on
your keyboard after `rvle.[tab]` give you the complete list of functions
available in rvle. Use `help(rvle.[COMMAND])` to see help.