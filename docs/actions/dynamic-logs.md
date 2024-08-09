When adding Lightrun dynamic logs, it is not required to relaunch the application or release a separate version for debugging. Lightrun logs are added dynamically during runtime, and the log output is visible immediately following insertion in the running code.

Once a Lightrun dynamic log has been inserted into an application, its output is printed to the agent’s standard output, for example, in Java the output is printed to the standard logging framework by the java.util.logging logger. This enables you to view Lightrun logs in the context of pre-existing log statements, which might provide further clues towards investigating and solving issues.

<iframe width="560" height="315" src="https://www.youtube.com/embed/Cz6Y2un_AZc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Typical use cases

With Lightrun dynamic logs, you can:

- Troubleshoot live applications by dynamically adding logs anywhere in the application code.
- Add as many logs as you want until you resolve an issue, using simple or complex conditional statement.
- Add as many logs as you need until you identify the problem.
- Add logs to multiple instances of a running production service (microservices, big data workers) using tags.
- Explore and inspect your logs in your log analysis tool of choice: DataDog, Splunk, Elastic, etc. under the context of existing logs.
- Print the log data straight in your IDE and analyze your code behavior locally.


### More on Dynamic Logs

- [Learn how to create and manage logs in the Jetbrains plugin](/logs)
- [Learn how to create and manage logs in the VSCode plugin](/vscode/vscode-plugin-dynamic-logs)
- [Learn how to manage your logs in the Lightrun Management Portal](/view-logs)
- [Customize Dynamic Logs format for integration into your app's logger](/dynamic-log-customization/)