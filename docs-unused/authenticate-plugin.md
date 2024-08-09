## Authenticate the Plugin

On each occasion you start to work with Lightrun from your IDE, you must first authenticate with your Lightrun account.

!!! reqs "Prerequisites"
    These instructions assume that you have:

    - [Created your Lightrun Account](create-account.md)

    - [Installed the Lightrun Jetbrains plugin](plugin.md) in your IDE.


###### To authenticate Lightrun from the IDE

1. From your IDE, click the Lightrun tab to expand the sidebar. 
   
    ![Login from IntelliJ -quarter](assets/images/intellij-disconnected.png)

2. Click the red banner from the top of the plugin display. 
	
	The browser opens to the Lightrun login page:
	
	![Login Dialog -quarter](assets/images/login-dialog.png)
    
  !!! note
        The display might appear differently, with the **Login** and **Register** options appearing as buttons in the center of the Lightrun pane, similarly to the following:
        ![Login Dialog -ten](assets/images/login2.png)
        In this case, click the relevant option to authenticate.
	
3. Log in to Lightrun with your user credentials. 

    Once you're logged in, the Lightrun page reloads with a confirmation message. Notice that there's a timeout configured; you might need to re-login if the timeout elapses.

4. Go back to your IDE.
    
	The Lightrun banner in the sidebar now appears green:
    
	![Status Button -third](assets/images/login-success.png)
	
  !!! imp "Important"
      If you authenticate Lightrun successfully, but relevant options are hidden, this means no agents are connected on the server where the application is running.
		
	The contextual Lightrun menu in your IDE displays relevant options:
    
	![Right Click Context Menu -third](assets/images/context-menu.png)
	
    And the Lightrun quick menu appears on your tool bar: 
	

	![IntelliJ Quick Menu -third](assets/images/intellij-quick-menu.png)

______________

Watch this video to get up and running: 


<iframe src="https://player.vimeo.com/video/538588632" width="400" height="250" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen></iframe>
<p><a href="https://vimeo.com/538588632">Lightrun - Getting started from IntelliJ</a> from <a href="https://vimeo.com/user118141507">Lightrun</a> on <a href="https://vimeo.com">Vimeo</a>.</p>