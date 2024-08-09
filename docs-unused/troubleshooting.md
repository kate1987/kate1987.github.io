# Troubleshooting guide

Sometimes issues may arise that interfere with smooth running. We've done our best to gather a list of some more common issues and possible solutions.

If you can't find solutions here, contact at [support@lightrun.com](mailto:support@lightrun.com){:target="_blank"} and we'll be happy to help.

=== "Java / JVM"

    ## Common error messages

    | Error        | Description                 | How to fix                 |
    | ------------- | --------------------------- | -------------------------- |
    | <div style="max-width:400px">`Cancelled. The condition evaluation % might affect the application performance%`</div> | Condition exceeds condition quota | 1. Simplify your condition <br> 2. Change the `quota` configurations for your agent <br> 3. Use `IGNORE_QUOTA` role if this condition can't be modified <br> 4. The condition is called too many times, change the condition | 
    | `The agent couldn't find the given filename. Verify the action filename` | Agent couldn't find the file | 1. Verify the file name <br> 2. Add the relevant jar to `lightrun_extra_class_path` <br> 3. Verify that you selected the correct agent or tab. |
    | `Identifier % not found` | Variable in expression was not found | 1. Make sure your application is compiled with debug symbols <br> 2. Verify the identifier is available in the Lightrun action scope | 
    | `Internal error at %` | The agent couldn't perform the requested operation | Verify you don't use another debugger in addition to Lightrun | 
    | `Invalid expression syntax` | Expression has syntax error | Validate your syntax and make sure you use Java syntax for expressions (Also when using Scala or Kotlin) | 

    ## Agents don't appear in IDE
    
    If agents don't appear in the IDE, it could be because they are not running on the server where your application is located. If you're sure the agent is running, then this error could be due to connection or authentication issues from the client side.
    
    To resolve these, try:
    
    - Restarting the IDE
    
    - [Logging in to Lightrun from the IDE again](/authenticate-plugin/)
    
    If the agents still don't appear, contact your administrator for assistance.
    
    ## Lightrun actions in this file were submitted against a different version
    
    ![Notification warning - \"Lightrun actions in this file were submitted against a different version...\"](assets/images/source-version-warning-notification.png)
    
    This notification warning pops up when one or more actions in the open file were set against different source code. This might happen if you set an action after making edits to the file, or if an action was set to the same file by another person whose source code differs from yours.
    
    This warning can be ignored, as it doesn't block the activation of the action. However, actions set on mismatching source code can cause unexpected behavior, so it is recommended that you solve this issue if it arises.
    
    ###### To solve the issue:
    
    - Make sure the application you are debugging is using the same file as the code that you've opened in your editor (or the editor of whoever set the action).
    
    - Try closing the file and reopening it.
    
    - If the problem persists, you can disable the warning:
         Click "Don't Show this Again" in the notification panel.
    
    !!! imp "Important"
         Disabling this notification will also affect the way other people view the actions that you have set.
    
    ## Self-signed certificate is blocked {#_self_signed_certificate_is_blocked}
    
    Troubleshooting for this issue may vary depending on browser, browser version or operating system. 
    
    The following links cover most of the certificate issues associated with popular browsers and operating systems:
    
    - [Getting Chrome to accept self-signed localhost certificate (per
        Chrome
        version)](https://stackoverflow.com/questions/7580508/getting-chrome-to-accept-self-signed-localhost-certificate)
    
    - [Ubuntu: Adding a self-signed certificate to the "trusted
        list"](https://unix.stackexchange.com/questions/90450/adding-a-self-signed-certificate-to-the-trusted-list)
    
    - [Creating and Trusting Self-Signed Certs on MacOS and
        Chrome/Safari](https://www.andrewconnell.com/blog/updated-creating-and-trusting-self-signed-certs-on-macos-and-chrome/)
    
    - [How to trust a self-signed SSL certificate in IE11 and
        Edge](https://medium.com/@ali.dev/how-to-trust-any-self-signed-ssl-certificate-in-ie11-and-edge-fa7b416cac68)
    
    - [How do you get Chrome to accept a self-signed certificate on
        Win10](https://www.pico.net/kb/how-do-you-get-chrome-to-accept-a-self-signed-certificate)
    
    ## Can't sign in from the plugin
    
    Possible issues:
    
    - No connectivity to server (cloud)
    
    - Check the Lightrun Server URL in the plugin's settings (under the IDE's **Preferences / Settings --> Lightrun**) and make sure it's the same URL that appears in the browser page from which you're trying to authenticate.
    
    ## Can't sign in from the browser for the plugin or CLI
    
    If you can't log in from your browser, check the following issues: 
    
    - Ensure the client can communicate with the server (the cloud).
    
    - There may be a problem with the embedded browser in your IDE - try disabling **Use Embedded Browser** option for IntelliJ from the IDE Settings menu and then try logging in again. 
    
    ## Agent exits unexpectedly
    
    If the agent exits immediately after you've run it, or if it exits unexpectedly, try checking these issues:
    
    - If you're running with classes (rather than with jars), ensure that the class path has been configured.
    
    - Ensure the path to the agent is correct.
    
    ## Can't see dynamic logs in my IDE
    
    Logs only appear in the IDE if [piping is configured](plugin.md#output) correctly. If you can't see logs, check these issues:
    
    - Double-check piping configuration to ensure it's set to **Plugin** or **Both**.
    
    - Check all of the **Lightrun Console** filters to make sure you haven't filtered out the dynamic logs you're looking for:
         ![Filter -half](assets/images/filter.gif)
    <!-- 
    
    ## Metrics not reported in integrated tool
    
    Try these options:
    
    - Double-check the configurations for your webhook and app settings and check the credentials you used to integrate. 
    
    - Ensure that any other [integration settings](integrations/overview.md) are correct for the third-party platform you're using in order to ensure our server can send information to it.
    
    - Ensure [piping](plugin.md#piping) is enabled.
    
    - Once you send logs, wait a little bit to give the platform time to index and make them available for search. This normally happens anywhere between seconds to one minute, but sometimes it can take longer.
    
    ## Can't create a new action
    
    Sometimes you can't create an active action for a variety of different reasons, as outlined here. 
    
    **Symptoms**
    
    - You can't create a new action
    - An action you create appears red in the IDE
    - The only actions that appear in the IDE are for tags
    - You can't find the agent list in the IDE
    
    **Suggested solutions**
    
    - Check to make sure you're logged in. Try logging out and then logging back in. 
    
    - Ensure you're attempting to insert the action from a line with code in it. From the IDE, ensure the cursor is positioned within your code. From the CLI, double-check that the line number you used is valid. 
    
    - The agent may down. Ask one of your account managers to check. 
    
    - Ensure the relevant agent still has at least one tag on it. The default tag is Production, but the manager may have removed this tag accidentally and left the agent with no tags.
    
    - You're not connected to the correct source code version (the same version currently running with the agent). Try closing the source code and reopening the file, ensuring you're opening the file directly from the running application. 
    
    - Your plugin might need to be upgraded to the newest version.
    
    ## Can't delete an existing action
    
    If you can't delete an action, check that:
    
    - You're logged in.
    
    - The agent you're using is currently running. Try running [`list-agents`](/cli/cli_reference/#list-agents) to check.
    
    --8<-- "ux-reference/no-code-found-error.md"
    
    ## Can't see the Lightrun plugin sidebar
    
    If you can't see the plugin from your IDE, check that:
    
    - The IntelliJ default is not set to **Collapse**. 
    
    - The plugin is installed and active.
    
    - Check the plugin's settings at **View->Tool Windows->Lightrun**.
    
    ## Can't switch user
    
    To switch users, you need to log out of the currently active user first. If this doesn't work, try to:
    
    - Clear cookies and try again. 
    
    - If you're working from the browser, try a different browser and try incognito. 
    
    ## Source file not found
    
    This usually happens when the relevant JAR is not on the classpath.
    
    When spinning up your application with the Lightrun agent attached, add the `lightrun_extra_class_path` command line argument to fix the problem:
    
    ```bash
    java -agentpath:<PATH_TO_AGENT>/lightrun_agent.so=--lightrun_extra_class_path=<PATH_TO_JAR> YourApplication
    ```

    ## Method xyz blocked (INVOKEDYNAMIC not supported)

    This error appears when a breakpoint expression calls a method whose bytecode contains invokedynamic instructions. Enable [Invokedynamic support in your JVM agent configuration](/jvm/agent-configuration/#invokedynamic-support) to fix this error.

    ## Type mismatch error

    This error occurs when you have a type mismatch in your Java expression or condition statement, i.e., you try to compare a boxed variable with an unboxed variable, assign a boxed variable to an unboxed variable, assign an unboxed variable to a boxed variable, etc. To fix the error, enable `boxing_unboxing_enabled` in your [agent configuration](/jvm/agent-configuration/)

    --8<-- "ux-reference/blocked-expressions.md"
    
=== "Python"

    ## Common error messages

    | Error        | Description                 | How to fix                 |
    | ------------- | --------------------------- | -------------------------- |
    | <div style="max-width:400px">`Multiple modules matching %`</div> | There is more than 1 possible match for the requested filename | 1. Provide absolute or distinguished path with the filename attribute <br> 2. Ensure that `Send source full path` is enabled in your plugin settings. | 
    | `No code found at %` | No executable code found on requested line | 1. Make sure you are using the same source version<br> 2. Place the Lightrun action on a line of code. <br> 3. Confirm that the Lightrun action was not inserted into your `__main__` method. | 
    | `Python module not found.` | Module is missing | 1. Verify the file name <br> 2. Add the relevant module to `lightrun_extra_class_path` <br> 3. Make sure you are using the same source version |

    ## Inserted actions fail to do anything
    
    A common problem that occurs when using Lightrun in Python applications, is if an action (for example, a log or snapshot) is successfully added by the agent while the application is running but nothing happens (no logs are printed, snapshots taken, etc.). 
    
    The reason for this behavior is that, in Python, Lightrun actions only take effect if they are added before the function in which it is inserted is called. When adding an action to a function while it is running, the function must close and be called again for the action to take effect. Particular care must be taken with main functions, which, do not return until the program exits.
    
    To resolve unresponsive actions, try:
    
    - Waiting for the function to be recalled
    - Avoid inserting actions in the main program
    - Restarting the application
    
    ## Agents don't appear in IDE
    
    If agents don't appear in the IDE, it could be because they are not running on the server where your application is running. If you're certain the agent is running, then this error could be due to connection or authentication issues from the client side.
    
    To resolve these, try:
    
    - Restarting the IDE
      
    - [Logging in](/authenticate-plugin/) again to Lightrun from the IDE
      
    - Checking for communication errors recorded in the agent's log files.
    
    If the agents still don't appear, contact your administrator for assistance.
    
    ## Self-signed certificate is blocked {#_self_signed_certificate_is_blocked}
    
    Troubleshooting for this issue may vary depending on the browser, browser version, or operating system.
    
    The following links cover most of the certificate issues associated with popular browsers and operating systems:
    
    - [Getting Chrome to accept self-signed localhost certificate (per
        Chrome
        version)](https://stackoverflow.com/questions/7580508/getting-chrome-to-accept-self-signed-localhost-certificate)
    
    - [Ubuntu: Adding a self-signed certificate to the "trusted
        list"](https://unix.stackexchange.com/questions/90450/adding-a-self-signed-certificate-to-the-trusted-list)
    
    - [Creating and Trusting Self-Signed Certs on MacOS and
        Chrome/Safari](https://www.andrewconnell.com/blog/updated-creating-and-trusting-self-signed-certs-on-macos-and-chrome/)
    
    - [How to trust a self-signed SSL certificate in IE11 and
        Edge](https://medium.com/@ali.dev/how-to-trust-any-self-signed-ssl-certificate-in-ie11-and-edge-fa7b416cac68)
    
    - [How do you get Chrome to accept a self-signed certificate on
        Win10](https://www.pico.net/kb/how-do-you-get-chrome-to-accept-a-self-signed-certificate)
    
    ## Can't sign in from the plugin
    
    Possible issues:
    
    - No connectivity to server (cloud)
    
    - Check the Lightrun Server URL in the plugin's settings (under the IDE's Preferences / Settings --> Lightrun) and make sure it's the same URL that appears in the browser page from which you're trying to authenticate.
    
    ## Can't sign in from the browser for the plugin or CLI
    
    If you can't log in from your browser, check the following issues:
    
    - Ensure the client can communicate with the server (the cloud).
    
    - There may be a problem with the embedded browser in your IDE - try disabling **Use Embedded Browser** option for PyCharm from the IDE Settings menu and then try logging in again.
    
    ## Agent exits unexpectedly
    
    If the agent exits immediately after you've run it, or if it exits unexpectedly, ensure the path to the agent is correct.
    
    
    ## Can't see dynamic logs in my IDE
    
    Logs only appear in the IDE if [piping is configured](plugin.md#output.md) correctly. If you can't see logs, check these issues:
    
    - Double-check piping configuration to ensure it's set to **Plugin** or **Both**.
    
    - Check all of the **Lightrun Console** filters to make sure you haven't filtered out the dynamic logs you're looking for:
    
    
    <!---
    INTELLIJ EXAMPLE FOR JAVA AGENT DELETED. INSERT IDE (PyCharm) PLAYBACK EXAMPLE FOR Python AGENT HERE
    --->
    
    ## Can't create a new action
    
    Sometimes you can't create an active action for a variety of different reasons, as outlined here.
    
    ### Symptoms
    
    - You can't create a new action
    - An action you create appears red in the IDE
    - The only actions that appear in the IDE are for tags
    - You can't find the agent list in the IDE
    
    ### Suggested solutions
    
    - Check to make sure you're logged in. Try logging out and then logging back in.
    
    - Ensure you're attempting to insert the action from a line with code in it. From the IDE, ensure the cursor is positioned within your code. From the CLI, double-check that the line number you used is valid.
    
    - The agent may down. Ask one of your account managers to check.
    
    - Ensure the relevant agent still has at least one tag on it. The default tag is Production, but the manager may have removed this tag accidentally and left the agent with no tags.
    
    - You're not connected to the correct source code version (the same version currently running with the agent). Try closing the source code and reopening the file, ensuring you're opening the file directly from the running application.
    
    - Your plugin might need to be upgraded to the newest version.
    
    ## Can't delete an existing action
    
    If you can't delete an action, check that:
    
    - You're logged in.
    
    - The agent you're using is currently running. Try running [`list-agents`](/cli/cli_reference/#list-agents) to check.
    
    --8<-- "ux-reference/no-code-found-error.md"
    
    ## Can't see the Lightrun plugin sidebar
    
    If you can't see the plugin from your IDE, check that:
    
    - The PyCharm IDE default is not set to **Collapse**.
    
    - The Lightrun plugin is installed and active.
    
    - Check the plugin's settings at **View -> Tool Windows -> Lightrun**.
    
    ## Can't switch user
    
    To switch users, you need to log out of the currently active user first. If this doesn't work, try to:
    
    - Clear cookies and try again.
    
    - If you're working from the browser, try a different browser, or try incognito.

    --8<-- "ux-reference/blocked-expressions.md"

=== "Node.js"

    ## Common error messages

    | Error        | Description                 | How to fix                 |
    | ------------- | --------------------------- | -------------------------- |
    | <div style="max-width:400px">`A script matching the source file was not found loaded on the debuggee`</div> | Agent could not find requested filename | 1. Verify the file name <br> 2. Make sure you are using the same source version. <br> 3.  If you inserted lightrun actions into an external file or third-party module like node_modules, make you specify the file/module path in your agent configuration. See [extraPaths](/node/agent-configuration/#extrapaths). | 
    | <div style="max-width:400px">`Could not determine the output file associated with the transpiled input file`</div> | Missing TypeScript mapping files | Include TypeScript mapping files, see [Running the agent in TypeScript applications](../node/agent/#running-the-agent-in-typescript-applications) | 
    | `Multiple files match the path specified` | There is more than 1 possible match for the requested filename | 1. Provide distinguished path with the filename attribute <br> 2. Use a complete path when specifying `extraPaths`. i.e., `node_modules/module_name` instead of `node_modules`. See [extraPaths](/node/agent-configuration/#extrapaths).  | 

    ## Agents don't appear in the Lightrun plugin
    
    If agents don't appear in the plugin, it may be because they are not running on the  server where your application is located. If you're sure the agent is running, then the error could be due to connection or authentication issues at the client side.
    
    **Possible solutions:**
    
    - Restart the IDE
    
    - [Log in](/authenticate-plugin/) to Lightrun again, from the plugin.
    
    If the agents still don't appear, contact your administrator for assistance.
    
    ## Self-signed certificate is blocked {#_self_signed_certificate_is_blocked}
    
    Troubleshooting methods for this issue may vary depending on browser, browser version or operating system.
    
    The following links address most of the certificate issues associated with popular browsers and operating systems:
    
    - [Getting Chrome to accept self-signed localhost certificate (per
        Chrome
        version)](https://stackoverflow.com/questions/7580508/getting-chrome-to-accept-self-signed-localhost-certificate)
    
    - [Ubuntu: Adding a self-signed certificate to the "trusted
        list"](https://unix.stackexchange.com/questions/90450/adding-a-self-signed-certificate-to-the-trusted-list)
    
    - [Creating and Trusting Self-Signed Certs on MacOS and
        Chrome/Safari](https://www.andrewconnell.com/blog/updated-creating-and-trusting-self-signed-certs-on-macos-and-chrome/)
    
    - [How to trust a self-signed SSL certificate in IE11 and
        Edge](https://medium.com/@ali.dev/how-to-trust-any-self-signed-ssl-certificate-in-ie11-and-edge-fa7b416cac68)
    
    - [How do you get Chrome to accept a self-signed certificate on
        Win10](https://www.pico.net/kb/how-do-you-get-chrome-to-accept-a-self-signed-certificate)
    
    ## Unable to sign in from the plugin
    
    **Symptoms**
    
    - No connectivity to server (cloud).  
    - The IDE cannot connect to the server (in Lightrun Cloud deployments or when using app.lightrun.com)
    
    **Suggested solutions**
    
      Resolve server URL mismatch. Check the Lightrun server URL in the plugin's settings (under the IDE's Preferences / Settings --> Lightrun) and verify that it's the same URL that appears in the browser page from which you're trying to authenticate.
    
    ## Unable to sign in from the browser for the plugin or CLI
    
    If you Unable to log in from your browser, check the following issues:
    
    - Verify that the client can communicate with the server (the cloud).
    
    - There may be a problem with the embedded browser in your IDE - From the Lightrun plugin settings menu in the WebStrom or IntelliJ IDE, disable the **Use Embedded Browser** option and then try logging in again.
    
    ## Agent exits unexpectedly
    
    If the agent exits unexpectedly or immediately after you've run it, verify that the path to the agent is `application_folder_name/node_modules/lightrun`.
    
    ## Unable to see dynamic logs in my IDE
    
    Logs only appear in the IDE if [piping](/logs/#configure-piping) is configured correctly in the Lightrun plugin. If you are unable to see any logs:
    
    - Verify that the piping configuration is set to either **Plugin** or **Both**.
    
    - Check all of the **Lightrun Console** filters to verify that you haven't filtered out the dynamic logs that you've applied.
    
    <!--
    **INTELLIJ EXAMPLE FOR JAVA AGENT DELETED. INSERT IDE (WEBSTORM OR INTELLIJ) PLAYBACK EXAMPLE FOR NODE.JS AGENT HERE**
    -->
    
    ## Unable to create a new action
    
    **Symptoms**
    
    - You're unable to create a new action.
    - An action you create appears red in the IDE.
    - The only actions that appear in the IDE are for tags.
    - You're unable to find the agent list in the Lightrun plugin.
    
    **Suggested solutions**
    
    - Verify that you're logged in. Try logging out and then logging back in.
    
    - Verify that you're attempting to insert the action from a line with code in it.
    - From the IDE, verify that the cursor is positioned within your code. From the CLI, verify that the line number you used is valid.
    
    - The agent might be down. Ask your account manager to check.
    
    - Verify that the relevant agent still has at least one tag on it. The default tag is **Production**, but the manager may have removed this tag accidentally and left the agent without tags.
    
    - You're not connected to the correct source code version (the same version currently running with the agent). Try closing the source code and reopening the file, ensuring you open the file directly from the running application.
    
    - Your plugin may need to be upgraded to the newest version.
    
    ## Unable to delete an existing action
    
    If you're unable to delete an action, verify that:
    
    - You're logged in.
    
    - The agent you're using is currently running. To verify, try running [`list-agents`](/cli/cli_reference/#list-agents).
    
    --8<-- "ux-reference/no-code-found-error.md"
    
    ## Unable to see the Lightrun plugin sidebar
    
    If you're unable to see the plugin from your IDE, verify that:
    
    - The WebStorm or IntelliJ IDE default is not set to **Collapse all**.
    
    - The Lightrun plugin is installed and active.
    
    - Check the plugin's settings at **View->Tool Windows->Lightrun**.
    
    ## Unable to see actions when using ts-node

    **Symptoms** 

    Snapshots and logs are not getting any hits when using `ts-node`.


    **Suggested solution**

    We recommend using the TypeScript Compiler (`tsc`) instead of `ts-node` in production environments. This choice not only ensures a more efficient memory footprint but also avoids generating unnecessary type information. For more information, see 
    [Running the Node.js agent in TypeScript applications](https://docs.lightrun.com/node/agent/#running-the-agent-in-typescript-applications).

    ## Unable to switch user
    
    To switch users, you must log out of the currently active user first. If this doesn't work, try to:
    
    - Clear cookies and try again.
    
    - If you're working from the browser, try a different browser, or open an incognito page.

    ## The agent could not find the given filename. Verify the action filename

    This error often occurs when you insert Lightrun actions into external files and Node.js third-party modules, i.e., node_modules because Lightrun does not scan these files for actions by default.
    
    See [extraPaths](/node/agent-configuration/#extrapaths) for more information on how to insert Lightrun actions into external files and Node.js third-party modules.

    ## ReferenceError: XXX is not defined

    This error appears when you try to call a Javascript variable or function from a global scope in a Lightrun expression. Lightrun only supports local variables and functions when creating a Lightrun expression.

    --8<-- "ux-reference/blocked-expressions.md"

=== ".NET"

    ## HRESULT 80131c30 error
    
    This error occurs when your .NET project is compiled with 32-bit support.

    **Suggested solutions**

    - Disable Prefer 32-bit or switch platform target to x64 in your Visual Studio debug and release configuration.

    ## Lightrun files are installed directly into your project’s directory.
    
    This error occurs when you install Lightrun in an outdated NuGet project structure.
    
    **Suggested solutions**

    - Change your project’s **Default package management format** to **PackageReference** in Visual Studio.
