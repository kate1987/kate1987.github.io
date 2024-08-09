# Example use cases for Lightrun

Here you can read through a few examples that show you how  you might leverage Lightrun to increase time to resolution. 

Using these examples, the following flows demonstrate:

* how you can implement useful actions and commands from the Lightrun CLI
* what the output looks like 
* how to view more debugging information than your compiler enables by default
* how Lightrun protects your resources when necessary.


## Example 1: Insert and view extended log output for variables

Assume you have an application that runs through prime numbers. The application is called PrimeMain.java. 

1. Compile your application and then open a new shell.

2. Try to print the current prime number counter.

    `lightrunc log 0 PrimeMain.java:20 "Current Count is {cnt}"`

    The output is something similar to the following:

    ```
    Feb 28, 2019 2:11:29 AM PrimeMain main
    INFO: LOGPOINT: current prime is 1467954
    Feb 28, 2019 2:11:29 AM PrimeMain main
    INFO: LOGPOINT: current prime is 1467955
    Feb 28, 2019 2:11:29 AM PrimeMain main
    INFO: LOGPOINT: current prime is 1467956
    Feb 28, 2019 2:11:29 AM PrimeMain main
    INFO: LOGPOINT: Logpoint is paused due to high call rate until log quota is restored
    ```

3. Now run the following command:
     ```
     lightrunc log 0 PrimeMain.java:20 "Current Prime is {i}"
     ```

4. Now notice the ouptut. The following log prints out:

    ```
    INFO: LOGPOINT: Current Prime is Identifier i not found
    Feb 28, 2019 2:05:07 AM PrimeMain isPrime
    ```
    
   ---
     **Note** that the agent does not allow too many log prints to be fired all at once - this is intentional. Lightrun caps the CPU overhead of the agent. Additionally, take note that not all variables are available for exploration. Some debug information might be missing due to compiler optimizations. 
   ---

5. Recompile your app, adding the `-g` flag this time in order to watch the value for the `i` variable, similar to the following command: 

     ```
     javac -g PrimeMain.java
     ```

6. Now run the following command to view the relevant output for the `i` variable:

     ```
     lightrunc log 0 PrimeMain.java:20 "Current Prime is {i}"
     ```


## Example 2: Debug integer overflow with a dynamic log

Assume you have a simple fibonacci series calculator application. The application details are as follows: 

* The application is called `Example.java`. 
* The package manager is Maven
* The web server is running on <http://localhost:8080>.

Whenever the user enters `http://localhost:8080/<number>/` in the application, the `<number>` fibonacci element is displayed. For example, <http://localhost:8080/33> prints 5702887.

An error occurs. The application has an integer overflow:

``` {.shell}
curl http://localhost:8080/50 # will print -1109825406o
```

1. Insert a Lightrun action to add a log to the application:
     ``` {.shell}
     lightrunc log 0 main/java/Example.java:20 "{n3} = {n1} + {n2}"
     ```
     
     The output prints similar to the following, giving you visibility in to the cause for the overflow:

    ```
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 1 = 0 + 1
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 2 = 1 + 1
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 3 = 1 + 2
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 5 = 2 + 3
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 8 = 3 + 5
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 13 = 5 + 8
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 21 = 8 + 13
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 34 = 13 + 21
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 55 = 21 + 34
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 89 = 34 + 55
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 144 = 55 + 89
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 233 = 89 + 144
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 377 = 144 + 233
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 610 = 233 + 377
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 987 = 377 + 610
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 1597 = 610 + 987
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 2584 = 987 + 1597
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 4181 = 1597 + 2584
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 6765 = 2584 + 4181
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 10946 = 4181 + 6765
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 17711 = 6765 + 10946
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 28657 = 10946 + 17711
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 46368 = 17711 + 28657
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 75025 = 28657 + 46368
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 121393 = 46368 + 75025
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 196418 = 75025 + 121393
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 317811 = 121393 + 196418
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 514229 = 196418 + 317811
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 832040 = 317811 + 514229
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 1346269 = 514229 + 832040
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 2178309 = 832040 + 1346269
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 3524578 = 1346269 + 2178309
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 5702887 = 2178309 + 3524578
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 9227465 = 3524578 + 5702887
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 14930352 = 5702887 + 9227465
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 24157817 = 9227465 + 14930352
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 39088169 = 14930352 + 24157817
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 63245986 = 24157817 + 39088169
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 102334155 = 39088169 + 63245986
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 165580141 = 63245986 + 102334155
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 267914296 = 102334155 + 165580141
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 433494437 = 165580141 + 267914296
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 701408733 = 267914296 + 433494437
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 1134903170 = 433494437 + 701408733
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: 1836311903 = 701408733 + 1134903170
    INFO 14911 --- [nio-8080-exec-1] com.google.DynamicLog   : LOGPOINT: -1323752223 = 1134903170 + 1836311903
    ```

## Example 3: Debug a Scala application

Assume you have a Game of Life simulation written with Scala. An error occurs. 

1. Run the simulation with the Lightrun agent: 

     ``` {.shell}
     cd scala-game-of-life
     sbt package
     java  -agentpath:<install_dir>/lightrun_agent.so \-cp /home/osboxes/.sbt/boot/scala-2.12.7/lib/scala-library.jar:target/scala-2.12/game-of-life-scala_2.12-0.1.0.jar \de.l7r7.lab.conway.GameOfLife
     ```


2. Insert a Lightrun action to add a log to the application:
     ``` {.shell}
     lightrunc log 0 de/l7r7/lab/conway/GameOfLife.scala:85 "Board Type {board.getClass().toString()}"
     ```

!!! note
     The results are logs that print per simulation. 
     Also, notice that the syntax is in Java. 

## Example 4: Debug a Groovy application

Assume you're running a prime number counter application written in Groovy. The application is designed to count prime numbers less than 1B. 

1. To test or debug the application, run it with the Lightrun agent: 
     ``` {.shell}
     cd groovy-app
     groovyc GroovyPrimeMain.groovy
     java -cp <path_to_groovy_jar.jar>:. -agentpath:<install_dir>/lightrun_agent.so GroovyPrimeMain
     ```
    **Note** that the syntax is in Java. 

2. Insert a log: 
     ``` {.shell}
     lightrunc log 0 GroovyPrimeMain.groovy:22 "{num} is prime"
     ```

3. The output might appear similar to the following: 
     ```
     Feb 23, 2020 3:25:39 PM GroovyPrimeMain isPrime
     INFO: LOGPOINT: 110389847 is prime
     Feb 23, 2020 3:25:39 PM GroovyPrimeMain isPrime
     INFO: LOGPOINT: 110389871 is prime
     Feb 23, 2020 3:25:39 PM GroovyPrimeMain isPrime
     INFO: LOGPOINT: 110389879 is prime
     Feb 23, 2020 3:25:39 PM GroovyPrimeMain isPrime
     INFO: LOGPOINT: 110389913 is prime
     Feb 23, 2020 3:25:39 PM GroovyPrimeMain isPrime
     INFO: LOGPOINT: 110389933 is prime
     Feb 23, 2020 3:25:39 PM GroovyPrimeMain isPrime
     INFO: LOGPOINT: 110389963 is prime
     Feb 23, 2020 3:25:39 PM GroovyPrimeMain isPrime
     INFO: LOGPOINT: Logpoint is paused due to high call rate until log quota is restored
     ```
