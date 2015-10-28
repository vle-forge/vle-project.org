+++
categories = ["documentation", "c++", "atomic-model"]
date = "2015-09-15T10:17:39+02:00"
description = ""
keywords = ["devs", "atomic", "model"]
title = "documentation"
menu = "main"
+++

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

- [VLE]({{< ref "documentation/vle-cli.md" >}}): the command line
  interface
- [GVLE]({{< ref "documentation/gvle.md" >}}): the graphical user
  interface
- [RVLE]({{< ref "documentation/rvle.md" >}}): the R project package
- [PyVLE]({{< ref "documentation/pyvle.md" >}}): the python package.

### C++

With VLE, a model or an [extension] is a system plugin (*dll* or *so*)
which is obtained from compiling a C++ code. Thus, it is necessary to
know the part of the VLE's C++ API corresponding to the model or
extension.

- API of the DEVS [Atomic model]
  * [Counter], Generator
- API of the DEVS Executive model
- Howto [debug model]

The VLE's C++ API documentations are daily generated from the source code and
are available for all actual branches maintained:

- [VLE 1.0]
- [VLE 1.1]
- [VLE in progress]

   [Atomic model]: atomic-model
   [Counter]: examples/counter
   [debug model]: debug-model
   [packages]: packages
   [extension]: extensions
   [extensions]: extensions
   [VLE 1.0]: http://www.vle-project.org/doxygen/1.0
   [VLE 1.1]: http://www.vle-project.org/doxygen/1.1
   [VLE in progress]: http://www.vle-project.org/doxygen/dev
