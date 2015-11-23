+++
categories = []
date = "2015-11-21T17:49:27+01:00"
description = ""
keywords = []
title = "VPZ files format"
+++

The VPZ file uses a DTD (Document Type Definition) to define the syntax
(http://www.vle-project.org/vle-1.1.0.dtd). In this page we give an example of
VPZ file with some explanations. You should not modify VPZ files unless you know
what you are doing. [GVLE]({{< ref "documentation/vle-1.1/gvle.md">}}) is the
GUI application for editing these files.

# Example of a VPZ file

Below is the declaration of the use of the vle DTD.

```xml
<!DOCTYPE vle_project PUBLIC "-//VLE TEAM//DTD Strict//EN"
  "http://www.vle-project.org/vle-1.1.0.dtd">
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
      <model name="a" type="atomic" dynamics="dynamicA"
                 conditions="conditionA" observables="obsA">
```

Submodels are possibly couple models or atomic models and are used to represent DEVS model hierarchy. 
Thus, the model `a` is a submodel of `topmodel` and is an atomic model. In VLE we use the syntax `topmodel::a` to refer to this submodel.

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

Below is the list of dynamics used into the structure defined above. They are C++ plug-ins and provide the dynamics behavior of atomic models (DEVS functions of atomic model). To write such dynamic, you have to define a C++ class (ie MyDyn) ``vle::dev::Dynamics`` and add the macro ``DECLARE_DYNAMICS(MyDyn)`` in the end of your cpp file. 

```xml
<dynamics>
  <dynamic name="dynamicA" library="libcounter" package="pkg1"/>
```

The dynamic declared above refers to the library into ``VLE_HOME/pkgs-1.1/pkg1/plugins/simulator/libcounter.dll`` 

```xml
    <dynamic name="dynamicB" library="big" package="pkg2" />
    <dynamic name="dynamicB" library="big" package="pkg3" />
    <dynamic name="dynamicB" library="big" package="pkg3" />
  </dynamics>
<experiment name="" duration="" begin="" combination="linear">
```

This is the definition of the experiment which gives initial conditions. These initial conditions possibly contains multiple values in order to simulate experiment plans.

```xml
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

There gives the observation system of the model, it allows to produce output files of the simulations. 

```xml
<outputs>
  <output name="outputa" format="local" package="vle.output" 
          location="" plugin="storage" />
```

The output plugin declared above refers to the c++ library ``VLE_HOME/pkgs-1.1/vle.output/plugins/output/libfile.so``.

```xml
<output name="outputb" format="local" package="vle.output" 
        location="" plugin="file" >
```

Some of the output plug-ins such as the `file` plug-in of `vle.output` can be parameterized, the parameters are given below as ``vle::value::Map``.

```xml
    <map><key name="julian-day"><boolean>true</boolean></map>
  </output>
</outputs>
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
```

Three values are possible for the type : `timed|event|finish`
<ol>
<li>timed : observation is called at each time-step.</li>
<li>event : observation is called after each DEVS transition (parameter time step is useless)</li>
<li>finish : observation is called only once at the end of simulation (parameter time step is useless)</li>
</ol>


```xml
    </views>
  </experiment>
</vle_project>
```

# XML format for `vle::value`

VLE provides a set of classes for representing data in a polymorphic way. All these classes inherit ``vle::value::Value`` and there are used for DEVS external transitions, observations, experimental conditions and some plug-in. The XML syntax is:

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

The vle::value::Table: a 2 dimension array of real (encapsulate a C++ ``boost::multi_array<2,double>``):

```xml
<table width="4" height="2"> 0 1 2 3 4 5 6 7 </table>
```

The vle::value::Tuple: a 1 dimension array of real (encapsulate a C++ ``std::vector<double>``):

```xml
<tuple> 1 2 3 4 5 6 7 8 9 10 11 12 </tuple>
```

The vle::value::Value: a 1 dimension array of values (encapsulates a ``std::vector<Value*>``):

```xml
<set>
  <string>totot</string>
  <integer>123</integer>
</set>
```

The vle::value::Map: a dictionary (encapsulates a ``std::map<std::string,Value*>``):

```xml
<map>
  <key name="tutu"><integer>123</integer></key>
  <key name="tata"><double>123.654987</double></key>
</map>
```

The vle::value::Matix: a 2 dim. array of values (encapsulate ``boost::multi_array<2,Value*>``):

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
