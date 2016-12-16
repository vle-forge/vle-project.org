+++
tags = [ "Windows", "POSIX" ]
topics = [ "Download"]
description = "How to install VLE-2.0"
date = "2016-12-15T16:44:07+01:00"
title = "Download"
+++

Quick installation links: [Windows](windows), [Linux](linux)

# Dependencies

Strong dependencies:

* libxml2 (≥ 2.8)
* boost (≥ 1.47)
* cmake (≥ 3.0)
* C++14 compiler (gcc ≥ 4.9, clang ≥ 3.3, intel icc (≥ 11.0)

For the MPI command line:

* Any MPI 2 library sush as [OpenMpi](https://www.open-mpi.org/),
  [mpich](https://www.mpich.org/)

For the GUI:

* Qt5

# Building options

The examples of buildings process that are given into this page can be modified
by using arguments of cmake line :

* `-DWITH_GVLE`: ON by default. Enable the building of GVLE based on QT5.
* `-DWITH_TEST`: ON by default. Enable the compilation of unit tests.
* `-DWITH_DOXYGEN`: OFF by default. Enable the compilation doxygen source
  documentation.
* `-DWITH_MVLE`: OFF by default. Enable the compilation of the old cluster
  experimental tool.
* `-DWITH_CVLE`: OFF by default. Enable the compilation of the new cluster
  experimental tool.
* `-DWITH_WIN32_INSTALLER`: OFF by default. Enable the building of the NSIS
  installer.
