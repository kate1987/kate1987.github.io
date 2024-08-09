# Configure Lightrun with WebSphere

WebSphere was one of the first major application servers to gain widespread adoption. It's still popular in large scale corporate deployments. Lightrun supports the current versions of WebSpehere and its Liberty profile.

To set up Lightrun with WebSphere, you need to add a JVM argument configuration. This varies based on your version of WebSphere. 

You can read the instructions for the standard WebSphere installation [here](https://www.ibm.com/support/pages/setting-generic-jvm-arguments-websphere-application-server) and for Liberty profile [here](https://www.ibm.com/support/pages/setting-generic-jvm-arguments-websphere-application-server-v85-liberty-profile).

Following that process you can add the following to your JVM arguments:

``` {.shell}
 -agentpath:<install_dir>/agent/lightrun_agent.so=--lightrun_extra_class_path=<websphere-deploy-path>/<app-name.war>. 
```
