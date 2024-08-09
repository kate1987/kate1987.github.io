# Learn how to scan your code for log waste in a JetBrains IDE, and see recommendations for fixing them.

## About the Lightrun LogOptimizer(™)

Lightrun LogOptimizer(™) is an automated log optimization solution that scans your code and returns information about potential logging issues with recommendations on how to fix these issues. 

This guide demonstrates how to use the Lightrun LogOptimizer in your JetBrains IDE. You will learn how to view and investigate potential logging issues based on suggestions provided by the LogOptimizer directly from within your editor.

## Prerequisites

This tutorial assumes that you have:

1. Created a Lightrun account. Visit [app.lightrun.com](http://app.ligthrun.com) to create your Lightrun account.
2. Installed the Lightrun JetBrains plugin (version 1.10 or later) in your IDE. To install the Lightrun JetBrains plugin in your JetBrains IDE, see [Installing the JetBrains plugin](https://docs.lightrun.com/plugin/).
3. Docker desktop or Docker engine installed and running on your local machine. See [docker.com](https://docs.docker.com/engine/install/) for Docker installation instructions.

!!! note
	You must have a Lightrun PRO or Enterprise plan to use the Lightrun LogOptimizer solution.

## Download Spring Framework GitHub Project

To demonstrate how to use the Lightrun LogOptimizer, we will be scanning the Spring framework GitHub project. You can also follow this tutorial using any of your Java, Node.js, or Python projects.

Clone the spring-framework project from the following repository - [https://github.com/spring-projects/spring-framework.](https://github.com/spring-projects/spring-framework)

## Authenticate your Plugin

To authenticate your Lightrun JetBrains plugin:

1. Open the Spring framework project in your JetBrains IDE.
2. Click the Lightrun tab on the top right-hand corner of your JetBrains IDE to open the Lightrun tool window.
3. Click Disconnected - Click to Login on the top part of the Lightrun tool window.
	![Authenticate Jetbrains --third](../assets/images/authenticate-jbp.png)

	Your browser will open automatically to the Lightrun login page.

4. Login with your credentials to authenticate your Lightrun plugin. A confirmation message will be displayed on successful authentication.
5. Go back to your IDE. You should have access to the Agents and Tags tab if the authentication process is successful.
	![Authenticate Jetbrains --third](../assets/images/authenticate-jbp2.png)

## Run the Lightrun LogOptimizer(™) tool.

After completing your plugin authentication process, we can now scan our code with the Lightrun LogOptimizer. We will be scanning the entire spring framework code repository for this tutorial.

!!! note
	You can also scan individual directories and files if you want to.

To scan the Spring Framework project:

1. Click the Project tab on the top left-hand side of your JetBrains IDE to open the JetBrains Project tool window for the Spring Framework project.
2. Right-click on the spring-framework project name to open the JetBrains context menu. 
3. Click on Log Optimizer in the JetBrains context menu.
4. Click Scan This Project to start the Log Optimizer scan.
	![Authenticate Jetbrains --half](../assets/images/log-optimizerscan.png)

The Log Optimizer will begin scanning and return all output in the Lightrun Log Optimizer tool window. The first time you run the LogOptimizer scan is expected to be longer as it needs to pull the LogOptimizer Docker image from the Docker Hub.

![Log Optimizer scan](../assets/images/log-optimizer.gif)

## Review your Results 

After completing the scanning process; the results will be displayed in the Lightrun LogOptimizer tool window.

An example result is shown in the code sample below.

```bash
Found 3 results

/home/Projects/logging-demo/LoggingDemo/src/main/java/org/example/LoggingDemo.java

	id: marker_log_first_line
	line: 11
	message: Method "doSomething" has a marker log in the beginning of the method

	10| 	public void doSomething() {
	11|     	log.info("Getting into method doSomething");
```

The LogOptimizer result is shown in the following format:

```bash
full/path/to/file/with/logging/issues

id: name of potential log problem
line: Line of code with the log issue
message: Description of the log issue

@Overide
public LineOfCodeWithLogIssue {
	<line of code with log issue>
}
```

Click on the file path to open the file with the log issue in your IDE.

## Further reading

- [LogOptimizer(TM) Overview](/logoptimizer/overview/)
- [Log statements identified by LogOptimizer(TM)](/logoptimizer/statements/)