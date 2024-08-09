# Customize .NET agent dynamic logs for logger integration

!!! note

    This feature is available for the Lightrun .NET Agent.

This guide describes how to customize Lightrun logs to align with your application's logger format. Lightrun supports the integration of dynamic logs into your application's existing logs, maintaining the application’s log format and structure. If your application is configured to send logs to log management tools such as Kibana or New Relic, you can also include dynamic logs in real-time during runtime. These dynamic logs will be piped to those tools along with your application's static logs. For more information, see [Dyanmic Logs Overview](https://docs.lightrun.com/actions/dynamic-logs/).

## Before you begin

- Keep in mind that later, when creating Lightrun logging actions, you will need to ensure that the [Target](https://docs.lightrun.com/actions/output-routing/) for the Lightrun action(s) includes `Stdout`.

    ![Source Stdout --half](../assets/images/stdout-target.png)

## Set up the custom dynamic logger

To configure a custom dynamic logger, add the `CustomDynamicLogger` property, which is of type `IDynamicLogger`.

```csharp
public interface IDynamicLogger
{
    void Log(LogEntry entry);
}
```

The `IDynamicLogger` interface consists of a single method, `Log`, which takes a LogEntry parameter containing the severity of the log entry and the corresponding message.

By implementing this interface and passing the implementation object to the `CustomDynamicLogger` property, you can seamlessly integrate support for any logging library.

!!! note

    While Lightrun offers a generic method for customizing dynamic logs, several popular logging frameworks are already supported without the need for implementing the `IDynamicLogger` interface. Instead, there exists a function specifically designed to convert the logger instance of a logging framework into an `IDynamicLogger`. It's important to note that the list of supported frameworks is continually expanding, reflecting our commitment to enhancing compatibility over time.

## Configure the dynamic logger with Log4Net

You can set up a Log4Net instance as a custom dynamic logger for the Lightrun .NET agent. The `LogManager` is a class from Log4Net to request logger instances. `Log4NetLogger` is a function from the Lightrun agent that creates the `IDynamicLogger` instance from a Log4Net `ILog` instance.

```csharp
// Get the logger instance.
// It's assumed that the Log4Net logger is already configured by this time.
var lightrunLogger = LogManager.GetLogger("LIGHTRUN");

var options = new AgentOptions
{
    // ...
    // other options
    // ...
    CustomDynamicLogger = Log4NetLogger(lightrunLogger)
};

LightrunAgent.Start(options);
```
