+++
tags = [
]
topics = [ "packages"
]
description = ""
date = "2016-12-15T16:40:27+01:00"
title = "packages"
+++

## Useful packages

VLE provides its own [packages distribution](../documentation/distributions/).
It contains packages for modelling extensions, outputs, generic tools and
generic models.

Packages provided with this distribution are:

Package | Description
:------ | :----------
ext.lua | Allow the use of lua
ext.muparser | Allow the use of muparser
gvle.discrete-time | GVLE's Discrete time modelling extension
gvle.simulating.log | GVLE's plug-in
gvle.simulating.plot | GVLE's plot plug-in
gvle.simulating.shape | GVLE's share plug-in
vle.discrete-time | Discrete time modelling extension
vle.examples | Lot of example
[vle-adaptative-qss](vle-adaptative-qss) | QSS ordinary differential equation solver without coding
vle.extension.celldevs | Cell DEVS modelling extension
vle.extension.cellqss | Cell QSS modelling extension
vle.extension.decision | Decision making modelling extension
vle.extension.dsdevs | Dynamic Structure generic model
vle.extension.fsa | Finite State Automaton modelling extension
vle.extension.petrinet | Petrinet modelling extension
vle.ode | Ordinary differential equation solver (QSS, Euler, RK4 etc.)
vle.reader | Generic model to parse file at simulation

To install packages using the CLI option remote, use to following command:

    vle-2.0 --remote update
    vle-2.0 --remote install vle.extension.decision

The distribution is available on [this website](http://www.vle-
project.org/pub/2.0/) and the [source code repository](https://github.com/vle-
forge/packages)
