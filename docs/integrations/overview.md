# Integrate with Lightrun

--8<-- "ux-reference/manager-role-only.md"

Lightrun seamlessly integrates with key third-party vendors to harness valuable and actionable telemetry data generated at runtime, providing a full-cycle observability platform. These integrations facilitate the troubleshooting of complex issues, contributing to the reduction of Mean Time To Resolution (MTTR).
The Lightrun integrations are set up in the Lightrun Management Portal, categorized under All, logs, metrics, and alerts, which can be triggered by events generated by Lightrun.
he currently supported integrations through the **Integrations** page in your Management Portal.

## Real-time integration with Lightrun data
The following real-time data generated and piped to your integrated third-party platforms provides the observability necessary for troubleshooting applications in production:

- Lightrun Metrics: Send Lightrun metrics generated in real-time to the designated partner. This functionality enables developers to collect, emit, visualize, and analyze code-level metrics from a running application. 
  
- Lightrun Logs: Easily Insert real-time dynamic logs into your live application with Lightrun and transmit the collected logs to the designated target for visualization and rapid analysis.


- Lightrun Events: Collect events related to activities in the Lightrun Management Portal, Lightrun plugins, and agents. Send these events to the target partner for valuable insights and continuous  monitoring. Events include user actions, agent registration, Lightrun action creation or deletion, and agent deletion.


![Integrations](../assets/images/integrations-page.png)


## Supported Lightrun integrations

The following table lists the Lightrun integrations categorized by action type.
This list of integrations officially supported by Lightrun is constantly expanding. If you don’t find your favorite tool listed, please reach out to us.

| <center>Vendor</center>             | <center>Metrics</center>                    | <center>Logs</center>                        | <center>Alerts</center>                      |
|--------------------|----------------------------|-----------------------------|-----------------------------|
| [AppDynamics](app-dynamic.md)        | <center>Prometheus external integration</center> | <center>N/A</center>                           | <center>✅</center>                          |                           | <center>External integration</center>       |
| [Datadog (events)](datadog-events.md)| <center>StatsD external integration</center> | <center>[Datadog (logs)](datadog-logs.md)</center>             | [Datadog (events)](datadog-events.md)           |
| [Dynatrace](dynatrace.md)          | <center>✅</center> |<center>✅<center>                           |   <center>N/A</center>                          |
|[Elastic Stack](elastic-stack.md)      | <center>✅</center>                          | <center>✅</center></center>                           |  <center>N/A</center>                           |
| [FluentD](fluentd.md)            | <center>✅</center>                          | <center>N/A</center>                            | <center>N/A</center>                         |
| [Grafana](/integrations/grafana/)            | <center>✅</center>                          | <center>External integration<center>       |<center>N/A</center>   |
| [HashiCorp Nomad](nomad.md)   |<center>N/A</center>  |<center>External intregration</center>  |<center>N/A</center>  |
| [Instana](instana.md)            | <center>StatsD external integration</center> | <center>✅</center>                           | <center>N/A</center>                            |                           |                             |
| [New Relic](/integrations/new-relic/)         | <center>N/A</center>                           | <center>StatsD external integration</center>| <center>✅</center>                           |
| [Prometheus](prometheus.md)         | <center>✅</center>                          | <center>N/A</center>                            | <center>N/A</center>                            |
| [Sentry](/integrations/sentry/)          | <center>N/A</center>                           |<center>N/A</center>                             | <center>✅</center>                           |
| [SIEM](/integrations/siem/)          | <center>N/A</center>                           |<center>N/A</center>                             | <center>✅</center>                           |
| [Slack](https://docs.lightrun.com/slack-alerts-overview-configuration/)              |<center>N/A</center>                            | <center>N/A</center>                            | <center>✅</center>                           |
| [StatsD](statsd.md)| <center>✅</center>                          | <center>N/A</center> | <center>N/A</center>                            |
| [Splunk](/integrations/splunk/) | <center>StatsD external integration</center>|<center>N/A</center>                             | <center>✅</center>                          |
| [Sumo Logic](/integrations/sumo-logic/)| <center>StatsD external integration</center>|<center>N/A</center>                             | <center>External integration<c/enter>       |
