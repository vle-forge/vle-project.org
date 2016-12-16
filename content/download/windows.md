+++
tags = [ "windows" ]
topics = [ "VLE 2.0", "Installation" ]
description = "How to install VLE on Windows 7, 8, 10"
date = "2016-12-16T15:13:55+01:00"
title = "Windows Installation"
+++

# Uninstall VLE 1.0 or 1.1

If you have already install VLE 1.0 or VLE 1.1

* Uninstall the previous version
* Remove the remaining variable `PKG_CONFIG_PATH` (only earlies versions)
* Uninstall/remove the Mingw compiler (if not needed by another application)
* Uninstall Cmake (if not required by another application)

# Installation of VLE

* Download [vle-2.0.0-dev-x86.exe](http://vle-
  project.org/pub/2.0/vle-2.0.0-dev-x86.exe)
* Install VLE, it is is highly recommended to not to use a path that contains
  spaces. For example, change the path `c:\Program Files\vle-2.0` to
  `c:\vle-2.0`).
