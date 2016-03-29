+++
topics = ["documentation"]
date = "2015-09-15T10:28:18+02:00"
description = ""
tags = ["package","distribution"]
title = "Packages"
+++

Packages in VLE are autonomous projects which gather for example source code of
PDEVS models, VPZ files, documentations or data. The goal of the packages in VLE
is to improve the development of big models and to facilitate the sharing of
models and code.

# Example of a package hierarchy

```
$mypackage
  |─ buildvle/           ; the compilation directory,
  |                      ; it should not be directly modified
  |─ cmake/              ; cmake scripts
  |─ data/               ; data of your package
  |─ doc/                ; documentation of your package
  |─ exp/                ; experience, ie. vpz, of your package
  │   └─ CMakeLists.txt  ; CMake file of the directory exp
  │   └─ mymodel.vpz     ; your experiment (vpz file)
  |─ src/                ; directory of the source code
  │   └─ CMakeLists.txt  ; CMake file of the directory src
  │   └─ mydynamics.cpp  ; cpp code for your dynamics
  |                      ; (DEVS atomic model)
  |─ test/               ; directory containing the unit tests
  |                      ; for your package
  └─ Authors.txt         ; a Authors file  
  └─ CMakeCPack.cmake    ; CMake packaging script
  └─ CMakeLists.txt      ; a root CMakeFile
  └─ Description.txt     ; a Description file
  └─ License.txt         ; a Licence file
  └─ News.txt            ; a News file
  └─ Readme.txt          ; a Readme file
```

A package or project in VLE have several directories and sub-directories.
Although all files have their importance we will detail only the most important.

# The VPZ files into the exp directory (eg. mymodel.vpz)

A VPZ file represents a model and the experiment associated to the model. It can
be simulated by [vle application](vle-cli). It contains the structure of the
model (seen as a graph) and inputs/outputs of the models. You can edit the model
with the [gvle application](gvle). The XML structure of this file is detailed
[here](vpz-files-format).

# The Description.txt file

The `Description.txt` gives the description of the project. You should fill it
with detailed informations about your package. There is an example of a
`Description.txt` file :

```
Package: mypackage
Version: 0.1.0
Depends: vle.extension.decision, vle.extension.difference-equation
Build-Depends: vle.output
Conflicts:
Maintainer: My name <mymail>
Description: Still in progress
.
Tags: examples
Url: http://mydistribution/
Size: 0
MD5sum: xxxx
```

You have to least to update the name of the package with the name of the
directory (ie. mypackage). You can set a version to your package. The `Depends`
tag should contain a list of packages you depend on for building your dynamics.
For example if you use the vle extension for modeling difference equations (see
[VLE package distribution](vle-packages-distribution)), it has to be listed. The
`Build-Depends` should contain the list of packages you use (this time, without
requiring them for the building process), typically it can be the vle.output
package.

# The cpp files into src directory (eg. mydynamics.cpp)

If you have the most integrated mode of use of VLE (using modeling plug ins into
[gvle](gvle), it is not required that you modify these files. They are generated
by the modeling plug ins.

Each `cpp` files into `src/` represents an atomic model. An atomic model is a
C++ class that inherits from `vle::devs::Dynacmis`. Moreover a macro such as
`DECLARE_DYNAMICS` has to be used in order to declare the class mentioned
above to be a DEVS atomic model.

# The CMakeLists.txt files

Once again, if you have the most integrated mode of use of VLE, it is not
required that you modify these files.

These file are present in each subdirectory of a package. Depending on their
location they have different roles. For examples the `CMakeLists.txt` file at
the root directory declares the project and search for VLE includes and
binaries. The `CMakeLists.txt` in `src/` declares the C++ target to compile and
to install.

# How to manipulate VLE packages

In order to design the model the application [gvle application](gvle) is
required. Designing the model means modifying the VPZ files of your package.
These files are basically XML files and could be edited directly with a text
editor; nevertheless `gvle` provides a gui to manipulate VPZ.   

Otherwise in order to perform simulations, using the [vle application](vle-cli)
in the _package_ mode is sufficient. Also `gvle` provides some of these commands
such as _clean_, _rclean_, _configure_, _build_ and _create_.
