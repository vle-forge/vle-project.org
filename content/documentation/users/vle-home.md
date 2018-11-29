+++
topics = ["documentation"]
date = "2016-12-16T12:32:04+01:00"
description = "How to use?"
tags = ["configuration"]
title = "vle-home variable"
weight = 14
+++


The VLE home directory contains binaries of packages, configuration file and
log files. You should not use directly this directory unless you know what you
are doing. It has the following hierarchy:

    $VLE_HOME
      ├─ pkgs-2.0       ; the directory of VLE's packages
      │   └─ vle.output ; an example of package: vle.output.
      │   └─ mypackage  ; another example of package: mypackage.
      │
      └─ vle.log        ; log of previous execution of VLE
      └─ rvle.log       ; log of previous execution of rvle
      └─ vle.conf       ; the configuration file of VLE

# The VLE_HOME environment variable

`VLE_HOME` refers to the location of the VLE home directory. It can be set
using the environment variable `VLE_HOME`. If the environment variable is not
defined, VLE uses the default path:

* `$HOME/.vle` on Unix/Linux systems (eg. `/home/user/.vle`).
* `$HOME/vle` on Win32 systems which corresponds to the variables: `%HOME%\vle`
(eg. `c:\\users\\vle`).

The packages in `VLE_HOME/pkgs-2.0` are binaries of packages, they are
automatically placed into this directory once a source package is built. To
compile a package see the [VLE application](../vle-cli) and more precisely the
commands `configure` and `build` in package mode.

The [vle.conf file](../configuration-file) contains the global settings for
VLE. It allows for example to give the number of threads when building a
package, or giving remote URL for downloading and installing packages.
