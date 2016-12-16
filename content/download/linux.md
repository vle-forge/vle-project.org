+++
tags = [ "linux", "bsd", "debian", "ubuntu" ]
topics = [ "VLE 2.0", "Installation" ]
description = "How to install VLE on Debian, Ubuntu, BSD, etc."
date = "2016-12-16T15:13:50+01:00"
title = "POSIX installation"
+++

# Debian stable or Ubuntu stable

The source tree is currently hosted on [Github](https://github.com/vle-forge)
and [Sourceforge](https://sourceforge.net/projects/vle/).

First, download the source using Git:

    git clone git://github.com/vle-forge/vle.git
    git checkout -b master-2.0 origin/master-2.0

You can use the tar-ball too:

    wget http://vle-project.org/pub/vle/2.0/2.0.0-alpha1/vle-2.0.0-alpha1.tar.gz

Install dependencies (recent ubuntu/debian):

    apt-get install libxml2-dev libboost-dev cmake pkg-config g++ \
            qttools5-dev qttools5-dev-tools qtbase5-dev qtbase5-dev-tools \
            qtchooser qt5-default

Once you have met requirements, compiling and installing is simple:

    cd vle
    mkdir build
    cd build
    export QT_SELECT=qt5
    cmake -DCMAKE_INSTALL_PREFIX=/usr/local -DCMAKE_BUILD_TYPE=RelWithDebInfo ..
    make -j4
    make install
    make test
