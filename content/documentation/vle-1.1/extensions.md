+++
categories = ["documentation", "extension"]
date = "2015-10-23T10:50:01+02:00"
description = "How to use the extension of VLE"
keywords = ["devs", "extension", "model"]
title = "Extensions"
+++

VLE provides several `vle::devs::Dynamics` subclass to simplify the
development of atomic models. These sub-classes provides behavior
like: finite state automaton, ordinary differential equation solver,
Petrinet, planning and decision making etc. Some extensions also
provide graphical interfaces and C ++ code generators.

# Extensions available

- `vle.output` provides output plug-ins.  These plugins are in charge
  of recording the outputs of simulations in files (using a csv, a R
  data or gnuplot format). This package is a dependency of several
  extensions.
- `vle.extension.fsa` provides a `vle::devs::dynamics` subclass to
  develop easily finite state automaton with a specific C++ syntax or
  be using a graphical interface and C++ generator.
- `vle.extension.differential-equation` provides `vle::devs::dynamics`
  generic classes to develop DEVS models that wrap ordinary
  differential equation using QSS, Runge kutta or Euler solver.
- `vle.extension.petrinet` provides a `vle::devs::dynamics` subclass
  to develop easily high level Petrinet with a specific C++ syntax or
  be using a graphical interface and C++ generator.
- `vle.extension.celldevs` provides a `vle::devs::dynamics` subclass
  to develop cellular automaton. Using this extension with an
  *executive* (to dynamically change structure of the model) create a
  high level modeling system.
- `vle.extension.decision` a `vle::devs::dynamics` class to develop
  planning system.
- `vle.extension.difference-equation` provides C++
  `vle::devs::dynamics` generic classes to develop models that compute
  the value of one or more real variables in t depends on itself at
  `t-1`, `t-2`, ... and according to other real variables at `t`,
  `t-1`, `t-2`, ... We called it the difference equations but this
  extension is more general because only the above property is
  respected.
- `vle.forrester` a graphical user interface to develop model using
  the Forrester formalism.

# Installation

First, download the packages repository from zip file or Git
repository and use the command line to build and install the
packages. For example for VLE 1.1:

```bash
cd $HOME
mkdir vle-extension-sources
cd vle-extension-sources
wget http://www.vle-project.org/pub/vle/1.1/1.1.2/packages-1.1.2.zip
unzip packages-1.1.2.zip
cd packages-1.1.2
vle-1.1 -P vle.output configure build
vle-1.1 -P vle.extension.fsa configure build
vle-1.1 -P vle.extension.difference-equation fsa configure build
vle-1.1 -P vle.extension.differential-equation configure build
vle-1.1 -P vle.extension.petrinet configure build
vle-1.1 -P vle.extension.celldevs configure build
vle-1.1 -P vle.extension.decision configure build
vle-1.1 -P vle.forrester configure build
```
