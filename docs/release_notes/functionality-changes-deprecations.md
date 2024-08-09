# Functionality changes and deprecations

This document aims to inform you about parameter or feature changes by category type that may result in breaking changes and require your attention. This can help you maintain and troubleshoot your Lightrun agents, plugins, and actions effectively.

Please note that these changes are also described in the relevant release notes.

## Java Agent

| **Parameter/Feature**         | **Description**                                          | **What’s Changed**                                                   | **Up to Version** | **From Version** |
|--------------------------------|----------------------------------------------------------|---------------------------------------------------------------------|-------------------|------------------|
| `max_snapshot_frame_count`    | Maximum allowed snapshot frame count.                    | Lowered the number of snapshots frames.                                    | **≤ 1.37** <br> `5`           | **≥ 1.38** <br>  `4` |
| `index_compressed_archives`   | Supports wildcard for file indexing.                    | Added wildcard support. | ≤ **1.18.0** <br> No wildcard support. | **≥ 1.18.1** <br> Added wildcard support. |
| `agent_log_target_dir`        | Sets the target directory for storing agent logs.        | Changed the format of the agent logs and how they are generated.    |**≤ 1.32** <br> The path for storing the logs was predefined as the default `/temp `file of the operating system.  | **≥ 1.33** <br> You can set the path where the logs are saved. The logs are generated automatically with the following format: <br>`lightrun_java_agent.<PID>.<TIMESTAMP>.<LOG_ROTATION_RUNNING_INDEX>.log`. <br> For example: `lightrun_java_agent.22840.20240513-153557.1.log`. |  

## Node.js Agent

| Parameter/Feature | Description | What’s Changed? | From Version | Up to Version |
|--------------------------------|-------------|-----------------|---------------|--------------|
| `maxExpandFrames`   | Maximum number of top frames for which to collect full data. | Increased the number of top frames. | **≤ 1.37** <br> `5` | **≥ 1.38** <br> `4` |
| `maxProperties`     | Number of properties gathered on a captured object. | Increased the number of properties. | **≤ .37** <br> `10` | **≥ 1.38** <br>`20` |
| `logsPath` | Sets the target directory for storing agent logs. | Parameter renamed. | **≤ 1.33** <br> `logsPath` | **≥ 1.34**  <br>`agentLogTargetDir` |
| `agentLogTargetDir` | Sets the target directory for storing agent logs. | Changed the format of the agent logs and how they are generated. | **≤ 1.33**  <br> Known as `logsPath`. The path for storing the logs was predefined as the default `/temp `file of the operating system.  | **≥ 1.34** <br> The log is generated automatically in the following format: `lightrun_nodejs_agent.<PID>.<TIMESTAMP>.<LOG_ROTATION_RUNNING_INDEX>.log`. For example: `lightrun_nodejs_agent.22840.20240513-153557.1.log`. |

## Python Agent

| Parameter/Feature                    | Description                                          | What’s Changed                              | From Version | Up to Version |
|--------------------------------------|------------------------------------------------------|---------------------------------------------|--------------|---------------|
| `agent_log_target_dir`                 | Sets the target directory for storing agent logs.    | Log syntax change. | **≥ 1.33** <br>The path for storing the logs was predefined as the default `/temp `file of the operating system.  | **≤ 1.34** <br> `<PID>.<TIMESTAMP>.<LOG_ROTATION_RUNNING_INDEX>.log.` 
| `max_snapshot_buffer_size_in_bytes`    | Maximum allowed total bytes for snapshots.  | Deprecated and replaced with a new field.  | **≥ 1.17.0**  <br>`max_snapshot_buffer_size_in_bytes` | **≤ 1.18**<br> `max_snapshot_buffer_size` |

## .NET Agent

| Parameter/Feature | Description                                | What’s Changed?                              | Up to Version | From Version | 
|--------------------------------|--------------------------------------------|----------------------------------------------|---------------|--------------|
| MaxStringLength   | Truncates strings to the set size.         | Lowered the string length truncation value.  | **≤ 1.34** <br> `1000` | **≥ 1.35**  <br> `256`|
| MaxFieldCount     | Maximum number of fields to capture on an object. | Increased the number of fields to capture on an object. | **≤ 1.34**  <br>`20`  | **≥ 1.35** <br> `100` |
