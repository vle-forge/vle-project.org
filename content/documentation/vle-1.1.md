+++
categories = ["vle-1.1", "documentation"]
date = "2015-11-20T12:56:48+01:00"
description = ""
keywords = []
title = "Documentation VLE 1.1"

+++

# Generic documentation

## Kernel

In VLE, we have implemented the [DSDE abstract
simulator](http://portal.acm.org/citation.cfm?id=293257) developed by [Fernando
J. Barros](http://eden.dei.uc.pt/~barros/) which enable parallelization of
atomic models and dynamic structure changes during simulation. We also
introduced an observation framework in the DEVS kernel simulator of VLE.

## Packages

VLE [packages] are standard Unix tar archives optionally compressed with gzip or
bzip2 which can store the source code of the models, documentation and data. The
accepted program for handling these [packages] are the *command line interface*
of VLE, *rvle* and *pyvle*.

## Extensions

VLE provides several [packages] to simplify the development of atomic models.
These packages are called [extensions] and provides behavior like: finite state
automaton, ordinary differential equation solver, Petrinet, planning and
decision making etc. Some extensions also provide graphical interfaces and C++
code generators.

## Distributions

[Package distributions]({{< ref "documentation/vle-1.1/distributions.md" >}})
are sets of VLE packages available through http. You can either use a
distribution which is already available or provide your own distribution. VLE
offers the possibility to automatically download and install packages from
distributions. The modeling extension and tools developed by the VLE development
team are thus provided into the [VLE package distribution]({{< ref
"documentation/vle-1.1/vle-packages-distribution.md">}}).

## Programs and ports

VLE provides the VFL (_VLE Foundation Library_). This library is used to
develop:

- [vle]({{< ref "documentation/vle-1.1/vle-cli.md" >}}): the command line
  interface. It can be used in particular for simulating models, installing
  packages. 
- [gvle]({{< ref "documentation/vle-1.1/gvle.md" >}}): the graphical user
  interface. It is required for developing models.
- [mvle]({{< ref "documentation/vle-1.1/mvle.md" >}}): a program for
  parallelizing simulations; it requires a MPI library.
- [rvle]({{< ref "documentation/vle-1.1/rvle.md" >}}): the R package. This port
  allows to use VLE Into a R session.
- [pyvle]({{< ref "documentation/vle-1.1/pyvle.md" >}}): the python package.
  This port allows to use VLE Into a python session.

## Download and install

* [Download page of vle-1.1](http://www.vle-project.org/vle-1.1) for downloading
  VLE, the packages and the ports.
* [Installation page of vle-1.1]({{< ref
  "documentation/vle-1.1/installation.md">}})
* [Installation page of rvle-1.1]({{< ref "documentation/vle-1.1/rvle.md">}})

---
# Technical details

## C++

The [C++ API documentations](http://www.vle-project.org/doxygen/1.1/) are daily
generated from the source code. With VLE, a model or an [extension] is a system
plug-in (*dll* or *so*) which is obtained from compiling a C++ code. Thus, it is
necessary to know the part of the VLE's C++ API corresponding to the model or
extension.

- API of the DEVS [Atomic model]
  * [Counter], Generator.
- API of the DEVS Executive model.
- How to [debug model].

## Compiler support

Operating Systems supported by VLE are Linux/Unix and Windows. Compilers used to
build VLE and VLE Packages are :

* g++ on Linux/Unix
* mingw on windows

## Requirements

* glibmm (>= 2.22)
* libxml2 (>= 2.8)
* libarchive (>= 2.0)
* boost (>= 1.41)
* cmake (>= 2.8.0)
* make (>= 1.8)
* c++ compiler (gcc >= 4.4, clang >= 3.1, intel icc (>= 11.0)
* any MPI 2 library as OpenMpi, mpich (for [mvle program]({{< ref
  "documentation/vle-1.1/mvle.md" >}}))
* gtkmm (>= 2.22.0) (for [gvle program]({{< ref "documentation/vle-1.1/gvle.md"
  >}}))

---
# Other details

## VPZ files

The VPZ (VLE Project file Zipped) is an XML file format use in VLE to represent:

* The structure of a model: hierarchy of coupled models, atomic models,
  connections, inputs and outputs port
* The experimental conditions: how to initialize atomic models, multiple values
  can be given in order to perform multiple simulations.
* The observation: how to observe atomic models, output file format, observation
  policy (constant timed observation, by event or at the end of the simulation).

The detail of the format is given here: [VPZ files format]({{< ref
"documentation/vle-1.1/vpz-files-format.md" >}}). The VPZ files are generally
located into the `exp` directory of a VLE [package]({{< ref
"documentation/vle-1.1/packages.md">}}).

## VLE home

The [VLE_HOME]({{< ref "documentation/vle-1.1/vle-home.md">}}) is a directory
that contains log files, binaries of [packages] and [configuration file]({{< ref
"documentation/vle-1.1/configuration-file.md">}}). You should not modify
directly this directory unless you know what you are doing.


   [Atomic model]: atomic-model
   [Counter]: examples/counter
   [debug model]: debug-model
   [packages]: packages
   [extension]: extensions
   [extensions]: extensions
   [VLE 1.0]: http://www.vle-project.org/doxygen/1.0
   [VLE 1.1]: http://www.vle-project.org/doxygen/1.1
   [VLE in progress]: http://www.vle-project.org/doxygen/dev
