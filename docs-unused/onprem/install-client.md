# Install the plugin

With Lightrun, you can add actions (logs, metrics, snapshots) from the source code of your live app either from your IDE, or from the CLI. To use Lightrun, [attach the Lightrun agent](../install.md) to your running application and then install the plugin in your IDE.

!!! info "Support"
    
	 Lightrun currently supports the IntelliJ IDE. 


###### To install the plugin

1. Log in to your Lightrun account from your browser. 

    The Lightrun Web Console loads.
    
2. Navigate to **Getting Started=>Install the Plugin**.
    
3. Scroll down to the **Install the Plugin** section. 

4. Click **Download plugin** and store the file in a memorable location. Don't unzip the file.

5. Now, navigate to your IntelliJ instance. 

6. From IntelliJ, navigate to **Preferences** (on Mac OS) or **Settings** (On Windows/Linux):

    ![IntelliJ Preferences Menu on Mac OS](../assets/images/intellij-preferences-mac.png)

7. Go to the **Plugins** section:
   
    ![The plugins section](../assets/images/plugins-section.png)
   
8. Click the settings cog from the top right and select **Install Plugin from Disk**:

    ![Install Plugin from Disk](../assets/images/install-plugin.png)

9. Select the plugin zip file from the folder where you stored it in **step 3**.
   
    Once installed, Lightrun options appear in the **Settings** menu. 
   
    **Plugins**:
	
	![Plugin Settings -three](../assets/images/intellijSettings.png)
	
	**Lightrun settings**:
	
	![Lightrun Settings -three](../assets/images/intellijSettings2.png)
    
    You can configure these settings as follows:
    
    * Lightrun Server URL - this is the URL to the Management server installed on premises;      
    
    * Source Version Warnings - we alert you if the code in the IDE doesn't match the code that is running alongside our agent
    
    * Use Embedded Browser - this enables login and authentication directly from the IDE; if disabled, when logging in you are redirected to your default browser

  !!! note
        The **Use an embedded browser** option uses such a browser for logging-in to the Lightrun server. If you are using the external browser but authentication fails, activate this option explicitly and update your IDE to 2020.2 or newer.
    
    * Certificate Pinning - verifies the server certificate matches your requests and that you are actually connecting to the Lightrun server; this feature enforces security and is highly recommended
    

10. When prompted, restart IntelliJ.

    Lightrun appears in the right-hand sidebar. 

!!! faq "What's next?"
     Once you're finished setting up, [authenticate](../authenticate-plugin.md) the plugin or [install and authenticate](../cli.md) the CLI and you can start debugging!