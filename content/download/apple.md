+++
description = "How to install VLE on MacOS X ?"
date = "2016-12-19T11:13:52+01:00"
title = "MacOS X Installation"
tags = [ "macos", "apple"]
topics = [ "VLE 2.0", "Installation" ]
+++

# Not alpha installation

Install [Homebrew](http://brew.sh/). Open Terminal and copy/paste the following
line and type enter.

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Install [Xcode](https://developer.apple.com/xcode/) from the *App Store*
application then copy the source tree frpm [Github](https://github.com/vle-
forge) or from this website.

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
Install dependencies:


```bash
brew install cmake libboost-dev qt5
```

Once you have met requirements, compiling and installing is simple:

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
