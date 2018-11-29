+++
date = "2016-12-16T12:32:04+01:00"
description = ""
tags = ["vle-2.0","configuration"]
title = "Configuration file"
topics = ["documentation"]
weight = 19
+++

**Description**

The VLE configuration file provides preferences that users can set. You can
find this file into the [VLE_HOME directory](../vle-home):
`VLE_HOME/vle-2.0.conf`. There are shared for all the projects on your
computer. Each line represents one preference, the format is the following
`variable=value`. The difference preferences are listed below:

```ini
gvle.editor.auto-indent=true
gvle.editor.font=Monospace 10
gvle.editor.highlight-brackets=true
gvle.editor.highlight-line=true
gvle.editor.highlight-syntax=true
gvle.editor.indent-on-tab=true
gvle.editor.indent-size=4
gvle.editor.show-line-numbers=true
gvle.editor.show-right-margin=true
gvle.editor.smart-home-end=true
gvle.graphics.atomic-color=#0000ffff0000
gvle.graphics.background-color=#ffffffffffff
gvle.graphics.connection-color=#000000000000
gvle.graphics.coupled-color=#00000000ffff
gvle.graphics.font=Monospace 10
gvle.graphics.font-size=10
gvle.graphics.foreground-color=#000000000000
gvle.graphics.line-width=3
gvle.graphics.selected-color=#ffff00000000
gvle.packages.auto-build=true
vle.command.dir.copy=cmake -E copy_directory '%1%' '%2%'
vle.command.dir.remove=cmake -E remove_directory '%1%'
vle.command.tar=cmake -E tar jcf '%1%' '%2%'
vle.command.untar=cmake -E tar jxf '%1%'
vle.command.url.get=curl --progress-bar '%1%' -o '%2%'
vle.command.vle.simulation=vle-2.0--write-output '%1%' '%2%'
vle.packages.build=cmake --build '%1%' --target all
vle.packages.clean=cmake --build '%1%' --target clean
vle.packages.configure=cmake -DCMAKE_INSTALL_PREFIX='%1%' -DWITH_DOC=OFF -DWITH_TEST=ON -DWITH_WARNINGS=ON -DCMAKE_BUILD_TYPE=RelWithDebInfo ..
vle.packages.install=cmake --build '%1%' --target install
vle.packages.package=cmake --build '%1%' --target package_source
vle.packages.test=cmake --build '%1%' --target test
vle.remote.url=http://www.vle-project.org/pub/2.0
vle.simulation.block-size=8
vle.simulation.thread=0
```

**How to modify the preferences**

You can directly edit the `vle-2.0.conf` file, or You can use the [command line
interface](../vle-cli) in _configuration_ mode. For example, the following
command will modify the font of the [GVLE](../gvle).

```bash
vle -C gvle.editor.font=Monospace 9
```

In these two cases, the modification can lead to dysfunctions of VLE. To reset
the preferences, simply remove the `vle.conf` file and call `vle --restart` from
the CLI.

**GVLE preferences**

The preferences that starts with `gvle.*` stands for graphical preferences of
[GVLE](../gvle). The GVLE application provides tools to modify them, but you
can directly set these preferences.

**The packages preferences**

The package preferences (starting with `vle.packages.*`) are essentially
preferences for the building process of [packages](../packages). For example if
you want to use parallel build of `make` you can use the following command (in
this example using 3 threads):

    vle -C  vle.packages.build=cmake --build '%1%'  --target all -- -j3

**The remote preferences**

The remote preferences (starting with `vle.remote.*`) are the preferences
related to the remote features of VLE. You can for example add remote URL
pointing to a [package distribution](../distributions).
