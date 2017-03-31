+++
title = "Qt Creator suport"
tags = ["qt", "vle-2.0"]
description = ""
topics = ["VLE 2.0"]
date = "2017-03-31T11:18:09+02:00"
+++

The next vle-2.0.0-alpha2 will support the Qt Creator IDE to allow easy
development of VLE and/or plug-ins. The [patch](https://github.com/vle-
forge/vle/commit/d63ea94ac5f013c7ad7ada641483e78fe4e83c7c) allows support of
the [Qt Creator IDE](https://www.qt.io/ide/) via qmake program and the
[`vle.pro`](https://github.com/vle-forge/vle/blob/d63ea94ac5f013c7ad7ada641483e78fe4e83c7c/vle.pro) file at root of the repository.

Qt Creator is a cross-platform IDE that includes productivity tools to speed up
development time. Thanks to qmake, an Official support for MacOS10 should
appear in future releases.

CMake remains the official project generator but qmake allow quick development
of GVLE or GVLE's plug-ins.
