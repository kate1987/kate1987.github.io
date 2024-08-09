# Node.js troubleshooting guide

Sometimes issues may arise that interfere with smooth running. We've done our best to gather a list of some more common issues and possible solutions.

## System error messages

| Error        | Description                 | How to fix                 |
| ------------- | --------------------------- | -------------------------- |
|`Encountered an issue with a Lightrun PII Redaction pattern. Please contact your admin for support.`|You cannot add an action to your code because a faulty PII redaction pattern was defined.| Try the following: <br><ul><li>Check that the PII Redaction patterns are valid in the PII Redaction page in the Lightrun Management Portal and test the redaction process.</ul></li>|
| <div style="max-width:400px">`A script matching the source file was not found loaded on the debuggee`</div> | Agent could not find requested filename. | Try the following: <br><ul><li>Verify the file name.</ul></li><ul><li> Make sure you are using the same source version. </ul></li><ul><li> If you inserted lightrun actions into an external file or third-party module like `node_modules`, make you specify the file/module path in your agent configuration. See [extraPaths](/node/agent-configuration/#extrapaths).</ul><l/i> | 
| <div style="max-width:400px">`Could not determine the output file associated with the transpiled input file`</div> | Missing TypeScript mapping files. | Try the following: <br><ul><li>Include TypeScript mapping files, see [Running the agent in TypeScript applications](/node/agent/#running-the-agent-in-typescript-applications). </ul></li>| 
| `Multiple files match the path specified` | There is more than 1 possible match for the requested filename. | Try the following: <br> <ul><li>Provide distinguished path with the filename attribute.</ul></li><ul><li>Use a complete path when specifying `extraPaths`. For example, `node_modules/module_name` instead of `node_modules`. See [extraPaths](/node/agent-configuration/#extrapaths). </ul></li> | 
| `Couldn't evaluate the given condition as it might affect app performance.`| An action may be placed on a frequently called line or if the condition takes a considerable amount of time to compute.| Try the following:<ul><li>Simplify the condition. </ul></li><ul><li>Place the action in a different location.</ul></li><ul><li>If needed, enable the `IGNORE_QUOTA` configuration. This requires the ignore quota permission. Be aware that enabling the ignore quota flag may impact the performance of the application.</ul></li>
| `The agent couldn't find the given filename. Verify the action filename.`| The Agent couldn't find the file.| Try the following: <br> <ul><li>Source & Location: Double-check the file name and make sure you have selected the correct source (agent/tag).</ul></li><ul><li> Source Version: Ensure you are using the correct source version.</ul></li><ul><li>If you have integrated Lightrun actions into an external file or a third-party module, such as `node_modules`, be sure to specify the file/module path in your agent configuration. For more information, see [Node.js Extrapaths](/node/agent-configuration/#extrapaths/).</ul></li>
| `Missing TypeScript mapping files. Make sure to include these in your remote app.`| Missing TypeScript mapping files.| Try the following:<br><ul><li>Make sure the mapping files are included in your remote application.</ul></li><ul><li> Remove the full file path and replace it with `/filename`.
|Expression not allowed.| Condition expression may have issues. The provided expression contains a syntax error or may have potential side effects| Try the following:<br><ul><li>Validate your expression.</ul></il>|
|`Invalid snapshot position: %`| Invalid row number.| Try the following:<br><ul><li>Source & Location: Double-check the file name and make sure you have selected the correct source (agent/tag).</ul></li><ul><li>Source Version: Ensure you are using the correct source version.</ul></li><ul><li> If you have integrated Lightrun actions into an external file or a third-party module, such as `node_modules`, be sure to specify the file/module path in your agent configuration. For more information, see [Node.js Extrapaths](/node/agent-configuration/#extrapaths/).</ul></li>
|`More than one possible match was found for the requested filename. Provide an absolute or distinguished path.`| Filename ambiguity.| Try the following:<br><ul><li> Provide an explicit path using the filename attribute.</ul></li><ul><li>Use a complete path when specifying extraPaths. For example, use `node_modules/module_name` instead of `node_modules`. For more information, see [Node.js Extrapaths](/node/agent-configuration/#extrapaths/).</ul></li>| 
|`Syntax error in condition: %`|Condition has an syntax error. The provided condition contains a syntax error.| Try the following:<br><ul><li> Validate your expression.</ul></li>|
|`Unable to set breakpoint in &`|A snapshot is set on an invalid location.| Try the following:<br><ul><li>Source & Location: Double-check the file name and make sure you have selected the correct source (agent/tag).</ul></li><ul><li> Source Version: Ensure you are using the correct source version.<br>• If you have integrated Lightrun actions into an external file or a third-party module, such as `node_modules`, be sure to specify the file/module path in your agent configuration. For more information, see [Node.js Extrapaths](/node/agent-configuration/#extrapaths/).</ul></li>
|`A script matching the source file was not found loaded on the debugger`|Agent could not find requested filename.| Try the following:<br> <ul><li>Verify the file name.</ul></li><ul><li>Make sure you are using the same source version.</ul></li><ul><li>If you inserted lightrun actions into an external file or third-party module like `node_modules`, make you specify the file/module path in your agent configuration. See [Node.js Extrapaths](/node/agent-configuration/#extrapaths/).</ul></li>
|`Could not determine the output file associated with the transpiled input file`|Missing TypeScript mapping files.| Try the following:<br><ul><li>Include TypeScript mapping files. For more information, see [Running the agent in TypeScript applications](/node/agent/#running-the-agent-in-typescript-applications/).</ul></li>|
|`Multiple files match the path specified`| There is more than 1 possible match for the requested filename.| Try the following: <br><ul><li>Provide distinguished path with the filename attribute.</ul></li><ul><li> Use a complete path when specifying extraPaths. For example, use `node_modules/module_name` instead of `node_modules`. For more information, see [Node.js Extrapaths](/node/agent-configuration/#extrapaths/).</ul></li>

## General issue

### Self-signed certificate is blocked {#_self_signed_certificate_is_blocked}

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

## Plugin issues

### Can't see the Lightrun plugin sidebar

If you're unable to see the plugin from your IDE, verify that:

- The WebStorm or IntelliJ IDE default is not set to **Collapse all**.

- The Lightrun plugin is installed and active.

- Check the plugin's settings at **View->Tool Windows->Lightrun**.

### Can't sign in from the plugin

**Symptoms**

- No connectivity to server (cloud).  
- The IDE cannot connect to the server (in Lightrun Cloud deployments or when using app.lightrun.com)

**Suggested solutions**

Resolve server URL mismatch. Check the Lightrun server URL in the plugin's settings (under the IDE's Preferences / Settings --> Lightrun) and verify that it's the same URL that appears in the browser page from which you're trying to authenticate.

### Can't sign in from the browser for the plugin or CLI

If you Unable to log in from your browser, check the following issues:

- Verify that the client can communicate with the server (the cloud).

- There may be a problem with the embedded browser in your IDE - From the Lightrun plugin settings menu in the WebStrom or IntelliJ IDE, disable the **Use Embedded Browser** option and then try logging in again.


## Agent issues

### Agents don't appear in the Agents tab in the Lightrun sidebar

If agents don't appear in the plugin, it may be because they are not running on the server where your application is located. If you're sure the agent is running, then the error could be due to connection or authentication issues at the client side.

If you are unable to see agents in the IDE, try the following:
    
1. Validate that you have selected the correct agent pool.

2. Restart the IDE.
    
3. [Re-authenticate Lightrun from within the IDE](/authenticate-plugin/).
    
If the agents still fail to appear, contact your administrator for assistance.

### The agent could not find the given filename. Verify the action filename

This error often occurs when you insert Lightrun actions into external files and Node.js third-party modules, for example, `node_modules` because Lightrun does not scan these files for actions by default.

See [extraPaths](/node/agent-configuration/#extrapaths) for more information on how to insert Lightrun actions into external files and Node.js third-party modules.


## Action issues

### Unable to see dynamic logs in my IDE

Logs only appear in the IDE if [piping](/logs/#configure-piping) is configured correctly in the Lightrun plugin. If you are unable to see any logs:

- Verify that the piping configuration is set to either **Plugin** or **Both**.

- Check all of the **Lightrun Console** filters to verify that you haven't filtered out the dynamic logs that you've applied.

<!--
**INTELLIJ EXAMPLE FOR JAVA AGENT DELETED. INSERT IDE (WEBSTORM OR INTELLIJ) PLAYBACK EXAMPLE FOR NODE.JS AGENT HERE**
-->

### Unable to create a new action

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

- You're not connected to the correct source code version (the same version currently running with the agent). Try closing the source code and reopening the file, ensuring you open the file directly from the correct source version.

- Your plugin may need to be upgraded to the newest version.

### Unable to delete an existing action

If you're unable to delete an action, verify that:

- You're logged in.

- The agent you're using is currently running. To verify, try running [`list-agents`](/cli/cli_reference/#list-agents).

### No code found

The `No code found at line # in <path>` error may occur even if the action (for example, a log) is inserted at a line that contains executable code.

![No code found error](/assets/images/no-code-found-error.png){: style="width:70%"}

**Symptoms and causes**

This error typically happens when inserting a log in a code line that doesn't have executable code. The probable cause of the error is that a log action, in most cases, triggers at the line preceding the log insertion position. If the previous line is empty or contains no executable code, then the `No code found` error is displayed.

**Suggested solution**

Try moving the action insertion position to the line following the one for which the log is intended to trigger.


### Unable to see actions when using ts-node

**Symptoms** 

Snapshots and logs are not getting any hits when using `ts-node`.


**Suggested solution**

We recommend using the TypeScript Compiler (`tsc`) instead of `ts-node` in production environments. This choice not only ensures a more efficient memory footprint but also avoids generating unnecessary type information. For more information, see 
[Running the Node.js agent in TypeScript applications](https://docs.lightrun.com/node/agent/#running-the-agent-in-typescript-applications).

### Expression not allowed

Lightrun blocks expressions that are considered harmful to your server, can overload the Lightrun agent and server, or expressions that carry a large performance penalty.

This includes:

- Expressions that change the state of your application. i.e., setting object fields, static fields, and changing array elements.
- Expressions that involves calling a native method.
- Expressions involving the creation of a global variable.
- Expressions that implements Division by zero, infinite recursions, out-of-bound reads, and null pointer reference.
- Expressions that halt CPU.
- Expressions that try to access external resources.
