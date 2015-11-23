+++
categories = ["documentation", "c++", "atomic-model"]
date = "2015-09-17T12:48:30+02:00"
description = ""
keywords = ["devs", "atomic", "model"]
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
MyModel(const DynamicsInit& init,
	const vle::devs::InitEventList&  events)
    : vle::devs::Dynamics(init, events)
{}

virtual ~MyModel()
{}

// Process the initialization of the model by
// initializing the initial state and return
// the duration (or timeAdvance) of the initial
// state.
virtual vle::devs::Time init(
	    const vle::devs::Time& time)
{}


// Process the output function: compute the output function.
virtual void output(
	    const vle::devs::Time& time,
	    vle::devs::ExternalEventList& output) const
{}

// Process the time advance function: compute the duration
// of the current state.
virtual vle::devs::Time timeAdvance() const
{}

// Process an internal transition: compute the new
// state of the model with the internal transition function.
virtual void internalTransition(
	    const vle::devs::Time& time)
{}

// Process an external transition: compute the new state
// of the model when an external event occurs.
virtual void externalTransition(
	    const vle::devs::ExternalEventList& events,
	    const vle::devs::Time& time)
{}

// Process the confluent transition, by default,
// confluentTransitions call internalTransition and
// externalTransition but this function can be overidden
// to develop its own dynamics.
virtual void confluentTransitions(
	    const vle::devs::Time& time,
	    const vle::devs::ExternalEventList& extEventlist)
{}

// Process an observation event: compute the current state
// of the model at a specified time and for a specified port
virtual vle::value::Value* observation(
	const vle::devs::ObservationEvent& event) const
{}

// When the simulation of the atomic model is finished,
// the finish method is invoked
virtual void finish()
{}
};

// Enable the link between VLE and your model.
DECLARE_DYNAMICS(MyModel);
```
