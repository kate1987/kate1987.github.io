# Lightrun for JetBrains Projector

Lightrun now provides a free, easy-to-install plugin for [JetBrains Projector](https://lp.jetbrains.com/projector/) - a self-hosted technology that runs IntelliJ-based IDEs and Swing-based apps on the server, allowing you access to them from anywhere using the browser. 

Our JetBrains projector plugin is compatiable with the Lightrun Desktop plugin version, with a few minor limitations listed [below](#limitations).

## Installing Lightrun for JetBrains Projector

* First run a [JetBrains Projector container](https://github.com/JetBrains/projector-docker) locally with the Community version of IntelliJ IDEA (you can also use ):
[the native installer instead]((https://github.com/JetBrains/projector-installer))

```bash
docker run --rm -p 8887:8887 -v ~/projector-docker:/home/projector-user  -it jetbrains/projector-idea-c
```

!!! note Docker Volume Required
    The addition of the volume in `~/projector-docker` is done in order to allow the Lightrun plugin to persist state; without it, the plugin will not work between restarts.

* Once the container is running, visit [http://localhost:8887](http://localhost:8887), accept the terms and conditions (and accept / deny the data sharing request) then make sure you see the following screen:

  <figure>
      <img src="/assets/images/jetbrains-projector/jetbrains-projector-welcome-screen.png" align="center" />
      <figcaption>IntelliJ on JetBrains Projector</figcaption>
  </figure>

* Once there, select **Plugins** in the left sidebar, search for "Lightrun" then install it:

  <figure>
      <img src="/assets/images/jetbrains-projector/jetbrains-projector-install-lightrun.png" align="center" />
      <figcaption>Install Lightrun</figcaption>
  </figure>


* Once installed, click "Restart IDE":

  <figure>
      <img src="/assets/images/jetbrains-projector/jetbrains-projector-restart-ide.png" align="center" />
      <figcaption>Restart the IDE</figcaption>
  </figure>

* The IDE will now restart, and you will need to stop the container and start it from scratch. Remember the volume we added to the container earlier? That volume persists state between container restarts, so your plugin will be installed on the next launch. To kill the container, either exit the terminal window or click CTRL + C to kill the process. Then, run the container again:

```bash
docker run --rm -p 8887:8887 -v ~/projector-docker:/home/projector-user  -it jetbrains/projector-idea-c
```

* When the container restarts, go back to the browser window and click on "reconnect":

 <figure>
      <img src="/assets/images/jetbrains-projector/jetbrains-projector-reconnect.png" align="center" />
      <figcaption>Reconnect to Projector</figcaption>
  </figure>

* Wait for the IntelliJ window to reappear, then choose any project from your system to open the editor view:
  
  <figure>
      <img src="/assets/images/jetbrains-projector/jetbrains-projector-choose-project.png" align="center" />
      <figcaption>Open a Project</figcaption>
  </figure>


* You can choose any folder inside the container, but `projector-user` is a good choice if you're not sure what to pick. 

  <figure>
      <img src="/assets/images/jetbrains-projector/jetbrains-projector-projector-user-project.png" align="center" />
      <figcaption>Choose Project</figcaption>
  </figure>

* Once you choose a folder, also click "Trust Project" in the next window:

  <figure>
      <img src="/assets/images/jetbrains-projector/jetbrains-projector-trust-project.png" align="center" />
      <figcaption>Trust Project</figcaption>
  </figure>

* Once the editor loads, click on the Lightrun tab on the left side:

  <figure>
      <img src="/assets/images/jetbrains-projector/jetbrains-projector-open-lightrun-sidebar.png" align="center" />
      <figcaption>Trust Project</figcaption>
  </figure>


* Then click "Login" in the Lightrun sidebar:
  <figure>
      <img src="/assets/images/jetbrains-projector/jetbrains-projector-login-plugin.png" align="center" />
      <figcaption>Trust Project</figcaption>
  </figure>

* If you have a Lightrun account with us simply sign in to it. If you don't have an account, create one:
  
  <figure>
      <img src="/assets/images/web-ides-register.png" align="center" />
      <figcaption>Lightrun Registration Screen</figcaption>
  </figure>

* After logging in or signing up, in the first onboarding page, choose "IntelliJ" and your language of choice:

  <figure>
      <img src="/assets/images/jetbrains-projector/jetbrains-projector-choose-ide-language.png" align="center" />
      <figcaption>Select IDE and Language</figcaption>
  </figure>

From there, depending on the language you choose, you will be directed to install the relevant Lightrun agent. Please see below for detailed instructions for each supported runtime:

* [JVM (Java, Scala & Kotlin)](../jvm/agent.md)
* [Node.js (JavaScript & TypeScript)](../node/agent.md)
* [Python](../python/agent.md)
