# Lightrun .NET Agent Beta Release Notes

## .NET Agent Version 1.25 (SaaS and On-Premise)

**Release Date**: 29 December, 2023 (Beta)

### Feature Enhancements

#### Log4net Support for Dynamic Logs

From this release, you can now customize the dynamic logger to work with Log4NET. As part of Lightrun support of the integration of dynamic logs into your application's existing logs, while maintaining the application’s log format and structure. If your application is configured to send logs to log management tools such as Kibana or New Relic, you can also include dynamic logs in real-time during runtime. For more information, see [Customizing Dynamic Logs](/dotnet_beta/dynamic-logs-customization/).

## .NET Agent Version 1.22 (SaaS)

**Release Date**: 12 December, 2023 (Beta)

### Highlights

#### .NET Agent Beta

We hereby announce the release of Lightrun .NET Agent version 1.22 (Beta). This release has been launched with limited capabilities. In the coming weeks, we will announce additional releases featuring enhanced functionality and resolution for  known issues.

To get started, please refer to the following documentation:

- [.NET Beta System Requirements](/dotnet_beta/system-requirements-beta/)
- [.NET Beta Installation](/dotnet_beta/agent-beta/)
- [.NET Beta Agent Configuration](/dotnet_beta/agent-configuration-beta/)
- [.NET Beta Running on IIS](/dotnet_beta/frameworks/iis/)
- [.NET Beta Dynamic logs customization](/dotnet_beta/dynamic-logs-customization/)

### Unsupported Features

The following features are not supported in the beta version but will be available in future versions:

- Unsupported Agent runtimes: MAC and Linux ARM
- PII Redaction on Agents. Functions on the server side.
- Certificate pinning 
- Blocklisting

### Known Issues and Limitations

- General: 
  - The Lightrun agent cannot run alongside the Datadog agent or with any product that uses the CLR profiler APIs.
  - The Lightrun agent cannot work when the application is executed by the IDE.
- Lightrun actions: 
  - Limitation on watch for property defined on an interface.
  - Actions cannot be added to constructors.
- Lightrun expressions: 
  
  - HashSet content cannot be viewed.
  - Math expressions are not supported.
  - Calling methods is not supported.
  - Properties with code in the getter functions are only collected when they are requested in evaluated expressions.