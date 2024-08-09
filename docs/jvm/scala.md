# Installing and using Lightrun with Scala

!!! reqs "Prerequisites"
    Before running the app with the agent, make sure you have downloaded the [Java agent](agent.md#getting-the-lightrun-agent).

## Using the Lightrun agent

Run your application with the following command:

```
java -agentpath:</path-to-agent>/lightrun_agent.so -cp <path-to-scala>/scala-library.jar:<path-to-jar> <your-main-class>
```

- `<path-to-agent>` - The absolute path to the agent's folder (~/ will not work)
- `<path-to-scala>` - The absolute path to the Scala installation directory
- `<path-to-jar>` - The absolute path to the Scala application to be run with the agent
- `<your-main-class>` - The application main class to be run

!!! tip "Optional"
    You can also automatically attach an agent to your launched Java processes with the `JAVA_OPTS` environment variable. 

    ```shell
    JAVA_OPTS=-agentpath:<path-to-agent>/lightrun_agent.so
    ```

## Known issues and limitations

- **Scala expressions are limited**    

    Expressions should be converted to their equivalent Java syntax.
  
 - **Lightrun snapshot results distortion**

  - In certain situations, Lightrun snapshot results may display duplicated variable values. The duplication happens due to the way Scala's compiler compiles the Scala multiple-return-values syntax into Java bytecode. As a result, a local duplication occurs for every local variable defined in the return values tuple of the multiple-return-values method. This is illustrated in the following example, where the variables `square` and `fib` will be duplicated locally.
  
    ```shell
    val (square, fib) = computeExample(num)
    ```

  - Scala allows the existence of variables with the same name within the same method scope. If variable 'A' is present in one scope within the method, another variable with the same name can coexist in a different scope within that method. Moreover, it is even possible for one variable's scope to be nested within another, presenting a challenge for Lightrun in distinguishing between them.
  
- Setting Method Duration metrics is not supported.