# Installing the Lightrun CLI

## Prerequisites

This tutorial assumes that you have:

- A Lightrun account.
- Java installed on your local machine.

## Install the Lightrun CLI

1. Download the Lightrun **Download CLI JAR** from the **Start using Lightrun** section of the Lightrun Management Portal.

	![Download CLI](/assets/images/lightrun_cli_download.png)

2. Open your terminal and navigate to the folder where the downloaded `lightrunc.jar` is stored.
3. Set the sever URL for the CLI `java -jar lightrunc.jar server-url app.lightrun.com`.
	```bash
	$ java -jar lightrunc.jar server-url app.lightrun.com
	```

After the Lightrun CLI has been installed, the next step is to [authenticate the Lightrun CLI](/cli/authentication/).