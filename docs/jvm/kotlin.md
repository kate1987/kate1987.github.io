# Attaching and running the JVM Agent with your Kotlin application

!!! reqs "Version Support"
    The instructions below apply to Kotlin v1.5 and higher.

!!! reqs "Prerequisites"
    Before running the app with the agent, make sure you have:

    - Installed the [Kotlin command-line compiler](https://kotlinlang.org/docs/command-line.html).
    - Downloaded the [Java agent](agent.md#getting-the-lightrun-agent).

## Running the Lightrun agent

For Kotlin v1.6 and higher:

1. Compile your application
    ```
    kotlinc <your-main>.kt -include-runtime -d myapp.jar
    ```

2. Run the application with the Java agent
    ```
    java -agentpath:<path-to-agent>/lightrun_agent.so -jar myapp.jar
    ```

    For Kotlin v1.5 you might get a "no main manifest attribute". You can put the `kotlin-stdlib` in your classpath instead.

3. Compile your application
    ```
    kotlinc <your-main>.kt
    ```

4. Run the application with the Java agent and kotlin-stdlib in your classpath
    ```
    java -cp <path-to-kotlin>/kotlin-stdlib/1.4.20/kotlin-stdlib-1.4.20.jar:. -agentpath:<path-to-agent>/agent/lightrun_agent.so <your-main>
    ```

!!! tip "Optional"
    You can also automatically attach an agent to your launched Java processes with the `JAVA_OPTS` environment variable. 

    ```shell
    export JAVA_OPTS=-agentpath:<path-to-agent>/lightrun_agent.so
    ```

!!! note

    Kotlin expressions are limited:    

    - All functions in the expression should be converted to their Java equivalent. For example, (pow -> Math.pow).
    - Expressions with Kotlin ranges and Coroutines are not supported.