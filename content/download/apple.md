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

    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

Install [Xcode](https://developer.apple.com/xcode/) from the *App Store*
application then copy the source tree from [Github](https://github.com/vle-
forge) or from this website.

With Git:

    git clone git://github.com/vle-forge/vle.git
    cd vle
    git checkout -b master origin/master

With wget:

    wget http://vle-project.org/pub/vle/2.0/2.0.0-alpha1/vle-2.0.0-alpha1.tar.gz
    tar zxf vle-2.0.0-alpha1.tar.gz
    cd vle-2.0.0-alpha1

Install dependencies:

    brew install cmake libboost-dev qt5

Once you have met requirements, compiling and installing is simple:

    cd vle
    mkdir build
    cd build
    export QT_SELECT=qt5
    cmake -DCMAKE_INSTALL_PREFIX=/usr/local -DCMAKE_BUILD_TYPE=RelWithDebInfo ..
    make -j4
    make install
    make test
