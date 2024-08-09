# Profiler chaining for the Lightrun .NET agent

Starting from version 1.33, Lightrun introduces support for profiler chaining in the .NET agent allowing you to run multiple profiling tools simultaneously on the same application or system. This feature allows developers and operators to gather performance data and insights from different profiling tools concurrently without conflicts or interference.

## What is profiler chaining in .NET?

In practical terms, profiler chaining enables the coexistence of multiple profiling agents or tools, such as Lightrun's .NET agent and other Application Performance Monitoring (APM) tools, such as Datadog on the same .NET application or environment. Each profiling tool can collect specific types of performance data or provide unique insights into the application's behavior.

## Profiler chaining rules and limitations

- Lightrun can run with one additional profiler.

- Profiler chaining is supported in all environments where the .NET agent is supported, except for macOS.

- Chaining is generally supported for any tool that utilizes the .NET Profiling API. However, some tools may offer non-standard configuration flows that could lead to unsupported scenarios.
  The following tools have been thoroughly tested and confirmed to function properly in a chained setup:
    - Dynatrace
    - Datadog
    - OpenTelemetry (OTEL)

- Azure Application Insights is supported for monitoring and telemetry, but attaching an Azure Application Insights profiler isn't possible.


## Handling conflicts on actions with other profilers

The profiler chaining actively monitors all method-modifying operations requested by both profilers, in case of conflicts, they are resolved according to the precedence as follows:

- If a Lightrun user attempts to place an action on a method already modified by the other profiler, the instrumentation request will be blocked, and an error will be generated for the action.
-  If the other profiler attempts to modify a method where a Lightrun action is present, the Lightrun action will be disabled with an error, allowing the other profiler’s operation to take precedence.

It's important to note that once the other profiler modifies a method, Lightrun actions will be prohibited on that method for the entire duration of the process.
## .NET profiler chaining environment variables

Configuring a .NET profiler involves setting up a series of environment variables. When employing profiler chaining, it's essential to configure variables for both Lightrun and any additional profiler that you intend to use. 

### Environment variables syntax conventions

Lightrun follows these conventions for it’s environment variables:

- Prefixing for additional Profiling Tool Variables: Variables related to the additional profiling tool should be prefixed with `OTHER_`. 

- The Lightrun profiler chaining uses a unique set of values for its ID and path, distinct from those employed by the standard Lightrun profiler without chaining. 

  For example, setting up a profile for Datadog will have the following GUID:

  The `OTHER_CORECLR_PROFILER=<profiler id>` environment variable is set as follows: 

  `OTHER_CORECLR_PROFILER={846F5F1C-F9AE-4B07-969E-05C26BC060D8}`
 

| Environment Variable     | Description                                                                                      | Syntax  |
|--------------------------|--------------------------------------------------------------------------------------------------|---------|
| `CORECLR_ENABLE_PROFILING` | Determines whether profiling is active for the current process. By default, if you do not specify this setting, profiling is turned off, which is the same as assigning a value of 0. | Integer |
| `CORECLR_PROFILER`         | Indicates the GUID of the profiler to be loaded into the active process.  | String  |
| `CORECLR_PROFILER_PATH`  |Defines the path to the profiler DLL to be loaded into the current process, applicable to either 32-bit or 64-bit environments. When multiple variables are set, the bitness-specific variables override others, specifying the appropriate profiler version to use. |String  |
| `OTHER_CORECLR_PROFILER`   | Identifies the `Other` alternative profile to run in parallel to Lightrun.                          | String  |
| `OTHER_CORECLR_PROFILER_PATH` | Specifies the path to the library of the Other profiler.                                         | String  |

For more information, see [Runtime configuration options for debugging and profiling](https://learn.microsoft.com/en-us/dotnet/core/runtime-config/debugging-profiling#profiler-location), 

### Example: Run Lightrun with Datadog for .NET Core on Linux

The following example illustrates how to configure the environment variables for running Lightrun and Datadog simultaneously on a Linux system with .NET Core.

```
CORECLR_ENABLE_PROFILING=1
CORECLR_PROFILER={C67C1FAC-843F-4C7A-9545-E09660CF10AB}
CORECLR_PROFILER_PATH=PUBLISH_DIRECTORY/lightrun/linux-x64/ProfilerChain.so
OTHER_CORECLR_PROFILER={846F5F1C-F9AE-4B07-969E-05C26BC060D8}
OTHER_CORECLR_PROFILER_PATH=/opt/datadog/linux-x64/Datadog.Trace.ClrProfiler.Native.so
```

## Configure profiler chaining for .NET environments

When configuring profiler chaining for .NET environments, consider the following setups.

### .NET Core on Linux

```
CORECLR_ENABLE_PROFILING=1
CORECLR_PROFILER={C67C1FAC-843F-4C7A-9545-E09660CF10AB}
CORECLR_PROFILER_PATH=PUBLISH_DIRECTORY/lightrun/linux-x64/ProfilerChain.so
OTHER_CORECLR_PROFILER=<profiler id>
OTHER_CORECLR_PROFILER_PATH=<profiler path>
```

### .NET Core on Alpine Linux

```
CORECLR_ENABLE_PROFILING=1
CORECLR_PROFILER={C67C1FAC-843F-4C7A-9545-E09660CF10AB}
CORECLR_PROFILER_PATH=PUBLISH_DIRECTORY/lightrun/linux-musl-x64/ProfilerChain.so
OTHER_CORECLR_PROFILER=<profiler id>
OTHER_CORECLR_PROFILER_PATH=<profiler path>
```

### .NET Core on Windows

```
CORECLR_ENABLE_PROFILING=1
CORECLR_PROFILER={C67C1FAC-843F-4C7A-9545-E09660CF10AB}
CORECLR_PROFILER_PATH_64=PUBLISH_DIRECTORY\lightrun\win-x64\ProfilerChain.dll
CORECLR_PROFILER_PATH_32=PUBLISH_DIRECTORY\lightrun\win-x86\ProfilerChain.dll
OTHER_CORECLR_PROFILER=<profiler id>
OTHER_CORECLR_PROFILER_PATH_64=<profiler path>
OTHER_CORECLR_PROFILER_PATH_32=<profiler path>
```

### .Net Framework

```
COR_ENABLE_PROFILING=1
COR_PROFILER={C67C1FAC-843F-4C7A-9545-E09660CF10AB}
COR_PROFILER_PATH_64=PUBLISH_DIRECTORY\lightrun\win-x64\ProfilerChain.dll
COR_PROFILER_PATH_32=PUBLISH_DIRECTORY\lightrun\win-x86\ProfilerChain.dll
OTHER_COR_PROFILER=<profiler id>
OTHER_COR_PROFILER_PATH_64=<profiler path>
OTHER_COR_PROFILER_PATH_32=<profiler path>
```