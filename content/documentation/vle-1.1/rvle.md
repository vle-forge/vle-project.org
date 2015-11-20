+++
categories = ["documentation", "rvle"]
date = "2015-10-28T11:05:53+01:00"
description = "RVLE description"
keywords = ["r", "rvle"]
title = "rvle"
+++

RVLE, is an [R Package](https://www.r-project.org/), to call [VLE]({{<
ref "about/vle-details.md" >}})'s API from
[R](https://www-r-project.org). This package allows to open packages,
to read VPZ, assign experimental conditions to the models, call the
simulator, build experimental frames and capture result of simulation
into matrix or dataframe.

### Install

Install VLE first then, install rvle from the source.

```bash
git clone https://github.com/vle-forge/rvle.git
cd rvle/
git checkout -b v1.1 origin/v1.1
./autogen.sh
cd ..
R CMD INSTALL rvle
```

### Usage

```R
f <- rvle.open(file="test_simulation.vpz", pkg="test_port")
result <- rvle.run(f)
checkEquals(class(result$view), "data.frame")
```
