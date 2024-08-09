# MicroProfile and Jakarta EE (TomEE, Geronimo and Payara)

MicroProfile is a standard not an implementation. It is a specification for a set of features that can be used in a variety of server implementations.

Jakarta EE is a standard whose roots date back to Java EE. The standards are complimentary and some application servers implement both e.g. TomEE.

There are many implementations of the MicroProfile specification but due to their variance it's hard to provide universal configuration guidelines.

!!! warning
    At this time Lightrun doesn't support native compilation with GraalVM. Some MicroProfile implementations place heavy emphasis on native compilers, that wouldn't work. We're actively working on a solution for GraalVM. If you're interested in that please [contact us](mailto:info@lightrun.com).

## TomEE

[TomEE](https://tomee.apache.org/) is an Apache application server with support for both Jakarta EE and MicroProfile.  It is built on top of Tomcat and as such can use the [same instructions as Tomcat](tomcat.md).

## Geronimo

Apache Geronimo is a newer application server implementation. You can configure Lightrun via the environment variable `JAVA_OPTS`.

Specifically:

```shell
export JAVA_OPTS="$JAVA_OPTS -agentpath:<install_dir>/agent/lightrun_agent.so=--lightrun_extra_class_path=path-to-application
```

!!! info 
    The `path-to-application` argument helps Lightrun locate the applicable JAR/WAR/EAR file so it can bind debug information correctly. Lightrun will appear to work without it but might fail to add actions.

Once this environment variable is defined you can run Geronimo as usual.

## Payara

[Payara](https://www.payara.fish/) is a Jakarta EE & MicroProfile compatible application server. It is built on top of GlassFish.

Payara supports a Micro uber JAR which works similarly to Spring Boot by packaging the entire application into a single JAR. This makes deployment very easy, just use the [standard agent syntax](../agent.md):

```shell
-agentpath:<install_dir>/agent/lightrun_agent.so
```

If you're using the full application server check out [this guide](https://docs.payara.fish/community/docs/5.194/documentation/payara-server/server-configuration/jvm-options.html) on customizing JVM arguments. And add the following to the JVM:

```shell
-agentpath:<install_dir>/agent/lightrun_agent.so=--lightrun_extra_class_path=path-to-application
```