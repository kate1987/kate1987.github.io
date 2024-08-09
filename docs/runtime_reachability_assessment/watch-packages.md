# Prioritize CVE resolution based on loaded packages

!!!note
    The Runtime Reachability Assessment feature is under limited availablity. Please contact us to gain access to this feature.

Understanding the libraries and classes loaded during runtime is crucial for effective prioritization and targeted resolution of potential CVEs. This knowledge enables you to concentrate on prioritizing fixes for CVE in loaded packages.

The [Lightrun Reachability feature](/runtime_reachability_assessment/overview/) enables you to focus on prioritizing CVEs, determining which CVEs have a higher severity since the affected packages are loaded in runtime, and assigning lower priorities to those with less severe threats. To gain further granularity, you can track specific classes within the vulnerable package that contains the vulnerability. This approach provides more precise results by determining whether those specific classes were loaded. This use case is tailored for teams already aware of specific libraries prone to CVEs. For more information, see Lightrun Runtime Reachability Assessment. 

Once you have added the package and classes to the watch list, Lightrun scans the package and its components, indicating whether they are loaded or not. The results are displayed in the Loaded Packages tab, available after a one-hour period. For instructions on viewing the results, see [View loaded and not loaded dynamic packages](/runtime_reachability_assessment/view-loaded-not-loaded-packages/).

Proceed to add packages and classes to the watchlist either manually, one by one, or utilize bulk import through a CSV file. Additionally, you can perform a set of housekeeping tasks, including editing or removing packages from the list, as described in the following sections.

## Add packages and classes to your watch list

1. Log in to your Lightrun account.
2. Click **Settings** on the top right-hand side of your screen to navigate to the Settings dashboard.
3. Navigate to the **Runtime Reachability** section and click **Watched Packages**.
   The Watched Packages page opens.
4. Click **+Add Package**. 
   
   The **Add a Package** dialog opens.

   ![Add a Package](/assets/images/cve-reachability-assessment-add-a-package.png)

5. Enter the following package details according to the Maven package naming convention:
   - `Name`: `groupId:artifactId`. 
   `artifactId` is the name of the Jar without the version using lower letters and no special characters.
   For example: `org.xerial.snappy:snappy-java`.
   Note that under certain circumstances where <groupid> cannot be determined, an empty string will be displayed and only the  <artifactid> will be displayed.
   - `Version`: This field is optional. if left empty, all versions for the package will be monitored. For example: When using version `1` the following versions will be matched: `1`, `1.x`, `1.x.y` (`1`, `1.2`, `1.0.3`). When using version `1.2` the following versions will be matched: `1.2`, `1.2.x` (`1.2`, `1.2.3`). 
   - `Watched Classes`: This field is optional. Use both lower or upper class letters with periods for each class abbreviation. For example: `foo.bar.ClassName`. 
6. Click **Add**.
   The results become available within, or up to, (it depends on when the last time the agent synced the watched packages), a 5-minute period, clearly specifying the status as either Loaded or Not Loaded in the Loaded Packages page.

## Import packages in bulk
You can effortlessly upload multiple packages at once by utilizing a predefined CSV file. 

The package names need to conform to the Maven package naming convention:

- **Name**: `groupId:artifactId`. 
  
  `artifactId` is the name of the Jar without the version using lower letters and no special characters. For example: `org.xerial.snappy:snappy-java`. 

- **Version**: This field is optional. when left empty, all versions for the package will be monitored.
- **Watched Classes**: This field is optional. Use both lower or upper class letters with periods for    each class abbreviation. For example: `foo.bar.ClassName`.

##### Import Packages in bulk using a CSV File
   
1. Create a CSV file containing the list of packages to be imported, following the format displayed in this example.

   ![CSV example file --third](/assets/images/runtime-reachability-csv-example.png)

2. Log in to your Lightrun account.
3. Click **Settings** on the top right-hand side of your screen to navigate to the Settings dashboard.
4. Navigate to the **Runtime Reachability** section and click **Watched Packages**. 
   
   The **Watched Packages** page opens.

   ![Watched Packages page](/assets/images/runtime-reachability-watch-packages.png)

5. Click **Upload from CSV**.

   This will prompt your file explorer to open, allowing you to select your predefined CSV file.

6. Select the CSV file to upload.

   The **Upload from CSV** dialog opens.
   
   ![Upload from CSV dialog](/assets/images/runtime-reachability-upload-from-csv.png)

7. Click **Upload File**.
 
   Note that all the history of your existing package included in your Watch list will be overwritten by the new packages imported from the uploaded file.

## Manage your packages in the watch list

You can perform various tasks on your watched packages including editing and removing watched packages.

###### EDIT A WATCHED PACKAGE

In cases where an error is detected in the package name or version, follow these steps to edit the package information. Note that saving the edited package classifies it as a new package, resulting in the removal of previously collected data.

1. Log in to your Lightrun account.
2. Click **Settings** on the top right-hand side of your screen to navigate to the Settings dashboard.
3. Navigate to the **Runtime Reachability** section and click the **Watched Packages** tab.
   The list of Loaded and Not Loaded packages is displayed.
4. In the selected package row, click ![Edit icon](/assets/images/runtime-reachability-edit-icon.png).
   
   The **Edit a Package** dialog opens.

   ![Edit a package](/assets/images/runtime-reachability-assessment-edit-a-package.png)

5. Modify the information as required and click **Save**.

###### REMOVE A PACKAGE FROM THE WATCH LIST

To remove a package from your watch list, follow these steps. Be aware that all information collected for this watched package will be erased.

1. Log in to your Lightrun account.
2. Click Settings on the top right-hand side of your screen to navigate to the Settings dashboard.
3. Navigate to the **Runtime Reachability** section and click the **Watched Packages** tab.
   The list of Loaded and Not Loaded packages is displayed.
4. To remove the package, click the selected package row, and click ![Delete icon](/assets/images/runtime-reachability-assessment-delete-icon.png).
   
   A confirmation message opens.

   ![Remove a package](/assets/images/runtime-reachability-assessment-remove-a-package.png)

5. Click **Remove**. Note that all the data generated for the loaded package will be deleted.
