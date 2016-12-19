+++
tags = [ "linux", "bsd", "debian", "ubuntu" ]
topics = [ "VLE 2.0", "Installation" ]
description = "How to install VLE on Debian, Ubuntu, BSD, etc. ?"
date = "2016-12-16T15:13:50+01:00"
title = "POSIX installation"
+++

# Debian stable or Ubuntu stable

First, copy the source tree frpm [Github](https://github.com/vle-forge) or from
this website.

```bash
# With Git
git clone git://github.com/vle-forge/vle.git
cd vle
git checkout -b master-2.0 origin/master

# Or with wget:
wget http://vle-project.org/pub/vle/2.0/2.0.0-alpha1/vle-2.0.0-alpha1.tar.gz
tar zxf vle-2.0.0-alpha1.tar.gz
cd vle
```

For [Ubuntu 16.04](http:://www.ubuntu.com) or [Debian GNU/Linux 8](http://www.debian.org):

```bash
sudo apt-get update
sudo apt-get install libxml2-dev libboost-dev cmake pkg-config g++ \
        qttools5-dev qttools5-dev-tools qtbase5-dev qtbase5-dev-tools \
        qtchooser qt5-default
```

For [Ubuntu 14.04](http:://www.ubuntu.com), we need a recent C++14 compiler. We
propose the use of the [Ubuntu Toolchain test
builds](https://launchpad.net/~ubuntu- toolchain-r/+archive/ubuntu/test). So,
use the following instructions.

```bash
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get install libxml2-dev libboost-dev cmake pkg-config g++ \
        qttools5-dev qttools5-dev-tools qtbase5-dev qtbase5-dev-tools \
        qtchooser qt5-default g++-6 gcc-6 gcc-4.8 g++-4.8

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-6 60 --slave /usr/bin/g++ g++ /usr/bin/g++-6
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 60 --slave /usr/bin/g++ g++ /usr/bin/g++-4.8
sudo update-alternatives --config gcc
```

Once you have met requirements, compile and install VLE using the following
command:

```bash
cd vle
mkdir build
cd build
export QT_SELECT=qt5
cmake -DCMAKE_INSTALL_PREFIX=/usr/local -DCMAKE_BUILD_TYPE=RelWithDebInfo ..
make -j4
make install
make test
```
