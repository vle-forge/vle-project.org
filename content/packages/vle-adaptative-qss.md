+++
tags = ["ode", "qss", "adaptative-qss"]
topics = ["packages", "extension"]
description = "To build ODE system without C++ coding"
date = "2016-12-19T14:31:21+01:00"
title = "vle.adaptative-qss"
+++

The `vle.adaptative-qss` package is system package. It is provided by
[VLE](../../documentation) during installation. The goal of this package is to
build ordinary differential system without C++.

# Generic models

These packages provides generic models. You can use it directly without changing their source code.

**AdaptativeQuantifier**

**Integrator**

**Adder**: Each value receives on input port is added to each other and send to
the output port.

**Generator**: Value read from experimental condition are send to the output
port.

**Mult**: Each value receives on input port is multiplied to each other and
send to the output port.

# Example

This example of a simple [lotka volterra system](https://github.com/vle-
forge/packages/tree/master/vle.adaptative-qss.examples) is available as source
code in the [packages repository](https://github.com/vle-forge/packages). To
get is, use the following commands:

```bash
git clone https://github.com/vle-forge/packages.git
cd package
vle -P vle.adaptative-qss.examples clean rclean configure build
```

{{% fluid_img src="../lotka-volterra.png" caption="VLE 2, vle.adaptative-qss, Lotka Volterra extension" %}}
