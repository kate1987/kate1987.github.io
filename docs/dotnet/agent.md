# Install the Lightrun .NET agent

The Lightrun agent is at the core of the Lightrun platform. It's the component that communicates requests for runtime observability to your running code, and gathers and relays the requested data back to the Lightrun Server, and eventually the developer's IDE.

Before running the agent, it must be installed on the system where your code to be monitored is running. In addition, you will need to provide credentials which will be used when the agent connects to the Lightrun server.

!!! reqs "System requirements"
	Lightrun for .NET supports Windows and Linux. For more information, please check out the .NET agent system requirements [here](/dotnet/system-requirements/).

## Direct installation

1. Open a terminal and change to the working directory where your project is located.
2. Install the .NET agent with the NuGet package manager:
	```
	dotnet add package Lightrun
	```

3. Add the Lightrun agent to the top of your application’s main file. (i.e., `Program.cs` file):
	```
	using Lightrun;
	```

4. Add the following lines of code to the entry point of your application.
	```
	LightrunAgent.Start(new AgentOptions {
		Secret = "<LIGHTRUN_SECRET>",
	});
	```

  !!! info "Getting Company Details"
      You can get your `<LIGHTRUN_SECRET>` key by logging into the [Management Portal](https://app.lightrun.com) and inspecting the **Set up an agent** section.


  !!! note
      Other configuration parameters can also be passed here. For example, add the `ServerUrl` parameter to the `LightrunAgent.Start` command when using Lightrun On premise.

      ```
		LightrunAgent.Start(new AgentOptions {
			Secret = "<LIGHTRUN_SECRET>",
			ServerUrl = “<server_url>”
		});
      ```

5. Make sure your project file (`.csproj`) includes the following:
      ```
       <PropertyGroup>
            <DebugType>portable</DebugType>
       </PropertyGroup>
      ```

6. Set the required environment variables for automatic instrumentation to attach to your application. For a list of the variables, see the 'Required Environment Variables' section.
7. Run your application.

## Required Environment Variables

For the Lightrun agent to attach to the .NET runtime, set the following environment variables.

### Use predefined `lightrun.sh` (Recommended for Linux)

The Lightrun package provides a `lightrun.sh` script to simplify setting these environment variables on Linux. When you build your project, the script is copied to the output directory, and to locate it, we recommend a straightforward search for `lightrun.sh`. The script can be used as follows:

```shell
PUBLISH_DIRECTORY/lightrun.sh dotnet YOUR_APP_ASSEMBLY.dll
```

`PUBLISH_DIRECTORY` should be changed to the actual directory where the web app is published.

### Set the variables manually

**.NET Core on Linux**

```ini
CORECLR_ENABLE_PROFILING=1
CORECLR_PROFILER={FC15CFC2-6CE8-45DF-A754-079254E0077B}
CORECLR_PROFILER_PATH=PUBLISH_DIRECTORY/lightrun/linux-x64/Lightrun.ClrProfiler.Native.so
```

**.NET Core on Alpine Linux**

```ini
CORECLR_ENABLE_PROFILING=1
CORECLR_PROFILER={FC15CFC2-6CE8-45DF-A754-079254E0077B}
CORECLR_PROFILER_PATH=PUBLISH_DIRECTORY/lightrun/linux-musl-x64/Lightrun.ClrProfiler.Native.so
```

**.NET Core on Windows**

```ini
CORECLR_ENABLE_PROFILING=1
CORECLR_PROFILER={FC15CFC2-6CE8-45DF-A754-079254E0077B}
CORECLR_PROFILER_PATH_64=PUBLISH_DIRECTORY\lightrun\win-x64\Lightrun.ClrProfiler.Native.dll
CORECLR_PROFILER_PATH_32=PUBLISH_DIRECTORY\lightrun\win-x86\Lightrun.ClrProfiler.Native.dll
```

**.Net Framework**

```ini
COR_ENABLE_PROFILING=1
COR_PROFILER={FC15CFC2-6CE8-45DF-A754-079254E0077B}
COR_PROFILER_PATH_64=PUBLISH_DIRECTORY\lightrun\win-x64\Lightrun.ClrProfiler.Native.dll
COR_PROFILER_PATH_32=PUBLISH_DIRECTORY\lightrun\win-x86\Lightrun.ClrProfiler.Native.dll
```

!!!Note

    `PUBLISH_DIRECTORY` should be changed to the actual directory where the web app is published.
