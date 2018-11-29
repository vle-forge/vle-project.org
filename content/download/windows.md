+++
tags = [ "windows" ]
topics = [ "VLE 2.0", "Installation" ]
description = "How to install VLE on Windows 7, 8, 10 ?"
date = "2016-12-16T15:13:55+01:00"
title = "Windows Installation"
+++

To avoid many problems with VLE, prefer uninstall the previous VLE software from your system.

VLE Windows comes with a complete Gnu GCC toolchain, Qt5 platform and the CMake software. The installed size will use more than 2GB of space disk.

First, download [the setup file](https://www.vle-project.org/pub/vle/2.0/2.0.2/Setup-VLE_2_0_2.exe) and execute the file. This setup embeds only a x86 32 bits installation of VLE. You can let the setup found the installation path for example into `c:\Program files(x86)\VLE_2_0`.

To use VLE in a terminal like on UNIX or MacOS, go to Windows menu and enter the string `cmd.exe`. A terminal appears. Enter the string (or update the string according to your installed path).

```
set PATH=%PATH%;"c:\Program files(x86)\bin"
```

From now, you can run VLE like on UNIX for example, you can run `vle --restart` to rewrite default configure files.

The setup normally installs icond on Windows menu and desktop. Just select the VLE's icon and starts it. GVLE will appear.

If an error occured, just add an issue on [vle-forge/vle github page](https://github.com/vle-forge/vle/issues) or send à e-mail to the mailing list.

## Uninstall VLE 1.0 or 1.1

If you have already install VLE 1.0 or VLE 1.1, you may:

* Uninstall the previous version
* Remove the remaining variable `PKG_CONFIG_PATH` (only earlies versions)
* Uninstall/remove the Mingw32 compiler (if not needed by another application)
* Uninstall CMake (if not required by another application)
