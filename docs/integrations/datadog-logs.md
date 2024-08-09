# Scrape Lightrun dynamic logs using Datadog

--8<-- "ux-reference/manager-role-only.md"

You can use Datadog to scrape the Lightrun log file and send the log data directly to you Datadog account.
	 
!!! reqs "Prerequisites"
    * A [Datadog account](https://docs.datadoghq.com/agent/) with API key access
    * A [Datadog Agent](https://docs.datadoghq.com/agent/) installed and configured with the aforementioned Datadog account

### Configure the Lightrun agent to output logs in JSON format - JVM
By default, the Lightrun logs are written in XML format.
The Datadog agent does not know how to parse XML logs without pre-processing, but it *does* know how to parse JSON Logs automatically.

You can configure the aggent to output logs in JSON format in the Lightrun agent's config file, located in `<PATH_TO_AGENT>/agent.config`:
```text
com.lightrun.DynamicLog.FileHandler.formatter=json
```
!!! note

    You can make sure the output is set to JSON by tailing the log files (make sure your Lightrun agent is currently printing logs):
    ```shell
    tail -f /tmp/lightrun_file_handler_logs*.log
    ```
### Configure the Lightrun agent to output logs in JSON format - Node.js & Python

The Lightrun Node.js & python agents write logs out to the console/stdout by default. 

There are 2 approaches you can take in order to make sure the datadog agent collects these logs:

1. Pipe the program's output directly to a file, and add it as a file source in `conf.yaml` below. This can be done on unix-like systems by `node app.js >> /tmp/lightrun_nodejs_logs.log` or `python app.py >> /tmp/lightrun_python_logs.log` respectively. 
2. You can use an application-level logger to write logs to a file - i.e. by using [`winston`](https://github.com/winstonjs/winston) in a node application or the common [logging facility for Python](https://docs.python.org/3/howto/logging.html#logging-to-a-file).  

### Configure Datadog to scrape the log files
First you need to enable log collection in `/etc/datadog-agent/datadog.yaml` by uncommenting the following property:
```shell
logs_enabled: true
```

Now you need to configure the Datadog agent to scrape the Lightrun log file.
Create the configuration folder:
```shell
mkdir /etc/datadog-agent/conf.d/lightrun.d/
```
Create the configuration file `/etc/datadog-agent/conf.d/lightrun.d/conf.yaml`:
!!! hint
    You can change the name `conf.yaml` to a more indicative name
```yaml
logs:
  - type: file
    path: "/tmp/lightrun_file_handler_logs*.log"
    service: "<YOUR_APPLICATION/SERVICE_NAME>"
    source: "Lightrun"
```

Restart your Datadog service
```shell
sudo service datadog-agent restart
```

### View Lightrun logs in your Datadog account

* Login to your [Datadog account](https://app.datadoghq.com)
* Go to [Live Tail](https://app.datadoghq.com/logs/livetail)

Your logs should now appear in Datadog's live tail console
<figure>
    <img src="/assets/images/integrations-datadog-logs-live-tail-console.png" alt="Live Tail console"/>
    <figcaption>Live Tail console</figcaption>
</figure>


## Troubleshooting
* Make sure the [Lightrun logs](../logs.md) are *continuously* printed to the log files and are in JSON format
```shell
tail -f /tmp/lightrun_file_handler_logs*.log
```
* Make sure Datadog agent is running
```shell
service datadog-agent status
```
* Make sure Datadog agent successfully found the log file
```shell
datadog-agent status
```
*Example output*
```shell
==========
Logs Agent
==========

    Sending compressed logs in HTTPS to agent-http-intake.logs.datadoghq.com on port 443
    BytesSent: 2.5242779e+07
    EncodedBytesSent: 738819
    LogsProcessed: 66557
    LogsSent: 66493

  lightrun
  --------
    - Type: file
      Path: /tmp/lightrun_file_handler_logs*.log
      Status: OK
        2 files tailed out of 2 files matching
      Inputs:
        /tmp/lightrun_file_handler_logs1.log
        /tmp/lightrun_file_handler_logs0.log
      BytesRead: 1.1758002e+07
      Average Latency (ms): 49
      24h Average Latency (ms): 49
      Peak Latency (ms): 1256
      24h Peak Latency (ms): 1256

```
* Make sure Datadog's API key is configured and that the [API key is valid](https://app.datadoghq.com/organization-settings/api-keys)
```shell
cat /etc/datadog-agent/datadog.yaml | grep api_key:
```
*Example output*
```shell
$ cat /etc/datadog-agent/datadog.yaml | grep api_key:
api_key: ****************************ac11
```