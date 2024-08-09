# Installing Lightrun .NET agent on IIS

You can install the Lightrun .NET agent on the IIS (Internet Information Services) framework, a flexible, secure, and manageable web server designed for hosting web apps.

Follow the initial instructions for installing the agent using the Lightrun NuGet package, as outlined in the [.NET Installation](/dotnet/agent/). Subsequently, proceed with the following steps to set the required environment variables, bearing in mind that this process differs in IIS and involves additional configuration steps for the application pool.

!!! note
    
    In IIS, each web application belongs to an `Application Pool`.
    To debug an IIS application, the corresponding `Application Pool` must contain only that application.
    This limitation arises because debugging is enabled for the entire `Application Pool`,  and other web application won't function properly without the `Lightrun` agent.
    

## Configuring the application pool in IIS

1. Open the IIS Manager and select `Configuration Editor`.
2. Select the `system.applicationHost/applicationPools` section.
3. Locate the required `Application Pool` to update its environment variables.

    ![Setting environment variables for .Net Core](/assets/images/dotnet-iis-application-pool.png)

    The environment variables differ for .NET Core and .Net Framework.

4. Proceed to set the environment variables based on their respective types.

### Set .NET Core environment variables

The .NET Core environment variables include the `CORCLR_` prefix and should be set as follows:

```ini
CORCLR_ENABLE_PROFILING=1
CORCLR_PROFILER={FC15CFC2-6CE8-45DF-A754-079254E0077B}
CORCLR_PROFILER_PATH_64=PUBLISH_DIRECTORY\lightrun\win-x64\Lightrun.ClrProfiler.Native.dll
CORCLR_PROFILER_PATH_32=PUBLISH_DIRECTORY\lightrun\win-x86\Lightrun.ClrProfiler.Native.dll
```

!!! imp "Important"
    `PUBLISH_DIRECTORY` should be changed to the actual directory where the web application is published.

![Setting environment variables .NET Core](/assets/images/dotnet-iis-core-variables.png)

### Set .NET Framework environment variables

To initialize the Lightrun agent in .Net Framework, set the `processModel/loadUserProfile` property to `True`.

![Enabling loadUserProfile](/assets/images/dotnet-iis-load-user-profile.png)

The .Net Framework environment variables include the `COR_` prefix and should be set as follows:

```ini
COR_ENABLE_PROFILING=1
COR_PROFILER={FC15CFC2-6CE8-45DF-A754-079254E0077B}
COR_PROFILER_PATH_64=PUBLISH_DIRECTORY\lightrun\win-x64\Lightrun.ClrProfiler.Native.dll
COR_PROFILER_PATH_32=PUBLISH_DIRECTORY\lightrun\win-x86\Lightrun.ClrProfiler.Native.dll
```

!!! imp "Important"
    `PUBLISH_DIRECTORY` should be changed to the actual directory where the web app is published.

![Setting environment variables .Net Framework](/assets/images/dotnet-iis-framework-variables.png)

!!! note
    
    **Applicable only to .NET agent versions lower than 1.36.3**.

    `DebugType` should be set to **embedded**.

    Locating PDB files works differently for .Net Framework apps on IIS.  
    Make sure your project file (`.csproj`) includes the following:
      ```
       <PropertyGroup>
            <DebugType>embedded</DebugType>
       </PropertyGroup>
      ```
