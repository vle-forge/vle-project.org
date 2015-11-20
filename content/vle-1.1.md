+++
categories = ["vle-1.1", "software"]
date = "2015-09-18T10:38:07+02:00"
draft = false
description = ""
keywords = ["vle", "download"]
title = "vle 1.1"
menu = "main"
+++

### Documentation

All documentation about packages, VLE, GVLE, PyVLE, RVLE, VPZ file format,
command line interface are available is the [specific documentation]({{< ref
"documentation/vle-1.1.md">}}) page.

### Download

#### VLE (includes VLE, GVLE, VFL)

| OS | URL |
| ---| --- |
| Windows | [vle-1.1.2-Windows.exe](http://www.vle-project.org/pub/vle/1.1/1.1.2/vle-1.1.2-Windows.exe) |
| Sources | [vle-1.1.2.tar.gz](http://www.vle-project.org/pub/vle/1.1/1.1.2/vle-1.1.2.tar.gz) |

#### RVLE (R Package to bind R and VLE)

| OS | URL |
| ---| --- |
| Windows | [rvle_1.1.2-0.zip](http://www.vle-project.org/pub/vle/1.1/1.1.2/rvle_1.1.2-0.zip) |
| Sources | [rvle_1.1.2-0.tar.gz](http://www.vle-project.org/pub/vle/1.1/1.1.2/rvle_1.1.2-0.tar.gz) |

#### PyVLE (Python binding)

| OS | URL |
| ---| --- |
| Sources | [pyvle-1.1.2.tar.gz](http://www.vle-project.org/pub/vle/1.1/1.1.2/pyvle-1.1.2.tar.gz) |

#### Packages (examples and extensions)

| OS | URL |
| ---| --- |
| Windows | [packages-1.1.2.zip](http://www.vle-project.org/pub/vle/1.1/1.1.2/packages-1.1.2.zip) |
| Sources | [packages-1.1.2.tar.gz](http://www.vle-project.org/pub/vle/1.1/1.1.2/packages-1.1.2.tar.gz) |


### Installation

#### Linux

- To use VLE 1.1 on linux, you need to build vle. See the
  [technical documentation for building vle](https://github.com/vle-forge/vle/wiki/Get-vle-from-sources-for-vle-1.1)

- To install RVLE 1.1, you can follow the instructions given here:
  [installing rvle](https://github.com/vle-forge/vle/wiki/rvle-port-for-vle-1.1)

#### Windows

##### Upgrading from VLE 1.0

- Uninstall the previous version
- Remove the remaining variable `PKG_CONFIG_PATH` (only earlies versions)
- Uninstall/remove the Mingw compiler (if not needed by another application)
- Uninstall Cmake (if not required by another application)
- Follow the next sections for installation

##### Installation of VLE

- Download the binary file (`vle-X.X.X-Windows-x86.exe` see above)
  where `X.X.X` is the last version.
- Install VLE, it is is highly recommended to not to use a path that
  contains spaces (e.g. change the path `c:\Program Files\vle-X.X.X`
  to `c:\vle-X.X.X`).

##### Installation requirement for RVLE

- Download R [here](http://cran.rstudio.com/bin/windows/base/) and
  install it. To use rvle, you have to use the 32 bits application R
  i386.
- Add an environment variable `VLE_HOME` with value
  `c:\users\login\vle` (replace `login` with your own login name). The
  directory must exist before launching application.
- Install the R Package RUnit from the CRAN:

        $ install.packages("RUnit") or use the menu 'Packages'

##### Installation of RVLE

- Download rvle (with the same version numbers as vle)
- Install rvle by choosing into the menu _install packages from local
  zip file_.

### Release highlights

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
- VPZ: Remove any reference to distant and local dynamics plugins and merge the
  libgraph.
- extension, geometry, eov and graph are removed.
