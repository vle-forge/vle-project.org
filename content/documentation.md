+++
categories = ["documentation", "c++", "atomic-model"]
date = "2015-09-15T10:17:39+02:00"
description = ""
keywords = ["devs", "atomic", "model"]
title = "documentation"
menu = "main"
+++

### packages

VLE [packages] are standard Unix tar archives optionally compressed with gzip
or bzip2 which can store the source code of the models, documentation and data.
The accepted program for handling these packages are the *command line
interface* of VLE, *rvle* and *pyvle*.

### C++

With VLE, a model or an extension is a system plugin (*dll* or *so*) which is
obtained from compiling a C++ code. Thus, it is necessary to know the part of the VLE's C++ API corresponding to the model or extension.

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
   [VLE 1.0]: http://www.vle-project.org/doxygen/1.0
   [VLE 1.1]: http://www.vle-project.org/doxygen/1.1
   [VLE in progress]: http://www.vle-project.org/doxygen/dev
