---
title: "FAQ and HOWTO"
date: 2018-11-29T13:24:48+01:00
lastmod: 2018-11-29T13:24:48+01:00
description: "Frequently Asked Questions"
weight: 20
---

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


## Upgrade your package developped under vle-1.1

To update the packages developped with vle-1.1 :

* you should first save your package before trying to update it.
* the modifications to perform on your package proposed here rely on the fact
that you did not modified the mentioned files.

You can use the python script  `VLE_INSTALL_DIR/share/convert-vpz11-vpz12.py`
or you can perfom manually the modifications listed below.


### Update the vpz files into  `mypkg/exp/`

a) using a text editor, remove the xml tag for duration and begin, e.g: replace:

```xml
<experiment name="ExtUpLV" duration="0.5" begin="0.0"
            combination="linear"  >
```
with
```xml
<experiment name="ExtUpLV"  combination="linear"  >
```

b) add the specific condition called "simulation_engine" with begin and
duration ports ; e.g

```xml
<conditions>
  <condition name="simulation_engine" >
    <port name="begin">
      <double>0.0</double>
    </port>
    <port name="duration">
      <double>0.5</double>
    </port>
  </condition>
  ...
</conditions>
```
