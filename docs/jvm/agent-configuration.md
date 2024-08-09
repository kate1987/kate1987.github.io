# Customize the Lightrun Java agent

According to the Lightrun actions you specify, the agent dynamically inserts logs, metrics, and snapshots into the target environment. The agent's behavior when performing these tasks is governed by a set of user-configurable properties.

## Agent properties

You can modify the agent's behavior by configuring its properties. Configuring the agent properties can be done either from the command line flags or from the `agent.config` file. The agent properties are defined per agent.

### Setting agent properties from the command line

You can flexibly set many of the available agent properties as part of the command when running your application.

Some are passed as “agent flags”, with additions to the agentpath parameter. 

```bash
-agentpath:<path-to-agent>/lightrun_agent.so=--<parameter>=<value>,--<parameter>=<value>... <AppName>
```

Others are passed as JVM flags using the -D syntax.

```bash
-agentpath:<path-to-agent>/lightrun_agent.so -D<flag>=<value> <AppName>

```

!!! example

    The example below shows both kinds of flags:

    ```bash
    java -agentpath:/agent/lightrun_agent.so=--lightrun_extra_class_path=<PATH_TO_JAR> -Dcom.lightrun.secret=<YOUR-SECRET>  <AppName>
    ```

See the tables below for details.

### Setting agent properties from the `agent.config` file

To manually set agent properties in the `agent.config` file:

1. On the server where the application is running, navigate to `<install_dir>/agent/agent.config`.
2. In the `agent.config` file, edit the values for the relevant properties.

!!! important
    You must save the changes and restart the application to apply the new configuration.

## Agent properties list

The following tables describe the agent properties that you can customize for an agent.

### JVM flags

!!! info
    Use `-D` to pass these through the command line

| Parameter name                       | Explanation                          | Default value                        | Type                                 |                     
| ------------------------------------ | ------------------------------------ | ------------------------------------ | ------------------------------------ |
| `com.lightrun.server` | URL of the Lightrun server.  The correct path is automatically inserted. Must not be modified.  | None | string |
| `com.lightrun.secret` | Lightrun agent API key | None | char(64)  |
| `com.lightrun.DynamicLog.handlers` |File  and error log handlers where to send logs | `java.util.logging.FileHandler` <br>`java.util.logging.ConsoleHandler` | string |
| `com.lightrun.DynamicLog.ConsoleHandler.formatter` | Specifies the name of a `Formatter` class to use | None | string |
| `com.lightrun.DynamicLog.ConsoleHandler.pattern` | Specifies the error log file name pattern | None | string |
| `com.lightrun.DynamicLog.FileHandler.formatter` | specifies the name of a `Formatter` class to use | None | string |
| `com.lightrun.DynamicLog.FileHandler.pattern` | Specifies a pattern for generating the output log file name. `"%u"` is a unique number automatically assigned at runtime | `/tmp/lightrun_file_handler_logs%u.log` | string  |

### Agent flags

!!! info
    Use `--` to pass these through the command line

| Parameter name                       | Explanation                          | Default value                        | Type                                 |                     
| ------------------------------------ | ------------------------------------ | ------------------------------------ | ------------------------------------ |
| `max_dynamic_log_rate`               | Maximum allowed ratio of logs printed (the higher ratio, the more logs are allowed to be printed)                        | 60                        |int32                        |
| `max_condition_cost`                 | Maximum allowed additional CPU load when inserting actions during condition evaluation (value between 0.1 and 1.0)  | 1.0 | float |
| `max_log_cpu_cost` | Maximum allowed additional CPU load when logging (value between 0.1 and 1.0) | 1.0 | float |
| `max_snapshot_buffer_size`           | Maximum allowed total bytes for snapshots                        | 655360                  | int32                 |
| `log_stats_time_micros`   | How often (in microseconds) to log debugger performance statistics. Set to zero to never log stats|  3000000                |  int32       |
| `breakpoint_expiration_sec`          | Time-to-live for actions                | 3600            | int32           |
| `dynamic_log_quota_recovery_ms`      | Time in milliseconds to pause a dynamic log after quota is reset | 500                           | int32 |
| `ignore_quota`                       | Disable performance safety measures - **USE WITH CAUTION** | 0 | bool |
| `pinned_certs` | 64 character sha256 certificate public key hash for pinning | 515a630cfd1fb908<br>e30087bcc20b7413<br>ad146b9bf2b23d3a<br>aa72c28e45b24fb2 |char(64) |
| `enable_pii_redaction`               | Enable personally identifiable information (PII) redaction at the agent's side (may affect the application's performance) | 0 | bool |
| `exit_after_report_all`                | Agent empties queues before the application exits. | 0 | bool|
| `longpolling_timeout_milli` | The timeout duration, in milliseconds, for long-polling requests. It defines the maximum time the server should wait for new data to become available before timing out the request. | 30000 | int32  |
| `max_dynamic_log_bytes_rate`         | Maximum allowed output rate for logs (bytes per second)          | 204800    | int32    |
| `max_snapshot_frame_count`           | Maximum allowed snapshot frame count                             | 5                     |  int32                    |
| `capture_object_explore_max_depth`| Sets the maximum depth of nested objects. <br> Note: Supported from version 1.38.  | 50 | int32|
| `snapshot_object_max_members`| Controls the number of properties captured in an object. <br> Note: Supported from version 1.38.|100| int37|
| `snapshot_expression_max_collection_size`|Controls the number of items captured for a collection in a watch expression. <br> Note: Supported from version 1.38.| 1024| int32|
| `transmission_bulk_max_size` | The maximum number of action updates allowed to be transmitted in a single batch. | 10 | int32 |
| `invokedynamic_enabled` | Enables invokedynamic bytecode instruction support | 0 | bool |
| `boxing_unboxing_enabled` | Enables or disables Java expressions and conditions autoboxing and unboxing support. Value can either be `0` (disabled), or `1` (enabled). | `1` (enabled) | bool |
| `agent_log_max_file_size_mb` | Maximum size in MB that a log file can reach before being rotated. | 10 | int32  |
| `agent_log_max_file_count`  | Maximum number of rotated log files to keep. Note that old files get deleted when this number of log files is reached.     | 5                                | int32  |
| `agent_log_target_dir `  | Sets the target directory for storing agent logs, which defaults to the operating system's temporary folder. <br>From version 1.33, the log filename will be generated automatically according to the format: `lightrun_java_agent.<PID>.<TIMESTAMP>.<LOG_ROTATION_RUNNING_INDEX>.log`. For example: `lightrun_java_agent.22840.20240513-153557.1.log`. <br><br> Note: For Java agents running on Windows, the path syntax requires the use of double backslashes, as demonstrated: `agent_log_target_dir=C:\\Users\\user\\AppData\\Local\\Temp` | String |
| `agent_log_level` | Minimum log level that is written to the log file. Available levels of severity, from the highest to lowest (not case sensitive): `None`, `Fatal`, `Error`, `Warning`, `Info`, `Debug`, and `Verbose` | `Info`  | String  |

### Additional command line flags

The following flags can be set only from the command line:

|Parameter|Explanation|Type|
|---|---|---|
|`lightrun_extra_class_path`   |Additional directories and files containing resolvable binaries. You can specify an absolute path with a range of filenames using wildcard characters that adhere to glob patterns. <br>Note:<br> - Wilcard support is supported from version 1.18.1.|string|
|`lightrun_extra_class_path_delimiter` | Set the delimiter character in the `lightrun_extra_class_path`. By default, the delimiter is set using a colon (`:`) character. You can specify an absolute path with a range of filenames using wildcard characters that adhere to glob patterns.<br><br> *Note: Wilcard support added in version 1.18.1. | bool |
|`lightrun_exclude_class_path`| Prevent `JAR`, `WAR` and `EAR` file types from being loaded and indexed when the Java agent launches, even though they are included in paths that are listed in the `CLASSPATH` environment settings. This option is intended to reduce the CPU and memory required for launching our agent by excluding these irrelevant classes. You can specify an absolute path with a range of filenames using wildcard characters that adhere to glob patterns.<br><br> *Note: Wilcard support added in version 1.18.1.| string |
| `lightrun_exclude_class_path_delimiter` | Set the delimiter character in the `lightrun_exclude_class_path`. By default, the delimiter is set using the colon (`:`) character. | bool
| `index_compressed_archives` | Allows loading compressed archives, In addition to native Java archive types such as `JAR`, `WAR` and `EAR`. The compressed archives are decompressed and any `JAR`, `WAR` or `EAR` file included in them is loaded and indexed. You can specify an absolute path with a range of filenames using wildcard characters that adhere to glob patterns. By default, this parameter is set as `false`. <br><br>Note:<br> - The field is availble from version 1.15 with support for `Zip` Archive types.<br> - Wilcard support is supported from version 1.18.1.| bool |
| `lightrun_wait_for_init`     | Block the application until the first time breakpoints are fetched from the server. This option is intended for short-running applications like serverless functions, and it ensures that the Lightrun agent has time to communicate with the Lightrun server before the short-running application disconnects.<br><br> *Note - using `lightrun_wait_for_init` in a cloud environment will likely incur additional costs from the cloud provider due to a longer application runtime.*| bool   |
| `lightrun_init_wait_time_ms`   | Timeout in milliseconds for wait if `lightrun_wait_for_init` is set.  | int32  |

!!! note 
    To add multiple values to the `lightrun_extra_class_path` flag, chain the values together just as you would in a regular JVM CLASSPATH environment value. Use the appropriate separator for your operating system.

## Enabling Lightrun support for invokedynamic bytecode instruction in Java methods

A number of language constructs, such as Lambda functions and plus-operator string concatenation, supported in Java, Groovy, Scala, and Kotlin, are compiled into a special bytecode instruction - `invokedynamic`.
Enabling support for the `invokedynamic` bytecode instruction in Lightrun requires enabling the feature in the agent.config file and specifying a dump folder for dynamically created classes. Once activated, Lightrun can process expressions or conditions containing calls to methods with the `invokedynamic` bytecode instruction. 

An example of a Lightrun condition or experssion can be demonstrated as follows:

`methodA().methodB() == methodC()`

In this example, if any of the methods — `methodA`, `methodB`,  or `methodC` include an `invokedynamic` bytecode instruction, Lightrun can process the condition. This includes scenarios where Lambda calls occur within their execution flow, whether immediately or recursively.

However, it is important to note this known limitation: You cannot add syntax reliant on the `invokedynamic` bytecode instruction directly within the condition or expression, such as Lambdas and plus-operator string concatenation. Nevertheless, when the `Invokedynamic` instruction is within a compiled class in your application, Lightrun conditions and expressions will be able to process it. 

##### TO ENABLE INVOKEDYNAMIC BYTECODE INSTRUCTION SUPPORT

1. Configure the `invokedynamic_enabled` parameter in your `agent.config` file.
   
    `invokedynamic_enabled = 1`
    
2. Specify a dump folder. The process differs depending on the Java version being used.
   - For Java versions 20 and lower

    1. Specify a dump folder to allow the JVM agent to read your generated Lambda classes.
    2. Create a new folder, for example: `/myapp/dump`.
    3. Add the new folder in your JVM options.
   
       `-Djdk.internal.lambda.dumpProxyClasses=/myapp/dump`

    4. Add the new folder to your CLASSPATH.

        `-classpath  [other_classpath_items]:/myapp/dump`

   - For Java versions 21 and higher
    
    1. Enable dumping of dynamically created Lambda classes. 
    Note that the JVM will dump the dynamically created lambda classes to the following path: 
    
        `{projectDir}/DUMP_LAMBDA_PROXY_CLASS_FILES`
       
        `-Djdk.invoke.LambdaMetafactory.dumpProxyClassFiles=true`

    2. Add the dump folder to your CLASSPATH. Note that the folder name is system-defined and cannot be altered.
       
        `-classpath [other_classpath_items]:{projectDir}/DUMP_LAMBDA_PROXY_CLASS_FILES`