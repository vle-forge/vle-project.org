+++
topics = ["documentation"]
tags = ["devs", "vle"]
title = "Documentation"
description = "VLE 2.0"
+++

**Keywords**

Concepts: [kernel](kernel), [packages](packages), [extensions](extensions),
[distributions](distributions).

Programs: [vle](vle-cli), [gvle](gvle), [rvle](rvle), [pyvle](pyvle).

C++: [VLE's API](http://www.vle-project.org/doxygen/dev/), [VPZ format](vpz-
format), [debug model](debug-model).

## Kernel

In VLE, we have implemented the [DSDE abstract
simulator](http://portal.acm.org/citation.cfm?id=293257) developed by [Fernando
J. Barros](http://eden.dei.uc.pt/~barros/) which enable parallelization of
atomic models and dynamic structure changes during simulation. We also
introduced an observation framework in the DEVS kernel simulator of VLE.

## Packages

VLE [packages](packages) are standard Unix tar archives optionally compressed
with gzip or bzip2 which can store the source code of the models, documentation
and data. The accepted program for handling these [packages](packages) are the
command line interface of VLE, GVLE, RVLE and PyVLE.

## Extensions

VLE provides several [packages](packages) to simplify the development of atomic
models. These packages are called [extensions](extensions) and provides
behaviour like: finite state automaton, ordinary differential equation solver,
Petrinet, planning and decision making etc. Some extensions also provide
graphical interfaces and C++ code generators.

## Distributions

[Package distributions](distributions) are sets of VLE packages available
through http. You can either use a distribution which is already available or
provide your own distribution. VLE offers the possibility to automatically
download and install packages from distributions. The modelling extension and
tools developed by the VLE development team are thus provided into the [VLE
package distribution](../packages).

## Programs and ports

VLE provides the VFL (_VLE Foundation Library_). This library is used to
develop:

- [vle](vle-cli): the command line interface. It can be used in particular for
  simulating models, installing packages.
- [gvle](gvle): the graphical user interface. It is required for developing
  models.
- [mvle](mvle): a program to run simulations in a parallel way; it requires a
  MPI library.
- [rvle](rvle): the R package. This port allows to use VLE Into a R session.
- [pyvle](pyvle): the python package. This port allows to use VLE Into a python session.

## API

The [C++ API documentations](http://www.vle-project.org/doxygen/dev/) are daily
generated from the source code. With VLE, a model or an [extension](extensions)
is a [system plug-in](https://en.wikipedia.org/wiki/Library_(computing)) (*dll*
or *so*) which is obtained from compiling a C++ code. Thus, it is necessary to
know the part of the VLE's C++ API corresponding to the model or extension.

API of the DEVS [Atomic model](atomic-model)  * [Counter](examples/counter), Generator.

API of the DEVS Executive model.

How to [debug model](debug-model)

---

**Other VLE 1.1, 2.0 and 3.0**

- [VLE 1.1]({{< ref "vle-11.md" >}}) stable version.
- [VLE 2.0]({{< ref "vle-20.md" >}}) work in progress.
- [VLE 3.0]({{< ref "vle-30.md" >}}) work in progress.
