+++
data =2017-04-24T16:33:20+01:00
title = "vle.adaptative-qss"
topics = ["packages", "extension" ]
tags = ["ode", "qss", "adaptative-qss"]
description = "Build ODE system without C++ coding"
+++

The **vle.adaptative-qss** package is a system package. It is available
with [VLE](../../documentationV) without installation of any package.
The goal of this package is to build ordinary differential equation
system without C++ coding.

Generic models
==============

These packages provides generic models. You can use it directly without
changing their source code.

| Dynamics             | Descriptions                                                                               |
|----------------------|--------------------------------------------------------------------------------------------|
| AdaptativeQuantifier | The quantifier of the variable.                                                            |
| Integrator           | The integrator of the variable.                                                            |
| Adder                | Each value receives on input port is added to each other and send to the output port.      |
| Generator            | Value read from experimental condition are send to the output port.                        |
| Mult                 | Each value receives on input port is multiplied to each other and send to the output port. |
| Constant             | Send a constant value on its output ports.                                                 |

Plot models
===========

This package shows at run-time of the simulation the output of atomic
models into a [GNUPlot](http://www.gnuplot.info/) window or windows if
several atomic models are used. Each input port is associated to a
column data with the input port name as label. The dynamic have two
optional parameters:

**gnuplot-duration** (double)
:   Duration in second between two redraw of the
    [GNUPlot](http://www.gnuplot.info/) window. The default value
    is 0.3s.

**gnuplot-command** (string)
:   The command to access the
    [GNUPlot](http://www.gnuplot.info/) executable. Default the
    `gnuplot` (or `gnuplot.exe`) command is search in `PATH`
    environment variable.

Examples
========

This example of a simple [lotka volterra system](https://github.com/vle-
forge/packages/tree/master/vle.adaptative-qss.examples) is available as source
code in the [packages repository](https://github.com/vle-forge/packages). To
get it, use the following commands:

```bash
git clone https://github.com/vle-forge/packages.git
cd package
vle -P vle.adaptative-qss.examples clean rclean configure build
```

{{< fluid_img class="pure-u-1-1" src="../lotka-volterra.png" alt="VLE 2, vle.adaptative-qss, Lotka Volterra extension" >}}
