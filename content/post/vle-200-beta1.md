+++
title = "VLE 2.0.0 Beta1"
date = "2018-02-15T14:16:15+01:00"
tags = ["release", "vle-2.0"]
topics = ["VLE 2.0"]
description = ""
+++

The first beta of VLE available. Highlights are: better Win32 support, many
small corrections and some improvements.

More details on the [VLE 2.0](../../vle-20) page. [Binary and source package](../../download) and [Git](https://github.com/vle-forge/) are up-to-date.

## VLE and VFL

Gauthier Quesnel (37):
- vle: add new preprocessor variables to enable/disable debug
- macx: improves the MacOS X port
- utils: fix unix findInstallPrefix function
- utils: update MacOS X findPrefix, Library
- utils: remove twice definition of is<bool>(str) and to<bool>(str)
- gvle: remove unused variable
- gvle: add `override` keyword for virtual functions
- gvle: rename `setModel` to `selectModel` to avoid conflicts
- gvle: remove explicit call to std::move
- utils: remove the unused de-mangle feature
- aqss: remove useless gcc warning
- template: update default cpp file
- CMake: remove unit_test_framework references
- REAME: add curl to the dependency list
- macos: update so/dylib management
- modernize: use `using` instead of `typedef`
- utils: fix va_list initializer in Exception
- modernize: replace C header with C++
- modernize: use override instead of virtual
- gvle: fix crash at start-up when reading bad Description files
- template: removes deprecated seed attribute
- utils: replaces and removes GVLE 1.x functions
- utils: fix crash when reading malformed [local|remote].pkg
- gvle: reports context message to the Logger widget
- 2018: bump the year
- gvle: fix build since QString::vasprintf available from QT5.5
- appveyor: enable Windows build
- template: fixed bad installation notice
- utils: remove old style exception qualifier
- windows: switch windows API to unicode
- qmake: update file
- cpack: rename the final nsis executable
- appveyor: update with fully package build
- template: improved find script
- vpz: fixed parsing of observation type
- win32: removed the use of CPack + NSIS
- vpz: fixed a conversion error

Patrick Chabrier (18):
- gvle: fix the port tag management
- gvle: fix the build and the install of the project
- gvle: add XML attributes order consistency
- gvle: fix the observables panel layout
- vle: update the package template
- gvle: enable to copy data files
- gvle: enable simulation plug-ins
- gvle: filter CMakeLists.txt file inside data
- gvle: fix renaming new empty coupled
- gvle: enhance the default plot panel.
- gvle: enable to rename a top model of a class
- gvle: add a VleLineEditItem
- gvle: add a VleCodeEdit widget
- gvle: add a VleDayEdit widget
- gvle.default: remove boost includes
- gvle: add a VleComboLineEdit widget
- cvle: fix the man installation
- vle: fix the usage of "qmake -query"

Raphaël Duboz (1):
- Add std::functional header to compile with gcc 7.2.

Ronan Trépos (18):
- gvle: fix the removing of model port
- gvle: set status log editable
- gvle: fix the build and the install of the project
- utils: fix the unique_path method
- vpz: fix the removal of views
- win32: update compiler version and doc
- win32: add QtXmlPatterns and QtSvg
- win32: update rvle building doc
- win32: fix missing libxml2 install in doc
- utils: fix RemoteManager join for win32
- win32: update pkgs version and cpack
- devs: improve instantiation of a model class
- gvle: fix paste of models
- win32: update doc install
- manager: remove temp. files for spawn simulation
- cmake: fix the use of WITH_DEBUG
- devs: in Executive, add debug param to createModel
- vpz: add a function to test existence of a port

Éric Casellas (3):
- pkgs: fix Builder mask parameter misuse in vle.generic.builder
- translator: fix missing mask empty cell detection in functions apply_mask and apply_wrap_mask
- pkgs: fix Builder generator misuse in vle.generic.builder

## RVLE

Gauthier Quesnel (1):
- project: fixed many conversion warnings
