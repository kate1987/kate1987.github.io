## Installing the .NET agent

The Lightrun agent is at the core of the Lightrun platform. It's the component that communicates requests for runtime observability to your running code, and gathers and relays the requested data back to the Lightrun Server, and eventually the developer's IDE.

Before running the agent, it must be installed on the system where your code to be monitored is running, and its credentials must be declared either inside the application code, as environment variables, or in an `agent.config` file.

!!! reqs "Version Support"
	The instructions below apply to .NET and .NET Core versions (5.0, 6.0, 7.0). If you're interested in support for other versions, please [reach out](https://go.lightrun.com/contact-us) and let us know!


!!! reqs "System requirements"
	Lightrun for .NET supports Windows and Linux. For more information, please check out the .NET agent system requirements [here](/dotnet/system-requirements/).

### Direct installation

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
      Other configuration parameters can also be passed here. For example, add the `ServerUrl` parameter to the `Lightrun.Start` command when using Lightrun On-prem.

      ```
		LightrunAgent.Start(new AgentOptions {
			Secret = "<LIGHTRUN_SECRET>",
			ServerUrl = “<server_url>”
		});
      ```

5. Make sure your project file (.csproj) includes the following:
      ```
       <PropertyGroup>
            <DebugType>portable</DebugType>
       </PropertyGroup>
      ```

6. Run your application.
