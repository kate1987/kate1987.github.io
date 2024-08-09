# Install the Lightrun plugin in your JetBrains IDE

To use Lightrun from your IDE, you must first install the Lightrun IDE plugin.

--8<-- "ux-reference/support-plugin.md"

!!! reqs "Version Support"
    The instructions below apply to JetBrains IDEs (IntelliJ IDEA, WebStorm, and PyCharm) v2022.3.0 and later. Follow the instructions [here](https://www.jetbrains.com/help/idea/update.html#toolbox) to update your JetBrains IDE.

Lightrun supports the following installer types to cater for the different deployment environments. When you access the Management Portal, the appropriate installer type for your specific deployment is automatically displayed.

- [JetBrains plugin marketplace](#installing-the-lightrun-plugin-from-the-jetbrains-plugin-marketplace) - For SaaS customers.
- [Manual Installation](#installing-the-lightrun-plugin-manually) -  For SaaS, On-prem, and Single-tenant customers.
- [Custom Plugin repository](#installing-the-lightrun-plugin-from-a-custom-plugin-repository) - For On-prem and Single-tenant customers.

!!! tip "How can I detect my deployment environment?"

    - If your lightrun account is at a URL that starts with [https://app.lightrun.com](https://app.lightrun.com), then you're on Lightrun’s SaaS offering, and should follow the instructions under ["Installing the Lightrun plugin from the JetBrains Plugin Marketplace"](#installing-the-lightrun-plugin-from-the-jetbrains-plugin-marketplace).
    - If your account's URL doesn't start with [https://app.lightrun.com](https://app.lightrun.com), then see if your server offers a custom plugin repository. If it does, this will make future upgrades simpler, so we recommend you follow the instructions under ["Installing the Lightrun plugin from a custom plugin repository"](#installing-the-lightrun-plugin-from-a-custom-plugin-repository).
    - If your server doesn't offer a custom repository, follow the steps [to install the plugin manually](#installing-the-lightrun-plugin-from-a-custom-plugin-repository).


## Installing the Lightrun plugin from the JetBrains Plugin Marketplace

1. Navigate to **Preferences** (Mac OS) or **Settings** (Windows/Linux) in your JetBrains IDE.

  ![JetBrains IDE Preferences](/assets/images/intellij-preferences-mac.png)

2. Go to the **Plugins** section and select the **Marketplace** tab. Search for Lightrun and click **Install**:
  ![Install Plugin from Marketplace --half](https://res.cloudinary.com/lightrun/image/upload/v1627329656/docs/Install-plugin-from-marketplace.png)

3. When prompted, restart the IDE. After the restart, Lightrun will appear in the right-hand sidebar and you can log into it by clicking the **Login** button.
  ![Lightrun In Your IDE --half](/assets/images/jvm-ide-sidebar.png)

4. Once logged in, you can move on to the final step - running the **Lightrun Agent** with your application:

    - [Java agent](jvm/agent.md){:target="_blank"}

    - [Python agent](python/agent.md){:target="_blank"}

    - [Node.js agent](node/agent.md){:target="_blank"}

    - [.NET agent](dotnet/agent.md){:target="_blank"}



## Installing the Lightrun plugin manually

**To install the Lightrun plugin manually:**

1. Open a browser and log in to your Lightrun account.
2. Navigate to **Install the Plugin in your IDE** > **JetBrains IDE**(**IntelliJ IDEA**, **PyCharm**, **Rider**, or **WebStorm**) > **Manual Installation**.
    ![Manual installation -half](/assets/images/jetbrains-manual-installation.png)

3. Click **Download the plugin** to download the Lightrun plugin `.zip` file.

  !!!note
      Do not unzip the downloaded file.

4. Navigate to Preferences (Mac OS) or Settings (Windows/Linux) in your JetBrains IDE.
    ![JetBrains IDE Preferences](/assets/images/intellij-preferences-mac.png)

5. Go to the **Plugins** section and click the cog icon ![cog icon --icon](/assets/images/jetbrains-cog-icon.png).
6. In the menu that opens, click **Install Plugin from Disk**, then select the `.zip` file that was downloaded in the first step.
    ![Install Plugin from disk --third](/assets/images/install-plugin-from-disk.png)

7. In the window that opens, click on **Restart IDE** and wait for the changes to take effect.
8. After the IDE restarts, authenticate your plugin by clicking the **Login** or **Register** button in the plugin tool window.

## Installing the Lightrun plugin from a custom plugin repository

!!! reqs "Requirements"
    This installation option is only available to our single tenant and on-premise customers. For more information, please reach out to our [support team](https://go.lightrun.com/contact-us).

**To install the Lightrun plugin from a custom plugin repository:**

1. Open a browser and log in to your Lightrun account.
2. Navigate to **Install the Plugin in your IDE** > **JetBrains IDE**(**IntelliJ IDEA**, **PyCharm**, **Rider**, or **WebStorm**) > **Custom repository Installation**.
3. Copy the custom repository URL.
    ![Custom Repository -half](/assets/images/jetbrains-custom-repository-url.png)

4. Navigate to **Preferences** (on Mac OS) or **Settings** (on Windows/Linux) in your JetBrains IDE.
  ![JetBrains IDE Preferences](/assets/images/intellij-preferences-mac.png)

5. Go to the **Plugins** section and click the cog icon ![cog icon --icon](/assets/images/jetbrains-cog-icon.png).
6. In the menu that opens, click **Manage Plugin Repositories...** to open the **Custom Plugin Repositories** dialog.
    ![Manage plugin repositoryes --third](/assets/images/manage-plugin-repositories.png)

7. Click **+** in the **Custom Plugin Repositories** dialog and add the copied repository URL.
8. Click **OK** in the **Custom Plugin Repositories** dialog to save the plugin repository.
9. Click **OK** in the **Settings** dialog to apply the change.
10. Go back to the **Plugins** section and select the **Marketplace** tab.
11. Search for Lightrun and click **Install** on the result which includes your organization's name.
    ![Custom plugin repository --half](/assets/images/custom-repository.png)

12. In the window that opens, click on **Restart IDE** and wait for the changes to take effect.
13. After the IDE restarts, authenticate your plugin by clicking the **Login** or **Register** button in the plugin tool window.