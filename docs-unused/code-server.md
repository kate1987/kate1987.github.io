# Lightrun for `code-server`

Lightrun now provides a free, easy-to-install plugin for [code-server](https://github.com/coder/code-server) - an open-source version of VS Code suitable for self-hosting and embedding in 3rd party applications. 

Lightrun's code-server plugin is compatible with the Lightrun desktop plugin version, with a few minor limitations listed [below](#limitations).

## Installing Lightrun for `code-server`

* First download, install and run `code-server` using the following command :

```bash
curl -fsSL https://code-server.dev/install.sh | sh
```

* Run `code-server`:

```bash
code-server
```

* Open [http://localhost:8080](http://localhost:8080). You will be prompted to enter a password:

  <figure>
      <img src="/assets/images/vscode/code-server-password.png" align="center" alt="code-server Password Screen" />
      <figcaption>code-server Password Screen</figcaption>
  </figure>

1. The password can be found in `~/.config/code-server/config.yaml`. Run the following command to get the password, then copy it into the browser window:

```bash
cat ~/.config/code-server/config.yaml | grep 'password:' | cut -d" " -f2
```

* When VS Code opens, select **Extensions** in the left sidebar:

  <figure>
      <img src="/assets/images/vscode/code-server-extensions.png" align="center" alt="Open The Extension Sidebar" />
      <figcaption>Open The Extension Sidebar</figcaption>
  </figure>

  !!! tip

      Alternatively, to open the **EXTENSIONS** sidebar, use the keyboard shortcut:
        
      - Ctrl+Shift+X (MS Windows and Linux)
      - Cmd+Shift+X (MacOS)

* Search for "Lightrun" in the input box and click Install:

  <figure>
      <img src="/assets/images/vscode/code-server-install-lightrun.png" align="center" alt="Install Lightrun"/>
      <figcaption>Install Lightrun</figcaption>
  </figure>

* Once installed, The Lightrun plugin icon ![Lightun VSCode plugin icon](../assets/images/vscode/vscode-plugin-icon.png) will appear in your VS Code left sidebar - click it to open Lightrun Sidebar:

  <figure>
      <img src="/assets/images/vscode/code-server-open-sidebar.png" align="center" alt="Open Lightrun Sidebar" />
      <figcaption>Open Lightrun Sidebar</figcaption>
  </figure>

* Click "Sign In" to authenticate to the plugin:

  <figure>
      <img src="/assets/images/vscode/code-server-sign-into-plugin.png" align="center" alt="Sign in to Lightrun" />
      <figcaption>Sign in to Lightrun</figcaption>
  </figure>

* If you have a Lightrun account with us simply sign in to it. If you don't have an account, create one:
  
  <figure>
      <img src="/assets/images/web-ides-register.png" align="center" alt="Lightrun Registration Screen" />
      <figcaption>Lightrun Registration Screen</figcaption>
  </figure>

* After logging in or signing up, in the first onboarding page, choose "Other IDE" and your language of choice:

  <figure>
      <img src="/assets/images/vscode/code-server-ide-selection.png" align="center" alt="Select IDE and Language" />
      <figcaption>Select IDE and Language</figcaption>
  </figure>

From there, depending on the language you choose, you will be directed to install the relevant Lightrun agent. Please see below for detailed instructions for each supported runtime:

* [JVM (Java, Scala & Kotlin)](../jvm/agent.md)
* [Node.js (JavaScript & TypeScript)](../node/agent.md)
* [Python](../python/agent.md)
## Lightrun for vscode.dev

For some developers, self-hosting VS Code is not something that they'd be interested to take on. For these developers - who still want the creature comforts VS Code provides without having to actually host it themselves, there is the option of using a Microsoft-hosted, web-based version of VS Code called [vscode.dev](https://vscode.dev).

Lightrun supports vscode.dev out of the box - see installation instructione [here](vscode-dev.md).
## Limitations

Since Lightrun for `code-server` runs completely within your browser, there are some limitations when compared to using Lightrun directly in your IDE.

* The [snapshot import and export feature](/vscode/vscode-plugin-snapshots/#exporting-snapshot-data) is currently not available in the VSCode.dev plugin.
* The [Log collector feature](/data-logs/) is currently not available in the VSCode.dev plugin.
