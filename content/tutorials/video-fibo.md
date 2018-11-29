---
title: "video: Discrete time"
date: 2018-11-29T15:45:40+01:00
lastmod: 2018-11-29T15:45:40+01:00
weight: 1
---

## Fibonacci with discrete time models

We used the **gvle.discrete-time** package to  model the [Fibonacci sequence]
(http://en.wikipedia.org/wiki/Fibonacci_number) into the discrete-time
extension (package [vle.discrete-time](../packages/vle.discrete-time))

{{< youtube _bUe46E2WC0 >}}

Video comments:

* 0:00 : Create the package _fibonacci_ and specify a dependency to the
  [vle.discrete-time](../packages/vle.discrete-time) package.
* 0:18 : Create a new atomic model based on the discrete time formalism. By
  default, its name is _NewCpp_.
* 0:25 : Specify the equation _F= F(-1) + F(-2)_ into the _Compute_ section.
* 0:35 : Declare the variable _F_ and the set an history size of 2.
* 0:45 : Set initial history _F{n=-1}=0_ and _F{n=0}=1_.
* 0:58 : Rename the atomic model to _Fibonacci_, configure and build the
  project.
* 1:19 : Open the default model _empty.vpz_ and add an atomic model, configure
  it with the newly created dynamic _Fibonacci_ from package _fibonacci_.
* 1:29 : Into the _Observables_ tab, attach the observable port _F_ to the
  available view of the _vpz_.
* 1:38 : Into the _Project_ tab, specify the duration of the simulation to 6.
* 1:48 : Into the _Simulation_ tab, launch simulation and select the variable
  _F_ for plotting.

