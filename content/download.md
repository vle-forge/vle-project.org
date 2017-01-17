+++
tags = [ "MacOS", "Windows", "POSIX" ]
topics = [ "Download"]
description = "How to install VLE-2.0 ?"
date = "2016-12-15T16:44:07+01:00"
title = "Download"
+++

<center>

| [<i class="fa fa-apple fa-5x" aria-hidden="true"></i>](apple) | [<i class="fa fa-linux fa-5x" aria-hidden="true"></i>](linux) | [<i class="fa fa-windows fa-5x" aria-hidden="true"></i>](windows) |
| :---: | :---: | :-----: |
| [OS X 10.10 or higher](apple) | [Linux](linux) | [Windows 7 or higher](windows) |

</center>

# Dependencies

Strong dependencies:

* libxml2 (≥ 2.8)
* boost (≥ 1.47)
* [CMake](https://cmake.org/) (≥ 3.0)
* C++14 compiler (gcc ≥ 4.9, clang ≥ 3.3, intel icc (≥ 11.0)

Optional MPI dependency for cluster:

* Any MPI2 library sush as [OpenMpi](https://www.open-mpi.org/),
  [mpich](https://www.mpich.org/)

Optional GVLE support:

* [Qt5](https://doc.qt.io/qt-5/)

# Building options

For each platform, building process can be controlled by using arguments of
[CMake](https://cmake.org/) line :

* `-DWITH_GVLE`: ON by default. Enable the building of GVLE based on QT5.
* `-DWITH_TEST`: ON by default. Enable the compilation of unit tests.
* `-DWITH_DOXYGEN`: OFF by default. Enable the compilation
  [doxygen](http://www.stack.nl/~dimitri/doxygen/) source documentation.
* `-DWITH_MVLE`: OFF by default. Enable the compilation of the old cluster
  experimental tool.
* `-DWITH_CVLE`: OFF by default. Enable the compilation of the new cluster
  experimental tool.
* `-DWITH_WIN32_INSTALLER`: OFF by default. Enable the building of the NSIS
  installer.

For example, to build VLE, GVLE, CVLE and MVLE with GCC heavy optimization
flags:

```bash
export CXXFLAGS=$(gcc -### -E - -march=native 2>&1 | sed -r '/cc1/!d;s/(")|(^.* - )|( -mno-[^\ ]+)//g')

cmake -DCMAKE_INSTALL_PREFIX=/usr/local \
      -DCMAKE_EXPORT_COMPILE_COMMANDS=ON \
      -DWITH_GVLE=ON \
      -DWITH_CVLE=ON \
      -DWITH_MVLE=ON \
      -DCMAKE_BUILD_TYPE=Release \
      ..
```
