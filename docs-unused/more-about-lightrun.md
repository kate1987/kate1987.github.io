## Lightrun benefits

Lightrun enables deep introspection of operational production code at the finest granularity with no side effects. By securely adding Lightrun's logs, snapshots, stack traces, and performance metrics, you can debug running production code, on demand in real time. The following table summarizes Lightrun's capabilities and their benefits to developers.

|**Lightrun capabilities** |  **Developer benefits**  |
|:---|:---|
|Multi-language support.   |**Lightrun** is fully validated in multiple runtime environments (Java, Node.js, Python, Scala, and Kotlin). More are in the pipeline.
|Developer-centric |Lightrun seamlessly integrates into your development workflow - from the Lightrun IDE plugin, or using Lightrun's CLI client, to a broad variety of compatible third-party application performance monitoring (APM) and logging tools. All Lightrun instrumentation is added from the IDE or CLI tools you’re already using. |
|Fully transparent code observability at expression level |Invoke logs, metrics, and snapshots, conditionally, from anywhere in your deployed application code. There's no need to replicate the production environment or re-deploy.|
|Guaranteed security    |**Lightrun** guarantees the security and privacy of your code with enterprise-level security measures: ISO 27001 certification, encryptions, RBAC and SSO, audit trail and logs and privacy blacklisting. The **Lightrun** agent is non-web-based and stateless, by design; no application code is ever exposed. Read our [white paper](https://go.lightrun.com/hubfs/Docs/Lightrun_Security_White_Paper.pdf){:target=blank} on **Lightrun** security. |
|Non-breakable  |Add multiple logs, snapshots, counters, timers, function durations, and more, without breaking the service and with minimal impact on performance. The **Lightrun Sandbox** verifies and validates full integrity of your application’s behavior when running with **Lightrun** actions. The **Lightrun Sandbox** guarantees no exceptions, system I/O, system calls, or state/flow changes, and ensures that only read-only code is ever added to your application.|
|Environment agnostic  |**Lightrun** operates everywhere and anywhere: on-prem, in the cloud (AWS, GCP, Azure), for microservices, for serverless, Kubernetes, and more. Debug in any environment across any infrastructure. |
|Pipe anywhere  |From your IDE, you can pipe **Lightrun** actions to your favorite logging, analytics, and APM tools. **Lightrun** integrates seamlessly with multiple monitoring, alerting, and big data capture and analytics platforms, such as [Prometheus](integrations/prometheus.md){:target=_blank}, [Datadog](integrations/datadog-events.md){:target=_blank}, and [Statsd](integrations/statsd.md){:target=_blank}. The list of supported integrations is constantly expanding.  |
|Contextual tags  |**Lightrun**'s powerful tagging feature enables you to group active agents according to any criterion: staging, production, QA, server, division, location, organization, etc. You can apply multiple tags in any combination to each agent. Once a **Lightrun** action (log, metric, snapshot) is bound to a tag, it implicitly is added to all of the agents that possess that tag. |

## Lightrun real-time capabilities

Lightrun's plugin for popular IDEs, such as IntelliJ, PyCharm, and VSCode provide integrated tools for instrumenting and debugging your application code in real-time and on demand. The three Lightrun "actions" that enable this are:

- Dynamic Logs
- Snapshots
- Metrics

For further information see the article on [Lightrun Actions](actions.md){:target="_blank"}.

## Lightrun's architecture {#architecture}

The Lightrun platform is comprised of three parts:

- Management Server: The "backbone" of the Lightrun platform, provided as a SaaS or on-prem deployment. Used as a SaaS, all you need to do is install and run the Lightrun agents within your live apps.

- Client: The Lightrun IDE plugin and command line utility. You can use either of these to add, remove, and modify actions - whichever is part of your natural workflow. Whenever you enter a command to insert an action, the agent receives your request and instruments the running code accordingly.

- Lightrun Agent:  The stateless agent, that runs alongside the application on your application, is at the heart of the Lightrun platform. The agent lets you dynamically insert logs, metrics, and snapshots into your running code.

The Lightrun platform components communicate with one another as illustrated below.

![Lightrun architecture diagram](assets/images/lightrun-architecture-diagram.png)

<figcaption>Lightrun Architecture</figcaption>

## How Lightrun works {#how}

When attaching the Lightrun Agent to your application during runtime, it connects (via HTTPS) to the Lightrun Management Server, allowing secure interaction with the application.

Applying Lightrun actions from your IDE, you can add logs, snapshots, and metrics directly into the running source code of your application - on-the-fly and in any environment.

Once you've added your Lightrun actions, you can immediately view the output directly from the IDE as well, or from the Management Portal in any browser.

For further details, read the Lightrun product [datasheet](https://go.lightrun.com/hubfs/Docs/Lightrun_Datasheet.pdf){:target=_blank}.

![How Lightrun works](assets/images/lightrun-how-it-works.png)

<figcaption>Lightrun Workflow</figcaption>

When a user action, invoked from the Lightrun IDE plugin or CLI, is received, the Lightrun Management Server sends a request to the agent. The agent verifies the stability, integrity, and security of each requested action through the Lightrun Sandbox, before adding the instrumentation to your application at runtime.

Read more [here](https://go.lightrun.com/hubfs/Docs/Lightrun_White_Paper.pdf){:target=_blank} about how Lightrun works.
