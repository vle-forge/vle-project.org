+++
date = "2017-05-04T11:48:08+02:00"
title = "VLE 2.0.0 alpha2"
description = ""
topics = ["VLE 2.0"]
tags = ["release", "vle-2.0"]
+++

The second alpha of VLE is available. Highlights are: Qt Project support, best
Win32 support, new editor in GVLE and many improvements, `i386/x86_64` rvle
support.

More details on the [VLE 2.0](../../vle-20) page. [Binary and source package](../../download) and [Git](https://github.com/vle-forge/) are up-to-date.

## VFL, VLE, mvle, cvle

- cmake: add a make uninstall rules
- test: remove access to template directory
- test: Fix the package test
- share: fix template installation in /usr
- vle: add experimental linux qmake support
- mailmap: update
- gvle: update aboutbox
- gvle: add Ctrl+Q shortcut to quit
- vle: fix the VLE_STRINGIFY macro
- gvle: add line number and syntax highlight for C++
- win32: fix several warning with i386/x86_64 architecture
- pkgs: add generic models in vle.adaptative-qss
- pkgs: add GNUPlot atomic model
- utils: be sure to flush last spawn message
- vle: fix `list` command line option
- qmake: fix missing vle.adaptative-qss/constant model
- cmake: fix vle.adaptative-qss/Generator model name
- qmake: fix gvle pkgconfig requirements
- utils: download remote package file into temporary file
- git: gitignore++
- vle: coding style++
- devs: add header dependencies in vle::devs::DynamicsInit
- mvle: fix memory leaks in error management
- devs: remove dead code in InitEventList
- vpz: fix potential segfault in Class and Model copy
- utils: remove dead code
- vpz: fix unit test with NULL pointer
- vpz: fix memory management and NULL pointer in unit-test
- vpz: fix sax parser graph initialization
- value: fix memory management in unit-test
- gvle: remove useless std::move function
- utils: move win32 headers in last position
- [gvle] extend configure to data metadata
- gvle: fix the status button visibility
- [cvle] add a withoutspawn option
- [cvle] add the possibility to read complex values
- [manager] give error in sub process
- [vpz] SaxParser: use BUFSIZ when parsing memory
- [cvle] report simulation erreur to master
- [gvle] improve diff stack traces
- [win gvle] avoid the use of std::make_unique
- [gvle default] fix segfault
- [gvle.default] fix the launching of simulation
- gvle.default: improve Date conditions
- gvle.default: modify debug mode of simulation
- gvle.default: remove useless update
- gvle.default: avoid resetting to top left
- gvle.default: improve VpzDiagScene
- cmake: fix management of system packages
- [gvle.default] simplify project page
- gvle.default: fix the renaming of view
- win32: fix the vle command for simulation
- gvle: fix the order of call to main application
- win32: fix doc
- gvle.default: remove header functions
- utils: add stats functions in Rand

## RVLE

- README: switches from Rst to Markdown
- project: add a mailmap file
- update DESCRIPTION
- build: simplify building package
- README: update
- DESCRIPTION: update
- add the possibility to run without spawn

## PyVLE

- project: add a mailmap file
