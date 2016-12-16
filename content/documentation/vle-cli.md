+++
topics = ["documentation"]
date = "2016-12-16T12:32:04+01:00"
description = "Description of the CLI"
tags = ["cli", "configuration"]
title = "Command Line Interface"
+++

To get access to this application :

* on Linux/Unix, simply type the command `vle --help` in a terminal. The
  CLI VLE has to be into the `PATH`.
* on Windows, open a command interpreter (application `cmd.exe`) and type the
  absolute path to the VLE binary location e.g.: `c:\vle-2.0\bin\vle-2.0
  --help`. By default VLE is not set into the default PATH environment
  variable, otherwise the command `vle --help` should work.

# The _package_ mode

The _package_ mode of vle application `vle -P mypackage` is used to manipulate
packages. A typical use case of these commands is :

First you can generate a template package in the current directory with  `vle
-P mypackage create`. Note that you can use any name for your package, if it is
not already used. To see the package names that are already used,  use the
command `vle --list`. The directory created has the structure detailed in the
[packages](../packages) page. Then you could configure and build the package
`vle -P mypackage configure build`.  The configure command actually calls
`cmake` in order to initiate the compilation process. A directory
`mypackage/buildvle` is then created. The build command will call `make all`
and `make install`. The binaries are installed into the [VLE_HOME](../vle-
home): more precisely into `VLE_HOME/pkgs-2.0/mypackage`. Note that you can
customize how vle calls `cmake` and `make` via the commands configure and build
by editing the [vle.conf file](../configuration-file).

Then you can start modelling (creating/modifying VPZ and cpp files) by using
the [gvle application](../gvle). Before simulation, you have to call
compilation processes (commands configure and build).

You can now simulate your models calling `vle -P mypackage mymodel.vpz`. It
will call the simulation of the model
`VLE_HOME/pkgs-2.0/mypackage/exp/mymodel.vpz`. The output files (if there are
some) are produced into the current directory. If your model contains an
experiment plan (many combinations of inputs) and you want to perform
simulation in parallel, you can use the commands `--manager` and `--processor`.
The first one declares that you will simulate all the input combinations, the
second is used to give the number of threads to use for parallel simulations.
Eg.:

    vle -P --manager --processor=5 -P mypackage mymodel.vpz

If you want to remove the binaries of your application you can use `vle -P
mypackage clean` or `vle -P mypackage rclean`. The first one will remove the
directory `mypackage/buildvle`. The second one will remove the directory
`VLE_HOME/pkgs-2.0/mypackage`. If you prefer, you can instead use your file
explorer directly  in order to remove those directories.

If you want to produce a compressed archive of your package in order to share
it with others, you can call the command `vle -P mypackage package`.

# The _remote_ mode

The _remote_ mode of vle application `vle --remote` is used to download or
install packages that are available in [distributions](../distributions). One
can declare new remote distributions by adding remote URL into the [vle.conf
file ](../configuration-file). Be very careful to add only URLs you trust in.
By default, there is the [VLE distribution](../../packages). A typical use case
of these commands is:

First you can update the state of your local packages with:

    vle -R update

This command modifies the `pkgs-2.0/local.pkg` and `pkgs-2.0/remote.pkg`
located into the [VLE_HOME](../vle-home). The first one lists the packages
installed on your computer, the second lists the packages available for
installation. They have the same format as the `packages.pkg` file of
[distribution](../../packages). The update command will also gives the packages
for which there are new updates on the remote distributions.

Then you can search for a particular remote package to install. For example, to
search for the package `vle.output` distributed by the [VLE
distribution](../../packages), you can use the command (eg. on windows):

    C:\>c:\vle-2.0\bin\vle -R search vle.output
    Found remote packages:
    vle.output       from http://www.vle-project.org/pub/2.0

The command gives the packages that have been found and the URL where they are
stored.

Finally you can install the package with the command:

    vle -R install vle.output

This will download into a temporary directory the package source and launch the
compilation processes described into the _package_ mode.

# The _config_ mode

The _configuration_ mode  `vle -C` is a feature that allows you to update
values of the [vle.conf file](../configuration-file). It is provided so that
users do not edit the `vle-2.0.conf` file directly.
