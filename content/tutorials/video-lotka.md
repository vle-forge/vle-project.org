---
title: "video: Forrester diagrams"
date: 2018-11-29T15:45:49+01:00
lastmod: 2018-11-29T15:45:49+01:00
weight: 2
---

## Lotka Volterra equation with Forrester diagrams

We used the **gvle.forrester** package to  model the [Lotka Volterra equations]
(https://en.wikipedia.org/wiki/Lotka%E2%80%93Volterra_equations) into the
Ordinary Differential Equations (package [vle.ode](../packages/vle.ode))

{{< youtube kvdTJuGQl9k >}}

Video Comments:

* 0:00 : Create the package _lotkavolterra_ and specify a dependency to the
  [vle.ode](../packages/vle.ode) package.
* 0:18 : Create a new atomic model based on the Forrester formalism. By
  default, its name is _NewCpp_.
* 0:24 : Define two compartments _x_ and _y_ and give their initial values.
* 0:46 : Define four parameters _alpha_, _beta_, _gamma_ and _delta_ and give
  their values.
* 1:36 : Define two material flows _flowX_ and _flowY_.
* 1:53 : Declare a hard link from flows to compartments.
* 1:59 : Declare dependencies between flows and parameters.
* 2:23 : Give equations of the flows (depending on compartments and
  parameters).
* 3:06 : Modify the time step to 0.01, for the Euler method, of the numerical
  integration.
* 3:22 : Close the atomic model description and rename it to _LotkaVolterra_.
* 3:24 : Configure and build the project.
* 3:44 : Open the default model _empty.vpz_ and add an atomic model, configure
  it with the newly created dynamic _LotkaVolterra_ from package
  _lotkavolterra_.
* 3:56 : Into the _Observables_ tab, attach the observable ports to the
  available view of the _vpz_.
* 4:11 : Save file and select the _Simulation_ tab to launch simulation.
* 4:18 : Change the duration of simulation, re-launch simulation, and plot the
  compartments _x_ and _y_.
