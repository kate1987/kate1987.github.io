# Managing data security

When running Lightrun agents in your application you can control retrieval of sensitive data in the instrumented code by using:

- **Blocklists** - to prevent developers from inserting snapshots inside sensitive classes

- **PII redaction** - to prevent sensitive data from appearing in snapshots and logs

--8<-- "ux-reference/manager-role-only.md"

!!! note
    For additional security, you can [manage users and their roles](/useradmin-roles/){target="_blank"} and [audit system use](audit-use.md){target="_blank"}.

## Blocklists

Use blocklists to prevent snapshots being inserted in classes that might expose sensitive data. Files and packages that include the patterns you've specified in the Blocklist table are protected and your team won't be able to add snapshots.

You can configure blocklists to include package and class names, file names, and directory paths. You can also add blocklist exceptions for any relevant subclasses in which you want to allow snapshot insertion.

Each time your application is started, the agent's blocklist configuration is downloaded and applied to all future actions. If you modify the blocklist configuration, you must restart the application to activate the modified blocklist.

!!! info

    All users can view blocklists and blocklist exceptions but only managers can create, edit, and delete blocklist and blocklist exception patterns.

!!! example

    Prevent snapshots for com.sales with this pattern:


    ```bash
    com.sales
    ```

    Add the following exception so that snapshots can still be added to com.sales.Admin:

    ```bash
    com.sales.Admin
    ```

###### To configure a blocklist and blocklist exceptions

1. Log in to your Lightrun account.
2. Click **Settings** on the top right-hand side of your screen to navigate to the Settings dashboard.
3. Select **Blocklist** under **Security** in the Settings dashboard sidebar.

    The **Blocklist** window opens, showing a table of existing blocklist and blocklist exception patterns.

4. To add a text pattern for a new blocklist or blocklist exception, click the ![Button to add blocklist or exception](/assets/images/add-blocklist-button.png) button next to **Blocklist** or **Blocklist Exceptions**.

    The **Add Pattern** dialog box opens.

   ![Add blocklist or exception pattern dialog](/assets/images/add-blocklist-pattern-dialog.png)

5. Respectively for Blocklist and Blocklist Exceptions, in the **Pattern** text field, enter a pattern to be blocked or allowed as an exception (for example, a class name, file name, or directory path).
6. In the corresponding **Name** text field, for each pattern, enter a unique name.
7. Click **OK**. The dialog box closes and the Blocklist (or Blocklist Exceptions) table updates to include the newly added patterns.

Lightrun agents will fetch updated blocklists when they start up. To apply new filters to your existing agents you'll need to restart those agents.

## PII redaction

Use PII redaction to prevent Lightrun from capturing sensitive data in snapshots and dynamic logs.

There are two options for redacting sensitive data:

- **Variable name** -  Data is redacted based on variable name. Any variables which match the supplied pattern will be excluded from the data Lightrun captures. For example, adding a pattern `apiToken` will prevent Lightrun from logging data from any variable which includes `apiToken` in the variable name. So variables `my_apiToken`, `theOtherapiToken`, and `someapiTokenVariable` will all be redacted.

- **Variable value** - Data is redacted based on a specified regex pattern. The regex pattern is matched to a value, not a variable name. For example, the following regex pattern `\b5[1-5]\d\d([\-\ ]?)(?:\d{4}\1){2}\d{4}\b` will redact all Mastercard debit or credit card data from Lightrun.

!!! imp "important"
     Data from a configured variable name will only be redacted when the variable name is referenced directly in an expression. Suppose the variable name is not referenced directly; for example, if the variable name is a member variable to an object reference in an expression, data from the variable will not be redacted. The best practice is to combine the Variable name and value Filters to fully redact a variable.

!!! note
     From Lightrun version 1.14, the Variable name pattern is set by default as case sensitive. By enabling the **Make Case Insensitive** field when specifying `accountName`, data will be redacted from `ACCOUNTNAME`, `accountname`, and `AccountName` variables.

###### To configure PII redaction

1. Log in to your Lightrun account.
2. Click **Settings** on the top right hand side of your screen to navigate to the Settings dashboard.
3. Select **PII Redaction** under **Security** in the Settings dashboard sidebar.

    The **Data Redaction** window opens with a table of existing patterns.

4. To add a new pattern for redaction, click the ![Button to add blocklist or exception](/assets/images/add-blocklist-button.png) button.

    The **Add Pattern** dialog box opens.

    ![Add PII pattern dialog](/assets/images/pii-add-pattern.png)

5. Select your preferred data redaction mode.
6. In the **Name** text field, enter a unique name for the added pattern.
7. (Optional) Enable the **Make case insensitive** option to support case insensitive values. The default is set as case sensitive.
8. Add a Variable name or Variable value pattern depending on the mode you selected. 
9. To verify the pattern, in the **Test Input** text field, enter a test string corresponding to the pattern specified in the previous step.  
   Pattern verification is confirmed when the entered test string is highlighted in yellow.
10. Click **Save**.  
   The dialog box closes and the list of redacted character string patterns updates to include the newly added pattern.

Lightrun agents will fetch updated PII filters when they start up. To apply new filters to your existing agents you'll need to restart those agents.

### Best Practices for PII Redaction

To protect user privacy and improve data security, it is important that Personally Identifiable Information (PII) is not included in snapshots or logged in IDE plugins. This includes information such as email addresses, credit card data, passwords, personal mobile numbers, social security numbers, etc. 

When implementing PII redaction with Lightrun, we recommend using the following best practices to reduce the risk of exposing sensitive data through Lightrun.

* **Access Minimization** - Ensure that only trusted users in your organization have access to specific roles and permissions in Lightrun. Only users with `role_manager` or `System administrator` permissions can specify or remove PII redaction patterns from Lightrun. For more information on how to manage users and user permissions, see [Manager Users and Roles](/useradmin-roles/).

* **Combine Variable values and Variable names for very sensitive information** - If you have data related to any of the following in your system:
  - Credit cards
  - Social security numbers
  - Phone numbers
  - API tokens
  - ID numbers
  - Addresses

  Specifying both the variable names and values helps to reduce the risk of sensitive data being exposed to Lightrun.

The following table shows a list of regex patterns for protecting PII data:

!!! note
    Note that only you know the format in which your system stores potentially sensitive data. It's crucial to test and tune PII patterns to ensure they effectively redact all sensitive data.

#### Credit Cards

|Type|Pattern|Example|
|----|--------|-------|
| MasterCard |  `\b5[1-5]\d\d([\-\ ]?)(?:\d{4}\1){2}\d{4}\b` | 5489-7909-9447-0834|
| Visa | `(\d{4}[-\s]?){3}\d{4}` | 4716-5637-1231-1231 |
| Diners club | `\b3(?:0[0-5]|[68][0-9])[0-9]{11}\b` | 30569309025904 |
| Amex Card | `\b3[47][0-9]{13}\b` | 378282246310005 |

#### Financials

|Type|Pattern|Example|
|----|--------|-------|
| SWIFT code | `\b[A-Z]{6}[A-Z0-9]{2}([A-Z0-9]{3})?\b` | BOFAUS3N |

#### General PII

|Type|Pattern|Example|
|----|--------|-------|
| email | `\b[a-z0-9._%\+\-—|]+@[a-z0-9.\-—|]+\.[a-z|]{2,6}\b` | asd@gmail.com |
| Phone numbers | `^(\+?\d{0,2})?[\D]?\(?(\d{3})\)?[\D]?(\d{3})[\D].*` | +00 (000) 000-0000 |
| Social Security Number | `\d{3}-?\d{2}-?\d{4}` | 123-45-6789 |
| IPv4 | `\b\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}\b` | 172.12.0.2 |
| IPv6 | `\b([\d\w]{4}|0)(\:([\d\w]{4}|0)){7}\b` | 2001:db83:4333:4444:5555:6666:7777:8888 |


