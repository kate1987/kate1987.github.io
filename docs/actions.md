# What Are Lightrun Actions?

A Lightrun Action is a snapshot, dynamic log, or metric that you add to specific lines of source code in your running application. Lightrun actions can be securely inserted into your application, whether it is running in the development, testing, staging, or production environment.

Adding a Lightrun Action to the application code triggers a request from the Lightrun Server to the Agent running together with the application. Once the request is verified and authenticated, the appropriate instrumentation is added to the running application, without interrupting the service.

By including Lightrun tags (for example, Development, QA, Production), you can attach Lightrun Actions to particular instances of your application code.

The following sections describe each type of Lightrun Action in detail.

- [Dynamic Logs](actions/dynamic-logs.md)
- [Snapshots](actions/snapshots.md)
- [Metrics](actions/metrics.md)