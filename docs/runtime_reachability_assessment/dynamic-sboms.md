# Prioritize CVEs using Lightrun dynamic SBOMs

!!!note
    The Runtime Reachability Assessment feature is under limited availablity. Please contact us to gain access to this feature.

Lightrun version 1.36 introduces the concept of Dynamic Software Bill of Materials (SBOMs), hereinafter referred to as SBOM. As a part of the [Runtime Reachability Assessment](/runtime_reachability_assessment/overview/), Lightrun generates an SBOM that offers insights into all the loaded libraries during runtime. This dynamic approach empowers developers to verify whether any of the loaded packages in their application have known CVEs (Common Vulnerabilities and Exposures). Additionally, it enables a comparison with a statically generated SBOM, helping identify packages included in the application but not actually being loaded. The SBOMs undergo updates every hour. 

In the Lightrun Management Portal, administrators can effortlessly view SBOMs on demand, with the option to export them as CSV, SPDX or CycloneDX files. The system provides an automatically updated SBOM for the current date by default, ensuring real-time accuracy. For enhanced flexibility, users with the manager-role can tailor SBOMs according to specific criteria using various filters such as SBOM creation time, package type, version number, or tag name. Unlike setting [watched packages](/runtime_reachability_assessment/watched-packages/), SBOMs report on all the loaded libraries and classes in an application, eliminating the need for selecting packages manually.


You can perform the following Dynamic SBOM-related tasks:

- Generate SBOMs by tags (Mandatory prerequisite)

- View an SBOM using customized filters

- Generate and export an SBOM to multiple file formats

## Prerequisite: Generate SBOMs by tags 

SBOMs are usually generated for specific services or applications. As a first step for collecting SBOM data you will need to choose for which application you wish to collect it. To do so, you should enter the list of Lightrun tags which represents the relevant application(s) and environments you wish to collect data from, for example, choose the tags: `MyService`, `Production`.

!!!Important
    This procedure is mandatory prior to collecting SBOM data.

1. Log in to your Lightrun account.
2. Click **Settings** on the top right-hand side of your screen to navigate to the Settings dashboard.
3. Navigate to **Runtime Reachability** and click **SBOM**. 
    
    The **SBOM** page opens.

    ![Set tags by SBOMS](/assets/images/runtime-reachability-sboms-assign-tags.png)

4. Enter the tag name or multiple tags, or click **Enter** and select tags from a list of existing tags or manually enter future tags which do no not yet exist.
    The tags are added to the list.
5. Click **Save**.
    The SBOMs will be generated from this point based on the selected tags and viewable in the Dynamic SBOM tab under Runtime Reachability Assessment page.


## View an SBOM using custom filters

By default, you can view the contents of an SBOM containing all your loaded or unloaded packages for your application, updated within the last 24 hours. You can customize the view by applying the following filters: SBOM Creation time, package type, version number, or tag.

1. Log in to your Lightrun account.
2. Click **Settings** on the top right-hand side of your screen to navigate to the Settings dashboard.
3. Navigate to **Runtime Reachability Assessment** and click the **Dynamic SBOM** tab.
    The default SBOM is displayed as a list of packages loaded within the last 24 hours.

    ![view sboms](/assets/images/runtime-reachability-assessment-sbom.png)

4. To customize the view of the Dynamic SBOM, set the filters such as SBOM Creation time, Package, Version, or Tag. The resulting list will display the loaded packages included in the Dynamic SBOM.

## Generate and Export SBOMs

You can generate and export SBOMs for the following formats:

- Export an SBOM an a CSV file
- Export an SBOM as am SPDX format
- Export an SBOM as a CycloneDX format


### Export an SBOM as a CSV file

You have the option to export your SBOM as a CSV file, providing detailed information about  the loaded packages in the runtime application. This export feature facilitates a more in-depth analysis of your CVE vulnerabilities.

1. Log in to your Lightrun account.
2. Click Settings on the top right-hand side of your screen to navigate to the Settings dashboard.
3. Navigate to **Runtime Reachability Assessment** and click the **Dynamic SBOM** tab.
    The list of SBOMs is displayed.

4. Select the specific SBOM from the list and click **Export as CSV**.
    The file is then downloaded to your local drive in the specified CSV format.

    ![view sboms as CSV](/assets/images/dynamic-sbom-csv.png)

### Export an SBOM as an SPDX file

[SPDX](https://spdx.dev/) is an open standard for communicating software bill of material information, including provenance, license, security, and other related information. It is an open source project hosted by the Linux Foundation. 

You can export your SBOM as an SPDX file, providing detailed information about the loaded packages in the runtime application. This export feature facilitates a more in-depth analysis of your CVE vulnerabilities.

1. Log in to your Lightrun account.
2. Click **Settings** on the top right-hand side of your screen to navigate to the Settings dashboard.
3. Navigate to Runtime Reachability Assessment and click the **Dynamic SBOM** tab. The list of SBOMs is displayed.
4. From the **Export Data** list, select the **SPDX Format**. 
The **Generate SPDX SBOM Report** dialog opens.

5. In the **Application Name** field, enter the name of your application or package for which you want to generate the SBOM.
6. In the **Supplier** field, enter the name of your organization or author who created the application described in the SBOM document. 
7. In the **Version** field, enter the version of your application or package for which you want to generate the SBOM.
8. Click **Download SPDX Report**.
   The file is then downloaded to your local drive as a JSON file in the specified SPDX format.

```json hl_lines="10"  
   "dataLicense":"CC0-1.0","relationships":[{"relationshipType":"DESCRIBES","relatedSpdxElement":"SPDXRef-RootPackage","spdxElementId":"SPDXRef-DOCUMENT"},{"relatedSpdxElement":"SPDXRef-Package-SPRING-EXPRESSION","comment":".spring-expression was loaded at runtime","relationshipType":"RUNTIME_DEPENDENCY_OF","spdxElementId":"SPDXRef-RootPackage"},{"relatedSpdxElement":"SPDXRef-Package-SLF4J-SIMPLE","comment":"org.slf4j.slf4j-simple was loaded at runtime","relationshipType":"RUNTIME_DEPENDENCY_OF","spdxElementId":"SPDXRef-RootPackage"},    
```
### Export an SBOM as a CycloneDX file
[CycloneDX](https://cyclonedx.org/) is a full stack Software Bill of Materials (SBOM) standard, offering advanced features to enhance cybersecurity risk mitigation within supply chains. It serves multiple purposes in vulnerability analysis, including identification of known vulnerabilities, exploration of unknown vulnerabilities, assessment of vulnerability exploitability, and verification of remediation efforts.
You can export your SBOM as a CycloneDX file, providing detailed information about the loaded packages in the runtime application. This export feature facilitates a more in-depth analysis of your CVE vulnerabilities.

1. Log in to your Lightrun account.
2. Click **Settings** on the top right-hand side of your screen to navigate to the Settings dashboard.
3. Navigate to **Runtime Reachability Assessment** and click the **Dynamic SBOM** tab. The list of SBOMs is displayed.
4. From the **Export Data list**, select the **CycloneDX Format**. 
   The **Generate CycloneDX SBOM Report** dialog opens.
5. In the **Application Name** field, enter the name of your application or package for which you want to generate the SBOM.
6. Click **Download CycloneDX Report**.

   The file is then downloaded to your local drive in the specified CycloneDX format.

```bash  
    {"specVersion":"1.5","metadata":{"tools":{"services":[{"name":"Lightrun Runtime Reachability Analyzer","provider":{"name":"Lightrun"},"version":"6.6"}]},"component":{"name":"simple-java-app","licenses":[],"purl":"pkg:maven/null/simple-java-app@null?type=jar","type":"library","bom-ref":"pkg:maven/null/simple-java-app@null?type=jar"},"timestamp":"2024-03-05T10:29:05.375968Z"},"components":[{"bom-ref":"pkg:maven//spring-expression@6.0.12?type=jar","evidence":{"occurrences":[{"location":"BOOT-INF/lib/spring-expression-6.0.12.jar"}]},"scope":"required","name":"spring-expression","hashes":[{"alg":"SHA-1","content":"TBD"}],"purl":"pkg:maven//spring-expression@6.0.12?type=jar","type":"library","version":"6.0.12","group":""},{"bom-ref":"pkg:maven/org.slf4j/slf4j-simple@2.0.9?type=jar","evidence":{"occurrences":[{"location":"BOOT-INF/lib/slf4j-simple-2.0.9.jar"}]}
```


