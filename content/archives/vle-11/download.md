+++
topics = ["documentation"]
tags = ["vle-1.1", "download"]
title = "vle 1.1"
+++

## Download

_VLE_ includes VLE (command line interface), GVLE (graphical user
interface) and the VFL (full C++ API to model and to simulate). _RVLE_
is the R package to bind (R)[https://www.r-project.org/] and
VLE. _PyVLE_ is the python package to bind Python and VLE. Finally,
_package_ is a lot of extensions and examples.

Windows (32bits binaries for Windows 7, 8, 10):

- [vle-1.1.3.exe](http://www.vle-project.org/pub/vle/1.1/1.1.3/vle-1.1.3.exe)
- [rvle_1.1.3-0.zip](http://www.vle-project.org/pub/vle/1.1/1.1.3/rvle_1.1.3-0.zip)

Sources (See the the README files in all tarballs):

* [vle-1.1.3.tar.gz](http://www.vle-project.org/pub/vle/1.1/1.1.3/vle-1.1.3.tar.gz)
* [rvle_1.1.3-0.tar.gz](http://www.vle-project.org/pub/vle/1.1/1.1.3/rvle_1.1.3-0.tar.gz)
* [pyvle-1.1.3.tar.gz](http://www.vle-project.org/pub/vle/1.1/1.1.3/pyvle-1.1.3.tar.gz)

## Requirements

Operating Systems supported by VLE are Linux/Unix and
Windows. Compilers used to build VLE and VLE Packages are :

* g++/clang on Linux/Unix
* Mingw32 on windows

The dependencies are:

* glibmm (>= 2.22)
* libxml2 (>= 2.8)
* libarchive (>= 2.0)
* boost (>= 1.41)
* cmake (>= 2.8.0)
* make (>= 1.8)
* c++ compiler (gcc >= 4.4, clang >= 3.1, intel icc (>= 11.0)
* any MPI 2 library as OpenMpi, mpich (for [mvle program](mvle))
* gtkmm (>= 2.22.0) (for [gvle program](gvle)).

## Changes from VLE 1.0

- From VLE 1.1, the extension (FSA, Petri net, Difference Equation,
  etc.) are provided into packages. A package can provides simulators,
  data, documentation, headers and static libraries. A package can
  depends of another package to be build and to be use at run-time of
  the simulation.
- The package can now be installed from remote repositories with the
  command line interface or via GVLE. Packages and theirs build
  dependencies and run-time dependencies are automatically downloaded
  and build.
- To improve the stability of VLE, We merge all shared libraries of
  vle (libvleutils, libvlevpz, libvledevs etc.) into an unique shared
  library called `libvle-1.1.so` or `vle-1.1.dll`. We provide a
  archive called `vle-1.1.a` or `vle-1.1.lib`.
- We remove the Eov program and the libvleeov shared library. Now,
  graphical output are available into the GVLE application.
- Add a dependency to the `boost::Asio` library. Now, VLE depends on
  Asio library to download data over http protocol.
- Add a dependency to the [libarchive](http://libarchive.github.com/)
  library to extract gzip, bzip2 tarball and Zip archives from the
  remote repositories.
- Add an MPI mode with the command line interface MPI. For MPI, VLE
  depends of an MPI library.
- We replace the init and finalize functions in old libvleutils,
  libvlevalue, libvlemanager with a new classical object.
- Add a new RemoteMananger class to access remote repositories. The
  command line interface is inspirited from the apt-get debian's
  command:

        $ vle --remote update
        $ vle --remote install glue
        $ vle --remote search '*gl*'
        $ vle --remote show glue

- Change the packages directory name. To allow the use of VLE 1.0 and
  1.1 on the same `VLE_HOME` directory, we need to clearly split the
  packages from the two versions. We add in the VLE's version.hpp
  file, a macro `VLE_ABI_VERSION` equal to
  `VLE_VERSION_MAJOR.VLE_VERSION_MINOR`. We use this macro to define
  the name of the pkgs directory. For example, in VLE 1.1, the package
  directory is defined as `vle/pkgs-1.1` and in VLE 1.2, the package
  directory is defined as `vle/pkgs-1.2`. The current stable version
  of VLE is not change and use packages in `vle/pkgs` directory.
- Remove Socket and Hosts classes. In VLE 1.1, we remove distant
  access to OOV and EOV. Thus, the `utils::Socket` and `utils::Hosts`
  are useless.
- Rewrite the Manager system: Add a new Manager class to improve the
  stability of the API. The manager class allows to run in thread and
  MPI mode the experimental frames.
  - Add a Simulation class to replace JustRun and Run classes.
  - Update the Types available in Manager. We prefer use the Matrix
    value instead of the OutputMatrix of the Oov namespace. Add
    operator and, or, xor, equal and different between
    SimulationOptions and LogOptions to ensure correct type casting.
- VPZ: Remove any reference to distant and local dynamics plugins and
  merge the libgraph.
- extension, geometry, eov and graph are removed.
