Lightrun lets you acquire, in real-time, a broad range of performance metrics for timing, synchronization, and business logic. These metrics provide immediate answers for identifying bottlenecks, with minimal impact on performance.

Lightrun Metrics come in four types:

- [Counter](#counter)
- [Method Duration](#method)
- [Tic & Toc (Block Duration)](#tic-toc)
- [Custom Metric](#custom-metric)

<iframe width="560" height="315" src="https://www.youtube.com/embed/dVLS7eeSKlQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

!!! info "Support"
  
    Metrics currently are supported only for Java/JVM applications.

### Typical use cases

With Lightrun Metrics, you can:

- Add metrics, on demand, to your running application code, until you identify the problem
- Count line execution occurrences
- Swiftly identify performance and synchronization issues in the same version you released
- Use timers, Tic & Toc function durations, and custom metrics, to investigate code behavior and measure performance
- Collect system statistics on latency, throughput, and other variables

### Counter {#counter}

A Lightrun Counter is added to a single line of code. It counts the number of times the code line is reached. You can add a counter to any and as a many lines of code you need. From the Lightrun IDE plugin, you can specify the conditions (as Boolean expressions) when to record the line execution.

### Method Duration {#method}

The Method Duration metric measures the elapsed time for executing a given method.

### Tic & Toc (Block Duration) {#tic-toc}

The Lightrun Tic & Toc metric measures the elapsed time for executing a specified block of code, within the same function.

### Custom Metric {#custom-metric}

Lightrun enables you to design your own custom metric, using conditional expressions that evaluate to an integer result. Custom metrics can be created using the configuration form in the Lightrun IDE plugin or from the [Lightrun CLI](/cli/installation/#custommetric){:target="_blank"}.

### More on Lightrun Metrics

-  [Learn how to create and manage metrics in the Jetbrains plugin](/metrics)
-  [Learn how to create and manage metrics in the VS Code plugin](/vscode/vscode-plugin-metrics)
