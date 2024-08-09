# Customize the Lightrun Node.js agent

According to the Lightrun actions you specify, the agent dynamically inserts logs and snapshots in the target environment. The agent's behavior when performing these tasks is governed by a set of user-configurable properties.

## Agent properties

You can specify the agent properties within the code, by using environment variables, or using the config file.

### Specifying agent properties within the code

You specify agent properties in the `start` method of your application file as JSON comma-separated parameter-value pairs. For example:

```js
require('lightrun').start({
     lightrunSecret: '<LIGHTRUN_SECRET>',
     propertyName1: 'value' ,
     propertyName2: 'value',
     .....
});
```

Optional metadata properties can be imported from a metadata file referenced in the `start` method. For example:

```js
require('lightrun').start({
    lightrunSecret: '<LIGHTRUN_SECRET>',
    metadata: {
        filename: './agent.metadata.json'
    }
});
```

For more information about metadata, see the [metadata and tagging](metadata-and-tagging.md) article.

When specified in the `start` method, the agent configuration persists between application runs.

### Specifying agent properties using environment variables

An alternative method for configuring agent properties is to enter them as environment variables when running the agent from the command line. A disadvantage of this method is that agent properties do not persist between runs and are required to be input at the command line each time the application is run.

For example, you can configure the Lightrun secret of your application by setting the `<LIGHTRUN_SECRET>` environment variable.

See the table below for all supported environment variables.

### Specifying agent properties using a config file

You can also specify the agent properties using an agent config file `agent.config`, specify the path to the config file using `agentConfigFile` parameter or `LIGHTRUN_AGENT_CONFIG` environment parameter.

For example:

```js
require('lightrun').start({
    agentConfigFile: '<PATH-TO-CONFIG>'
});
```

### Order of precedence

When an application is run with a Lightrun agent, properties are defined in the following order of precedence:

1. Environment variables
2. Start configuration
3. Default configuration

!!! imp "Important"
     Whenever changing agent configurations, save the changes and restart the application to apply the new configuration.

## Configuration properties supported by the Node.js agent

The following table lists agent configuration properties that can be configured either in the application's `start` method, or through environment variables when available.

|Property name|Environment variable|Default value|Description|
|--|--|--|--|
|`lightrunSecret`|`LIGHTRUN_SECRET`|No default value|The company's secret API key, to connect to Lightrun.|
|`apiEndpoint`|`LIGHTRUN_API_ENDPOINT`|`app.lightrun.com`|The endpoint URI, with which the agent communicates|
|`noCheckCertificate`|-|false|If set to true, the agent will not perform certificate pinning when communicating with the API endpoint.|
|`caPath`|-|`node_modules/lightrun/build/src/resources/lightrun-self-signed.pem`|Path to the `pem` file of the CA signing the server's certificate (useful for self-signed certificates).|
|`transmissionBulkMaxSize`|-|10|The maximum size of updates to transmit in a single batch to the server|
|`pinnedCerts`|-|`515a630cfd1fb908e30087bcc20b7413ad146b9bf2b23d3aaa72c28e45b24fb2','ee80811b38e7e6c2dc4cc372cbea86bd86b446b012e427f2e19bf094afba5d12`|List of sha256 certificate public keys for pinning.|
|`agentLog`|-|[Agent Log table](https://docs.lightrun.com/node/agent-configuration/#agent-log)|Configuration related to the internal logs of the agent (not to be confused with the dynamic logs the user adds with the help of the agent).<br><br>Suggested syntax:<br>`agentLog: {agentLogTargetDir: '/foo/bar, level: 'info'}` |
|`metadata`|-|[Metadate table](https://docs.lightrun.com/node/agent-configuration/#metadata)|Agent metadata (such as tags and display name).<br><br>Suggested syntax:<br>`metadata: { filename: ‘./agent.metadata.json’ }`||
|`log`|-|[Log table](https://docs.lightrun.com/node/agent-configuration/#log)|Configuration related to the log action.|
|`capture`|-|[Capture table](https://docs.lightrun.com/node/agent-configuration/#capture)|Configuration related to the Capture (snapshot) action.|
|`quota`|-|[Quota table](https://docs.lightrun.com/node/agent-configuration/#quota)|Configuration related to the quotas on the agent's performance.|
|`extraPaths`|-|-| An array of strings specifying the paths to external files and third-party modules to be scanned for Lightrun actions. For more information, see [ExtraPaths](#extrapaths).|
|`lightrunWaitForInit`|-|false| Block the application until the first time breakpoints are fetched from the server. This option is intended for short-running applications like serverless functions, and it ensures that the Lightrun agent has time to communicate with the Lightrun server before the short-running application disconnects.<br><br> *Note - using `lightrun_wait_for_init` in a cloud environment will likely incur additional costs from the cloud provider due to a longer application runtime.*      |
|`lightrunInitWaitTimeMs`|-|-|  Timeout in milliseconds for wait if `lightrun_wait_for_init` is set.  |
| `redactionEnabled`|-|false|Enable PII redaction in dynamic logs from the agent side.|

### Agent log

|Property name       |Environment variable|Default value|Description|
|--|--|--|--|
|`agentLogTargetDir`|`AGENT_LOG_TARGET_DIR`|OS temp folder|Sets the target directory for storing agent logs, which defaults to the operating system's temporary folder.<br>From version 1.34, the log filename will be generated automatically according to the format: `lightrun_nodejs_agent.<PID>.<TIMESTAMP>.<LOG_ROTATION_RUNNING_INDEX>.log`. For example: `lightrun_nodejs_agent.22840.20240513-153557.1.log`. Prior to release 1.33, the parameter was set as`logsPath`|
| `agentLogLevel` |`AGENT_LOG_LEVEL` |`info`| Minimum log level that is written to the log file. Available levels of severity, from the highest to lowest (case sensitive): `debug`, `info`, `warn`, and `error`. | string  |
| `agentLogMaxFileSizeMb` | `AGENT_LOG_MAX_FILE_SIZE_MB`| Maximum size in MB that a log file can reach before being rotated. | 10 | int32  |
| `agentLogMaxFileCount`|`AGENT_LOG-MAX_FILE_COUNT` | Maximum number of rotated log files to keep. Note that old files get deleted when this number of log files is reached.     | 5 | int32  |
|`collectCooldownMs`|-|1000 * 60|The time to wait before resuming logging activity when logging is paused due to CPU throttling in milliseconds.|
|`maxLogFileBytes`|-|1024 * 1024|The maximum volume of log data to send to the server upon log collection request.|

### Metadata

|Property name|Environment variable|Default value|Description|
|--|--|--|--|
|`filename`|`LIGHTRUN_METADATA_FILE`|No default value|Path to file containing json with the metadata.|
|`registration`|-|{tags: ['Production']}|Metadata registration: <br/>- `tags`: array of strings with the tags to register the agent with. Can also be assigned with the Environment variable `LIGHTRUN_TAGS` that should contain a string of the tags, separated by commas with no spaces.<br/>-`displayName`: the name of the agent that will be displayed by Lightrun.|

### Log

|Property name|Environment variable|Default value|Description|
|--|--|--|--|
|`maxLogsPerSecond`|-|50|Maximum number of logs to record per second per log action.|
|`logDelaySeconds`|-|1|Number of seconds to wait, before resuming, after the `maxLogsPerSecond` rate is reached.|
|`logger`|-|console|Object that implements info(msg), error(msg), warn(msg).|

### Capture

|Property name|Environment variable|Default value|Description|
|---|--|--|--|
|`includeNodeModules`|-|false|Whether to include details about stack frames belonging to `node-core`.|
|`maxFrames`|-|20|Maximum number of stack frames for which to capture data in a single snapshot.|
|`maxVariableSize`|-|256| The maximum snapshot variable string size. To retrieve large values, add them as watch expressions to a snapshot. Note: Introduced in version 1.16.|
|`maxVariableDepth`|-|50| Limit the number of nested properties to reduce the overall capture time. Gathered for deeply nested objects. For example a->b->c with a value of 2 will only take values of a and b.|
|`maxExpandFrames`|-|4|The maximum number of top frames for which to collect full data for (locals and arguments).<br> **Breaking Change**: From version 1.38, the default value has been changed from `5` to `4`.|
|`maxProperties`|-|20|Number of properties gathered on a captured object. Value of `0` disables the limit.<br> **Breaking Change**: From version 1.38, the default value has been changed from `10` to `20`.|
|`maxWatchProperties`|-|1024| Limits the number of properties gathered on large objects to reduce the overall capture time. This also applies to objects that are a collection. For example, setting `const a = [1,2,3]` with `maxProperties: 1` and `maxWatchProperties: 2`, will return `1`,`2`,  when using a watch expression for `a`. Note that this is an extended limitation for Watch expressions.  |
|`maxDataSize`|-|20000|Total 'size' of data to gather. This is a coarse approximation based on the length of names and values of the properties. Value of 0 disables the limit.|
|`maxStringLength`|-|100|Maximum length of captured strings. Value of 0 disables the limit.|
|`maxSnapshotBufferSize`|-|65653| Maximum allowed total bytes for snapshots. This field cannot be set to `0`. Note: Introduced in version 1.16.|
|`maxWatchlistVariableSize`|-|32K| The maximum size of snapshot variables that were specified via watch expressions. Note: Introduced in version 1.16.|

### Quota

|Property name|Environment variable|Default value|Description|
|--|--|--|--|
|`maxConditionCost`|-|1.0|Maximum cost in percentage of CPU consumption of condition evaluation (value between 0.1 and 1.0).|
|`maxCPUCost`|-|1.0|Maximum cost of dynamic logging in percentage of CPU consumption (value between 0.1 and 1.0).|
|`maxDynamicLogRate`|-|30|Maximum rate of dynamic log entries in this process.|
|`maxDynamicLogByteRate`|-|20480|Maximum rate of dynamic log bytes in this process.|
|`ignoreQuota`|-|false|Determines whether quota need to be ignored or not.|

### ExtraPaths

The Lightrun Node.js agent does not scan external files and third-party modules, i.e., `node_modules`, for Lightrun actions by default. To execute Lightrun actions in these files and modules, you have to specify the path to the files/modules using the `extra_path` parameter in your agent configuration.

###### TO specify `extra_paths` with the `start` method.

You can specify the path to the external files/third-party modules in your `start` method using the `extraPath `parameter.

```js
require('lightrun').start({
    lightrunSecret: '<LIGHTRUN_SECRET>',
    extraPaths: ['path/to/file']
});
```

!!! note
	You can add more than one path to the extraPath parameter.
	```js
	require('lightrun').start({
		lightrunSecret: '<LIGHTRUN_SECRET>',
		extraPaths: ['path/to/file', 'path/to/module']
	});
	```


###### To specify `extra_paths` in your `agent.config` file.

You can specify the path to the external files/third-party modules in your `agent.config` file using the `extra_path` parameter.

```
extra_paths = path/to/file, path/to/module
```


!!! imp "Important"
	When specifying `extraPaths`, it is better to use the complete path to the `file/module`. i.e., `node_modules/module_name` instead of just `node_modules` to prevent duplicate file errors.

