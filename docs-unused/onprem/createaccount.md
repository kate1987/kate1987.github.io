# Create your account

Once Lightrun has set the Management server up for you in your private network, you can create a user for yourself and get started setting things up. When you do this, you are automatically assigned a Manager role. Once you access your new account, you can send invitations to others by email. 


Lightrun defaults to port 8080 and requires HTTPS. 


1. Log in to your Lightrun instance with your admin credentials at <https://192.168.1.108:8080/>. 

    !!! note 
        1. Be sure to change the port number if you changed the configuration from your docker-compose file.
        2. SSL certificates can be applied to domains only. Therefore, the page loads with an HTTPS warning.

2. Add an exception for this URL to any relevant firewall configurations, in order to bypass the certificate warning that loads. 
   The landing page loads with *customized* installation instructions for the agent, plugin and CLI.

3. Complete the fields with your personal details. Choose a strong password that includes at least one lower case and upper case letter, one special character and one number. Alternatively, click **Sign up with Google** to use your Google address for quick registration.

    ![Register your account -quarter](../assets/images/register-user.png) 
    

4. Check the reCAPTCHA box and then click **Register**.

    You are redirected to our onboarding wizard. 

5. From the left panel, click the operating system of the environment in which you'll run the Web Console for relevant agent installation instructions.
        
    Once you've installed the agent, the **Next** button appears:
    
    ![Register your account -quarter](../assets/images/onboard-agent-wizard.png)
    

  !!! imp "Important"
      You must install the agent before proceeding to step 6. If you log out without installing the agent, when you log back in you will be redirected to the onboarding wizard again.
      
  !!! tip
      Once you've installed the agent, when you log in the next time, you're redirected to the app. If you still need help with onboarding, go to the **Getting started** menu.
    
6. Click **Next**.

    Install the plugin for your IDE or click **Next** to go to the Web Console and install the plugin later.
    
    ![Register your account -quarter](../assets/images/getting-started-menu.png) 
    



        
