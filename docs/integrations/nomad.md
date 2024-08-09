# Integrate Lightrun and Nomad

--8<-- "ux-reference/manager-role-only.md"

[Nomad](https://www.nomadproject.io/) is a flexible workload orchestrator that enables an organization to easily deploy and manage any containerized or legacy application using a single, unified workflow. Nomad can run a diverse workload of Docker, non-containerized, microservice, and batch applications.

You can run Lightrun with Java applications that are deployed and managed by Nomad, using the [Lightrun Nomad driver](https://www.nomadproject.io/docs/drivers/external/lightrun).

!!! reqs "Prerequisites"

    To run Lightrun with Nomad you need your `lightrun_server` and `YOUR_COMPANY_SECRET` configuration details. To find these, log into the [Management Portal](https://app.lightrun.com) and look inside the **Download the Agent** section.

## Run a Nomad job with the Lightrun driver

### Prerequisites

1. Download or clone the [Lightrun driver repository](https://github.com/lightrun-platform/lightrun-n-nomad).
1. Find the `lightrun-java-driver` driver in the repository's root folder.
1. Copy the driver to your Nomad plugins directory (or create one if it doesn't exist).
1. Grant executable permissions to the driver file: `chmod +x ./plugins/lightrun-java-driver`.
1. When running the Nomad's agent, make sure to specify the path to your plugins directory:

    ```sh
    sudo nomad agent -dev -bind 0.0.0.0 -log-level DEBUG -plugin-dir=<path_to_plugins_directory>
    ```

### Task Configuration

The `lightrun-java` driver accepts all configuration options of the Nomad [`java`](https://www.nomadproject.io/docs/drivers/java) driver.

1. Add `lightrun-java` as a driver to your job file.
1. Set `lightrun_server`, `YOUR_COMPANY_SECRET` and `lightrun_certificate` as part of the config object.

For example:

```hcl
task "run-with-lightrun" {
   driver = "lightrun-java"

   ...

   config {
      ...
      lightrun_server = "https://app.lightrun.com/"
      COMPANY_SECRET = "<YOUR_COMPANY_SECRET>"
      lightrun_certificate = "ee80811b38e7e6c2dc4cc372cbea86bd86b446b012e427f2e19bf094afba5d12"
   }
}
```

A complete job file example can be found at `example/example.driver.nomad`

The Lightrun driver uses the arguments provided in the config section and automatically downloads and runs the Lightrun agent.

#### Setting the Lightrun configuration globally

To set Lightrun configuration globally for any Nomad job, you must run the Nomad agent with an `agent.hcl` file.

See an example at `example/agent.hcl`.

To run the Nomad agent with the configuration file, use:

```sh
sudo nomad agent -dev -bind 0.0.0.0 -log-level DEBUG -config=./agent.hcl -plugin-dir=<path_to_plugin_directory>
```

## FAQ

1. Why don't I see Lightrun logs in the **Lightrun Console**?

    --8<-- "ux-reference/config-pipe.md"
