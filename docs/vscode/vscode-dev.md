# Lightrun for vscode.dev

Lightrun offers a free, easy-to-install plugin for VSCode for the web ([vscode.dev](https://vscode.dev/)). Lightrun's VSCode.dev plugin is compatiable with the Lightrun desktop plugin version, with a few minor limitations.

## Installing Lightrun for VSCode.dev

VSCode.dev does not require authentication or any additional downloads to function.

1. Go to [vscode.dev](https://vscode.dev/) in your browser.

2. Select **Extensions** in the left sidebar.
  
  !!! tip

      Alternatively, to open the **EXTENSIONS** sidebar, use the keyboard shortcuts:
        
      - **Ctrl+Shift+X** (MS Windows and Linux)
      - **Cmd+Shift+X** (MacOS)

  ![Open The Extension Sidebar --half](/assets/images/vscode/vscode-dev-get-started.png)

3. Search for **Lightrun** in the input box and click **Install**.

    ![Install Lightrun --half](/assets/images/vscode/vscode-dev-install-lightrun.png)


  Once installed, The Lightrun plugin icon ![Lightun VSCode plugin icon](../assets/images/vscode/vscode-plugin-icon.png) will appear in your VSCode left sidebar 
  
4. Click to open the Lightrun sidebar.

    ![Open Lightrun Sidebar --half](/assets/images/vscode/vscode-dev-lightrun-sidebar-icon.png)

5. Click **Sign In** to authenticate to the plugin.

    ![Sign in to Lightrun --half](/assets/images/vscode/vscode-dev-sign-in.png)
      

1. After logging in or signing up, in the first onboarding page, choose **vscode.dev** and your language of choice:
 
    ![Select IDE and Language --half](/assets/images/vscode/vscode-dev-ide-selection.png) 
  
2. Depending on the language you choose, you will be directed to install the relevant Lightrun agent.    Please see below for detailed instructions for each supported runtime:

   - [JVM (Java, Scala & Kotlin)](../jvm/agent.md)
   - [Node.js (JavaScript & TypeScript)](../node/agent.md)
   - [Python](../python/agent.md)

## Known limitations

Given that Lightrun for VSCode.dev operates entirely within your browser, it's subject to certain limitations when compared to the full-fledged Lightrun experience directly integrated into your IDE. The following features are not supported:

- [snapshot import and export](/vscode/vscode-plugin-snapshots/#exporting-snapshot-data)
- [Log collector](/data-logs/)
- Certificate Pinning for websockets