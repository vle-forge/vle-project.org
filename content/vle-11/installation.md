+++
topics = ["documentation"]
tags = ["vle-1.1","installation"]
title = "installation"

+++

# Installation on Windows.

## Upgrading from VLE 1.0 (optionnal)

* Uninstall the previous version
* Remove the remaining variable `PKG_CONFIG_PATH` (only earlies versions)
* Uninstall/remove the Mingw compiler (if not needed by another application)
* Uninstall Cmake (if not required by another application)
* Follow the next sections for installation

## Installation of VLE

* Download the [binary file](download)
(`vle-1.1.X-Windows-x86.exe`) where `1.1.X` is the last version.
* Install VLE, it is is highly recommended to not to use a path that
  contains spaces (e.g. change the path `c:\Program Files\vle-1.1.X`
  to `c:\vle-1.1.X`).

# Get source code
You can get sources from either the git repository

```bash
git clone https://github.com/vle-forge/vle.git
cd vle/
git checkout -b v1.1.2 v1.1.2
```

Or the source archive :

* Download VLE-1.1 on the [Download Page](download)
* Decompress the archive (use eg. `tar xfz` on linux or `7zip` on windows)

# Building options.

The examples of buildings process that are given into this page can be modified
by using arguments of cmake line :

* `-DWITH_MPI` : if OFF , the mpi application `mvle` will not be built, if ON it
  will require that mpi is installed on your computer.
* `-DWITH_GTK` : if OFF, the gui application `gvle` will not be built, this can
  be useful if it is not required. For example if you just want to launch
simulations on a cluster, you do not need gvle for the design of the model.
* `-DWITH_GTKSOURCEVIEW` : on several linux OS gtksourceview which is used for
  the syntax highlighting on the gvle editor is not available. This option has no
  meanings if WITH\_GTK is OFF.
* `-DWITH_QT` : if OFF, the gui application `gvle2` will not be built, this can
  be useful if it is not required. For example if you just want to launch
  simulations on a cluster, you do not need gvle2 for the design of the model.

# Build on...
## Build on Debian Sid, Jessie and Wheezy

```bash
# install the dependencies
sudo aptitude install cmake g++ libgtkmm-2.4-dev libglademm-2.4-dev \
  libgtksourceview2.0-dev libboost-dev libboost-serialization-dev \
  libboost-date-time-dev libboost-filesystem-dev libboost-test-dev \
  libboost-regex-dev libboost-program-options-dev libboost-thread-dev \
  libboost-mpi-dev libboost-graph-dev libboost-serialization-dev \
  libboost-chrono-dev libarchive-dev libasio-dev libopenmpi-dev openmpi-bin
# download and build VLE
cd vle-1.1
mkdir build
cd build
cmake -DWITH_GTKSOURCEVIEW=ON -DWITH_GTK=ON -DWITH_CAIRO=ON -DWITH_MPI=ON \
      -DCMAKE_BUILD_TYPE=RelWithDebInfo -DCMAKE_INSTALL_PREFIX=/usr ..
make
sudo make install
```

## Build on Ubuntu 12.04

```bash
# install the dependencies
sudo apt-get install cmake g++ libgtkmm-2.4-dev libgtksourceview2.0-dev \
  libglademm-2.4-dev libboost1.48-dev libboost-serialization1.48-dev \
  libboost-date-time1.48-dev libboost-filesystem1.48-dev libboost-test1.48-dev \
  libboost-regex1.48-dev libboost-program-options1.48-dev \
  libboost-thread1.48-dev libboost-chrono1.48-dev libarchive-dev
# download and build VLE
cd vle-1.1
mkdir build
cd build
cmake -DWITH_GTKSOURCEVIEW=ON -DWITH_GTK=ON -DWITH_CAIRO=ON -DWITH_MPI=ON \
      -DBUILD_SHARED_LIBS=ON -DCMAKE_BUILD_TYPE=RelWithDebInfo              \
      -DCMAKE_INSTALL_PREFIX=/usr ..
make
sudo make install
```

## Build on Ubuntu 14.04

```bash
# install the dependencies
sudo apt-get install cmake g++ libgtkmm-2.4-dev libglademm-2.4-dev \
  libgtksourceview2.0-dev libboost1.55-dev libboost-serialization1.55-dev \
  libboost-date-time1.55-dev libboost-filesystem1.55-dev \
  libboost-test1.55-dev libboost-regex1.55-dev \
  libboost-program-options1.55-dev libboost-thread1.55-dev \
  libboost-chrono1.55-dev libarchive-dev libqt4-dev
# build vle
cd vle
mkdir build
cd build
cmake -DWITH_GTKSOURCEVIEW=ON -DWITH_GTK=ON -DWITH_CAIRO=ON -DWITH_MPI=OFF \
      -DBUILD_SHARED_LIBS=ON -DCMAKE_BUILD_TYPE=RelWithDebInfo              \
      -DCMAKE_INSTALL_PREFIX=/usr ..
make
make install
```

# Building a Deb package (Ubuntu or Debian)

Rather than installing directly the binaries and include, you can build a Debian
package. Replace :

```bash
make
make install
```

With:

```bash
make
cpack -G DEB
sudo  dpkg -i vle-1.1-Linux-i686.deb
```

# Build on Win32 (not recommended)

You should consider using the binaries of vle.

1) Declare a build environment

```bash
set VLE_BUILD_ENV=c:\natifvle
```

2) Downloads and pre install

Get dependencies and dowload vle:

* Download Boost into `%VLE_BUILD_ENV%`      (e.g. boost_1_54_0)
* git clone vle sources into %VLE_BUILD_ENV% (e.g. dev)
* Install Mingw                              (e.g. mingw-get-inst-20120426.exe)
* Install gtkmm                              (e.g. gtkmm-win32-devel-2.22 .0-1.exe)
* Install gtksourcevieww                     (e.g. gtksourceview-2.10.0.zip)
* Install cmake                              (e.g. cmake-2.8.12-2)
* Install doxygen                            (e.g. latest doxygen version 1.8.6)

2.1) Download and install mingw : mingw-get-inst-20120426

```
** You can find it here :
** http://www.vle-project.org/pub/3rd-party
** During install:
** 1) use pre-packaged repository catalogues;
** 2) select C, C++, Fortran compilers, Msys (Msys is for rvle build only)
** 3) install into the default directory C:\MinGW
** 4) Do NOT Add C:\MinGW\bin to the path
```

2.2) Download and install CMake-2.8

```
** You can find it here :
** http://www.cmake.org/files/v2.8/cmake-2.8.11-win32-x86.exe
** or http://www.vle-project.org/pub/3rd-party
** During install:
** 1) choose install path c:\CMake
** 2) Do NOT Add C:\CMake\bin to the path
```

2.3) Install gtkmm binaries

```
** You can fing it here
** http://ftp.gnome.org/pub/GNOME/binaries/win32/gtkmm/2.22/gtkmm-win32-devel-2.22.0-2.exe
** During install, install into the default directory C:\gtkmm
```

2.4) Download `boost_1_54_0.zip` and unzip into `%VLE_BUILD_ENV%\boost_1_54_0`

2.5) Download doxygen-1.8.6 and install into the default installation directory

2.6) Download Gtksourceview-2.0

```
** You can fing it here
** http://ftp.acc.umu.se/pub/GNOME/binaries/win32/gtksourceview/2.10/gtksourceview-2.10.0.zip
** http://ftp.acc.umu.se/pub/GNOME/binaries/win32/gtksourceview/2.10/gtksourceview-dev-2.10.0.zip
** Unzip files into the default directory C:\gtkmm
** Copy libgtksourceview-2.0-0.dll into C:\gtkmm\redist
```

2.7) Clone VLE

```bash
git clone vle into %VLE_BUILD_ENV%\vle
```

3) Building script

```bash
set VLE_BUILD_ENV=c:\natifvle
set PKG_CONFIG_PATH=c:\gtkmm\lib\pkgconfig;C:\MinGW\lib\pkgconfig
set boostversion=1_54

set builddir="%VLE_BUILD_ENV%\build"
set sourcedir="%VLE_BUILD_ENV%\vle"
set installdir=%VLE_BUILD_ENV%\install
set boost_src="%VLE_BUILD_ENV%\boost_%boostversion%_0"
set boost_root="%VLE_BUILD_ENV%\install\boost"
set boost_include_path="%boost_root%\include"
set boost_library_path="%boost_root%\lib"
set vlepathtestbin=%installdir%\vle\bin
set cmakepath=c:\CMake
set OLDPATH=%PATH%
set PATH=c:\mingw\bin;%PATH%
set PATH=c:\gtkmm\bin;%PATH%
set PATH=%cmakepath%\bin;%PATH%
set PATH=%vlepathtestbin%;%PATH%

mkdir %builddir%\vle
mkdir %installdir%\vle

mingw-get install libarchive
mingw-get install gettext

cd %boost_src%\tools\build\v2
bootstrap.bat gcc
b2 toolset=gcc install --prefix=%boost_src%\b2
cd %boost_src%
b2\bin\b2 --toolset=gcc --with-date_time --with-filesystem --with-program_options --with-random --with-regex --with-system --with-test --with-thread --with-timer variant=release threading=multi link=shared runtime-link=shared stage
mkdir %boost_root%
mkdir %boost_include_path%
mkdir %boost_include_path%\boost
xcopy /E %boost_src%\boost %boost_include_path%\boost
xcopy /E %boost_src%\stage\lib %boost_library_path%\

cd %builddir%\vle
cmake.exe -G "MinGW Makefiles" -DWITH_MPI=OFF -DWITH_GTKSOURCEVIEW=ON -DWITH_DOXYGEN=ON -DCMAKE_INSTALL_PREFIX=%installdir%\vle -DCMAKE_BUILD_TYPE=RelWithDebInfo -DVLE_CMAKE_PATH="c:\cmake" -DVLE_MINGW_PATH="c:\mingw" -DVLE_GTK_PATH="c:\gtkmm" -DVLE_BOOST_INCLUDE_PATH=%boost_include_path% -DVLE_BOOST_LIBRARIES_PATH=%boost_library_path% %sourcedir%
mingw32-make install
mingw32-make test

cpack.exe -G NSIS
set PATH=%OLDPATH%
```

# Build for Win32 : cross compilation with MXE (not recommended, deprecated)

You should consider using the binaries of vle.

We use the [MXE Environment](http://mxe.cc/) to build the Windows 32 bits
binaries.

```bash
# Settings the MXE environment
export MXEENV=/cross/env
export VLEENV=/cross/env/vle

cd $MXEENV

# Install the dependencies
aptitude install -R autoconf automake bash bison bzip2 \
      flex gettext git g++ intltool \
      libtool libltdl-dev openssl libssl-dev \
      libxml-parser-perl make patch perl \
      pkg-config scons sed unzip wget \
      xz-utils yasm

# download the latest version of CMake and remove the installed version.
wget http://www.cmake.org/files/v2.8/cmake-2.8.9.tar.gz
tar zxf cmake-2.8.9.tar.gz
cd cmake-2.8.9
./booststrap && make -j 2 && sudo make install

# Build the cross compilation environment
cd $MXEENV
git clone -b stable https://github.com/mxe/mxe.git
cd mxe

# Cross compile the dependencies of VLE
make gcc JOBS=2
make gtkmm2 JOBS=2
make libxml2 JOBS=2
make gtksourceviewmm2 JOBS=2
make boost JOBS=2
make libarchive JOBS=2
make curl JOBS=2
make pthreads JOBS=2

# Assign environment variables to build VLE
export PATH=$MXEENV/mxe/usr/bin:$PATH
export PKG_CONFIG_PATH=/
export PKG_CONFIG_PATH_i686_pc_mingw32=$MXEENV/mxe/usr/lib/pkgconfig
export BOOST_ROOT=$MXEENV/mxe/usr/i686-pc-mingw32
export BOOST_INCLUDEDIR=$MXEENV/mxe/usr/i686-pc-mingw32/include
export BOOST_lIBRARYDIR=$MXEENV/mxe/usr/i686-pc-mingw32/lib

# Cross compile pkg-config
cd $MXEENV
wget http://pkgconfig.freedesktop.org/releases/pkg-config-0.27.1.tar.gz
tar zxf pkg-config-0.27.1.tar.gz
cd pkg-config-0.27.1
./configure --enable-static --disable-shared --host=i686-pc-mingw32 --prefix=$MXEENV/install
make
make install

# Cross compile VLE
cd $MXEENV
git clone git://github.com/vle-forge/vle.git

mkdir $MXEENV/build
cd $MXEENV/build
cmake -DCMAKE_BUILD_TYPE=Debug \
    -DBoost_USE_STATIC_LIBS=ON \
    -DBoost_USE_MULTITHREADED=ON \
    -DBoost_USE_STATIC_RUNTIME=OFF \
    -DWITH_MPI=OFF \
    -DWITH_TEST=OFF \
    -DBUILD_SHARED_LIBS=OFF \
    -DMXE_PATH=$MXEENV/mxe/usr/i686-pc-mingw32 \
    -DPKG_CONFIG_EXE_PATH=$MXEENV/install/bin \
    -DCMAKE_TOOLCHAIN_FILE=$MXEENV/mxe/usr/i686-pc-mingw32/share/cmake/mxe-conf.cmake \
    -DCMAKE_INSTALL_PREFIX=$MXEENV/install \
    $VLEENV
make VERBOSE=1 -j 2 && make install
```

To complete the compilation process, use one of the two solutions.

For users (recommended), generate a windows installer which can be exuted

```bash
cpack -G NSIS
```

For developers only, we rely on a shared directory (in this example:
/cross/shared) between the linux host  and a windows virtual machine drive
(in this example: z:).

```bash
ln -s  $MXEENV/install /cross/shared
```

On the windows virtual machine, one has to set the registry key used by vle:

For windows 32 bits, execute the .reg file:

```bash
Windows Registry Editor Version 5.00
[HKEY_LOCAL_MACHINE\SOFTWARE\VLE Development Team\VLE 1.1.0]
@="z:\\install"
"path"="Z:\\install"
```

For windows 64 bits, execute the .reg file:

```bash
Windows Registry Editor Version 5.00
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\VLE Development Team\VLE 1.1.0]
@="z:\\install"
"path"="Z:\\install"
```
