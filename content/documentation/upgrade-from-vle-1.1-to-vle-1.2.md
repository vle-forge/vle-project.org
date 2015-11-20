+++
categories = []
date = "2015-11-20T15:53:52+01:00"
description = ""
keywords = []
title = "upgrade from vle 1.1 to vle 1.2"

+++

### Upgrade your package developped under vle-1.1

To update the packages developped with vle-1.1 :

* you should first save your package before trying to update it. 
* the modifications to perform on your package proposed here rely on the fact
that you did not modified the mentioned files. 

You can use the python script  `VLE_INSTALL_DIR/share/convert-vpz11-vpz12.py`
or you can perfom manually the modifications listed below.


#### Update the vpz files into  `mypkg/exp/`

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