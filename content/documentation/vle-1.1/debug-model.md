+++
categories = ["documentation", "c++", "atomic-model"]
date = "2015-09-17T13:09:54+02:00"
description = ""
keywords = ["devs", "atomic", "model"]
title = "debug model"
+++

### Debugging Macros

To debug your model, you may use the `DECLARE_DYNAMICSY_DBG` instead of
`DECLARE_DYNAMICS` and use some functions (`TraceAlways`, `TraceModel` etc.) to
enable debugging of your model in the C++ source code.

Default, the debug file is located at `$VLE_HOME/vle.log` but it can be
redirected to the standard output with the command line option `--log-to-
stdout`.

| Level | Description | Command line | C++ |
| ----- | ----------- | ------------ | --- |
| 0 | Minimum debug: messages are always printed | `vle -v 0` or `vle` | ` TraceAlways()` or `DTraceAlways()` |
| 1 | Model Debugging: to be used by model developer | `vle -v 1` |    `TraceModel()` or `DTraceModel()` |
| 2 | Extension debugging: extension functions tracking (e.g. "compute" function of "DifferenceEquation" extension) | `vle -v 2` | `TraceExtension()` or `DTraceExtension()` |
| 3 | DEVS debugging: DEVS functions tracking (e.g "internalTransition" of "Dynamics") | `vle -v 3` | `TraceDevs()` or `DTraceDevs()` |

The level modes are cumulative. For example, if one uses mode 2, traces
available at levels 0, 1 and 2 are printed into the log file.

For example the following atomic model will show always the string "MyModel
constructor" but show the string "time is odd" only when time is odd and VLE is
launched with `vle -v x` with `x` equal 1, 2 or 3.

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
            TraceAlway("MyModel constructor");
        }

        virtual void internalTransition(
                    const vle::devs::Time& time)
        {
            if (static_cast<int>(time) % 2 == 0)
                TraceModel("time is odd");
        }
    };
    DECLARE_DBG_DYNAMICS(MyModel)

The `DTrace*` macros are removed when the compile mode *Release* is declared, on
contrary of `Trace*` macros. To declare the compile mode *Release* use either:
in the CMake configuration.

    cmake -DCMAKE_BUILD_TYPE=Release ...
    As options of any compiler :
    CFLAGS=-O3 -DNDEBUG


