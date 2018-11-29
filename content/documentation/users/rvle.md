+++
topics = ["documentation"]
date = "2016-12-16T12:32:04+01:00"
description = "RVLE description"
tags = ["r", "rvle"]
title = "rvle"
+++

RVLE, is a [R Package](https://www.r-project.org/), to call VLE's API from
[R](https://www-r-project.org). This package allows to open packages, to read
VPZ, assign experimental conditions to the models, call the simulator, build
experimental frames and capture result of simulation into matrix or dataframe.

# Installation

## Windows

* Download [R](http://cran.rstudio.com/bin/windows/base/) and
  install it. You have to use the 32 bits application R i386.
* [install vle](../installation)
* add an environment variable `VLE_HOME` with value
  `c:\users\login\vle` (replace `login` with your own login name). The
  directory must exist before launching application.
* install the R Package RUnit from the CRAN:
* [Download RVLE](http://vle-project.org/pub/vle/2.0/2.0.0-alpha1/rvle-2.0.0_0.zip).
* install rvle by choosing into the menu _install packages from local
  zip file_.


## Linux/Unix

You can get source code of RVLE from the Git repository or using the tar ball
release.

    git clone https://github.com/vle-forge/rvle.git
    cd rvle
    git checkout -b master-2.0 origin/master-2.0

Or by wget/curl:

    wget http://vle-project.org/pub/vle/2.0/2.0.0-alpha1/rvle-2.0.0_0.tar.gz

* install R
* install package RUnit
* read the README.rst file at the root of the directory (rvle)

```
cd rvle/
./autogen.sh
cd ..
R CMD INSTALL rvle
```

# Usage

Documentation is included into the R package.

    help(rvle)
    help(Rvle)

A simple example of the basic API usage:

    f <- rvle.open(file="test_simulation.vpz", pkg="test_port")
    result <- rvle.run(f)
    checkEquals(class(result$view), "data.frame")

