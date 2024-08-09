# Setting up the agent

To enable developers to insert instrumentation on the fly, you need to download and attach the agent to a running application.

###### Set up the agent


1. From the server where your application is running, log in to Lightrun from the browser. 


2. Navigate to **Getting started=>Install the agent**.

    ![Install the agent -half](../assets/images/install-agent.png)

3. From the **Install the Agent** section, select the tab for the operating system installed on your server.

4. Copy and run the script. The script on this page already includes your `server IP` and `port` values, similar to this:

     <iframe src="https://player.vimeo.com/video/542166389?title=0&amp;byline=0&amp;portrait=0&amp;speed=0&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=56727" width="400" height="300" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen title="Download the agent"></iframe>
     


5. Once you've downloaded the agent, optionally [customize the agent configurations](../agentadmin-agentprops.md).


  !!! tip
       You can customize agent configurations any time you want. Check out the content of the file `agent/agent.config`. To apply any changes, restart the agent as described in the next step.

###### Attaching the agent to your application

  1. From the server where your application is running, open a terminal and navigate to your application's folder.

  2. From the browser, copy the command, replace `RestofArgumentsHere` with the name of your application and any other [relevant options](../agentadmin-agentprops.md), and follow the instructions to run it; similar to this GIF:
  
       <iframe src="https://player.vimeo.com/video/542152672?title=0&amp;byline=0&amp;portrait=0&amp;speed=0&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=56727" width="400" height="300" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen title="Add Agent to Application"></iframe>
       
       !!! tip
            Optionally, add the `JAVA_OPTS` environment variable to the server so that all Java processes launched on that server have an agent attached. Copy the following command from the server and replace the `agentpath` value with the path to the Lightrun agent where you downloaded it:
            ```
            export JAVA_OPTS=-agentpath:/path/to/agent/lightrun_agent.so
            ```

  3. [Install the CLI](../cli.md) and validate that the agent registered correctly by running `lightrunc list-agents`. Assuming the agent is running, something similar to the following should print in the terminal: 

       ```
       0 : ID 5c84e29871f7a700010ca737UPDATE Sun, 10 Mar 2019 10:10:32 GMT
       ```
