+++
categories = []
date = "2015-11-21T17:15:23+01:00"
description = ""
keywords = []
title = "vle home"

+++


The VLE home directory contains binaries of packages, configuration file and log
files. You should not directly this directory unless you know what you are 
doing. It has the following hierarchy:

```
$VLE_HOME 
  ├─ pkgs-1.1       ; the directory of VLE's packages
  │   └─ vle.output ; an example of package: vle.output.
  │   └─ mypackage  ; another example of package: mypackage.
  │   
  └─ vle.log        ; log of previous execution of VLE
  └─ rvle.log       ; log of previous execution of rvle
  └─ vle.conf       ; the configuration file of VLE
```

# The VLE_HOME environment variable

VLE_HOME refers to the location of the VLE home directory. It can be set using
the environment variable `VLE_HOME`. If the environment variable is not defined,
VLE uses the default path:

* `$HOME/.vle` on Unix/Linux systems (eg. `/home/user/.vle`).
* `$HOME/vle` on Win32 systems which corresponds to the variables: `%HOME%\vle`
(eg. `c:\\users\\vle`).

# The content of pkgs-1.1 environment variable

The packages in `VLE_HOME/pkgs-1.1` are binaries of packages, they are
automatically placed into this directory once a source package is built.
To compile a package see the [VLE application]({{< ref 
"documentation/vle-1.1/vle-cli.md">}}) and
more precisely the commands `configure` and `build` in package mode.

# The configuration file

The [vle.conf file](VLE-configuration-file-for-vle-1.1) contains the global settings for VLE. It allows for example to give the number of threads when building a package, or giving remote URL for downloading and installing packages.
