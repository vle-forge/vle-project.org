+++
date = 2016-12-15T16:44:07+01:00
title = "Download"
topics = ["documentation"]
tags = ["MacOS", "Windows", "Posix"]
description = "How to install VLE-2.0?"
markup = "mmark"
+++

Sources and Binaries
====================

VLE is available as source (`src` and needs to be compiled) or as binary (`bin` and just be executed) dependently to your platform.

| Name    | Details                      | Linux                                                                                               | Windows 7+                                                                                     | MacOSX 10.10+                                                                                  |
| ------- | ---------------------------- | --------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| VLE     | VFL, vle, gvle, mvle, cvle   | [tar.gz (src 961K)](http://www.vle-project.org/pub/vle/2.0/2.0.1/vle-2.0.1.tar.gz)                  | [exe (bin 257M)](http://www.vle-project.org/pub/vle/2.0/2.0.1/Setup-VLE_2_0_1.exe)             | [zip (src 1.3M)](http://www.vle-project.org/pub/vle/2.0/2.0.1/vle-2.0.1.zip)                   |
| PyVLE   | Python port                  | [tar.gz (src 86K)](http://www.vle-project.org/pub/vle/2.0/2.0.1/pyvle-2.0.1.tar.gz)                 | [zip (src 102K)](http://www.vle-project.org/pub/vle/2.0/2.0.1/pyvle-2.0.1.zip)                 | [zip (src 102K)](http://www.vle-project.org/pub/vle/2.0/2.0.1/pyvle-2.0.1.zip)                 |
| Rvle    | R port                       | [tar.gz (src 101K)](http://www.vle-project.org/pub/vle/2.0/2.0.1/rvle_2.0.1-6.tar.gz)               | [zip (bin 4.5M)](http://www.vle-project.org/pub/vle/2.0/2.0.1/rvle_2.0.1-6.zip)                | [tar.gz (src 101K)](http://www.vle-project.org/pub/vle/2.0/2.0.1/rvle_2.0.1-6.tar.gz)          |

Installation details for each platform:

- [Linux](linux)
- Minimum [Windows 7+](windows)
- Minimum [OSX 10.10+](apple)

Dependencies
============

Strong dependencies:

- libxml2 (≥ 2.8)
- boost (≥ 1.49)
- [CMake](https://cmake.org/) (≥ 3.0)
- C++14 compiler (gcc ≥ 5.0, clang ≥ 3.3, intel icc (≥ 11.0)

Optional MPI dependency for cluster:

- Any MPI2 library sush as [OpenMpi](https://www.open-mpi.org/), [mpich](https://www.mpich.org/)

Optional GVLE support:

- [Qt5](https://doc.qt.io/qt-5/)
- [Qt Creator IDE](https://www.qt.io/ide/)

Building options
================

For each platform, building process can be controlled using arguments of [CMake](https://cmake.org/) line:

| Options                  | Default value | Description                                                                                   |
|--------------------------|---------------|-----------------------------------------------------------------------------------------------|
| `-DWITH_GVLE`            | ON            | Enable the building of GVLE based on QT5.                                                     |
| `-DWITH_TEST`            | ON            | Enable the compilation of unit tests.                                                         |
| `-DWITH_DOXYGEN`         | OFF           | Enable the compilation [doxygen](http://www.stack.nl/~dimitri/doxygen/) source documentation. |
| `-DWITH_MVLE`            | OFF           | Enable the compilation of the old cluster experimental tool.                                  |
| `-DWITH_CVLE`            | OFF           | Enable the compilation of the new cluster experimental tool.                                  |

Examples
========

To build VLE, GVLE, CVLE and MVLE with heavy optimization flags GCC:

``` bash
export CXXFLAGS=$(gcc -### -E - -march=native 2>&1 | sed -r '/cc1/!d;s/(")|(^.* - )|( -mno-[^\ ]+)//g')

cmake -DCMAKE_INSTALL_PREFIX=/usr/local \
      -DCMAKE_EXPORT_COMPILE_COMMANDS=ON \
      -DCMAKE_COLOR_MAKEFILE=ON \
      -DCMAKE_VERBOSE_MAKEFILE=OFF \
      -DWITH_GVLE=ON \
      -DWITH_CVLE=ON \
      -DWITH_MVLE=ON \
      -DCMAKE_BUILD_TYPE=Release \
      ..
```

To build only VLE with debug flags with `clang++`:

``` bash
export CXX=clang++
export CC=clang

cmake -DCMAKE_INSTALL_PREFIX=/usr/local \
      -DCMAKE_EXPORT_COMPILE_COMMANDS=ON \
      -DCMAKE_COLOR_MAKEFILE=ON \
      -DCMAKE_VERBOSE_MAKEFILE=OFF \
      -DCMAKE_BUILD_TYPE=Debug \
      ..
```
