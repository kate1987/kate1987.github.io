# Configure Lightrun with Oracle WebLogic

WebLogic is a Java application server by Oracle. The Enterprise Application (EAR) file contains the WebLogic Server configurations that need to be updated for Lightrun integration.

To start using Lightrun with a WebLogic server, first add the agent path as an additional `JAVA_OPTS` parameter in the WebLogic EAR. 

###### To configure Lightrun with Oracle WebLogic

Add the parameter with one of the following options:

- from the WebLogic Admin console: 

    1. Copy the agent path option. 
         ```
         -agentpath:<install_dir>/agent/lightrun_agent.so=--lightrun_extra_class_path=<glassfish-domain-path>/applications/<app-name>/WEB-INF/classes/
         ```
	
    2. Navigate to the Admin panel (usually at [http://localhost:7001/console](https://docs.oracle.com/cd/E13167_01/aldsp/docs21/admin/console.html))
	
	3. Press **Lock & Edit**.
	
	4. Go to **(environment) => Servers => (server)**
	
	5. Go to the Start/Stop tab and update the Arguments with the agent path.
	
- manually from the WebLogic `sh` file of the EAR file

    1. Copy the agent path and update it according to your configuration: 
         ```
         -agentpath:<install_dir>/agent/lightrun_agent.so=--lightrun_extra_class_path=<weblogic-deploy-path>/<app-name.ear>. e.g. '--lightrun_extra_class_path=Oracle/Middleware/user_projects/domains/mydomain/deployments/myapp.ear'
         ```
	
	3. Add the path to `Oracle/Middleware/user_projects/domains/<your-domain>/bin/setDomainEnv.sh` as an additional parameter to the `JAVA_OPTS` (see WebLogic documentation for [help](https://docs.oracle.com/cd/E35976_01/general.240/eid_install/src/tidi_studio_weblogic_update_memory_arguments.html))


!!! note
    This configuration enables the Lightrun agent to run every time the webserver restarts.