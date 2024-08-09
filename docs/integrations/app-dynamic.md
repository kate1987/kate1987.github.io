# Integrate Lightrun dynamic logs with AppDynamics cloud monitoring

Lightrun allows Developers and DevOps Engineers to add real-time logs, metrics, and traces to live applications on demand. This means, in practice, that information that was once only accessible by pushing new code with more instrumentation or by profiling your application can now be added on demand - right from the IDE

[AppDynamics](https://www.appdynamics.com/) is a business observability platform that gives you a powerful view into the performance of your entire stack through the lens of your business. By integrating Lightrun with AppDynamics, you can insert dynamic logs into your live application with Lightrun and gain full business context around application issues in one place with AppDynamics log analytics.


## Get Started

To integrate Lightrun with AppDynamics, configure your AppDynamics Analytics agent to collect [Logs analytics data](https://docs.appdynamics.com/appd/20.x/en/application-analytics/configure-application-analytics/collect-log-analytics-data). Add the path to your Lightrun internal agent logs file as the Analytics agent source file. 

The captured logs data will appear in your AppDynamics Application Analytics UI. For more information on how to collect logs from a log file into AppDynamics, see [Configure Log Analytics Using Job Files](https://docs.appdynamics.com/appd/20.x/en/application-analytics/configure-application-analytics/collect-log-analytics-data/configure-log-analytics-using-job-files).
