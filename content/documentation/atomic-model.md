+++
date = "2016-12-16T12:32:04+01:00"
topics = ["documentation"]
tags = ["vle-2.0", "c++", "atomic-model"]
title = "Atomic model"
+++


VLE implements the DEVS abstract simulators and more precisely the DSDE which
merge Parallel DEVS and DS-DEVS.

In VLE, a DEVS atomic model is represented as a object which inherits of the
`vle::devs::Dynamics` [C++
class](https://github.com/vle-forge/vle/blob/master/src/vle/devs/Dynamics.hpp).

```c++
class MyModel : public vle::devs::Dynamics
{
public:
MyModel(const DynamicsInit& init, const vle::devs::InitEventList&  events)
    : vle::devs::Dynamics(init, events)
{}

~MyModel() override = default;

// Process the initialization of the model by
// initializing the initial state and return
// the duration (or timeAdvance) of the initial
// state.
vle::devs::Time
init(vle::devs::Time time) override
{}

// Process the output function: compute the output function.
void
output(vle::devs::Time time,
       vle::devs::ExternalEventList& output) const override
{}

// Process the time advance function: compute the duration
// of the current state.
vle::devs::Time
timeAdvance() const override
{}

// Process an internal transition: compute the new
// state of the model with the internal transition function.
void
internalTransition(vle::devs::Time time) override
{}

// Process an external transition: compute the new state
// of the model when an external event occurs.
void
externalTransition(const vle::devs::ExternalEventList& events,
                   vle::devs::Time time) override
{}

// Process the confluent transition, by default,
// confluentTransitions call internalTransition and
// externalTransition but this function can be overridden
// to develop its own dynamics.
virtual void
confluentTransitions(vle::devs::Time time,
                     const vle::devs::ExternalEventList& events) override
{}

// Process an observation event: compute the current state
// of the model at a specified time and for a specified port
std::unique_ptr<vle::value::Value>
observation(const vle::devs::ObservationEvent& event) const override
{}

// When the simulation of the atomic model is finished,
// the finish method is invoked
void finish() override
{}

}; // End of class definition

// Finally, this macro enables the link between VLE, the shared library
// produced by C++ compiler and your model.
DECLARE_DYNAMICS(MyModel);
```
