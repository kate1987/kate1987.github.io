# Python troubleshooting guide

Sometimes issues may arise that interfere with smooth running. We've done our best to gather a list of some more common issues and possible solutions.

## System error messages

| Error        | Description                 | How to fix                 |
| ------------- | --------------------------- | -------------------------- |
| `An issue was encountered with a Lightrun PII Redaction pattern. Please contact your admin for support.`|You cannot add an action to your code because a faulty PII redaction pattern was defined.| Try the following: <br><ul><li>Check that the PII Redaction patterns are valid  in the PII Redaction page in the Lightrun Management Portal and test the redaction process.</ul></li>|
| <div style="max-width:400px">`Multiple modules matching %`</div> | There is more than 1 possible match for the requested filename. | Try the following:<br> 1. Provide absolute or distinguished path with the filename attribute. <br> 2. Ensure that `Send source full path` is enabled in your plugin settings. | 
| `No code found at %` | No executable code found on requested line. |Try the following:<br> 1. Make sure you are using the same source version.<br> 2. Place the Lightrun action on a line of code. <br> 3. Confirm that the Lightrun action was not inserted into your `__main__` method. | 
| `Python module not found.` | Module is missing. | Try the following:<br> 1. Verify the file name. <br> 2. Add the relevant module to `lightrun_extra_class_path`. <br> 3. Make sure you are using the same source version. |

## General issues

### Self-signed certificate is blocked {#_self_signed_certificate_is_blocked}

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

## Plugin issues

### Can't see the Lightrun plugin sidebar

If you can't see the plugin from your IDE, check that:

- The PyCharm IDE default is not set to **Collapse**.

- The Lightrun plugin is installed and active.

- Check the plugin's settings at **View -> Tool Windows -> Lightrun**.

### Can't sign in from the plugin

Possible issues:

- No connectivity to server (cloud)

- Check the Lightrun Server URL in the plugin's settings (under the IDE's Preferences / Settings --> Lightrun) and make sure it's the same URL that appears in the browser page from which you're trying to authenticate.

### Can't sign in from the browser for the plugin or CLI

If you can't log in from your browser, check the following issues:

- Ensure the client can communicate with the server (the cloud).

- There may be a problem with the embedded browser in your IDE - try disabling **Use Embedded Browser** option for PyCharm from the IDE Settings menu and then try logging in again.

## Agent issues

### Agents don't appear in the Agents tab in the Lightrun sidebar

If agents don't appear in the IDE, it could be because they are not running on the server where your application is running. If you're certain the agent is running, then this error could be due to connection or authentication issues from the client side.

If you are unable to see agents in the IDE, try the following:
    
1. Validate that you have selected the correct agent pool.

2. Restart the IDE.
    
3. [Re-authenticate Lightrun from within the IDE](/authenticate-plugin/).
    
If the agents still fail to appear, contact your administrator for assistance.

## Action issues

### Inserted actions fail to do anything
    
A common problem that occurs when using Lightrun in Python applications, is if an action (for example, a log or snapshot) is successfully added by the agent while the application is running but nothing happens (no logs are printed, snapshots taken, etc.). 
    
The reason for this behavior is that, in Python, Lightrun actions only take effect if they are added before the function in which it is inserted is called. When adding an action to a function while it is running, the function must close and be called again for the action to take effect. Particular care must be taken with main functions, which, do not return until the program exits.

To resolve unresponsive actions, try:

- Waiting for the function to be recalled
- Avoid inserting actions in the main program
- Restarting the application

<!---
INTELLIJ EXAMPLE FOR JAVA AGENT DELETED. INSERT IDE (PyCharm) PLAYBACK EXAMPLE FOR Python AGENT HERE
--->

### Can't create a new action

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

- You're not connected to the correct source code version (the same version currently running with the agent). Try closing the source code and reopening the file, ensuring you're opening the file from the correct source version.

- Your plugin might need to be upgraded to the newest version.

### Can't delete an existing action

If you can't delete an action, check that:

- You're logged in.

- The agent you're using is currently running. Try running [`list-agents`](/cli/cli_reference/#list-agents) to check.

### No code found

The `No code found at line # in <path>` error may occur even if the action (for example, a log) is inserted at a line that contains executable code.

![No code found error](/assets/images/no-code-found-error.png){: style="width:70%"}

**Symptoms and causes**

This error typically happens when inserting a log in a code line that doesn't have executable code. The probable cause of the error is that a log action, in most cases, triggers at the line preceding the log insertion position. If the previous line is empty or contains no executable code, then the `No code found` error is displayed.

**Suggested solution**

Try moving the action insertion position to the line following the one for which the log is intended to trigger.

