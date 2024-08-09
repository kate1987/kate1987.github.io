# Customize the Lightrun Python agent

According to the Lightrun actions you specify, the agent dynamically inserts logs and snapshots in the target environment. The agent's behavior when performing these tasks is governed by a set of user-configurable properties.

## Agent properties

You can specify the agent properties within the code or by using a config file.

## Specifying agent properties within the code

You set agent configuration properties by entering keyword arguments in the `lightrun.enable()` call function. For example:

   ```python
   lightrun.enable(server_url="https://mycompany.com/myserver", company_key="123456-abcde")
   ```

 The `server_url` keyword is required only if Lightrun is used as an on-premise deployment.

## Specifying agent properties using a config file

When using `lightrun.enable`, you can either pass the `company_key` parameter (as above), or use the `agent_config` parameter as shown in <a href="https://github.com/lightrun-platform/lightrun/blob/main/examples/other-examples/python/sleep_main.py" target="_blank" download>this example</a>.

  The `agent_config` keyword must reference the full path to a user-created `agent.config` file.

You can see this <a href="https://github.com/lightrun-platform/lightrun/blob/main/examples/other-examples/python/agent.config" target="_blank" download>an example `agent.config`</a> file. The default parameter values can be modified for your own applications.

!!! note
    The above methods for passing keywords can be combined. However, configuration parameters passed as keyword arguments override the parameter values in `agent.config` (if provided).

## Configuration parameters

The following table lists the configuration parameters that can be set in both the `agent.config` file and the `lightrun.enable()` call function.

|  Flag name   | Description | Default value |
|--|--|--|
|`company`|Company name.| - |
| `server_url` | The URL of the Lightrun backend server (default: [https://app.lightrun.com/](https://app.lightrun.com/.server_url) should only be changed when using Lightrun on-premise. | -|
| `com_lightrun_server` | Combined URL of of the company and the Lightrun backend server. This single parameter can be used instead of the combination of `company` and `server_url`. | -|
| `company_key` | The company's secret API key. | -|
| `breakpoint_expiration_sec` | The default expiration time for Lightrun actions. | -|
| `ignore_quota` | Whether or not to disable all performance safety measures. <br> **Warning: Use with caution**. | -|
| `agent_regmetadata_file` | Path to a JSON file containing the agent's registration metadata (such as tags, and display name). | -|
| `metadata_registration_tags` | Array of tags for the agent, can be used when there is no metadata file. You set agent tags by entering `metadata_registration_tags` argument in the `lightrun.enable()` call function. <br>For example: `lightrun.enable(company_key="<COMPANY_SECRET>", metadata_registration_tags='[{"name": "Production"},{"name": "EastUS"}]')`| -|
| `dynamic_log_console_handler_format` | The format for the logs to be printed by inserted logpoints to the console. For example: `'%(levelname)s: %(message)s'`. |-|
| `dynamic_log_file_handler_file_pattern` | The pattern for writing logpoints to a file. If this parameter is left empty, logs from inserted actions are not written to a file. | -|
| `dynamic_log_file_handler_format` | The format for logs from inserted log points to be printed to the file specified in the `dynamic_log_file_handler_file_pattern` | -|
| `base_dir` | Files from this directory will have a higher priority in the case of name conflicts. | sys.path[0]|
| `lightrun_wait_for_init` | Block the application until the first time breakpoints are fetched from the server. This option is intended for short-running applications like serverless functions, and it ensures that the Lightrun agent has time to communicate with the Lightrun server before the short-running application disconnects.<br><br> Note: Using `lightrun_wait_for_init` in a cloud environment will likely incur additional costs from the cloud provider due to a longer application runtime.  | `False` |
| `lightrun_init_wait_time_seconds` | Timeout in seconds for wait if `lightrun_wait_for_init` is set.   | -|
| `max_condition_cost`                 | Maximum allowed additional CPU load when inserting actions during condition evaluation (value between 0.1 and 1.0).  | 1.0 |
| `max_log_cpu_cost` | Maximum allowed additional CPU load when logging (value between 0.1 and 1.0). | 1.0 |
| `max_snapshot_buffer_size` <br/><br/>`max_snapshot_buffer_size_in_bytes` | Maximum allowed total bytes for snapshots. Introduced in version 1.16, and replaces `max_snapshot_buffer_size_in_bytes`. <br/><br/> **Deprecation note:** From version 1.16, This field is deprecated and replaced by `max_snapshot_buffer_size`. <br/> | 65653 <br/><br/><br/> 32768 |
| `max_variable_size`| Maximum snapshot variable string size. To retrieve large values, add them as watch expressions to a snapshot. <br> Note: Introduced in version 1.16 | 256 |
| `max_watchlist_variable_size`| Maximum size of snapshot variables that were specified via watch expressions. Note: Introduced in version 1.16. | 32768 |
|`max_collection_size`| Controls the number of items captured for a collection. <br> Note: Introduced in version 1.36.| 25|
|`max_watchlist_collection_size`| Controls the number of items captured for a collection in a watch expression.<br> Note: Introduced in version 1.36.| 1024 |
|`max_frames_with_vars`| Controls the number of top stack frames for which to read values of local variables.<br> Note: Introduced in version 1.36.| 4|
|`max_object_members`| Controls the number of properties captured in an object. <br> Note: Introduced in version 1.36.|100|
| `default_certificate_pinning_enabled`| Enable/disable certificate pinning. Setting to `false` skips certificate checking. | True |
| `enable_pii_redaction` | Enable personally identifiable information (PII) redaction at the agent's side (may affect the application's performance)	| False |
| `alsologtostderr` | Sends the logs to `STDERR` standard file as opposed to typically sending them over to `STDOUT`. | True |
| `agent_log_max_file_size_mb` | Maximum size in MB that a log file can reach before being rotated. | 10 | int32  |
| `agent_log_max_file_count` | Maximum number of rotated log files to keep. Note that old files get deleted when this number of log files is reached. | 5 | int32  |
| `agent_log_target_dir` | Sets the target directory for storing agent logs, which defaults to the operating system's temporary folder. <br>From version 1.34, the log filename will be generated automatically according to the format: `lightrun_python_agent.<PID>.<TIMESTAMP>.<LOG_ROTATION_RUNNING_INDEX>.log`. For example: `lightrun_python_agent.22840.20240513-153557.1.log`. | String |
| `agent_log_level` | Minimum log level that is written to the log file. Available levels of severity, from the highest to lowest (not case sensitive): `None`, `Fatal`, `Error`, `Warning`, `Info`, `Debug`, and `Verbose`. | Info  | String  |

!!! info
    Except for the parameter `company_key`, all other configuration options have default values.
