+++
categories = []
date = "2015-11-20T15:12:49+01:00"
description = ""
keywords = []
title = "upgrade from vle 1.0.3 to vle 1.1"

+++

### Upgrade vle to vle 1.1

On linux: install missing packages, see the [building from source page](Get-vle-from-sources-for-vle-1.1). 
Then install from sources.

On Win32, remove the `Mingw` and `CMake` software since they are now 
embedded into VLE, unless you use it for other applications. 
And install vle-1.1.

### Upgrade your package developped under vle-1.0.3

First of all you should save your package before trying to update it.
The modifications to perform on your package proposed here rely on the fact that
you did not modified the mentioned files. While updating these files, you should
also take into account the modifications you performed.

#### Update the cmake scripts. 

a) In the directory `mypkg/cmake`, remove all files and add all files are here: 
https://github.com/vle-forge/vle/tree/master1.1/share/template/package/cmake. 

b) Replace the file `mypkg/CMakeLists.txt` by this one 
https://github.com/vle-forge/vle/blob/master1.1/share/template/package/CMakeLists.txt. 
Update the project name : replace `MyProject` into the line `PROJECT(MyProject)`
by your package name. Uncomment all extensions you need for your package, eg. 
remove the symbol # in front of 

```cmake
VLE_CHECK_PACKAGE(DIFFERENCE_EQU vle.extension.difference-equation)  
..... 
if (NOT DIFFERENCE_EQU_FOUND)
  message(SEND_ERROR "Missing vle.extension.difference-equation")
endif (NOT DIFFERENCE_EQU_FOUND)
```


c) Replace the file `mypkg/src/CMakeLists.txt` with the file here 
https://github.com/vle-forge/vle/blob/master1.1/share/template/package/src/CMakeLists.txt. 
Into this file declare the dynamics you compile for example replace the line 
`DeclareDevsDynamics(Simple "Simple.cpp")` by :

```cmake
DeclareDifferenceEquationDynamics(Mymodel "Mymodel.cpp")
DeclareFsaDynamics(MymodelFsa "MymodelFsa.cpp")
```

#### Update the cpp files into `mypkg/src/`

a)  replace macros `DECLARE_NAMED_DYNAMICS` with `DECLARE_DYNAMICS`.
Only one dynamic can be defined into a library. If you have more than one of
these macro (for example also ``DECLARE_DYNAMICS_DBG``), you should split them
into different cpp files and declare as many as dynamics as those files 
(see 1.c).

b) if the dynamic uses the random number generator `utils::Rand`, it has to be
declared as a class member of the dynamic because PRNG is not provided at the
level of the simulation. So add a class member to your dynamic.

```c++
#include <vle/utils/Rand.hpp>
...
vle::utils::Rand mrand;
```

c) replace all occurences of  `vle::devs::Time::infinity` with 
`vle::devs::infinity`.

d) many includes have changed : no more global include for value, utils, devs...
For example :

replace `#include <vle/value.hpp>` with `#include <vle/value/Matrix.hpp>` if 
you intend to use matrices. 
   
replace `#include<vle/utils.hpp>` with `#include <vle/utils/DateTime.hpp>` if
you need to convert dates 

This is also true for extensions, which are now part of packages: For example,

replace `#include <vle/extension/DifferenceEquation.hpp>`  with 
`#include <vle/extension/difference-equation/Multiple.hpp>`.
 
e) replace the call to `output.addEvent(evt)` by `output.push_back(evt)` 
(mainly in Decision and Executive extensions) 

#### Update the vpz files into  `mypkg/exp/`

a) using a text editor, remove the xml tag for replicas,
remove a line which looks like : 

```xml
<replicas seed="581869302" number="1" /> 
```

b) update the output tag to point output plugins to vle.output ; e.g : replace 
```xml
<output name="vueHorloge" location="" format="local" plugin="file" >
``` 
with:
```xml
<output name="vueHorloge" location="" format="local"
        package="vle.output" plugin="file" >
```

c) update the dynamics : set the name of the package and the library. The tag 
"Model" is no more used because there is only one dynamic by library 
 
 