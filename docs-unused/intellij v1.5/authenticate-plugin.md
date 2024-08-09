# Authenticate Lightrun

To start using Lightrun in your Jetbrains IDE, you must first authenticate your Jetbrains Plugin.

!!! reqs "Prerequisites"
    These instructions assume that you have:

    - [Created your Lightrun Account](create-account.md)

    - [Installed the Lightrun Jetbrains plugin](plugin.md) in your IDE.

!!! imp "Important"
	Please note that you still have to install a Lightrun agent in your app to use Lightrun in your IDE.

	- Follow the instructions [here](/jvm/agent/) to set up a Lightrun agent in your Java application.

	- Follow the instructions [here](/python/agent/) to set up a Lightrun agent in your Python application.

	- Follow the instructions [here](/node/agent/) to set up a Lightrun agent in your Node.js application.


###### To authenticate lightrun from your IDE

1. From your Jetbrains IDE, click the Lightrun tab on the top right-hand corner of your IDE to display the Lightrun sidebar.
	![Status Button -third](assets/images/intellij-disconnected0.png)
2. Click the red banner on top of the Lightrun sidebar. Your browser will open automatically to the Lightrun login page.
3. Login to Lightrun with your credentials to authenticate your Jetbrains plugin.
	A confirmation message will be displayed on successful authentication.
4. Go back to your IDE. The top red banner should turn green if the plugin authentication is successful.

	![Status Button -third](assets/images/intellij-connected.png)

!!! note
	- Please note that there's a timeout configured in the authentication process, and you might need to re-login if the timeout elapses.
	![Status Button -third](assets/images/intellij-countdown.png)

	- The Lightrun sidebar display might appear differently, with the **Login** and **Sign Up** options appearing as buttons in the center of the Lightrun pane, similarly to the following:
	![Login Dialog -third](assets/images/login3.png)
	In this case, click **Login** to authenticate your plugin, or click **Sign Up** to create a free Lightrun account.

______________

Watch this video to get up and running: 


<iframe src="https://player.vimeo.com/video/538588632" width="400" height="250" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen></iframe>
<p><a href="https://vimeo.com/538588632">Lightrun - Getting started from IntelliJ</a> from <a href="https://vimeo.com/user118141507">Lightrun</a> on <a href="https://vimeo.com">Vimeo</a>.</p>