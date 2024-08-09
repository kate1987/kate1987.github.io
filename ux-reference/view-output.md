To view data from the IDE, you must configure the routing accordingly.

There are three levels of routing for output from Lightrun dynamic logs and metrics:

- App/Stdout - Output appears only in the application's standard output.

- Plugin - Output appears in the Lightrun Management Portal, Lightrun console, and integrations.

- Both - Output appears in the Lightrun Management Portal, Lightrun console, integrations, and standard output.

**To configure routing:**

1. In the Lightrun plugin, navigate to the right-hand sidebar:

  <figure>
      <img src="/assets/images/agents-tags-exceptions.png" align="left" width="400" />
      <figcaption>The Sidebar</figcaption>
  </figure>

2. From the relevant agent, click ![Sidebar -icon](assets/images/i-pipe.png) to open the **Piping** menu:

  <figure>
      <img src="/assets/images/log-piping.png" align="left" width="250" />
      <figcaption>Log Piping</figcaption>
  </figure>

3. To view Lightrun Logs and Metrics from the IDE, set either the **Plugin** or the **Both** option.

!!! note
    Dynamic logs and metrics are sent from the agent to the plugin via the Lightrun management server. As this process is batched, output may appear with a slight delay.
