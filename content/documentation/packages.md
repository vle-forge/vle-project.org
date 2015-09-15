+++
categories = []
date = "2015-09-15T10:28:18+02:00"
description = ""
keywords = []
title = "packages"
menu = "documentation"
+++

Packages in VLE are autonomous project which regroup source code of DEVS
models, VPZ files, documentations and data. The goal of the packages in VLE are
to propose an easily aspect to develop big models and share models between
modeler.

The home directory of VLE is defined by the environment variable `VLE_HOME`. If
the environment variable is not defined, VLE use the default path:

- `$HOME/.vle` on Unix/Linux systems (eg. `/home/user/.vle`).
- `$HOME/vle` on Win32 or Win64 systems which corresponds to the variables:
  `%HOMEDRIVE%%HOMEPATH%\vle` (eg. `c:\documents and settings\user\vle`).

The home directory of VLE have the following hierarchy:

	VLE_HOME
	 ├─ pkgs           ; the directory of VLE's packages
	 │   └─ firemanqss ; an example of paquet: firemanqss
	 │       ├─ build  ; One directory per package
	 │       ├─ data
	 │       ├─ doc
	 │       ├─ exp
	 │       ├─ lib
	 │       └─ src
	 └─ vle.log        ; log of previous execution of VLE

Hierarchy of the package
------------------------

A package or project in VLE have several directory and sub-directory. Each file
and directory are important. The following description is a default package in
provide in VLE:

	VLE_HOME/pkgs/firemanqss
	 ├─ build          ; the compilation directory (temporary directory)
	 ├─ cmake          ; cmake scripts
	 ├─ data           ; data of your package
	 ├─ doc            ; documentation of your package
	 ├─ exp            ; experience, ie. vpz, of your package
	 ├─ lib            ; shared library directory
	 ├─ plugins        ; simulators, modeling plugins
	 ├─ src            ; models' sources of your package
	 ├─ Authors.txt    ; authors of your package
	 ├─ License.txt    ; license of your package
	 ├─ News.txt       ; news about evolution of your package
	 ├─ Readme.txt     ; some notes about your package
	 └─ CMakeList.txt  ; a CMake script

How to use VLE with packages
----------------------------

The key, in command line interface:

	vle -P name_of_the_directory [command...] files...

Commands available are:

- `create` to build a new package in the `VLE_HOME/pkgs`
- `configure` try to run the CMake program in your package.
- `build` try to compile your package.
- `test` try the unit test of your package if they exist.
- `packages` try to build source and binary Zip of your package.
- `depends` show the depends of your packages.
- `list` lists all Vpz and plug-ins of your packages.

For example, to configure, build and install the package:

- `vle -P firemanqss configure build`
  - execute in the build directory, the cmake command.
  - execute in the build directory, the make command.
  - execute in the src, the make install command.
