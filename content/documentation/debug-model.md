+++
topics = ["documentation"]
date = "2016-12-16T12:32:04+01:00"
description = "How to debug or log model"
tags = ["vle-2.0", "c++", "atomic-model", "debug"]
title = "Debug and Log model"
+++

# Debug model

To debug your model, you may use the _debug_ option when you right click on an
atomic model under [GVLE](../gvle).

Default, the debug file is located at `$VLE_HOME/vle-2.0.log` but it can be
redirected to the standard output with the command line option `--log-to-
stdout` or `--log-to-stderr`.

Warning, in order to have the debug service available, make sure that vle
is built with the debug option for example like this(Unix case):

````bash
cd vle-your_release
mkdir build && cd build
export QT_SELECT=qt5

cmake -DCMAKE_INSTALL_PREFIX=/usr/local -DCMAKE_BUILD_TYPE=Debug ..

make -j4
make install
make test
````

# Log model

For example the following atomic model will show always the string "MyModel
constructor" but show the string "time is odd" only when time is odd and VLE is
launched with `vle -v x` with `x` equal 1, 2 or 3.

```c++
#include <vle/devs/Dynamics.hpp>
#include <vle/devs/DynamicsDbg.hpp>
#include <vle/utils/Debug.hpp>
#include <vle/utils/Trace.hpp>

class MyModel : public vle::devs::Dynamics
{
public:
    MyModel(const vle::devs::DynamicsInit& init
            const vle::devs::InitEvents& events)
        : vle::devs::Dynamics(init, events)
    {
        Trace(context(), 1, "MyModel constructor");
    }

    virtual void internalTransition(vle::devs::Time time)
    {
        if (static_cast<int>(time) % 2 == 0)
            Trace(context(), 7, "time is odd: %f", time);
    }
};
DECLARE_DYNAMICS(MyModel)
```
