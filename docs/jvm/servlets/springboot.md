# Configure Lightrun with Spring Boot

Lightrun has excellent support for Spring Boot applications right out of the box.

Spring Boot has several deployment methods and each requires a different integration approach:

* [Executable JAR](#executable-jar)
* [Linux Service](#linux-service)
* [WAR/EAR deployment](#warear-deployment)
* [Spring Native](#spring-native)

## Executable JAR

Executable JAR is one of the most common deployment methods and the easiest to support. Adding [the standard agent code](../agent.md) `-agentpath:<install_dir>/agent/lightrun_agent.so` to the `-jar` command line will work seamlessly.

## Linux Service

The Executable JAR can be deployed as a Linux service under `systemd` or `init.d`. When enabling this mode you need to first define an environment variable that would pass the agent configuration to the service.

This environment variable must be defined before the service. It uses the [standard agent syntax](../agent.md):

``` {.shell}
JAVA_OPTS=-agentpath:<install_dir>/agent/lightrun_agent.so
```

## War/EAR deployment

This mode runs Spring Boot hosted within an application server e.g. Tomcat. To support such a deployment please read the respective documentation e.g. for Tomcat you can read [this](tomcat.md).

## Spring Native

At this time Spring Native isn't supported by Lightrun. We're actively investigating the related process, please [contact us](mailto:info@lightrun.com) if you're interested in this integration.
