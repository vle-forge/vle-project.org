+++
topics = ["documentation"]
date = "2015-11-20T16:00:15+01:00"
description = ""
tags = ["vle-2.0","upgrade"]
title = "upgrade from vle 1.2 to vle 2.0"

+++

WARNING: The vle-2.0 is not yet released. This page is under
construction.

# Upgrade your package developped under vle-1.2

To update the packages developped with vle-1.2 :

* you should first save your package before trying to update it.
* the modifications to perform on your package proposed here rely on the fact
that you did not modified the mentioned files.

## Update the cmake scripts.

a) In the directory `mypkg/cmake`, remove all files and add all files are
here: https://github.com/vle-forge/vle/tree/master/share/template/package/cmake.

b) Replace the file `mypkg/CMakeLists.txt` by this one
https://github.com/vle-forge/vle/blob/master/share/template/package/CMakeLists.txt.
Update the project name : replace `MyProject` into the line `PROJECT(MyProject)`
by your package name.

c) Replace the file `mypkg/src/CMakeLists.txt` by this one
https://github.com/vle-forge/vle/blob/master/share/template/package/src/CMakeLists.txt.

If you need to install hpp files you can add the following line:

```cmake
install(DIRECTORY . DESTINATION src FILES_MATCHING PATTERN "*.hpp")
```

## Update the cpp files into ``mypkg/src/``.

a) In the directory `mypkg/src`, the cpp files which are VLE dynamics should
have this header into cpp comments:

```
// @@tagdynamic@@
// @@tagdepends: vle.extension.decision, myotherpkg @@endtagdepends
```

The first line states that this cpp is a VLE dynamic and should be compiled by
the cmake project.
The second line gives the list of packages which are required for compiling
the current package (mypkg).
For more documentation, take a look at the `VleUtilsConfig.cmake`
file into `mypkg/cmake`.

## Update the file `mypkg/Description.txt`

The list of packages required to build all VLE dynamics (see tagdepends above)
must be given to fill the `Build-Depends` part.
