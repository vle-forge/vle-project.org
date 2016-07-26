+++
date = "2016-07-26T10:52:53+02:00"
tags = ["release", "alpha", "vle-2.0"]
title = "VLE 2.0 alpha coming soon"
topics = ["VLE 2.0"]
description = "Version 2.0 will be declared as stable"
+++


The new stable version of VLE, now called 2.0 is coming soon. This
version introduces new stable API, new GUI, new features.

More details on the [VLE 2.0]({{< ref "vle-20.md" >}}) page. The
source are available in [Github](https://github.com/vle-forge/).

Please try it!

#### Public API changes are important

* C++11/14 is now the default for the API and all public pointer are
  managed with `std::unique_ptr` and `std::shared_ptr` to limit user
  memory management.
* Many public API are move into the darkness.
* All singleton are removed.
* Public API depends only of the standard C++.

#### Threaded kernel

Parallelization is available with threads in the simulation kernel. It
is the more pessimist parallelization approach and gains are obtained
with big models, costly transition functions and big PDEVS bags (many
transitions to a same date).

#### System package

The VLE framework comes with some packages installed in the
`$prefix/lib/vle-2.0/pkgs`.

* `vle.adaptative-qss` To model DEVS model without coding in C++ as in
  [PowerDEVS](https://sourceforge.net/projects/powerdevs/).
* `vle.output` To store observation into files or memory (useful for R
  and Python portage).

#### Debug

The new *Debug* system is available at run-tine. We replace the C++
`DECLARE_DYNAMICS_DBG` macros with a new element in the structure of
the model. This change can be found in the VPZ API and VPZ file
format.

#### Observation

Observations can now be done one each DSDE functions (internal,
external or confluent transitions or output).

#### Model in executable

The new API can load symbol into the main program instead of the
shared libraries specified by the package information. So, no package
and no shared libraries are necessary.

#### Build and run-time dependencies are reduced:

* *libarchive* and all *libboost* binary dependencies are removed.

----

More details on the [VLE 2.0]({{< ref "vle-20.md" >}}) page.

As usual, the source are available in [Github](https://github.com/vle-forge/).
