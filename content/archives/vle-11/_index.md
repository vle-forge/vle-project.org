+++
topics = ["VLE 1.1"]
tags = ["vle-1.1"]
title = "VLE 1.1"
+++

# Download

Windows (32bits binaries for Windows 7, 8, 10):

- [vle-1.1.3.exe](http://www.vle-project.org/pub/vle/1.1/1.1.3/vle-1.1.3.exe)
- [rvle_1.1.3-0.zip](http://www.vle-project.org/pub/vle/1.1/1.1.3/rvle_1.1.3-0.zip)

Sources (See the the README files in all tarballs):

* [vle-1.1.3.tar.gz](http://www.vle-project.org/pub/vle/1.1/1.1.3/vle-1.1.3.tar.gz)
* [rvle_1.1.3-0.tar.gz](http://www.vle-project.org/pub/vle/1.1/1.1.3/rvle_1.1.3-0.tar.gz)
* [pyvle-1.1.3.tar.gz](http://www.vle-project.org/pub/vle/1.1/1.1.3/pyvle-1.1.3.tar.gz)

More details are available for [downloading](download) and
[installation](installation) of VLE, packages and ports. A specific page is
available for the [installation](rvle) of RVLE.

---

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

[Package distributions](distributions) are sets of VLE packages available
through http. You can either use a distribution which is already available or
provide your own distribution. VLE offers the possibility to automatically
download and install packages from distributions. The modeling extension and
tools developed by the VLE development team are thus provided into the [VLE
package distribution](vle-packages-distribution).

## Programs and ports

VLE provides the VFL (_VLE Foundation Library_). This library is used to
develop:

- [vle](vle-cli): the command line interface. It can be used in particular for
  simulating models, installing packages.
- [gvle](gvle): the graphical user interface. It is required for developing models.
- [mvle](mvle): a program for parallelizing simulations; it requires a MPI library.
- [rvle](rvle): the R package. This port allows to use VLE Into a R session.
- [pyvle](pyvle): the python package. This port allows to use VLE Into a python session.

---

# Technical details

## How to upgrade models

[upgrade from vle 1.0.3 to vle 1.1](upgrade-from-vle-1.0.3-to-vle-1.1)

## API

The [C++ API documentations](http://www.vle-project.org/doxygen/master1.1/) are
daily generated from the source code. With VLE, a model or an [extension] is a
system plug-in (*dll* or *so*) which is obtained from compiling a C++ code.
Thus, it is necessary to know the part of the VLE's C++ API corresponding to
the model or extension.

- API of the DEVS [Atomic model]
  * [Counter], Generator.
- API of the DEVS Executive model.
- How to [debug model].

## Tutorials

Some [tutorials] are provided.

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

The detail of the format is given here: [VPZ files format](vpz-files-format).
The VPZ files are generally located into the `exp` directory of a VLE
[package](packages).

## VLE home

The [VLE_HOME](vle-home) is a directory that contains log files, binaries of
[packages] and [configuration file](configuration-file). You should not modify
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
   [tutorials]: tutorials
