# Configure Lightrun with Eclipse Glassfish

Glassfish is an open source Java application server by Oracle. The `domain.xml` file contains most of the Oracle GlassFish Server configurations.

To start using Lightrun with a Glassfish server, first add the agent path as a `JVM` option to the Glassfish `java-config` block [as in this example from lines 165-169](https://github.com/javaee/glassfish/blob/master/nucleus/core/kernel/src/main/resources/org/glassfish/embed/domain.xml) to the domain.xml file, or by any of the other options described below. 

When adding the option, insert the relevant values for the parameters as follows: 

- `install_dir` is the path where the agent is saved
- `glassfish-domain-path` is the path to the glassfish project
- `app-name` is the name of the Glassfish application


###### To configure Lightrun with Glassfish

You can add the agent path option with any of these options described here. 

- from the Glassfish Admin panel 

    1. Copy the agent path option.
	     ```
		 -agentpath:<install_dir>/agent/lightrun_agent.so=--lightrun_extra_class_path=<glassfish-domain-path>/applications/<app-name>/WEB-INF/classes/
		 ```
	
    2. Navigate to the Admin panel (usually at [http://localhost:4848](https://docs.oracle.com/cd/E18930_01/html/821-2432/ggllq.html)
	
	3. Go to **Configurations=> server-config**.
	
	4. Select the JVM Options tab.
	
	5. Paste the option in the dialog box.

- from your CLI

    1. Connect to your Glassfish server (usually at <http://localhost:4848>). 
	
	2. Copy the following, update it based on your configurations and then run the `asadmin create-jvm-options` command from the terminal:
	    ```
		asadmin create-jvm-options -agentpath:<install_dir>/agent/lightrun_agent.so=--lightrun_extra_class_path=<glassfish-domain-path>/applications/<app-name>/WEB-INF/classes/
		```

- manually from the Glassfish `domain.xml` file 

    1. Copy the agent path option. 
	     ```
		 -agentpath:<install_dir>/agent/lightrun_agent.so=--lightrun_extra_class_path=<glassfish-domain-path>/applications/<app-name>/WEB-INF/classes/
		 ```
	
	2. Navigate to `<glassfish-domain-path>/config/domain.xml`
	
	3. Paste the option in the `java-config` block of the file and save the changes.

!!! note
    -  This configuration enables the Lightrun agent to run every time the webserver restarts.
    -  Glassfish autodeploy (dynamic deployment) does not start a new agent. The agent should be restarted in order to apply new actions.