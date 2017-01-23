+++
tags = [ "windows" ]
topics = [ "VLE 2.0", "Installation" ]
description = "How to install VLE on Windows 7, 8, 10 ?"
date = "2016-12-16T15:13:55+01:00"
title = "Windows Installation"
+++

# Uninstall VLE 1.0 or 1.1

If you have already install VLE 1.0 or VLE 1.1, you may:

* Uninstall the previous version
* Remove the remaining variable `PKG_CONFIG_PATH` (only earlies versions)
* Uninstall/remove the Mingw32 compiler (if not needed by another application)
* Uninstall CMake (if not required by another application)

# Installation of VLE

First, download the installer from this website
[vle-2.0.0-alpha1.exe](http://vle-project.org/pub/vle/2.0/2.0.0-alpha1/vle-2.0.0-alpha1.exe)
(380 MB) and install VLE in a path without spaces. For example use `c:\vle-2.0`
instead of the `c:\Program Files\vle-2.0`.

# What is available?

The previous executable install the CMake program, the Mingw32 compiler suite
and the libxml2, libboost and QT5 dependencies.
