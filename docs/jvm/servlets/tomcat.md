# Configure Lightrun with Apache Tomcat

Tomcat is an open source Java application server by Apache. Applications are installed on Tomcat with a compressed Java web application resource (WAR) file. 

To start using Lightrun, first add an additional parameter to the `JAVA_OPTS` configuration variable in the WAR file. 

###### To configure Lightrun with Apache Tomcat

1. Copy the following agent path configuration: 

    ``` {.shell}
    -agentpath:<install_dir>/agent/lightrun_agent.so=--lightrun_extra_class_path=<tomcat-path>/webapps/<app-name.war>
    ```
2. Insert relevant values for each of the parameters, as follows:
    - `install_dir` is the path where the agent is saved
    - `tomcat-path` is the path to the Tomcat project
    - `app-name.war` is the name of the war file of the project

2. Paste the agent path as an additional parameter to the `JAVA_OPTS` variable in your WAR file.


3. Restart the Tomcat server to apply the configuration:

    ``` {.shell}
    ./catalina.sh stop
    ./catalina.sh start
    ```

!!! note
    -  This configuration enables the Lightrun agent to run every time the webserver restarts.
    -  Tomcat autodeploy (dynamic deployment) does not start a new agent. The agent should be restarted in order to apply new actions.