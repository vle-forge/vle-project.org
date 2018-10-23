+++
tags = [ "linux", "bsd", "debian", "ubuntu" ]
topics = [ "VLE 2.0", "Installation" ]
description = "How to install VLE on Debian, Ubuntu, BSD, etc. ?"
date = "2016-12-16T15:13:50+01:00"
title = "POSIX installation"
+++

# Get the source

VLE First, copy or update the source tree from [Github](https://github.com/vle-
forge).

**With Git**

````bash
cd $HOME

# you never git clone vle, the use git clone:
git clone git://github.com/vle-forge/vle.git
cd vle

# else, just update vle from git:
cd vle
git pull -r
````

**With Wget or Curl**

````bash
cd $HOME
wget http://vle-project.org/pub/vle/2.0/2.0.1/vle-2.0.1.tar.gz
tar zxf vle-2.0.1.tar.gz
cd vle-2.0.1
````

# Install dependencies

## Ubuntu 16.04 and Debian 8 *Jessie*

For [Ubuntu 16.04](http:://www.ubuntu.com) or [Debian GNU/Linux 8](http://www.debian.org):


````bash
sudo apt-get update
sudo apt-get install curl libxml2-dev libboost-dev cmake pkg-config g++ \
            qttools5-dev qttools5-dev-tools qtbase5-dev qtbase5-dev-tools \
            qtchooser qt5-default libqt5svg5-dev
````

## Debian 7 *Wheezy*

For the [Debian old](https://www.debian.org/releases/wheezy/), VLE 2 can compile with `clang++` and `libc++`:


````bash
sudo apt-get update
sudo apt-get install curl libxml2-dev libboost-dev cmake pkg-config clang++ libc++-dev linv++abi-dev \
            qttools5-dev qttools5-dev-tools qtbase5-dev qtbase5-dev-tools \
            qtchooser qt5-default

export CXX=clang++-libc++
export CC=clang
````

## Ubuntu 14.04

For [Ubuntu 14.04](http:://www.ubuntu.com), we need a recent C++14 compiler. We
propose the use of the [Ubuntu Toolchain test
builds](https://launchpad.net/~ubuntu- toolchain-r/+archive/ubuntu/test). So,
use the following instructions.

````bash
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get install curl libxml2-dev libboost-dev cmake pkg-config g++ \
     qttools5-dev qttools5-dev-tools qtbase5-dev qtbase5-dev-tools \
     qtchooser qt5-default g++-6 gcc-6 gcc-4.8 g++-4.8

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-6 60 --slave /usr/bin/g++ g++ /usr/bin/g++-6
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 60 --slave /usr/bin/g++ g++ /usr/bin/g++-4.8
sudo update-alternatives --config gcc
````

# Build the code

Once you have met requirements, compile and install VLE using the following
command:

````bash
cd vle                   # or cd vle-2.0.1 is you use wget
mkdir build && cd build
export QT_SELECT=qt5

cmake -DCMAKE_INSTALL_PREFIX=/usr/local -DCMAKE_BUILD_TYPE=RelWithDebInfo ..

make -j4
make install
make test
````

If you install VLE outside `/usr` like above, you must define these
variables into your `.bashrc` or equivalent. For example, with
`prefix=/usr/local`:

````bash
export PATH=/usr/local/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH
export MANPATH=/usr/local/man
export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig
````
