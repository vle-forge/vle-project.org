+++
categories = ["documentation", "vle", "cli"]
date = "2015-10-28T11:31:40+01:00"
description = "VLE command line interface description"
keywords = ["cli", "vle"]
title = "vle cli"
+++

Table of content:

* <a href="#howtouse">How to use CLI application</a>
* <a href="#packageMode">The _package_ mode</a>
* <a href="#remoteMode">The _remote_ mode</a>
* <a href="#configMode">The _config_ mode</a>

### <a id="howtouse"></a> How to use CLI application

To get access to this application :

* on Linux/Unix, simply type the command `vle --help` in a terminal. The
CLI vle has to be into the `PATH`. 
* on Windows, open a command interpreter (application `cmd`) and type the
absolute path to the vle binary location e.g. : `c:\vle-1.1\bin\vle --help`. 
By default vle is not set into the path, otherwise the command `vle --help`
should work.

### <a id="packageMode"></a> The _package_ mode


The _package_ mode of vle application `vle -P mypackage` is used to manipulate
packages. A typical use case of these commands is :

First you can generate a template package in the current directory with 
`vle -P mypackage create`. Note that you can use any name for your package,
if it is not already used. To see the package names that are already used, 
use the command `vle --list`. The directory created has the structure detailed
in the [packages]({{< ref "documentation/vle-1.1/packages.md">}}) page. Then you
could configure and build the package `vle -P mypackage configure build`. 
The configure command actually calls `cmake` in order to initiate the
compilation process. A directory `mypackage/buildvle` is then created.
The build command will call `make all` and `make install`. The binaries are
installed into the [VLE_HOME]({{< ref "documentation/vle-1.1/vle-home.md">}}):
 more precisely into  `VLE_HOME/pkgs-1.1/mypackage`. Note that you can customize
 how vle calls `cmake` and `make` via the commands configure and build by
 editing the [vle.conf file]({{< ref 
 "documentation/vle-1.1/configuration-file.md">}}). 

Then you can start modeling (creating/modifying VPZ and cpp files) by using the
[gvle application]({{< ref "documentation/vle-1.1/gvle.md">}}). Before
simulation, you have to call compilation processes (commands configure and 
build). 

You can now simulate your models calling `vle -P mypackage mymodel.vpz`. It will
call the simulation of the model  `VLE_HOME/pkgs-1.1/mypackage/exp/mymodel.vpz`.
The output files (if there are some) are produced into the current directory.
If your model contains an experiment plan (many combinations of inputs) and you
want to perform simulation in parallel, you can use the commands `--manager` and
`--processor`. The first one declares that you will simulate all the input
combinations, the second is used to give the number of threads to use for
parallel simulations. Eg.: 

```bash
vle -P --manager --processor=5 -P mypackage mymodel.vpz
```

If you want to remove the binaries of your application you can use
`vle -P mypackage clean` or `vle -P mypackage rclean`. The first one will remove
the directory `mypackage/buildvle`. The second one will remove the directory
`VLE_HOME/pkgs-1.1/mypackage`. If you prefer, you can instead use your file
explorer directly  in order to remove those directories.

If you want to produce a compressed archive of your package in order to share
it with others, you can call the command `vle -P mypackage package`.

### <a id="remoteMode"></a> The _remote_ mode

The _remote_ mode of vle application `vle --remote` is used to download or
install packages that are available in [distributions]({{< ref 
"documentation/vle-1.1/distributions.md">}}). One can declare new remote
distributions by adding remote URL into the [vle.conf file]({{< ref 
"documentation/vle-1.1/configuration-file.md">}}). Be very carefull to add only
URLs you trust in. By default, there is the [VLE distribution]({{< ref 
"documentation/vle-1.1/vle-packages-distribution.md">}}). 
A typical use case of these commands is :

First you can update the state of your local packages with `vle -R update`.
This command modifies the `pkgs-1.1/local.pkg` and `pkgs-1.1/remote.pkg` located
into the [VLE_HOME]({{< ref "documentation/vle-1.1/vle-home.md">}}).
The first one lists the packages
installed on your computer, the second lists the packages available for
installation. They have the same format as the `packages.pkg` file of
[distribution](Package-distribution-for-vle-1.1). The update command will
also gives the packages for which there are new updates on the remote
distributions.

Then you can search for a particular remote package to install. For example,
to search for the package `vle.output` distributed by the 
[VLE distribution]({{< ref 
"documentation/vle-1.1/vle-packages-distribution.md">}}),
you can use the command (eg. on windows):   

```bash
C:\>c:\vle-1.1\bin\vle -R search vle.output
Found remote packages:
vle.output       from http://www.vle-project.org/pub/1.1
```

The command gives the packages that have been found and the URL where they are
stored.

Finally you can install the package with the command `vle -R install vle.output`
this will download into a temporary directory the package source and launch the
compilation processes described into the _package_ mode. 

### <a id="configMode"></a> The _config_ mode

The _configuration_ mode  `vle -C` is a feature that allows you to update
values of the [vle.conf file]({{< ref 
"documentation/vle-1.1/configuration-file.md">}}). It is
provided so that users do not edit the vle.conf file directly.
