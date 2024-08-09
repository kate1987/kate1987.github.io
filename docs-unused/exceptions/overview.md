# Monitor and handle exceptions

--8<-- "ux-reference/java-agent-only.md"

Dynamic actions are important in supporting your work in real time. At the same time, exceptions are still important and you should continue to insert exceptions in your applications where issues might be anticipated. 

Lightrun can monitor all of these exceptions when they are thrown in your application, and then offer insights about those exceptions. Whenever an exception is thrown, Lightrun stores details about the exception and also takes and saves a snapshot for you automatically, making investigation of any issues far easier.

You can:

- [Configure the agent to handle exceptions](configure.md)

- [View exceptions from the browser](web.md)

- [View exceptions from the IDE](ide.md)

!!! note
    By default, once [configured](configure.md), every exception in the application is reported, including those caught by your exception handler.

--8<-- "ux-reference/manager-role-only.md"
