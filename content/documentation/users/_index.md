+++
title = "Users Pages"
topics = ["documentation"]
tags = ["devs", "users"]
description = ""
weight = 20
+++

## Software

VLE provides the VFL (_VLE Foundation Library_). This library is used to
develop:

- [VLE](vle-cli): the command line interface. It can be used in particular for
  simulating models, installing packages.
- [GVLE](gvle): the graphical user interface. It is required for developing
  models.
- [MVLE](mvle): a program to run simulations in a parallel way; it requires a
  MPI library.
- [RVLE](rvle): the R package. This port allows to use VLE Into a R session.
- [PYVLE](pyvle): the python package. This port allows to use VLE Into a python
  session.

## Concepts

With VLE, [a model](../theory/atomic-model) or an [extension](extensions) is
a [system plug-in](https://en.wikipedia.org/wiki/Library_(computing)) (*dll* or
*so*) which is obtained from compiling a C++ code. Thus, it is necessary to
know the part of the VLE's C++ API corresponding to the model or extension.
Since VLE2, it is possible to develop VLE and GVLE with the [Qt Creator
IDE](../dev/qtcreator).

* Packages: VLE [packages](packages) are standard Unix tar archives optionally
  compressed with gzip or bzip2 which can store the source code of the models,
  documentation and data. The accepted program for handling these
  [packages](packages) are the [command line interface of VLE](vle-cli),
  [GVLE](gvle), [RVLE](rvle) and [PyVLE](pyvle).

* Extensions: VLE provides several [packages](packages) to simplify the
  development of atomic models. These packages are called
  [extensions](extensions) and provides behaviour like: finite state automaton,
  ordinary differential equation solver, Petri net, planning and decision
  making... Some extensions also provide graphical interfaces and C++ code
  generators.

* Distributions: [Package distributions](distributions) are sets of VLE
  packages available through http. You can either use a distribution which is
  already available or provide your own distribution. VLE offers the
  possibility to automatically download and install packages from
  distributions. The modelling extension and tools developed by the VLE
  development team are thus provided into the [VLE package
  distribution](../../packages).

## Howto?

- How to [develop atomic model](../theory/atomic-model).
- How to [debug my model](debug-model).
- How to change [default settings of VLE](configuration-file).

## Whatis?

- What is the [VLE home directory](vle-home).

