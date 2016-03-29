+++

date = "2015-11-21T16:58:32+01:00"
description = ""
tags = ["vle-1.1","configuration"]
title = "Configuration file"
topics = ["documentation"]
+++

# Description

The VLE configuration file provides preferences that users can set. You can find
this file into the [VLE_HOME directory](vle-home): `VLE_HOME/vle.conf`. There
are shared for all the projects on your computer. Each line represents one
preference, the format is the following `variable=value`. The difference
preferences are listed below:

```ini
gvle.editor.auto-indent=1
gvle.editor.font=Monospace 10
gvle.editor.highlight-brackets=1
gvle.editor.highlight-line=1
gvle.editor.highlight-syntax=1
gvle.editor.indent-on-tab=1
gvle.editor.indent-size=4
gvle.editor.show-line-numbers=1
gvle.editor.show-right-margin=1
gvle.editor.smart-home-end=1
gvle.graphics.atomic-color=
gvle.graphics.background-color=
gvle.graphics.connection-color=
gvle.graphics.coupled-color=
gvle.graphics.font=Monospace 10
gvle.graphics.font-size=10
gvle.graphics.foreground-color=
gvle.graphics.line-width=3
gvle.graphics.selected-color=
gvle.packages.auto-build=1
vle.daemon.hosts=localhost
vle.daemon.ports=8001
vle.daemon.processes=1
vle.packages.build=cmake --build '%1%'  --target all
vle.packages.clean=cmake --build '%1%' --target clean
vle.packages.configure=cmake -DCMAKE_INSTALL_PREFIX='%1%' -DWITH_DOC=OFF -DWITH_TEST=ON -DWITH_WARNINGS=ON -DCMAKE_BUILD_TYPE=RelWithDebInfo ..
vle.packages.install=cmake --build '%1%' --target install
vle.packages.package=cmake --build '%1%' --target package_source
vle.packages.test=cmake --build '%1%' --target test
vle.packages.unzip=unzip
vle.remote.proxy_ip=
vle.remote.proxy_port=
vle.remote.url=http://www.vle-project.org/pub/1.1
```

# How to modify the preferences.

There are two possibilities for modifying the preferences:

* You can directly edit the `vle.conf` file, or You can use the [vle
* CLI](vle-cli) in _configuration_ mode. For example, the following command will
* modify the font of the [gvle program](gvle).

```bash
vle -C gvle.editor.font=Monospace 9
```

In these two cases, the modification can lead to dysfunctions of VLE. To reset
the preferences, simply remove the `vle.conf` file and call `vle --restart` from
the CLI.

# The GVLE preferences

The preferences that starts with `gvle.*` stands for graphical preferences of
[GVLE](gvle). The GVLE application provides tools to modify them, but you can
directly set these preferences.

# The packages preferences

The package preferences (starting with `vle.packages.*`) are essentially
preferences for the building process of [packages](packages). For example if you
want to use parallel build of `make` you can use the following command (in this
example using 3 threads):

```bash
vle -C  vle.packages.build=cmake --build '%1%'  --target all -- -j3
```

# The remote preferences

The remote preferences (starting with `vle.remote.*`) are the preferences
related to the remote features of VLE. You can for example add remote URL
pointing to a [package distribution](distributions).
