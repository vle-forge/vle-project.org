+++
categories = ["documentation", "pyvle"]
date = "2015-10-28T11:16:42+01:00"
description = "PyVLE description"
keywords = ["python", "pyvle"]
title = "PyVLE"
+++

PyVLE is a [Python](https://www.python.org/) package for using VLE
framework into Python. It provides features such as loading VPZ files,
modifying conditions values of models, simulating VLE models and
recovering simulation results. It provides other features regarding
the experiment such as modifying duration or seed, obtaining
information on models and views.

PyVLE is one component of a generic solution for developing web
applications for VLE framework.

# Installation

- you can get source code of pyvle on the 
[Download Page of vle-1.1](http://www.vle-project.org/vle-1.1)
- or on github 

```
git clone https://github.com/vle-forge/pyvle.git
```

# Usage

Once VLE and PyVLE are installed, you can launch python and import pyvle.

```bash
$ python
Python 2.7.2+ (default, Oct  4 2011, 20:06:09)
[GCC 4.6.1] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import pyvle
```

or

```python
>>> from pyvle import Vle
```

The package is mostly based on a Python class `Vle`. In order to know
what functions are available into this package.

```python
>>> dir(pyvle.Vle)
```

In the following example:
* a vpz file is loaded
* initial conditions are modified
* simulation is launched

Outputs are not recovered since the output plugin of the view is not
storage.

```python
>>> from pyvle import Vle
>>> f = Vle("scale1.vpz","glue")
>>> print(f)
<pyvle.Vle instance at 0x7fe231515e60>
>>> f.listConditions()
['condA', 'condB', 'condScale']
>>> f.listConditionPorts('condScale')
['InputTimeStep', 'OutputTimeStep']
>>> f.getConditionPortValues('condScale', 'OutputTimeStep')
1.0
>>> f.clearConditionPort('condScale', 'OutputTimeStep')
>>> f.addRealCondition('condScale', 'OutputTimeStep', 0.5)
>>> f.getConditionPortValues('condScale', 'OutputTimeStep')
0.5
>>> f.run()
```

Notes:
* this example requires that the VLE package *glue* is installed.
* outputs are not recovered since the output plugin of the view is not
  storage.

```python
>>> from pyvle import Vle
>>> f=Vle('/tmp/myModel.vpz', 'glue')
>>> ...
```

It can be useful to recover the results of a simulation. To do this,
the output plugin of views of the vpz (or at least the view that is
expected) should be set to *storage*. Call to function `run` will
return dictionaries (one per view) odf results.

Here is an example:

```python
>>> from pyvle import Vle
>>> f = Vle("scale1.vpz","glue")
>>> f.setOutputPlugin('view', '', 'local', 'storage')
>>> result = f.run()
>>> result['view']['Top model:B4.b'][5]
20.0
```

To access to the ith value of observables `obs` into the view `view`,
the syntax to use is: result[`view`][`obs`][`i`]:

* `view` the name of the view
* `obs` the path to the model concatenated with the port name. For
  example if the top model, called `C1` is a coupled model containing
  the atomic model `C2` which is observed through the observable port
  `p`, so obs = `C1:C2.p`
* `i` index of the matrix. In a view configured as a timed-view, i
  represents the time step value.

Examples above show how to launch one simulation.  Nevertheless it is
possible to launch a bag of simulations with one call of command

In the case only one simulation is required, method `run()` can be
used.  In the other case, methods `runManager` or `runManagerMatrix`
are available to simulate one bag of simulations.

For one simulation (see above for interpreting results):

```python
>>> import pyvle
>>> v=pyvle.Vle('weed1.vpz','weed')
>>> result=v.run()
# result['view']['path:model.port'][index]
```

For a bag of simulations, results is more complex since they are as
many view dictionaries as couples replica, combination.

```python
>>> import pyvle
>>> v=pyvle.Vle('weed1.vpz','weed')
>>> result=v.runManager()
# result[replicat_index][combinaison_index]['view']['path:model.port'][index]
```

One can find the connection between `combinaison_index` and the
initial conditions values it corresponds to.

```python
>>> import pyvle
>>> v=pyvle.Vle('weed1.vpz','weed')
>>> v.getCombinations()
# n tuples containing the list of initial conditions of the n combinations
>>> v.getCombinations()[0]
#  the list of initial conditions of the first combination
>>> v.listConditions()
#the list of combinations
>>> listConditionPorts('xxx')
# the list of names of conditions port of condition 'xxx' where 'xxx' is the first condition
```
