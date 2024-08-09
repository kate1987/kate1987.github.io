# Configure Lightrun with Eclipse Jetty

Jetty is a Java application server by Eclipse. As part of Jetty installation, the `start.d` directory is automatically added to the system. For Lightrun integration, you need to add a new file to this directory.

###### To configure Lightrun with Eclipse Jetty
 
1. Create a new file `lightrun.ini` and add it to the `start.d` directory. 

2. Copy and paste the following content in the new `.ini` file:

    ``` {.bash}
    --exec
    -agentpath:<install_dir>/agent/lightrun_agent.so
    ```
