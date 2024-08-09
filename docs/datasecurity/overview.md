# Data security in Lightrun

!!! role "Permissions"

    Security management requires administrative permissions.

Lightrun places a strong emphasis on data security, considering it a fundamental aspect of software development. The platform demonstrates its commitment by implementing stringent security measures and adhering to the highest security standards. 

As part of Lightrun's commitment to protecting your data, our platform adheres to enterprise-grade certifications, including ISO-27001, SOC-2, GDPR, and HIPAA certifications. Additionally, the platform employs certificate pinning on both the client and agent sides. This proactive approach enhances security by ensuring that only authorized certificates are accepted during the communication process. 

Lightrun ensures secure data transmission by employing encrypted communication channels and supporting TLS 1.2 for all services. Additionally, customer data hosted in AWS is safeguarded using Amazon's AES-256 encryption algorithm on Elastic Block Store (EBS) and Relational Database Service (RDS) databases.

## Lightrun data security features

Lightrun offers the following features for ensuring that sensitive data is not exposed to unauthorized individuals:

### PII redaction

The Lightrun PII (Personal Identifiable Information) redaction feature protects user privacy and improves data security within Production environments. By preventing the exposure of sensitive data in snapshots and dynamic logs this feature not only supports individual’s privacy but also ensures compliance with data protection regulations. Organizations applying PII redaction demonstrate a commitment to data privacy, thereby enhancing trust and reputation. For more information, see [Lightrun PII Redaction Overview](/piiredaction/overview).

### Blocklists

Blocklists can be used to prevent Lightrun actions from being inserted in classes that might expose sensitive data. Files and packages that include the patterns you've specified in the Blocklist table are protected and your team won't be able to add actions into those code areas. You can configure blocklists to include package and class names, file names, and directory paths. You can also add blocklist exceptions for any relevant subclasses in which you want to allow action insertion. Each time your application is started, the agent's blocklist configuration is downloaded and applied to all future actions. For more information, see [Blocklists](/blocklists).

### Audit Lightrun system usage

Lightrun maintains a record of your organization's Lightrun system usage, including actions, and changes that are logged and can be audited, which is crucial for observing continuous compliance, performing system audits, and maintaining security. The stored audit logs include data about activities related to the Management Portal, Lightrun plugins, and agents. For more information, see [Audit System Usage](/audit-use).

## Data protection by Lightrun deployment types

| Deployment type | Description  | Data transmission strategies| Encryption as REST |
|-----------------|--------------|-----------------------------|-------------------|
| SaaS             | Lightrun hosts the server components in the highly-secure and available AWS environment, based on hardened virtual servers and services and supports these SaaS deployment types: <br> • **Multi-tenant**: Infrastructure is shared with other customers. <br> • **Single tenant**: Isolated from other customers <br><br> | • Action data is sent from agents to Lightrun   as a gateway to transmission to developers.<br><br> • All the communication is encrypted in  transit via TLS 1.2. <br><br> • Data stored in the Lightrun server is configurable and can be redacted by customers to just the bare minimum required to transfer the data to the developers who requested it. <br><br>| All customers’ data hosted in AWS is encrypted using Amazon’s AES-256 encryption algorithm and stored on Elastic Block Store (EBS) storage and Relational Database Service (RDS) databases | 
| On Premise | Lightrun is installed within your organizational network or through a private cloud, via Docker or Kubernetes. | No customer data leaves the customer premises or is sent to Lightrun. | All customers' data is stored in a self managed Database. We strongly recommend encrypting the database using industry standards.|


## Strategies for securing your data

We recommend using the following measures for keeping data privacy and safeguarding your customers’ sensitive information:

- Manage developers’ access to runtime environments, such as production, using Lightrun role based access control.
- Ensure that only authorized individuals can access environments which contains sensitive user data.
- Create separate agent pools for environments which contain sensitive users data and use them when applying access controls.
- Connect Lightrun with your identity management system and leverage the SAML and SCIM integrations to ensure that only authorized developers have access to Lightrun.
- Configure PII redaction rules for both variable names and values to make sure that sensitive data is not accessible to Lightrun actions.
- Use standard regular expression patterns for redacting sensitive information such credit card numbers, secrets such as tokens and API keys, email addresses and social security numbers.
- Add blocklist rules for preventing developers from adding Lightrun actions in sensitive code sections, for example one which deals with payment processing or user’s personal details.
- Routinely review Lightrun audit logs to identify any instances where an attempt was made to log sensitive data.
- Consider forwarding the audit logs to you SIEM solution.
