# Lightrun for .NET Framework

**To use Lightrun in a .NET Framework application:**

1. Open a terminal and change to the working directory where your project is located.
2. Install the .NET agent with the NuGet package manager.
	```
	dotnet add package Lightrun
	```

3. Add the Lightrun agent to the top of your application’s main file. (i.e., `Program.cs` file).
	```
	using Lightrun
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

5. Run your application.