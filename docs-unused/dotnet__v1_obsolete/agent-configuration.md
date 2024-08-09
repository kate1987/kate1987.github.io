# Tuning the agent configuration

According to the Lightrun actions you specify, the agent dynamically inserts logs and snapshots in the target environment. The agent's behavior when performing these tasks is governed by a set of user-configurable properties.

## Agent properties

You can specify the agent properties within your code, by using environment variables, or using an `agent.config` file.

### Specifying agent properties within the code

You can specify your agent configuration parameters by entering the parameters in the `Lightrun.Start` command. 

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

You can also specify the agent properties using an `agent.config` file. Add the path to the `agent.config` file in your `Lightrun.Start` command using the `AgentConfigFile` parameter as shown in the example below.

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

The following table lists the configuration parameters that can be set in the `agent.config` file, environment variables, or the `Lightrun.Start` command.

|Parameter name| Description| Type | Default value|
|----|----|-----|-----|
|`ServerUrl`| Lightrun server URL | URL | app.lightrun.com|
|`Secret`| Your organization's Lightrun secret key| String | |
| `Tags` | An array of strings containing the tags to register the agent with. See [metadata and tagging](/dotnet/metadata-and-tagging/) for more information. | Array | Production|
| `DisplayName` | A unique name to identify the agent. | String | |
| `MaxConditionCost`| Maximum allowed additional CPU load when inserting actions during condition evaluation (value between 0.1 and 1.0).| double | 1.0 |
| `MaxDynamicLogRate`| Maximum rate of dynamic log entries (logs produced per second) in this process. | Integer | 60 |
| `DynamicLogQuotaRecoveryMs` | Time in milliseconds to pause a dynamic log after quota is reset. | Integer | 500 |
| `MaxSnapshotBufferSize` | Maximum allowed total bytes for snapshots | Integer | 65536 |
| `MaxSnapshotFrameCount` | Maximum number of snapshot frames that should contain variables. | Integer | 5 |
| `MaxStackDepth` | Maximum number of stack frames for which to capture data in a single snapshot. | Integer | 20 |
| `IgnoreQuota` | Disable performance safety measures - *USE WITH CAUTION*. | Boolean | false| 
| `LogDir` | The directory in which internal agent logs file are stored. If the value is empty (undefined or empty string), the logs are transmitted to the console. | String | Temp Folder | 
| `RegistrationMetadataFile` | Path to a JSON file containing the agent's registration metadata (such as tags, and display name). | String | |
| `CertificatePinningEnabled` | Enable/disable certificate pinning. Setting to false skips certificate checking. | Boolean | true |
| `PinnedCerts` | 64 character sha256 public key certificates hashes for certificate pinning. | String | |
| `RedactionEnabled` | Enable personally identifiable information (PII) redaction at the at the agent's side, as opposed to server side which is the default. This may be enabled to ensure that sensitive data never reaches the server, but at a cost of additional compute done within the agent which may affect application performance. Regardless of the setting, PII filters ensure sensitive data never reaches the IDE plugin or 3rd party integrated APMs. | Boolean | false |
| `LogCollectionCooldownMs` | The time to wait before resuming logging activity when logging is paused due to CPU throttling, in milliseconds. | Integer | 0 |
| `LogCollectionMaxBytes` | The maximum volume of log data to send to the server upon log collection request. | Integer | 0 |
| `MethodEvaluation` | If enabled, the debugger will attempt to perform method calls (including property getters) when evaluating conditions or expressions of a dynamic log or snapshot. <br> <br> - *USE WITH CAUTION. Enabling this option can result in modification of application state.* | Boolean | false |
| `PropertyEvaluation` | If enabled, the debugger will attempt to evaluate class properties. <br> <br> - *USE WITH CAUTION. Enabling this option can result in modification of application state.* | Boolean | false |
| `CollectBaseClassMembers` |  If enabled, the debugger will attempt to collect members of objects' base classes. <br> <br> - *Experimental flag, disabled by default, use if base class members are necessary.* | Boolean |false|
| `DisableStructPropertiesEvaluation` |  If enabled, the debugger will disable the evaluation of struct properties. | Boolean |false|