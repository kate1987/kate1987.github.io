# Lightrun Overview

test2
Lightrun is a developer-centric observability platform created by developers, for developers.  Its core mission is to empower developers like you to dynamically check for issues and debug your code on the fly, liberating you from the need to predict every imaginable edge case or attempt to recreate unexpected issues in different environments.
At the heart of Lightrun are its proprietary Lightrun Actions, which encompass dynamic logs, snapshots, and metrics. These Actions grant you unparalleled access to code-level insights from any line of code, providing invaluable context during exceptions and augmenting your ability to monitor and comprehend code execution across various pathways.

<iframe width="560" height="315" src="https://www.youtube.com/embed/z-mGBJQt7fM?si=7CLtzNyTn2Xfkmua" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## What can I use Lightrun for?

Lightrun offers code-level deep inspection at the micro-granular level, allowing you to troubleshoot, test, and debug your applications by investigating issues directly from the environment where they are running, whether it's development, staging, or production. No hotfixes, restarts, or redeployment are required. Seamlessly integrating into your personal workflow and toolchain including IDEs and APMs (Application Performance Monitoring), and logging tools, Lightrun facilitates swift code instrumentation and issue resolution.

Furthermore, Lightrun eliminates the need for costly developer lifecycle operations like local replication or software version updates merely to incorporate new logs or metrics. By enabling developers to observe and tackle the ‘unknown unknowns’ on the fly, Lightrun delivers unparalleled observability without necessitating redeployment, ensuring maximum efficiency and productivity.

## Bridging the observability gap

Traditionally, exceptions, logs, performance metrics and traces have been embedded in code during the development stage. But, with the advent of the cloud, followed by microservices and serverless architectures, an observability gap emerged between development and production environments, rendering it nearly impossible to anticipate production-only issues or reproduce them.
Lightrun is the first platform to shift observability left, granting developers 100% visibility into their code, regardless of the deployment environment or infrastructure, whether it's monolithic or highly distributed.

Using Lightrun, developers enjoy transparent access to exceptions as they occur, allowing them, on demand and in real time, to securely add logs, metrics, and traces to their application code while its running in production, staging, or development environments.

## Lightrun typical use cases

Developers use Lightrun for multiple and diverse code-level observability goals, including:

### Testing and debugging

- Implementing code-level alerts.
- Verifying new features as part of progressive enhancement delivery, utilizing techniques like blue/green toggles and feature flags.
- Testing and debugging within progressive enhancement workflows.
- Onboarding new developers with legacy applications.
- Investigating code flows for better understanding and optimization.
- Shifting left observability by debugging:
  - CI/CD Pipeline.
  - Distributed cloud-native applications.
  - Legacy and monolith applications.
  - Third-party or operating system code.
  - ML pipelines and Big Data infrastructure.
  - Feature flag activations providing full visibility into the delivery process.

### Performance analysis

- Running performance analysis with on-demand metrics.
- Conducting pinpoint performance monitoring.
- Prioritizing security CVEs.
  
### Troubleshooting

- Migrating data centers to cloud or microservices architectures.
- Troubleshooting microservices, serverless computing, and Big Data workers.

## Lightrun features and benefits

Lightrun enables in-depth introspection of operational production code at the finest granularity, without any adverse effects. By securely adding Lightrun's logs, snapshots, and performance metrics, you can debug running production code, on demand in real-time, as needed.

The following table provides a summary of Lightrun's capabilities and the benefits it offers to developers.

| Lightrun features                         | Developer benefits                                                                                                                                                                                                                                                                                         |
|------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Multi-language support                   | The Lightrun plugin is fully supported and validated across multiple languages, including Java, Scala, Kotlin, Node.js, Python, and .NET.                                                                                                                                                                 |
| Developer-centric                        | Lightrun seamlessly integrates into your development workflow, whether through the Lightrun IDE plugin, using Lightrun's CLI client, or with a wide range of compatible third-party application performance monitoring (APM) and logging tools. All Lightrun instrumentation is added from the IDE or CLI tools you’re already using. |
| Fully transparent code observability     | You can invoke logs, metrics, and snapshots conditionally from anywhere in your deployed application code. There is no need to replicate the production environment or re-deploy.                                                                                                                      |
| Guaranteed security                      | Lightrun guarantees the security and privacy of your code with enterprise-level security measures including ISO 27001 certification, encryptions, RBAC and SSO, audit trails, logs, and privacy blacklisting. The Lightrun agent is non-web-based and stateless by design, ensuring that no application code is ever exposed.     |
| Non-breakable                            | Add multiple logs, snapshots, counters, timers, function durations, and more without breaking the service and with minimal impact on performance. The Lightrun Sandbox verifies and validates full integrity of your application’s behavior when running with Lightrun actions.                         |
| Environment agnostic                    | Lightrun operates everywhere: on-premises, in the cloud (AWS, GCP, Azure), for microservices, for serverless architectures, Kubernetes, and more. Debug in any environment across any infrastructure.                                                                                                   |
| Pipe anywhere                            | From your IDE, you can pipe Lightrun actions to your favorite logging, analytics, and APM tools. Lightrun seamlessly integrates with multiple monitoring, alerting, and big data capture and analytics platforms, such as Prometheus, Datadog, and Statsd.                                                     |
| Contextual tags                          | Lightrun's powerful tagging feature enables you to group active agents according to any criterion such as staging, production, QA, server, division, location, organization and more. You can apply multiple tags in any combination to each agent. Once a Lightrun action (log, metric, snapshot) is bound to a tag, it is automatically added to all of the agents possessing that tag. |

## Lightrun supported deployment types

Lightrun comes in the following deployment types:

- Multi-Tenant SaaS deployment: Utilize a management server hosted on shared infrastructure.
- Single-Tenant SaaS deployment: Utilize a Lightrun-hosted, private management server.
- Private Deployment In the Cloud: Utilize a privately exposed (not accessible from the public internet) management server, on a dedicated AWS account.
- Fully Air-Gapped, on-premise deployment: Utilize a self-hosted management server without exposing any data to the outside world.

## What's next

1. Learn about [Lightrun's architecture](architecture.md){:target="_blank"} and how the platform works.

2. Give [Lightrun a try](/get-started/) or embark on your journey to experience its debugging capabilities firsthand.

3. Start using Lightrun in 3 easy steps.

  1. Install the Lightrun plugin for your IDE:

      - [IntelliJ, PyCharm, and WebStorm](plugin.md)

      - [Visual Studio Code](vscode/vscode-install-plugin.md)

  2. Install the Lightrun agent for your runtime environment:

      - [Java agent](jvm/agent.md){:target="_blank"}

      - [Python agent](python/agent.md){:target="_blank"}

      - [Node.js agent](node/agent.md){:target="_blank"}
      
      - [.NET agent](dotnet/agent.md){:target="_blank"}

  3. Add your [first action](logs.md){:target="_blank"}.