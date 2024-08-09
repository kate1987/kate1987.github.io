# Action Output Target

You can configure where you would like to view your Logs and Metrics output by specifying the preferred target in the action configuration. 

There are two main action targets.

| Target | Description                                                  |
| ---- | ------------------------------------------------------------ |
| **Stdout**  | The default option. Logs and Metrics are routed only to the application's standard output.|
| **Plugin**  | Logs and Metrics appear in the Lightrun Console, Management Portal, and any other configured logging tool( see [integrations](/integrations/overview){:target="_blank"}). |

Lightrun Snapshot stack traces are displayed under the Snapshots tab within the Lightrun plugin and also sent to the [Lightrun Management Portal](/snapshots), where they can be retrieved by any authorized user for offline analysis.

!!! guard "Quota configuration"
    Lightrun limits its usage of CPU, memory, I/O (the amount of outputted logs) and other system resources to protect the app performance.
    Users with `IGNORE_QUOTA` role can choose to ignore the agent quota limitations.
    The quota limits can be changed per agent by passing different Lightrun configuration, one way to change the configurations is using the `agent.config` file.

    See each runtime's advanced configuration section for particular details:  

     - [Java/JVM](/jvm/agent-configuration){:target="_blank"}
     - [Node.js](/node/agent-configuration){:target="_blank"}
     - [Python](/python/agent-configuration){:target="_blank"}