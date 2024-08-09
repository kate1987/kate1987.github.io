# Lightrun PII Redaction

The Lightrun PII (Personal Identifiable Information) redaction feature protects user privacy and improves data security within Production environments. By preventing the exposure of sensitive data in snapshots and dynamic logs this feature not only supports individual’s privacy but also ensures compliance with data protection regulations. Organizations applying PII redaction demonstrate a commitment to data privacy, thereby enhancing trust and reputation. During the debugging process, it is important that Personally Identifiable Information (PII) is not exposed to users in snapshots or logs in IDE plugins. Such sensitive information includes email addresses, credit card data, passwords, personal mobile numbers, and social security numbers.

Lightrun supports the redaction of PII in various data structures, including strings, arrays, and nested objects, within both snapshots and dynamic logs. This is achieved through patterns formulated using regular expressions, specifically supporting [Google's RE2 regular expressions engine](https://github.com/google/re2/wiki/Syntax). When the redaction patterns are activated, lightrun takes charge of processing them. It applies redaction rules to the data, ensuring sensitive information is masked on all outputs.

!!! note

    Starting from Lightrun version 1.22, PII Redaction patterns can now be created using Google's RE2. Customers are not required to install anything when upgrading to this latest version. Although older Regex patterns will be automatically RE2 specification compliant across various runtime languages, it is highly recommended to validate the functionality of PII Redaction for your desired patterns to ensure proper behavior.

## Get started with PII Redaction

To start using PII redaction, you are required to configure patterns with rules governing the redaction functionality. These rules are defined using Regex 2.0 regular expressions. 
Start by reviewing the [Lightrun PII Redaction Best Practices](/piiredaction/pii-redaction-best-practices/).

Lightrun supports two methods for setting patterns. You have the flexibility to create custom templates tailored to your specific requirement and to simplify this setup, Lightrun provides access to a library of predefined patterns.

- **Configure custom PII Redaction patterns**

    Depending on your Lightrun subscription, you can apply a single pattern to the default agent pool or create templates for multi-agent environments.

  - Configure PII Redaction for a single Agent Pool environment:
  Follow the step-by-step [Configure PII Redaction](/piiredaction/configure-pii-redaction/) guide to set up PII redaction in a single-agent pool environment.

  - Configure PII Redaction templates to be used accross multiple Agent Pools (RBAC required):
  You have the flexibility to either apply a single template across all agent pools or create specific patterns for individual agent pools. 
  For environments with multiple agent pools, see [manage PII Redaction templates for Agent Pools](/rbac/agent-pool-pii-redaction/).

- **Apply a predefined PII Redaction pattern from the pattern library**
  
  The option to use predefined Personally Identifiable Information (PII) Redaction patterns from the Patterns library offers a practical advantage. This approach eliminates the need for custom pattern creation, saving time and effort. The library provides tested patterns, ensuring reliability in PII redaction. Once selected, these patterns are integrated into the user's set of PII rules/templates based on their license, enhancing convenience. 
  For more information, see [Set a PII Redaction Pattern Using Predefined Patterns](/piiredaction/configure-pii-redaction/#set-a-pii-redaction-pattern-using-predefined-patterns).

