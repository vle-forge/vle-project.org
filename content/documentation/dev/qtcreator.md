+++
topics = ["documentation"]
tags = ["qt", "gvle"]
description = "Qt Creator IDE to develop VLE, GVLE and plug-ins"
date = 2017-03-29T11:07:51+02:00
title = "Qt Creator support"
+++

Since version 2.0, VLE supports the [Qt Creator IDE](https://www.qt.io/ide/) and
qmake. Qt Creator is a cross-platform IDE that includes productivity tools to
speed up development time. Thanks to qmake, an Official support for MacOS10
should appear in future releases. CMake remains the official project generator
but qmake allow quick development of GVLE or GVLE's plug-ins.

Installation
============

Install **Qt Creator** with Qt5 development files from your package manager on
Linux or from the [Qt website](https://www.qt.io/ide/) on MacOS or Windows then,
import VLE from the Git version control. Be sure you have install libxml2 and
the boost libraries and you may configure and build the VLE project.

Linux
-----

Under Linux, the default installation is done in the `$HOME/usr` prefix.
To enable the use of the debugger, you may add a `make install`
deployment pre-process and use the `$PREFIX/usr/bin/gvle` executable in
the executable project settings.

{{< fluid_img class="pure-u-1-1" src="../qt-creator-00.png" caption="Initialize the debugger settings" >}}
