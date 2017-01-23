+++
title = "VLE 2.0.0 alpha1"
tags = ["release", "vle-2.0"]
description = ""
topics = ["VLE 2.0"]
date = "2017-01-23T10:02:33+01:00"
+++


The first alpha stable version of VLE is available. This version introduces new
stable API, new GUI, new features.

More details on the [VLE 2.0](../../vle-20) page. The
source are available in [Github](https://github.com/vle-forge/).

Please try it!

----

**Public API changes are important**

* C++11/14 is now the default for the API and all public pointer are
  managed with `std::unique_ptr` and `std::shared_ptr` to limit user
  memory management.
* Many public API are move into the darkness.
* All singleton are removed.
* Public API depends only of the standard C++.

**GVLE2**

VLE comes with a new graphical user interface in Qt5.

**Threaded kernel**

Parallelization is available with threads in the simulation kernel. It
is the more pessimist parallelization approach and gains are obtained
with big models, costly transition functions and big PDEVS bags (many
transitions to a same date).

**System package**

The VLE framework comes with some packages installed in the
`$prefix/lib/vle-2.0/pkgs`.

* `vle.adaptative-qss` To model DEVS model without coding in C++ as in
  [PowerDEVS](https://sourceforge.net/projects/powerdevs/).
* `vle.output` To store observation into files or memory (useful for R
  and Python portage).

**Debug mode**

The new *Debug* system is available at run-tine. We replace the C++
`DECLARE_DYNAMICS_DBG` macros with a new element in the structure of
the model. This change can be found in the VPZ API and VPZ file
format.

**Observation**

Observations can now be done one each DSDE functions (internal,
external or confluent transitions or output).

**Model in executable**

The new API can load symbol into the main program instead of the
shared libraries specified by the package information. So, no package
and no shared libraries are necessary.

**Build and run-time dependencies are reduced**

* *libarchive* and all *libboost* binary dependencies are removed.

----

More details on the [VLE 2.0](../../vle-20) page.

As usual, the source are available in [Github](https://github.com/vle-forge/)
or on [this server](http://www.vle-project.org/pub/vle-2.0/vle-2.0.0-alpha1).
