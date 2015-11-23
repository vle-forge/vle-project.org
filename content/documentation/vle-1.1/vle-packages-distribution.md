+++
categories = []
date = "2015-11-21T17:23:13+01:00"
description = ""
keywords = []
title = "vle packages distribution"

+++

VLE provides its own packages distribution (see [Package Distribution]({{< ref 
"documentation/vle-1.1/distributions.md">}})).
It contains packages for modeling extensions, outputs and tools. 

The VLE packages provided by this distribution are :

* vle.output : management of simulation outputs (file, console, etc..)
* ext.muparser : required for vle.forrester only
* vle.extension.difference-equation : modelisation of difference equations
* vle.extension.differential-equations : modelisation of differential equations 
(Euler, RK4 and QSS2 integration scheme)
* vle.extension.decision : modelisation of decision processes
* vle.extension.dsdevs : Dynamic Structure DEVS
* vle.extension.fsa : finite state automata
* vle.extension.petrinet : modelisation of petrinets
* vle.extension.celldevs : cellular automata
* vle.extension.cellqss
* vle.forrester : Forrester based modelisation (system dynamics)
* vle.examples : some VLE examples and packages tests 

# Install packages using the CLI option remote

```bash
vle --remote update
vle --remote install vle.extension.difference-equation
```

# Install packages by downloading the source code

The URL of the distribution is : http://www.vle-project.org/pub/1.1/. 
A global archive is also provided on the VLE website :
[VLE 1.1 specific page](http://www.vle-project.org/vle-1.1).

# Install packages using the package repository

The source code is on a separate github repository:
https://github.com/vle-forge/packages.
