+++
title = "VLE 2.0.0 Beta2"
date = "2018-06-26T10:17:54+02:00"
tags = ["release", "vle-2.0"]
topics = ["VLE 2.0"]
description = ""
+++

The second and last beta of VLE available. Highlights are **windows**, **cvle**
and **gvle**. Simulation kernel can now be build with the MSVC 2017 compiler.
The **Appveyor** script is updated and produce a windows installer for each
commit. **cvle** now supports empty value in csv file and use default value of
the original vpz. **gvle**: qcustomplot updated to version 2, svg export, more
console feedback.

More details on the [VLE 2.0](../../vle-20) page. [Binary and source package](../../download) and [Git](https://github.com/vle-forge/) are up-to-date.

## VLE and VFL

### Gauthier Quesnel (58):

- cmake: remove old valgrind suppression list
- win32: updated documentation and scripts
- cmake: replaced old win32 documentation
- appveyor: updated to automatically produce the Win32 installer
- README: improved links to appveyor
- devs: replaced Trace macro with function
- devs: added two Trace functions in Dynamics class
- all: fixed implicit integer/real conversion
- vpz: removed old GVLE 1.x functions
- utils: simplified the DateTime API
- all: updated source code
- cvle: updated coding style
- cvle: removed unused variables
- cvle: manage empty columns in cvle plan
- vle: removed boost::mpi boost::serialization dependencies
- cvle: replaced boost::mpi source code with mpi.h API
- cvle: fixed csv template generation
- devs: fixed visibility of the global Trace function
- cvle: fixed bad access to indices vectors
- value: fixed csv output stream for Map and Matrix
- cvle: fixed csv format generation
- travis: added gcc 6, 7 and 8
- utils: fixed compilation error with gcc >= 6
- travis: removed gcc 8
- utils: fixed DataTime buffer
- utils: fixed a catch code
- utils: fixed use of noexcept in swap member
- cvle: added missing standard header
- cvle: fixed compilation error with gcc >= 8
- travis: re-enabled gcc 8
- cvle: added row id in simulation name
- devs: enabled the instance in plug-in output
- cvle: added row id in output file
- travis: enable cvle and mvle build
- travis: replace libopenmpi 1.6 with libmpich 3
- devs: fixed Trace function output
- cli: protects access to log attribute
- aqss: adds some new line in Trace functions
- vle: modernize source code
- utils: remove useless typepdef
- vpz: remove useless typepdef
- gvle: add a popup/notification widget
- gvle: throw exception if domparser fails
- gvle: fixes invalid vpz detection
- gvle: fixes vpz xml structures in test
- utils: remove C macro from context
- aqss: fix integer cast from std::size_t to long
- all: add ciso646 standard header
- test: fix integer cast from size_t to long
- fs: fix integer cast from size_t to DWORD
- test: remove useless code in C++ version > 11
- fs: fix header for both mingw and vs
- win32: hides implementation details in cpp
- iss: fix installation paths for opengl libraries
- cmake: fix windows port with UtilsWin in cpp file
- utils: fix context with local initialization for win32
- win32: fix API/ABI problem between Qt and Rtools gcc
- utils: add missing header algorithm

### Patrick Chabrier (4):

- gvle: update qcustomplot to Version: 2.0.0
- gvle: enhancing zoom for the simulation panel
- gvle: add a DEVS diagram SVG export
- gvle: add a file loading control

### Ronan Trépos (1):

- cmake: fix the use of WITH_DEBUG for static lib

### Eric Casellas (1):

- gvle: added console log feedback

## RVLE

### Gauthier Quesnel (2):

- context: use Rprintf/REprintf to show message
- Use Rprintf/REprintf to show error message
