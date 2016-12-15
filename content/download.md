+++
tags = [ "vle-2.0"]
topics = [ "download"]
description = "How to install VLE-2.0"
date = "2016-12-15T16:44:07+01:00"
title = "download"
+++

## How to install

### Linux, BSD

* libxml2 (≥ 2.8)
* boost (≥ 1.47)
* cmake (≥ 3.0)
* c++ compiler (gcc ≥ 4.9, clang ≥ 3.3, intel icc (≥ 11.0)

For the MPI command line:

* Any MPI 2 library as OpenMpi, mpich

For the GUI:

* Qt5

The source tree is currently hosted on Github and Sourceforge. To view
the repository online: https://github.com/vle-forge/vle The URL to
clone it:

    git clone git://github.com/vle-forge/vle.git
    git checkout -b master-2.0 origin/master-2.0

Install dependencies (recent ubuntu/debian):

    apt-get install libxml2-dev libboost-dev cmake pkg-config g++ \
            qttools5-dev qttools5-dev-tools qtbase5-dev qtbase5-dev-tools \
            qtchooser qt5-default

Once you have met requirements, compiling and installing is simple:

    cd vle
    mkdir build
    cd build
    export QT_SELECT=qt5
    cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=RelWithDebInfo ..
    make
    make install
