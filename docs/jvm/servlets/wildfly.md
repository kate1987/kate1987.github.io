# Configure Lightrun with Wildfly (JBoss)

Wildfly is a Java application server by RedHat. The Wildfly Server configurations are stored in either the domain.conf for multiple instance deployments, or the [standalone.conf](https://docs.wildfly.org/17/Admin_Guide.html) for standalone implementations. 

To start using Lightrun with a Wildfly server, first add the agent path as an additional `JAVA_OPTS` parameter in the [relevant](https://docs.wildfly.org/18/Admin_Guide.html) Wildfly configuration file. 

This section gives high-level assistance for standalone servers.

!!! info "Support"
    The Lightrun support for Wildfly has been verified on CentOS 7.6/WildFly 18 (the official WildFly Docker image).
	
###### To configure Lightrun with Wildfly


For a standalone JVM deployment, JVM settings can be added as a `JAVA_OPTS` variable in the `standalone.conf` file.

1. Copy the agent path, update it according to your configuration and then add it to `standalone.conf`: 

```shell
-agentpath:<install_dir>/agent/lightrun_agent.so=--lightrun_extra_class_path=<widlfly-deploy-path>/<app-name.war>. 
```
     

     
  !!! tip
      - The default server dynamic logs are in `/opt/jboss/wildfly/standalone/log/server.log`
      - To deploy the Management Portal copy a .war file to the deployment dir `/opt/jboss/wildfly/standalone/deployments/`
      - To redeploy an app, copy a new file to the deployment dir and then run `touch <app_name>.war` in the same dir. Then see `/opt/jboss/wildfly/standalone/log/server.log` to verify; the server stops working following these updates.

2.  Restart WildFly - [How to start/stop the WildFly server](https://subscription.packtpub.com/book/networking_and_servers/9781784392413/2/ch02lvl1sec29/shutting-down-and-restarting-an-instance-via-the-cli)

