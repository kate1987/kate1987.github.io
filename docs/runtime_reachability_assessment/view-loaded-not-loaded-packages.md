# View loaded dynamic packages in your application

!!!note
    The Runtime Reachability Assessment feature is under limited availablity. Please contact us to gain access to this feature.

Lightrun enables you to monitor and receive notifications about dynamically loaded packages in your application during runtime. This functionality operates by tracking a predefined list of packages that you've added to a watchlist.

As part of the [Runtime Reachability Assessment](/runtime_reachability_assessment/overview) feature, once you've [set up the watch list](/runtime_reachability_assessment/watch-packages/), you can proceed to manually review the status of the monitored packages and classes or set up notifications to be triggered in your target third-party applications using [webhooks](/webhooks). 

## Before you begin

1. [Add the packages you want to track to the watch list](/runtime_reachability_assessment/watch-packages/).
2. (Optional) To receive automated notifications in your third-party applications, configure at least one [webhook](/webhooks).

##  View loaded/ not loaded dynamic packages based on watch list

1. Log in to your Lightrun account.
2. Navigate to **Runtime Reachability Assessment** and click the **Loaded Packages** tab.
   
   The list of Loaded and Not Loaded packages and classes are displayed.

3. (Optional) You can filter using a set of filters to narrow down the view based on your requirements.
   ![Loaded/Not Loaded Package ---three quarters](/assets/images/runtime-reachability-assessment-loaded-packages.png)
4. You can expand this list by adding more packages to the Watch list. Simply click **Add Packages**, and you will be directed to the Watched Packages page.

## Get notifications for loaded packages {#notifications}

To help you keep track of your monitored loaded packages without needing to manually review the Loaded packages list constantly, you can create notifications for each of your monitored packages. This way, you'll receive alerts when they are loaded into your live application based on the integration with [webhooks](/webhooks/).

!!! Prerequisite
    Before proceeding, ensure you have set up at least one webhook. For more information, see [Webhooks](/webhooks/).

### Set up a notification

1. Log in to your Lightrun account.
2. Click **Settings** on the top right hand side of your screen to navigate to the Settings dashboard.
3. Navigate to the **Runtime Reachability Assessment** section and click the **Loaded Packages** tab. 

   The Loaded Packages page opens.

   ![Loaded/Not Loaded Package ---three quarters](/assets/images/runtime-reachability-assessment-loaded-packages-notifications.png)

4. In the required Watched package line, click the **Notifications** icon.
   
   The **Set notification** dialog opens.

   ![Set a notification ---half](/assets/images/runtime-reachability-set-a-notification.png)

5. Set the notification details:

   a. Enter the **Package Name**. 

   b. **Package Version**: Select a specific version. Leave it empty to apply all versions.

   c. **Notification Method**: Select a Webhook from a preset list.  
      
   When a webhook is triggered, it sends a notification to a web location that is listening for that specific event notification. To learn more, click [Webhooks](/webhooks/). 
 
6. Click **Set Notification**.

### Manage notifications

#### About notifications icons

The following table lists the supported notification icons and what they indicate:

| Icon | Description                                     |
|------|-------------------------------------------------|
|![Set alert ---third](/assets/images/runtime-reachability-notification-tobeset.png)| Set a notification for when a package is loaded.|
|![No alert ---third](/assets/images/runtime-reachability-loaded-packages-notifications-notification-set.png)| A notification has been set on the package. Click the icon to remove the notification.|
 ![no alert ---third](/assets/images/runtime-reachability-notification-icon-loaded.png)| The notification has been triggered. Note that it may take up to an hour for it to appear in the targeted tool. |
| ![no alert ---third](/assets/images/runtime-reachability-notifications-icon-notoarlerted.png)| Cannot be configured since the package is already loaded.

###### Delete a notification

You can delete an active notification for a package that has not yet been loaded. However, you cannot delete a notification for a package that has already been tagged as loaded.

1. Log in to your Lightrun account.
2. Click **Settings** on the top right hand side of your screen to navigate to the Settings dashboard.
3. Navigate to the **Runtime Reachability** section and click **Loaded Packages**. 
   
   The Loaded Packages page opens.

4. Hover over the Notification.
   
   The **Delete notification** tooltip is displayed.

   ![Delete a notification](/assets/images/runtime-reachability-notification-delete.png)

5. Click **Delete Notification**.

## Export watched loaded/ not loaded packges to a JSON file

You have the option to export your SBOM as a JSON file, providing detailed information about the loaded packages in the runtime application. This export feature facilitates a more in-depth analysis of your CVE vulnerabilities.

1. Log in to your Lightrun account.
2. Click **Settings** on the top right-hand side of your screen to navigate to the Settings dashboard.
3. Navigate to **Runtime Reachability Assessment** and click the **Loaded Packages** tab.
    The list of packages is displayed.
4. Click **Export as JSON**.
   
   The file is then downloaded to your local drive as a dedicated JSON file as displayed in the following example. `lightrun_loaded_packages-2024-02-08T07_28_58.992Z.json`

   ```shell
      [
         {
         "package": {
               "name": "org.json:json",
               "version": "20230618",
               "agents": 5,
               "tags": [],
               "status": "LOADED",
               "classes": [
               {
                  "name": "org.json.JSONObject",
                  "status": "NOT_LOADED",
                  "agents": 5,
                  "tags": []
               },
               {
                  "name": "org.json.JSONObjection",
                  "status": "LOADED",
                  "agents": 5,
                  "tags": []
               }
               ]
            }
         },
         {
            "package": {
               "name": "org.apache.commons:commons-lang3",
               "version": "3.14.0",
               "agents": 5,
               "tags": [],
               "status": "NOT",
               "classes": []
            }
         },
         {
            "package": {
               "name": "org.springframework:spring-web",
               "version": "6.0.13",
               "agents": 4,
               "tags": [],
               "status": "NOT_LOADED",
               "classes": [
               {
                  "name": "org.springframework.http.HttpStatus.Series",
                  "status": "LOADED",
                  "agents": 4,
                  "tags": []
               },
               {
                  "name": "org.spring.net.load",
                  "status": "NOT_LOADED",
                  "agents": 4,
                  "tags": []
               },
               {
                  "name": "org.springframework.http.HttpMethod",
                  "status": "LOADED",
                  "agents": 4,
                  "tags": []
               }
               ]
            }
         }
      ]
   ```   