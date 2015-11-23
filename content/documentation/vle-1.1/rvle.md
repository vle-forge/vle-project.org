+++
categories = ["documentation", "rvle"]
date = "2015-10-28T11:05:53+01:00"
description = "RVLE description"
keywords = ["r", "rvle"]
title = "RVLE"
+++

RVLE, is a [R Package](https://www.r-project.org/), to call [VLE]({{<
ref "about/vle-details.md" >}})'s API from
[R](https://www-r-project.org). This package allows to open packages,
to read VPZ, assign experimental conditions to the models, call the
simulator, build experimental frames and capture result of simulation
into matrix or dataframe.

# Usage

Documentation is included into the R package.

```R
help(rvle)
help(Rvle)
```

A simple example of the basic API usage:
```R
f <- rvle.open(file="test_simulation.vpz", pkg="test_port")
result <- rvle.run(f)
checkEquals(class(result$view), "data.frame")
```

# Install requirements for rvle (Windows)

* download [R](http://cran.rstudio.com/bin/windows/base/) and
  install it. You have to use the 32 bits application R i386.
* [install vle]({{< ref "documentation/vle-1.1/installation.md" >}}) 
* add an environment variable `VLE_HOME` with value
  `c:\users\login\vle` (replace `login` with your own login name). The
  directory must exist before launching application.
* install the R Package RUnit from the CRAN:

```R
install.packages("RUnit") #or use the menu 'Packages'
```

# Install rvle for Windows

* you can get Win32 binary of rvle on the 
[Download Page of vle-1.1](http://www.vle-project.org/vle-1.1)
* install rvle by choosing into the menu _install packages from local
  zip file_.


# Get source code

An archive of source code can be found on the 
[Download Page of vle-1.1](http://www.vle-project.org/vle-1.1) 

You can also get sources from  git repository 

```bash
git clone https://github.com/vle-forge/rvle.git
cd rvle/
git checkout -b v1.1 origin/v1.1 
```

# Install package for Linux

* install R
* install package RUnit
* <a href="#getcode">get source code</a>
* read the README.rst file at the root of the directory (rvle).

```bash
cd rvle/
./autogen.sh
cd ..
R CMD INSTALL rvle
```

# Generate binary on Win32 (not recommended)

It is assumed that you used the standard procedure described [here] 
({{< relref "documentation/vle-1.1/installation.md#buildwin32" >}}) to build vle. 

First, install <a href="#requirements">requirements</a> for rvle. Then,
use a MinGW shell, not that we used the windows prompt for vle .

```bash
export PATH=/C/MinGW/msys/1.0/bin:/c/Program\ Files/R/R-3.1.0/bin/:/c/Rtools/bin:/c/gtkmm/bin:/c/natifvle/install/vle/bin:$PATH
export PKG_CONFIG_PATH=/c/gtkmm/lib/pkgconfig:/C/MinGW/lib/pkgconfig:/c/natifvle/install/vle/lib/pkgconfig
export BOOST_ROOT=/C/natifvle/install/boost
cd /c/natifvle/rvle
./autogen.sh
./configure
cd ..
R CMD INSTALL --build rvle
```






