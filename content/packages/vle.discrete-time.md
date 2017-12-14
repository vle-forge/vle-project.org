+++
tags = ["discrete time"]
topics = ["packages", "extension"]
description = "To build discrete time models"
date = "2016-12-01T12:48:00+01:00"
title = "vle.discrete-time"
+++

# Introduction <a name="Introduction"></a>

The vle extension **vle.discrete-time** can be used to model and simulate
discrete time atomic models into VLE. Discrete time atomic models are models
that compute at time _t_ outputs of variables _v1, ..., vn_ taking into account
values of variables _v1,..., vn_, given a user specified parameter _D_, at times

_t, t - D, t - 2 * D,..._,

The packages related to this extension are:

* **vle.discrete-time** provides the discrete time extension
 itself.
* **vle.discrete-time.decision** provides a decision agent having
 a discrete time dynamic. It embeds a _KnowledgeBase_ from package
 **vle.extension.decision**. This is an experimental package.
* **vle.discrete-time_test** provides tests for discrete time
models.

Evolution of state variables _vi_ is described by C++ equation syntax close to
mathematical formulation. These expressions must be written in the
_compute_ function.

For example the expression _V1 = V1(-1) + V2() + V3(-2)_ computes, at current
time _t_, the value of _V1_ as the sum of the value of _V1_ at time
_t - D_, the current value of _V2_ and the value of _V3_ at time
_t - 2*D_.

{{% fluid_img src="../userInterfaceDiscreteTime.png" caption="Behavior of temporal structures into discrete time models" %}}

**Fig:** A discrete-time atomic model with 6 variables, 3 can be
updated from external event (inputs), 3 are sent by default at each time step
on the network (outputs)

The interface (input and output ports) is given for an example in the above
figure. Note that variables _v1, ..., v3_ are not necessary
inputs they could also be outputs. And variables _v4, ..., v6_ could also
have their input ports.

# Writing atomic models <a name="WritingAtomicModels"></a>

The _vle/discrete-time/TemporalValues.hpp_ API provides functionnalities
to handle variables (double, vector or polymorphic _vle::value_) and their
history. Particularly, access operators are defined for these data structures.
Available variables types are :

* double. To use a temporal value of type double, you must use the struct
  _vle::discrete\_time::Var_ (see examples below).
* vector of double. To use a temporal value of type vector of double,
    you must use the struct _vle::discrete\_time::Vect_.
* _vle::value::Value_: To use a temporal value of this type
 you must use the struct _vle::discrete\_time::ValueVle_.

Temporal values maintain an historic of updates with dates and
are browseable using access operator. Updates can be directly set
by a _devs::Dynamic_ if the temporal value is declared
(in constructor or not) using the function _Var::init_,
_Vect::init_ or _ValueVle::init_ (see lines 13, 14 in code).

{{% fluid_img src="../temporal_values.png"  caption="Behavior of temporal structures into discrete time models" %}}

**Fig:** Example of updates for a temporal value of type _Var_.

In example depicted in the above figure, at current time _t_, the state
of historic of _Var_ _S_ is:

 _[t1, a1],[t2, a3],[t3, a2],[t4, a1]_.

Operator _()_ on _S_ will give one of the update value. The signal is
supposed to be piecewise constant function. Then

* _S(-0.3)_ returns value at time _t - 0.3 * D_, ie _a1_.
* _S(-3.6)_ returns value at time _t - 3.6 * D_, ie _a3_.
* _S()_ returns last update value, ie _a1_.

Operator _=_ of _Var_ allows to set an update
(for example into the _compute_ function of discrete-time model).

For Vectors (struct _Vect_):

* _S\[1\](-0.3)_ returns value at time _t - 0.3 * D_ for the
  dimension 1.
* _S\[0\](-3.6)_ returns value at time _t - 3.6 * D_
  for the dimension 0.
* _S\[2\]()_ returns last update vector at index 2.
* _S\[2\]=1.5_ updates value of _S_ at dim 2 with 1.5.

Below is given an example of dynamic for an atomic model that relies
on the extension **vle.discrete-time**.

````c++
class MyModel : public DiscreteTimeDyn
{
public:
  //Declaration of variables
  Var x;
  Vect y;
  Var z; // used in this module as an input
  MyModel(const vd::DynamicsInit& model, const vd::InitEventList& events) :
            DiscreteTimeDyn(model, events)
  {
    //Initialisation of variables from experimental conditions
    x.init(this, "x", events);
    y.init(this, "y", events);
    //Overwrite initialisations (Optionnal)
    x.init_value(3.0);
    x.history_size(3);
    y.dim(2)
  }
  void compute(const vd::Time& /*time*/)
  {
    x =  x(-1) - y[1]() / z();
    y[0] = z() - 1;
    y[1] = y[0]() + 1;
  }
};
````

# Configuring atomic models <a name="ConfiguringAtomicModels"></a>

To configure discrete time atomic models, one can use the parameters from the
_vpz_ conditions listed below. The *X* refers to an internal variable
(a real, a vector or a vle value).

Basic settings:

* **time_step** (double, default 1.0) : the time step of the discrete time
  atomic model.
* **dim_X** (int, default 2) : if *X* is a vector, it defines
  the dimension of the vector. Used only if *X* is a vector.
* **history_size_X** (uint, default 1) : it gives the size of the
  history of internal variable *X*.
* **init_value_X** (vle::Value, default vle::Double(0.0)) :
  the initial value of the internal variable *X*. It can be a vv::Double for a
  variable without history, a vv::Tuple for a variable with history or a
  vv::Table for a vector. Checks are performed with *dim_X* and
  *history_size_X*.
* **syncs** (set of strings, default empty): each variable into this set are
  parameterized with a value of 1 for sync parameter.
* **sync_X** (uint, default 0): if *sync_X* > 0, the value of
  *X* at times n * *sync_X* * *time_step*, with n > 0 is
  expected to be provided by an external event before calling the *compute*
  function. This option has priority on *syncs*.

Advanced settings for output configurations:

* **output_period** (uint, default 1): gives the time step of output.
  Output will produce values each *time_step* * *output_period*.
* **output_period_X** (uint, default 1): a specific value of *output_period*
  for variable *X*. This option has priority on *output_period*.
* **output_nil** (bool, default false): if true, the output function will
  produce a Null value for a variable which last update is not equals to
  current time, otherwise it will gives the last updated value.
* **output_nil_X** (bool, default false): a specific value of *output_nil*
  for variable *X*. This option has priority on *output_nil*.
* **output_init** (bool, default false): if true, output is performed at
  time of initialisation.

Advanced settings for debugging:

* **snapshot_before** (bool, default false) : if true, a snapshot of variable
  values is done before the compute function. It can be observed on the
  port *X_before*.
* **snapshot_after** (bool, default false) : if true, a snapshot of variable
  values is done after the compute function. It can be observed on the
  port *X_after*.
* **error_no_sync_X** (bool, default false) : if true, the
  access to *X* at the current time _X()_ will send an error if the
  last time of update of *X* is before the current time.

Advanced settings for multiple update:

* **allow_update_X** (bool, default false): if false, the first
  value set for *X* at a given time step is kept. The following updates for
  *X* at this time step are ignored.
* **forcing_X** (a vle Map or Set, default empty): this option can not be used
 simultaneously with *allow_update*. The map (or set of such map)
 represents a forcing event. A forcing event forces the model to set a value
 to *X* at a given time. The map should contain:
  * **time** (double): the time of forcing event
  * **value** (real, vector or vle Value): the value of forcing event
  * **before_output** (bool, default false): true if the forcing event
    should occur before the output function of the dynamic.

Advanced settings for dynamic management of variables (this configuration can
be dynamically set by an external event on port *dyn_init* with a map):

* **dyn_allow** (bool, default false): if true, input and output ports added
  for example by an executive are automatically added as state variables after
  the_compute_ function.
* **dyn_type** ('Var', 'Vect' or 'ValueVle', default 'Var'): gives the type
  of new state variables to add. Used only if  *dyn_allow* is true.
* **dyn_sync** (uint, default 0): gives the type of synchronisation of new state
  variables to add as with *sync_X*. Used only if *dyn_allow* is true.
* **dyn_init_value** (vle::Value, default vle::Double(0.0)): gives the initial
  value of new variables as with *init_value_X*. Used only if  *dyn_allow* is
  true.
* **dyn_dim** (uint, default 2): gives the dimension when creating a new _Vect_.
   Used only if *dyn_allow* is equal to true and *dyn_type* == _Vect_.
* **dyn_denys** (set of strings, default empty): port names into this set are
  not added as state variables, even if dynamic managment is allowed.
* **dyn_allow_X** (bool, default true): if *sync_X* is true, if the port
  named X exist, a variable of the name X can be added dynamically.
  If *sync_X* is false, the port named X is not considered for dynamic
  managment of variables. This option has priority on *dyn_denys*.


Advanced settings for synchronisation:

* **bags_to_eat** (int, default 0) : the number of bags to wait before
  computing the values of variables (calls of _compute_ user function).


# Technical details <a name="TechnicalDetails"></a>

{{% fluid_img src="../dt_activity_diagram.png" caption="Diagram activity of discrete time models" %}}

**Fig:** The activity diagram of a discrete time model: sequence of calls at
a given time step.

{{% fluid_img src="../DEVS_states.png" caption="DEVS state of disctrete time models" %}}

**Fig:** The DEVS state transition graph  for discrete-time atomic models.


This extension is intended to improve the functionnalities of extension
**vle.extension.difference-equation**, to improve perfomance results and to
limit the behavior in order to facilitate the coupling with other extensions :

* there is no propagation of the perturbation :
  it requires a state backup and other extensions do not have this.
* there is no initialization process of the dynamics (no _initValue_
  function): synchronisation at the time of instantiation of the atomic model
  makes it difficult to couple with DSDEVS.
* there is no external variables. All variables are internal variables.
* it provides vector of variables and polymorphic vle values.
* It uses a DEVS state approah for the code of transitions
