# Configure the agent to handle exceptions

Use the agent.config properties to set exception reporting based on your needs. This is a global file, meaning that once you update the file, all applications attached to the same agent are updated accordingly.

The configuration file is located at the following path:

```bash
    <install_dir>/agent/agent.config
```

!!! note
    Read more about advanced agent configuration [here](../jvm/agent-configuration.md)

--8<-- "ux-reference/manager-role-only 2.md"

###### To enable exception handling 

To start handling exceptions through Lightrun, and to enable your team to view exceptions directly from their IDE, configure the agent as follows:

1. From the relevant server where your application is running, go to the folder where you stored the downloaded agent zip and extracted its files.

2. Open the `agent.config` file.

3. Find the `exceptions_monitoring_enabled` property and set it to `1` so that it looks like this: `exceptions_monitoring_enabled=1`

4. To configure the agent to ignore exceptions that your exceptions handler catches along the way, set the `exceptions_should_report_caught` property to `0`.

     It should look like this: `exceptions_should_report_caught=0`

5. Restart the relevant applications and their installed agents to apply the changes.

!!! tip
     You can also configure exception handling for the agent [from the terminal](/manager_cli_reference/).

## View exception details

Once you've enabled Lightrun to handle exceptions, you can view them [from the Lightrun app](web.md) in the browser and [from the IDE](ide.md) with the Lightrun plugin.
