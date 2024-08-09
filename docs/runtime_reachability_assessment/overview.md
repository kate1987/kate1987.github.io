# Lightrun Runtime Reachability Assessment

!!!note
    The Runtime Reachability Assessment feature is under limited availablity. Please contact us to gain access to this feature.

As a developer, safeguarding your application goes beyond debugging; it involves ensuring overall quality and security to prevent vulnerabilities and breaches. The task of scrutinizing software libraries for Common Vulnerabilities and Exposures (CVEs) can be daunting, often involves reviewing extensive lists from security analysis tools. The Lightrun Runtime Reachability Assessment feature simplifies this challenge by enabling the easy identification of packages and classes loaded in real-time. It aids in prioritizing CVEs by providing insights into their current usage, emphasizing the urgency for remediation.

To prioritize the resolution of CVEs, Lightrun offers two mechanisms for examining loaded packages and classes in your application. When used together, these mechanisms provide a multilayered solution to enhance the protection of your data. The first is designed for setting watches on specific packages with known CVEs, providing a targeted approach. In contrast, the second allows for a comprehensive review of all loaded packages in the application for prioritization. These mechanisms provide flexibility and efficiency in managing and prioritizing security concerns throughout the development process.

## Prerequisites

- This feature is available for the Lightrun Java Agent.
- It is accessible to a limited number of customers as part of a private Beta release and will be gradually expanded to a broader audience.
- To enable the feature, add the following parameters to your `agent.config` file: 
        
    ```bash
    runtime_reachability_watched_packages_enabled=1
    runtime_reachability_dynamic_sbom_enabled=1
    
    ```

- You can modify elements related to the Runtime Reachability Assessment’s behavior by configuring the following properties. Configuring the agent properties can be done either from the command line flags or from the `agent.config` file. 


    | Parameter Name  | Description | Default value  | Type  |
|---------------------|-------------|----------------|-------|
| `runtime_reachability_watched_packages_enabled`| Enables adding watched packages.Value can be 0 (disabled), or 1 (enabled).|0| bool|
| `package_tracking_thread_frequency_sec` | Set the frequency of the package tracking thread in seconds. | 10                       | int32 |
| `watched_packages_sync_frequency_sec`   | Set the frequency of syncing watched packages with server in seconds. | 5 * 60 </br> (5 minutes)   | int32 |
|`runtime_reachability_dynamic_sbom_enabled`|Enables viewing and exporting SBOMs. Value can be 0 (disabled), or 1 (enabled)| 0| bool|
| `dynamic_sbom_report_frequency_sec`    | Set how often the dynamic SBOM report will be refreshed.      | 60 * 60 (1 hour)         | int32 |
| `report_sbom_on_shutdown`             | Send the Dynamic SBOM report on agent shutdown.        | `true `                    | bool  |
| `dynamic_sbom_first_report_max_delay_sec`| Maximum time in seconds to start reporting a SBOM for the first time.| 600 (10 minutes)| int32|

## Get Started

The Runtime Reachability Assessment feature can be configured using two of the fowllowing methods and requires administrative permissions:

- [The Lightrun REST API](/public_api/api-reference/).

- The Lightrun Management Portal. 

  - Add selected packages and classes to the loaded packages watch list:
   
    1. [Add Java libraries to the Watched Packages for tracking vulnerable packages](/runtime_reachability_assessment/watch-packages/).
   
    2. [View and track which of the watched packages are loaded at runtime](/runtime_reachability_assessment/view-loaded-not-loaded-packages/).

  - Manage Dynamic SBOMS:
  - [View all loaded packages in a Dynamic SBOM](/runtime_reachability_assessment/dynamic-sboms/)
    
    To conduct a more in-depth investigation of CVEs, we support Dynamic SBOMs. You can review a dynamic SBOM displaying all the loaded packages in your application, or utilize a set of filters to focus on specific information.

  - Export your SBOM as a downloadable file
    
    Export your SBOM as an external file, that includes detailed information about the loaded packages in the runtime application. Multiple export formats are supported including CSV, SPDX, and Cyclone.

