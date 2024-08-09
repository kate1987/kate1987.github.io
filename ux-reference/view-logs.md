
Lightrun dynamic logs and metrics, by default, are printed into the application’s standard output(**Stdout**). This process enables them to be analyzed in the context of pre-existing logs or metrics, which might provide further clues towards solving issues.

At the same time, you can also configure your action target to **Plugin**. This configuration lets you view your dynamic logs and metrics output directly in your IDE through the Lightrun Console, the Lightrun Management Portal, and third-party integrated apps like Slack or Prometheus.

#### Viewing logs and metrics from the JetBrains Lightrun Console

Once you've configured your action target to **Plugin** and added at least one dynamic log or metric to your code, the Lightrun Console should display real-time output from the added dynamic log or metric.

  <figure>
      <img src="/assets/images/console.gif" align="left" width="1000" alt="The Lightrun Console" />
      <figcaption>The Lightrun Console</figcaption>
  </figure>

See [JetBrains plugin quick tour](/getting-around/#console) to learn more about the Lightrun Console tool window.
