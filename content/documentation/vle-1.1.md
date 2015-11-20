+++
categories = ["vle-1.1", "documentation"]
date = "2015-11-20T12:56:48+01:00"
description = ""
keywords = []
title = "Documentation VLE 1.1"

+++

### Kernel

In VLE, we have implemented the [DSDE abstract
simulator](http://portal.acm.org/citation.cfm?id=293257) developed by [Fernando
J. Barros](http://eden.dei.uc.pt/~barros/) which enable parallelization of
   atomic models and dynamic structure changes during simulation. We also
   introduced an observation framework in the DEVS kernel simulator of VLE.

### Packages

VLE [packages] are standard Unix tar archives optionally compressed
with gzip or bzip2 which can store the source code of the models,
documentation and data. The accepted program for handling these
[packages] are the *command line interface* of VLE, *rvle* and
*pyvle*.

### Extensions

VLE provides several [packages] to simplify the development of atomic
models. These packages are called [extensions] and provides behavior
like: finite state automaton, ordinary differential equation solver,
Petrinet, planning and decision making etc. Some extensions also
provide graphical interfaces and C++ code generators.

### Programs and ports

VLE provides the VFL (_VLE Foundation Library_). This library is used
to develop:

- [VLE]({{< ref "documentation/vle-1.1/vle-cli.md" >}}): the command line
  interface
- [GVLE]({{< ref "documentation/vle-1.1/gvle.md" >}}): the graphical user
  interface
- [RVLE]({{< ref "documentation/vle-1.1/rvle.md" >}}): the R project package
- [PyVLE]({{< ref "documentation/vle-1.1/pyvle.md" >}}): the python package.

### C++

With VLE, a model or an [extension] is a system plugin (*dll* or *so*)
which is obtained from compiling a C++ code. Thus, it is necessary to
know the part of the VLE's C++ API corresponding to the model or
extension.

- API of the DEVS [Atomic model]
  * [Counter], Generator
- API of the DEVS Executive model
- Howto [debug model]

### C++ API

The [C++ API documentations](http://www.vle-project.org/doxygen/1.1/) are daily
generated from the source code.


   [Atomic model]: atomic-model
   [Counter]: examples/counter
   [debug model]: debug-model
   [packages]: packages
   [extension]: extensions
   [extensions]: extensions
   [VLE 1.0]: http://www.vle-project.org/doxygen/1.0
   [VLE 1.1]: http://www.vle-project.org/doxygen/1.1
   [VLE in progress]: http://www.vle-project.org/doxygen/dev
