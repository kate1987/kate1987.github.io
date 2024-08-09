# Customize the Lightrun .NET agent

According to the Lightrun actions you specify, the agent dynamically inserts logs and snapshots in the target environment. The agent's behavior when performing these tasks is governed by a set of user-configurable properties.

## Agent properties

You can specify the agent properties within your code, by using environment variables, or using an `agent.config` file.

### Specifying agent properties within the code

You can specify your agent configuration parameters by entering the parameters in the `LightrunAgent.Start` command. 

For example, 

```
LightrunAgent.Start(new AgentOptions {
    Secret = "<LIGHTRUN_SECRET>",
    PropertyName1 = "value" ,
    PropertyName2 = "value",
});
```

### Specifying agent properties using environment variables

An alternative method for configuring agent properties is to enter them as environment variables. This can be done by adding a `LIGHTRUN_` prefix to the configuration parameter. For example, to set the Lightrun secret key and server url in a `.env` file, we would use something similar to the following:

```.env
//.env file

LIGHTRUN_SECRET=<lightrun_secret_key>
LIGHTRUN_SERVERURL=<lightrun_server_url>
```
 

### Specifying agent properties using an `agent.config` file

You can also specify the agent properties using an `agent.config` file. Add the path to the `agent.config` file in your `LightrunAgent.Start` command using the `AgentConfigFile` parameter as shown in the example below.

```
LightrunAgent.Start(new AgentOptions {
   AgentConfigFile: '<PATH-TO-CONFIG>'
});
```

### Order of precedence

When an application is run with a Lightrun agent, properties are defined in the following order of precedence:

1. Start method parameter
2. Environment variables
3. `agent.config` file

!!! imp "Important"
     Whenever changing agent configurations, save the changes and restart the application to apply the new configuration.

## Configuration parameters

The following table lists the configuration parameters that can be set in the `agent.config` file, environment variables, or the `LightrunAgent.Start` command.

|Parameter name| Description| Type | Default value|
|----|----|-----|-----|
|`ServerUrl`| Lightrun server URL | URL | app.lightrun.com |
|`Secret`| Your organization's Lightrun secret key| String | |
| `Tags` | An array of strings containing the tags to register the agent with. See [metadata and tagging](/dotnet/metadata-and-tagging/) for more information. | Array | Production |
| `DisplayName` | A unique name to identify the agent. | String | |
| `AgentConfigFile` | The path to the config file with extra agent properties | String | agent.config |
| `AgentLogTargetDir` | The directory in which internal agent logs file are stored. | String | Temp Folder | 
| `LogToStandardError` | Switch to logging to STDERR instead of logging to a file.| Boolean | false |
| `AlsoLogToStandardError`| Enable logging to STDERR additionally to logging to a file.| Boolean | false |
| `AgentLogLevel` | Minimum log level that is written to the log file (or to the Standard Error if such logging is enabled)| AgentLogLevel | `AgentLogLevel.Information`|
| `StdErrThreshold` | Minimum log level that is written to the Standard Error. | AgentLogLevel | `AgentLogLevel.Fatal` |
| `AgentLogMaxFileSize` | Maximum size in MB that a log file can reach before being rotated. | Integer | 10 |
| `AgentLogMaxFileCount` | Maximum number of rotated log files to keep, old files get deleted when this value is reached. | Integer | 5 |
| `RegistrationMetadataFile` | Path to a JSON file containing the agent's registration metadata (such as tags, and display name). | String | |
| `CertificatePinningEnabled` | Enable/disable certificate pinning. When set to false, the agent will not perform certificate pinning when communicating with the API endpoint. | Boolean | true |
| `PinnedCerts` | 64 character sha256 public key certificates hashes for certificate pinning. | String | `ee80811b38e7e6c2dc4cc372cbea86bd86b446b012e427f2e19bf094afba5d12` |
| `RedactionEnabled` | Enable personally identifiable information (PII) redaction at the agent's side (may affect the application's performance)| Boolean| false |
| `CustomDynamicLogger` | Custom logger for dynamic logs. Follow the instructions [here](/dotnet/dynamic-logs-customization/) to configure the `CustomDynamicLogger`. | IDynamicLogger | |
| `MaxStringLength`| Truncates strings to the set size. | Integer | 1000 |
| `MaxCollectionSize`| Truncate collections to set size. | Integer | 100 |
| `MaxFieldCount` | Maximum number of fields to capture on an object. | Integer | 20 |
| `MaxDepthToSerialize` | Maximum object depth to serialize. | Integer | 3 |
| `MaxTimeToSerializeMs` | Maximum time in milliseconds for serializing an object. | Integer | 200 |
| `MaxActionCost` | Maximum cost in % of CPU consumption of breakpoint callback. | Double | 1 |
| `IgnoreQuota` | Disable CPU cost limitation. | Boolean | false |
| `RequestTimeoutMs` | Timeout (in ms) used for long-polling the server. | Integer | 20000 |
| `UseSandbox` | Enable/disable sandbox for evaluating expressions | Boolean | false |
| `LogCollectionCooldownMs` | How much time to wait (in milliseconds) between log collection requests from the server. | Integer | 0 |
| `LogCollectionMaxBytes` | The maximum volume of log data to send to the server upon log collection request. | Integer | 0 |
