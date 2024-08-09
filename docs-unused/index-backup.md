# Introducing Lightrun

Lightrun is a developer-centric observability platform. By securely adding logs, metrics, and traces in real time and on demand, Lightrun empowers you to observe and troubleshoot your running application code. No hotfixes, restarts, or redeployment are required.

<iframe width="560" height="315" src="https://www.youtube.com/embed/5hR17z4Qm3g" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Bridging the observability gap

Traditionally, exceptions, logs, performance metrics and traces have been specified during the development stage. But, with the advent of the cloud, followed by microservices and serverless architectures, an observability gap emerged between development and production environments, rendering it nearly impossible to anticipate production-only issues or reproduce them.

Lightrun is the first platform to shift observability left, granting developers 100% visibility into their code, regardless of the deployment environment or infrastructure, whether it's monolith or highly distributed.

Using Lightrun, developers enjoy transparent access to exceptions as they occur, allowing them, on demand and in real time, to securely add logs, metrics, and traces to their application code while it's running in production, staging, or development environments.

## Enhanced productivity

Lightrun was created by developers for developers. Lightrun enables rapid code instrumentation and resolution of issues by seamlessly integrating into the developer's personal workflow and toolchain (IDE, APM, and logging tools).

Lightrun eliminates the need to predict every edge case imaginable or reproduce environments that can’t be reproduced, by enabling you to dynamically check issues on the fly.

Lightrun Actions - logs, snapshots and metrics - expose all code-level information from any line of code. This fine granularity provides developers rich context during exceptions and the ability to understand and observe code running in any given code pathway.

With Lightrun providing code-level deep introspection at the micro-granular level, you can troubleshoot, test, and debug your applications by investigating issues directly from the environment where they are running, whether it's development, staging, or production.

Lightrun eliminates the need for costly developer lifecycle operations, such as local replication or issuing a new software version, just for adding new logs or metrics.

Lightrun enables developers to observe and tackle the "unknown unknowns", on the fly, offering maximum observability without redeployment.

## Typical use cases

Developers use Lightrun for multiple and diverse code-level observability goals, including:

- Code-level alerts
- New feature verification, as part of progressive enhancement delivery (blue/green toggles and feature flags)
- Testing and debugging within progressive enhancement workflows
- Performance analysis with metrics on demand
- On-boarding new developers with legacy applications
- Code flows investigation
- Debugging 3rd party/OS code
- Migrating data centers to cloud/microservices
- Troubleshooting microservices, serverless computing, and Big Data workers
- Pinpoint performance monitoring
- Debugging ML pipelines and Big Data infrastructure

Go [here](more-about-lightrun.md){:target="_blank"} to learn about Lightrun's architecture and how the platform works.

## Getting started with Lightrun

Start using Lightrun in 3 easy steps.

1. Install the Lightrun plugin for your IDE:

    - [IntelliJ, PyCharm, and WebStorm](plugin.md)

    - [Visual Studio Code](vscode/vscode-install-plugin.md)

2. Install the Lightrun agent for your runtime environment:

    - [Java agent](jvm/agent.md){:target="_blank"}

    - [Python agent](python/agent.md){:target="_blank"}

    - [Node.js agent](node/agent.md){:target="_blank"}

3. Add your [first action](logs.md){:target="_blank"}
