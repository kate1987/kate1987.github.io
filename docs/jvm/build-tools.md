## Build Tool Configuration

Maven and Gradle compile Java class files seamlessly, but they might exclude some debugging symbols. This is done to reduce the binary size and make reverse engineering harder for distributed apps. 

To ensure these details are included, add a flag to the compiler. This flag has no impact on compiler optimization or performance, it only enhances the bytecode with additional debug information. 

### Maven

#### Building the project 
Lightrun's agent needs to find several symbols, including your project's variables, so that later it would be possible to add [actions](../actions.md). 

In order to find those symbols, it is needed to add debug options to the Java compiler via Maven. Maven compiles with the `maven-compiler-plugin`, which can be configured in the `<configuration>` tag. Under that clause, in the `<compilerArgs>` tag, we will add `-g` which is the debugging information option for the Java compiler. To that we will append the keywords `source`, `lines` and `vars` (you can view their meaning [here](https://www.ibm.com/docs/en/adfz/fafz/14.1?topic=analyzer-compiling-java-optimal-debugging)).

Add the following lines to the `pom.xml` file: 
``` {.xml}
<configuration>
  <compilerArgs>
    <arg>-g:source,lines,vars</arg>
  </compilerArgs>
</configuration>
``` 
The `pom.xml` file should match this structure after insertion:

``` {.xml}
<project>
  [...]
  <build>
    [...]
    <plugins>
      <plugin>
      <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>[...]</version>
        <configuration>
          <compilerArgs>
            <arg>-g:source,lines,vars</arg>
          </compilerArgs>
        </configuration>
      </plugin>
    </plugins>
    [...]
  </build>
  [...]
</project>
```

#### Running the project with Maven Wrapper
Set the MAVEN_OPTS environment variable, in order to pass the Lightrun agent as a parameter to the JVM running Maven.
From the server terminal, enter the following command (replace the `agentpath` value with the path to the Lightrun agent, after it has been downloaded):
```shell
MAVEN_OPTS=-agentpath:/path/to/agent/lightrun_agent.so ./mvnw
```

!!! important
    Change `/path/to/agent/` to the downloaded agent folder full path.( Note - using `~/ ` will not work)

!!! imp "Troubleshooting"
    * Make sure that the JAVA_TOOL_OPTIONS environment variable is unset, otherwise it will interfere with the MAVEN_OPTS variable. 
    You can check the value of JAVA_TOOL_OPTIONS with:
    ```shell
    echo $JAVA_TOOL_OPTIONS
    ```
    If the environment variable is assigned, backup the value if needed and then delete the variable with:
    ```shell
    unset JAVA_TOOL_OPTIONS
    ```
    * Make sure that your mvnw file includes the MAVEN_OPTS environment variable when executing the project. If not, add it like so (usually in the last command in the file):
    ```shell
    exec "$JAVACMD" \
    $MAVEN_OPTS \
    [...]
    ```

### Gradle

In the Gradle build file, ensure that the following properties are specified:

```
compileJava.options.debugOptions.debugLevel = "source,lines,vars"
compileTestJava.options.debugOptions.debugLevel = "source,lines,vars"
```
