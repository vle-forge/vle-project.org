+++
description = "How to install VLE on MacOS X ?"
date = "2017-11-13T10:47:32+01:00"
title = "MacOS X Installation"
tags = [ "macos", "apple"]
topics = [ "VLE 2.0", "Installation" ]
+++

The installation of VLE 2.0 on MacOS requires to get and compile the
source code of VLE 2.0. This process requires the use of
[Homebrew](https://brew.sh/) to install the dependencies: git, CMake,
Boost and QT5. Tests are made with the [Xcode
application](https://developer.apple.com/xcode/) from the MacOS *App
Store*. However, the Homebrew gcc compiler suite seems to work too.

# First installation

First time you install VLE 2.0. you need to install VLE's dependencies, get the
source with Git, configure your environment the install VLE.

## Install dependencies

Install [Homebrew](http://brew.sh/). Open Terminal and copy/paste the following
line and type enter:

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Then, into the same Terminal, copy/paste the following lines to
install VLE's dependencies:

```bash
brew update
brew upgrade
brew install cmake libxml2 boost pkgconfig qt5 git
```

If you want to use `gcc` instead of the [Xcode
application](https://developer.apple.com/xcode/) (available from the
MacOS App Store), copy/paste the following line:

```bash
brew install gcc
```

## Get and build VLE

From the `$HOME/vle` path, we use git to download source code of VLE and install
under the `$HOME/usr` path:

```bash
cd $HOME
git clone git://github.com/vle-forge/vle.git
cd vle
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX=$HOME/usr -DCMAKE_BUILD_TYPE=RelWithDebug ..
make -j4
make install
```

## Configure the environment

Into your `$HOME/.bashrc` or equivalent, write the following line:

```bash
export CMAKE_PREFIX_PATH=/usr/local/Cellar/qt/5.9.2
export PATH=$PATH:$HOME/usr/bin:/usr/local/Cellar/qt/5.9.2/bin
export DYLD_LIBRARY_PATH=$DYLD_LIBRARY_PATH:$HOME/usr/lib
export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:$HOME/usr/lib/pkgconfig:/usr/local/opt/libxml2/lib/pkgconfig:/usr/local/opt/qt/lib/pkgconfig
```

Then into your `$HOME/.bash_profile`, add the following line if not present:
```bash
if [ -f $HOME/.bashrc ]
then
        source $HOME/.bashrc
fi
```

Now, you can use `vle-2.0` and `gvle-2.0` from the Terminal application.

# Upgrade installation

To upgrade installation, first update the Homebrew installation. In the Terminal
application, copy/paste the following line et type enter:

```bash
brew update
brew upgrade
```

The, go into the `vle` source directory, update the source with git then rebuild
VLE:

```bash
cd $HOME/vle
git pull -r
rm -fr build
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX=$HOME/usr -DCMAKE_BUILD_TYPE=RelWithDebug ..
make -j4
make install
```
