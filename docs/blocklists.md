# Lightrun Blocklists

Use blocklists to prevent Lightrun actions being inserted into classes that might expose sensitive data. Files and packages that include the patterns specified in the Blocklist table are protected, and your team won't be able to add actions.

You can configure blocklists to include package and class names, file names, and directory paths. You can also add blocklist exceptions for any relevant subclasses in which you want to allow action insertion.

Each time your application is started, the agent's blocklist configuration is downloaded and applied to all future actions. If you modify the blocklist configuration, you must restart the application to activate the modified blocklist.

This is a common blocklist example. In this scenario, you aim to prevent actions for `com.sales` using the following pattern:

```bash
com.sales
```

To allow actions specifically for the `com.sales.Admin` class, you can add the following exception:

```bash
com.sales.Admin
```

## Configure blocklist and exceptions

!!! info

    All users can view blocklists and blocklist exceptions but only managers can create, edit, and delete blocklist and blocklist exception patterns.

###### To configure a blocklist and blocklist exceptions

1. Log in to your Lightrun account.
2. Click **Settings** on the top right-hand side of your screen to navigate to the Settings dashboard.
3. Select **Blocklist** under **Security** in the Settings dashboard sidebar.

    The **Blocklist** window opens, showing a table of existing blocklist and blocklist exception patterns.

4. To add a text pattern for a new blocklist or blocklist, click the ![Button to add blocklist or exception](/assets/images/add-blocklist-button.png) button next to **Blocklist** or **Blocklist Exceptions**.

    The **Add Pattern** dialog box opens.

   ![Add blocklist or exception pattern dialog --half](/assets/images/blocklist-add-pattern.png)

5. In the **Name** text field, for each pattern, enter a unique name.
6. Respectively for Blocklist and Blocklist Exceptions, in the **Regex** text field, enter a Regex pattern to be blocked or allowed as an exception (for example, a class name, file name, or directory path).
7. Click **Save**. 
    
    The dialog box closes and the Blocklist (or Blocklist Exceptions) table updates to include the newly added patterns.

    Lightrun agents will fetch updated blocklists during startup. To apply new filters to your existing agents you'll need to restart those agents.
