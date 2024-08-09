# Lightrun release information


Lightrun offers dedicated release notes for each of its releases, encompassing key highlights, feature enhancements, and bug fixes. This document outlines the Lightrun release cycle, its components, and various considerations to keep in mind when upgrading your Lightrun application.

## Which Lightrun components are impacted during an upgrade?

For optimal performance and access to the latest features, bug fixes, and security fixes, it is advisable to keep the Lightrun environment up-to-date with the most recent version. To fully benefit from the features introduced in a specific release, it is essential to ensure that all three components are upgraded to the corresponding version that includes these new functionalities.

The Lightrun solution consists of three main components, all of which are required to be upgraded as part of the upgrade to the latest Lightrun release. These components include:

- Lightrun Management Portal: Referred to as the Lightrun server.
- Lightrun Plugin: Locally installed by users in their IDE.
- Lightrun Agents: Installed, usually by the customer’s DevOps team, in the various runtime environments: Production, Staging, etc.

## What Lightrun deployment types are supported?

Lightrun provides a number of  deployment options: Software as a Service (SaaS), Single tenant, and On-premise. Here's how they work:

- SaaS: Lightrun follows the Cloud-first strategy, with SaaS versions receiving updates every two weeks.
- Single-Tenant: A Lightrun-hosted, private management server private deployment In the cloud on a dedicated deployment and infrastructure. Updates for the single-tenant versions are released every two weeks.
- On-Premise: A fully-air gapped, on-premise management server, without exposing any data to the outside world. 

## How can I detect what Lightrun version is currently running?

Ensuring you're up to date with the latest Lightrun versions for each of the Lightrun components is crucial for optimal performance. Here's how you can detect what Lightrun version is currently running. 

| Component                  | Instructions|
|----------------------------|-------------|
| [Lightrun Management Portal](/nav/)|  - Visit `https://<app-name>.lightrun.com/version` to check the server version.                                       |
| [Lightrun Agent](/introduction/agents/)|  - Navigate to **Entities > Agents > Agent Version** in the Lightrun Management Portal and check the `Agent Version` column. |
| [Lightrun Plugin](/docs/introduction/plugins/) | - Open your IDE, go to the **Marketplace** (JetBrains: Plugins, VSCode: Extensions), and find the **Lightrun plugin**. Check the version in the **Overview** tab. |


## What actions are required for the upgrade?

The procedure for upgrading these Lightrun components to the latest version may differ based on your deployment type. To assist you in determining if any action is necessary on your part after the server has been upgraded, please consult the following table.

| Deployment Type    | Lightrun Server | Lightrun Plugin | Lightrun Agents |
|------------------ |-----------------|----------------|------------------|
| SaaS            | No action required <br> Automatically upgraded  | Requires user action <br> - User gets indication when a new release is available in the relevant IDE Marketplace. | Requires user action <br> - Download Agents from the Management Portal|
| Single Tenant    | No action required <br> Automatically upgraded | Requires user action <br> - User gets indication when a new release is available in the relevant IDE Marketplace <br>  | Requires user action <br> - Download Agents from the Management Portal | 
| On-Premise | Requires manual upgrade | Requires user manual upgrade <br> Note: For JetBrains plugin users, you can also download from the custom plugin repository. | Requires user action <br> - Download Agents from upgraded Management Portal |




