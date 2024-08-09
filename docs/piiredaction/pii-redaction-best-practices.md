# Lightrun PII Redaction best practices

To protect user privacy and improve data security, it is important that Personally Identifiable Information (PII) is not included in snapshots or logged in IDE plugins. This includes information such as email addresses, credit card data, passwords, personal mobile numbers, social security numbers, etc.

When implementing PII redaction with Lightrun, we recommend using the following best practices to reduce the risk of exposing sensitive data through Lightrun.

## Restrict Admin roles to enhance security

Ensure that only trusted users in your organization have access to specific roles and permissions in Lightrun. Only users with role_manager or System administrator permissions can specify or remove PII redaction patterns from Lightrun. For more information on how to manage users and user permissions, see [Manage Users and Roles](/useradmin-roles/).

## Apply case insensitivity
Patterns are initially set as case-insensitive by default, and it is advisable to retain this default setting. Default code identifiers, such as variable names, classes, and packages, are inherently case-insensitive. Consequently, redaction will apply to all variations, whether uppercase or lowercase, of the identifier.

## Update PII Redaction filters on existing agents
Lightrun agents fetch updated PII filters during startup. To apply the new filters on your existing agents, simply restart them.

## Use patterns from Lightrun's dedicated patterns library

To reduce the risk of errors due to patterns containing incorrect syntax compared to the time consuming process of manual creation, Lightrun provides a dedicated Regex Patterns library containing a set of predefined common PII patterns that conform with RE2 Google-compliant Regex expressions. 
In the Patterns library, the patterns are grouped according to these main categories:  Credit Cards, Financials, General and Network. These categories help streamline the process of locating specific PII patterns based on their characteristics. For more information, see [Set a pii redaction pattern using predefined patterns](/piiredaction/configure-pii-redaction/#set-a-pii-redaction-pattern-using-predefined-patterns).


## Test your PII Redaction are working correctly

It is highly recommended to validate the functionality of PII Redaction for your desired patterns to ensure proper behavior. Only you know the format in which your system stores potentially sensitive data. It's crucial to test and tune PII patterns to ensure they effectively redact all sensitive data.

