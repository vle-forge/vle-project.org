+++
tags = ["ode"]
topics = ["packages", "extension"]
description = "To build Ordinary Differential Equations models (ODE)"
date = "2016-12-01T12:48:00+01:00"
title = "vle.ode"
+++

# Table of Contents

1. [Introduction](#Introduction)
2. [Writing ODE atomic models](#WritingAtomicModels)
3. [Configuring ODE atomic models](#ConfiguringAtomicModels)
4. [Technical details](#TechnicalDetails)

# Introduction <a name="Introduction"></a>

The vle extension **vle.ode** allow to model and simulate ordinary 
differential equations (ode) into VLE. It provides three numerical methods 
for integration of ode:

* Euler: referred below as a time slicing method
* Runge-Kutta 4: referred below as a time slicing method
* QSS2: quantized state systems of order 2; the implementation is the one proposed
by Kofman in 'A Second Order Approximation for DEVS Simulation of Continuous 
Systems' (Simulation, 2002).

{{% fluid_img src="../vle_ode_userInterface.png" caption="User interface of ODE models" %}}

**Fig:** The user interface of an atomic model of type ODE.

Evolution of state variables _Vi_ is described by differential equations. 
These expressions can rely on the value of external variables _Ei_.
For time slicing methods, external variables _Ei_  are expected to be
piecewise constant functions computed from continuous and derivable functions. 
For QSS2, external variables are expected to be
piecewise linear functions.

Atomic model ports _Ei_ and _Vi_ can carry data at time _t_ that contain:

* 'value': this is the value at $t$ of the variable 'name'.
* 'gradient' (optional): this is the value of the gradient of
  the variable 'name' at _t_.

# Writing ODE atomic models <a name="WritingAtomicModels"></a>

Below is given an example of dynamic for an atomic model that relies 
on the **vle.ode**

```
class MyModel : public DifferentialEquation
{
public:
 MyModel(const DynamicsInit& model,
	     const InitEventList& events) :
    DifferentialEquation(model,events)
 {
    //Initialization of variables is done 
    //into the class constructor:
    V1.init(this, "V1", events);
    E1.init(this, "E1", events)
 }
 
 //gradients of state variables are expressed 
 //into the 'compute' function 
 void compute(const Time& time)
 {
    grad(V1) = V1() - E1();
 }
 //states and external variables are attributes of the class
 Var V1;
 Var E1;//considered here as external variable
};
```

# Configuring ODE atomics models <a name="ConfiguringAtomicModels"></a>

Basic settings:

* **method** (either 'euler', 'rk4' or 'qss2', default 'euler'): it specifies
  the method used for numerical integration.
* **init_value_X** (double, default 0.0): initial value of the variable *X*.
* **init_grad_X** (double, default 0.0): initial first order
  derivative of the variable *X*.

Settings for time slicing methods methods ('euler' or 'rk4'):

* **time_step** (double, default 1.0) : the time step for the numerical
  integration.
* **output_period** (uint, default 1): gives the time step of output.
  Output will produce values each *time_step* * *output_period*.

Settings for quantized methods ('qss2'):

* **quantum_X** (double, default 0): it gives the quantum for quantization
  of variable *X*. If it equals 0, then it is expected to be an external
  variable, then no quantization is performed on *X*.

# Technical details <a name="TechnicalDetails"></a>

Description of the dynamic is based on DEVS state graph transition.
For QSS2 implementation, the most general case is considered; ie. derivative 
expressions are non linear functions depending on all state variables and thus:

* gradient derivatives are computed numerically and not analytically as
 proposed for linear gradients.
* quantization of variables involves an update of all variables. 

{{% fluid_img src="../vle_ode_TimeSlicingMethods.png" caption="DEVS state for TSM" %}}

**Fig:** The DEVS state transition graph for Time Slicing integration methods 
Euler and Rung Kutta 2.

{{% fluid_img src="../vle_ode_QSS2.png" caption="DEVS state for QSS2" %}}

**Fig:** The DEVS state transition graph for QSS2 integration method.



