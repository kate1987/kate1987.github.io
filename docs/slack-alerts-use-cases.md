# Lightrun Alerts with Slack use cases

The following use cases for Lightrun alerts are not intended to be exhaustive. However, they should serve as a convenient starting point when investigating whether Lightrun alerts are right for you. If you have more ideas for use cases, feel free to contact Lightrun Support at [email](mailto:support@lightrun.com).

### Edge cases and rarely occurring bugs

In many reasonably large applications, there are specific, hidden corners where things can fail in extraordinary ways. For instance, calls to external APIs that are unreliable, underlying infrastructure problems that your tests don't account for, and various delays and timeouts resulting from running your application in the wild and not on your local machine or staging environment.

By placing *conditional* Lightrun Logs and Snapshots at strategic locations in the code, then connecting the Lightrun Slack integration to a dedicated channel, you can "catch" bugs in real time and observe the situation with full contextual information - including the structure and contents of every object across all the relevant frames.

### Developer-friendly investigation

When setting an alert, based on some sort of metric, it is common practice to define a threshold - an upper limit above which the alert is triggered. In most cases this is sufficient - you want to know when something bad happens and fix it then and there.

However, in most cases there isn't a straightforward way to code business logic into the alerts, which means the only way to get a clear picture of what's happening inside the application is to look at the application logs. If the logs aren't telling the full story when the alert is triggered, developers are forced to deploy hotfixes, with more logs, to better understand what's going on inside the system.

With Lightrun, you can define highly granular and informative alerts, providing details about the global state of the application, the values of different variables, and, allowing you to define the exact data objects you want to extract from the application. This is a familiar and comfortable way for developers to conduct investigations, resulting in a more streamlined and intuitive approach to incident resolution.

### Following long-running jobs

Some code paths take a long time to complete. These include batch jobs, data workers, and various intensive computation tasks that starve system resources, while you wait for their completion.

In such cases, it is useful to be able to track the code path as the application executes. With Lightrun, you can place logs at various places in the running code and get alerted in real time when log points are reached. This allows you to follow the code path, without adding new logs or configuring alerts inside your APM.
