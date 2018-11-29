+++
topics = ["documentation"]
tags = ["devs", "vle"]
title = "Documentation "
description = "VLE 2.0"
hasMath = true
weight = 11
+++

**Keywords**: [devs](theory/devs), [packages](users/packages),
[extensions](users/extensions), [distributions](users/distributions).

The _Virtual Laboratory Environment_ is a multi-modeling and simulation
platform. It is a powerful modeler and simulator supporting the use of
different formalisms for models specification and simulation.

VLE is particularly well adapted for complex models where the coupling of
different formalisms is required. In addition to the classical use of one
single formalism for modeling and simulation, VLE can integrate, i.e. couple,
heterogeneous formalisms in one coherent simulation model.

For instance, VLE supports, and is not limited to, the modeling and simulation
of the following formalisms (stand alone or coupled together):

- Discrete Event Specifications
- Differential equations
- Difference equations
- Petri net
- Finite State Automata

VLE supports the following modeling and simulation paradigms:

- System Dynamics
- Multi-Agent Systems, Multi-Agent Simulation
- Decision support systems
- Learning systems

VLE is based on the theory of modeling and simulation initially developed by
B.P. Zeigler in the 70's and continuously enriched until now by an active
international community.

VLE is based on the [DEVS](theory) formalism (_Discrete Event systems
Specification_). VLE provides a set of C++ libraries, the VFL (_VLE Foundation
Libraries_) and a lot of programs like a simulator, a graphical user interface
to model and develop models and tools to analyse and visualize simulation
outputs. The VFL are sufficiently well designed to allow the development of new
simulators, models or new programs for modeling and analysis.

Our goal with VLE is to provide powerful tools for modeling, simulating and
analysing complex dynamics systems. We hope build an easy to use software. Our
development are complying with the [DEVS] specification [DEVS] and works made
by the simulation community. We are also pursuing the objective to develop and
maintain a community of users and developers using an open, agile and community
oriented development.

VLE is a free environment of multi-modelling and simulation developed under the
[licence GPL v3.0]. All source code are available on [Github](https://github.com/vle-forge/).

## What's DEVS

[DEVS](theory/devs), *Discrete Event System Specification* is a modular and
hierarchic formalism for modelling, simulation and study of complex systems.
These system can be discrete event systems describe by state transition
functions or continuous systems describe by differential equation for instance
or hybrid systems.

## VLE

In VLE, we have implemented the [DSDE abstract
simulator](http://portal.acm.org/citation.cfm?id=293257) developed by [Fernando
J. Barros](http://eden.dei.uc.pt/~barros/) which enables parallelization of
atomic models and dynamic structure changes during simulation. We also
introduced an observation framework in the DEVS kernel simulator of VLE.

VLE is a C++ implementation of a [DEVS kernel](theory/devs). The [C++ API
documentations](http://www.vle-project.org/doxygen/master2.0/) are daily
generated from the source code.

* [DEVS initiation](theory/devs)
* Empty [Atomic model](theory/atomic-model)
* [Counter](theory/counter)
* Empty Executive model
* How to [debug model](users/debug-model)
* [VPZ format](dev/vpz-format)

With VLE, [a model](theory/atomic-model) or an [extension](users/extensions) is
a [system plug-in](https://en.wikipedia.org/wiki/Library_(computing)) (*dll*
or *so*) which is obtained from compiling a C++ code. Thus, it is necessary to
know the part of the VLE's C++ API corresponding to the model or extension.
Since VLE2, it is possible to develop VLE and GVLE with the [Qt Creator
IDE](dev/qtcreator).

* Packages

    VLE [packages](users/packages) are standard Unix tar archives optionally
    compressed with gzip or bzip2 which can store the source code of the
    models, documentation and data. The accepted program for handling these
    [packages](users/packages) are the [command line interface of
    VLE](users/vle-cli), [GVLE](users/gvle), [RVLE](users/rvle) and
    [PyVLE](users/pyvle).

*   Extensions

    VLE provides several [packages](users/packages) to simplify the development
    of atomic models. These packages are called [extensions](users/extensions)
    and provides behaviour like: finite state automaton, ordinary differential
    equation solver, Petri net, planning and decision making... Some extensions
    also provide graphical interfaces and C++ code generators.

*   Distributions

    [Package distributions](users/distributions) are sets of VLE packages
    available through http. You can either use a distribution which is already
    available or provide your own distribution. VLE offers the possibility to
    automatically download and install packages from distributions. The
    modelling extension and tools developed by the VLE development team are
    thus provided into the [VLE package distribution](../../packages).

*   Programs and ports : VLE provides the VFL (_VLE Foundation Library_). This library is used to develop:

    - [VLE](users/vle-cli): the command line interface. It can be used in
      particular for simulating models, installing packages.
    - [GVLE](users/gvle): the graphical user interface. It is required for
      developing models.
    - [MVLE](users/mvle): a program to run simulations in a parallel way; it
      requires a MPI library.
    - [RVLE](users/rvle): the R package. This port allows to use VLE Into a R
      session.
    - [PYVLE](users/pyvle): the python package. This port allows to use VLE
      Into a python session.
