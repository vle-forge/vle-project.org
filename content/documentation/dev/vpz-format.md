+++
topics = ["documentation"]
date = "2016-12-16T12:32:04+01:00"
description = "Description of the VPZ format"
tags = ["vle-2.0", "vpz"]
title = "vpz format"
+++

The VPZ file uses a DTD (Document Type Definition) to define the syntax
(http://www.vle-project.org/vle-2.0.dtd). In this page we give an example of
VPZ file with some explanations. You should not modify VPZ files unless you
know what you are doing. [GVLE](../../users/gvle) is the GUI application for
editing these files.

# XML format for VPZ

```xml
<!DOCTYPE vle_project PUBLIC "-//VLE TEAM//DTD Strict//EN"
  "http://www.vle-project.org/vle-2.0.dtd">
<vle_project author="..." date="..." version="...">
<structures>
  <model name="topmodel" type="coupled">
    <in>
      <port name="..." />
      <port name="..." />
    </in>
    <out>
      <port name="..." />
      <port name="..." />
    </out>
    <submodels>
      <model name="a" type="atomic" dynamics="dynamicA" debug="true"
                 conditions="conditionA" observables="obsA">
```

Submodels are possibly couple models or atomic models and are used to represent
DEVS model hierarchy. Thus, the model `a` is a sub-model of `topmodel` and is
an atomic model. In VLE we use the syntax `topmodel::a` to refer to this sub-
model.

```xml
      <in>
        <port name="..." />
        <port name="..." />
      </in>
      <out>
        <port name="..." />
        <port name="..." />
      </out>
    </model>
    <model name="b" type="atomic">
      <in>
        <port name="..." />
        <port name="..." />
      </in>
      <out>
        <port name="..." />
        <port name="..." />
      </out>
    </model>
  </submodels>
    <connections>
      <connection type="input|output|internal">
        <origin model="..." port="..." />
        <destination model="..." port="..." />
      </connection>
    </connections>
  </model>
</structures>
```

Below is the list of dynamics used into the structure defined above. They are
C++ plug-ins and provide the dynamics behaviour of atomic models (DEVS
functions of atomic model). To write such dynamic, you have to define a C++
class (ie MyDyn) `vle::dev::Dynamics` and add the macro
`DECLARE_DYNAMICS(MyDyn)` in the end of your cpp file.

```xml
<dynamics>
  <dynamic name="dynamicA" library="libcounter" package="pkg1"/>
  <dynamic name="dynamicB" library="big" package="pkg2" />
  <dynamic name="dynamicB" library="big" package="pkg3" />
  <dynamic name="dynamicB" library="big" package="pkg3" />
</dynamics>
```
The dynamics declared above refers to the library into:

    VLE_HOME/pkgs-2.0/pkg1/plugins/simulator/counter.dll
    VLE_HOME/pkgs-2.0/pkg2/plugins/simulator/big.dll
    VLE_HOME/pkgs-2.0/pkg3/plugins/simulator/big.dll
    VLE_HOME/pkgs-2.0/pkg4/plugins/simulator/big.dll


This is the definition of the experiment which gives initial conditions. These
initial conditions possibly contains multiple values in order to simulate
experiment plans.

```xml
<experiment name="" duration="" begin="" combination="linear">
<conditions>
  <condition name="conditionA">
    <port name="...">
      <double>34.23</double>
      <double>33.23</double>
      <double>32.23</double>
      <double>31.23</double>
    </port>
  </condition>
</conditions>
<views>
```

There gives the observation system of the model, it allows to produce output
files of the simulations.

```xml
<outputs>
  <output name="outputa" format="local" package="vle.output"
          location="" plugin="storage" />
  <output name="outputb" format="local" package="vle.output"
          location="" plugin="file" >
    <map><key name="julian-day"><boolean>true</boolean></map>
  </output>
</outputs>
```

Some of the output plug-ins such as the `file` plug-in of `vle.output` can be
parametrized, the parameters are given below as ``vle::value::Map``. The output
plug-in declared above refers to the c++ library:

    VLE_HOME/pkgs-2.0/vle.output/plugins/output/storage.so
    VLE_HOME/pkgs-2.0/vle.output/plugins/output/file.so


```xml
<observables>
  <observable name="obsA">
    <port name="x">
      <attachedview name="measureA" />
    </port>
    <port name="y" />
    <port name="z" />
  </observable>
  <observable name="obsB">
    <port name="x" />
    <port name="y">
      <attachedview name="measureA" />
    </port>
    <port name="z" />
  </observable>
</observables>
<view name="viewA" type="timed|event|finish" output="outputa"
      timestep="0.5" />
    </views>
  </experiment>
</vle_project>
```

Three values are possible for the type : `timed|event|finish`

1. **timed**: observation is called at each time-step.
2. **output**: observation is called after each output DEVS transition
3. **internal**: observation is called after each internal DEVS transition
4. **external**: observation is called after each external DEVS transition
5. **confluent**: observation is called after each confluent DEVS transition
6. **finish**: observation is called after each finish DEVS transition

Note that modes 2, 3, 4, 5 and 6 can be combined. Mode 1 forbid combination
with other modes.

# XML format for `vle::value`

VLE provides a set of classes for representing data in a polymorphic way. All
these classes inherit the `vle::value::Value` class and there are used for DEVS
external transitions, observations, experimental conditions and some plug-in.
The XML syntax is:

The vle::value::Integer (encapsulate a C++ long integer)

```xml
<integer>10</integer>
```

The vle::value::Double (encapsulate a C++ double)

```xml
<double>20.003</double>
```

The vle::value::Boolean (encapsulate a C++ bool)

```xml
<boolean>true</boolean>
<boolean>1</boolean>
```

The vle::value::String (encapsulate a C++ ``std::string``):

```xml
<string>this is a string.</string>
```

The vle::value::Table: a 2 dimension array of real (encapsulate a C++
``boost::multi_array<2,double>``):

```xml
<table width="4" height="2"> 0 1 2 3 4 5 6 7 </table>
```

The vle::value::Tuple: a 1 dimension array of real (encapsulate a C++
``std::vector<double>``):

```xml
<tuple> 1 2 3 4 5 6 7 8 9 10 11 12 </tuple>
```

The vle::value::Value: a 1 dimension array of values (encapsulates a
``std::vector<Value*>``):

```xml
<set>
  <string>totot</string>
  <integer>123</integer>
</set>
```

The vle::value::Map: a dictionary (encapsulates a
``std::map<std::string,Value*>``):

```xml
<map>
  <key name="tutu"><integer>123</integer></key>
  <key name="tata"><double>123.654987</double></key>
</map>
```

The vle::value::Matix: a 2 dim. array of values (encapsulate
``boost::multi_array<2,Value*>``):

```xml
<matrix rows="" columns="" rowmax="" columnmax="" rowstep=""
        columnstep="">
  <!-- rows * columns values -->
</matrix>``
```

The vle::value::Xml: a Xml code (encapsulates a C++ ``std::string``):

```xml
<xml>
  <![CDATA[
        [...] ### free data
  ]]>
</xml>
```
