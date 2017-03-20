+++
topics = ["tutorial"]
tags = ["tutorial"]
title = "Tutorials"
+++

# Fibonacci with discrete time models

We used the **gvle.discrete-time** package to  model the [Fibonacci sequence]
(http://en.wikipedia.org/wiki/Fibonacci_number) into the discrete-time extension
(package [vle.discrete-time](../packages/vle.discrete-time))

{{< youtube _bUe46E2WC0 >}}

Video comments:

* 0:00 : Create the package _fibonacci_ and specify a dependency to the
  [vle.discrete-time](../packages/vle.discrete-time) package.
* 0:18 : Create a new atomic model based on the discrete time formalism.
  By default, its name is _NewCpp_.
* 0:25 : Specify the equation _F= F(-1) + F(-2)_ into the _Compute_ section.
* 0:35 : Declare the variable _F_ and the set an history size of 2.
* 0:45 : Set initial history _F{n=-1}=0_ and _F{n=0}=1_.
* 0:58 : Rename the atomic model to _Fibonacci_, configure and build the project.
* 1:19 : Open the default model _empty.vpz_ and add an atomic model, configure
 it with the newly created dynamic _Fibonacci_ from package _fibonacci_.
* 1:29 : Into the _Observables_ tab, attach the observable port _F_ to the
 available view of the _vpz_.
* 1:38 : Into the _Project_ tab, specify the duration of the simulation to 6.
* 1:48 : Into the _Simulation_ tab, launch simulation and select the variable _F_
 for plotting.

# Lotka Volterra equation with Forrester diagrams

We used the **gvle.forrester** package to  model the [Lotka Volterra equations]
(https://en.wikipedia.org/wiki/Lotka%E2%80%93Volterra_equations) into the Ordinary
Differential Equations (package [vle.ode](../packages/vle.ode))

{{< youtube kvdTJuGQl9k >}}

Video Comments:

* 0:00 : Create the package _lotkavolterra_ and specify a dependency to the
  [vle.ode](../packages/vle.ode) package.
* 0:18 : Create a new atomic model based on the Forrester formalism.
  By default, its name is _NewCpp_.
* 0:24 : Define two compartments _x_ and _y_ and give their initial values.
* 0:46 : Define four parameters _alpha_, _beta_, _gamma_ and _delta_ and give
  their values.
* 1:36 : Define two material flows _flowX_ and _flowY_.
* 1:53 : Declare a hard link from flows to compartments.
* 1:59 : Declare dependencies between flows and parameters.
* 2:23 : Give equations of the flows (depending on compartments and parameters).
* 3:06 : Modify the time step to 0.01, for the Euler method, of the numerical
  integration.
* 3:22 : Close the atomic model description and rename it to _LotkaVolterra_.
* 3:24 : Configure and build the project.
* 3:44 : Open the default model _empty.vpz_ and add an atomic model, configure
 it with the newly created dynamic _LotkaVolterra_ from package _lotkavolterra_.
* 3:56 : Into the _Observables_ tab, attach the observable ports to the
 available view of the _vpz_.
* 4:11 : Save file and select the _Simulation_ tab to launch simulation.
* 4:18 : Change the duration of simulation, re-launch simulation, and plot the
  compartments _x_ and _y_.


# Old VLE 1.1 tutorials

These tutorials are made for the [version 1.1](../vle-11) of VLE.

## First model

- [First models](tuto-01): create two models from scratch and assign
  observation. Keywords: C++, package and observation.

## Lotka-Volterra

- [Lotka-Volterra](tuto-02): create a simple Euler model, assign observation
  and experiment conditions. Keywords: C++, package, observation, conditions
  and RVLE.

## Forrester

This [tutorial](http://www.youtube.com/watch?v=WAsqKIuIOqg&feature=youtu.be)
shows how to use the Forrester extension:

- See [System Dynamics](http://en.wikipedia.org/wiki/System_dynamics) to get the
  basic concepts.
- The example in this tutorial consists in modeling the
  [Lotka Volterra equations](http://en.wikipedia.org/wiki/Lotka%E2%80%93Volterra_equation).

{{< youtube WAsqKIuIOqg >}}
