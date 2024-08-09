

--8<-- "ux-reference/index.md"


Read more about: 

- [Lightrun architecture](#architecture)
- [How it works](#how)



## Lightrun architecture {#architecture}

Lightrun comprises these parts:

- **Management Server** -  this is the Lightrun server, responsible for service management; this is the fundamental "backbone" of the platform. For on-prem deployments, our Lightrun team schedules a time that's suitable for your team and comes to help set up this server on your site.  

- **Java Agent** - the JVMTI agent that runs alongside the application to be observed; this agent dynamically inserts the logs, metrics and snapshots in the code based on the Lightrun actions you run.

- **Client** - the IDE plugin and command line utility; you can use either of these in order to add, remove and modify actions - whichever is part of your natural workflow. Whenever you run a command to insert an action, the agent receives your request and adds those actions accordingly.

These three components communicate with one another as illustrated in the following diagram: 

![Lightrun architecture -three](../assets/images/diagram.png) 

## How it works {#how} 

Using **Lightrun actions** from your IDE, Lightrun enables you to add logs, metrics and more on-the-fly directly in to your already-compiled source code for the live application - in any environment.  

Whenever you send a Lightrun action to be added, the inserted code is run in a dedicated sandbox before being added to your application. The Lightrun Sandbox validates there are no side effects to your application’s behavior, and it verifies integrity, stability and security of the instrumentation. Lightrun Sandbox guarantees no exceptions, system I/O, system calls or state/flow changes, and only read-only code is ever added to your running application.

Once you've added the action, you can immediately view the output directly from the IDE as well, or from the Web Console in any browser.

###### This is how it works: 

1. With the help of the Lightrun team, set up and [configure](install.md) the Management server.
    
2. [Configure](install.md) the agent. The stateless Lightrun agent is the heart of the Lightrun product.  

3. Optionally, [customize](../exceptions/configure.md) agent configuration, such as to enable exceptions to be handled through Lightrun as well.

4. Add the agent to the running application. This small library then connects to the Lightrun Management Server, managing communications with the IDE plugin, with the Management Server and with your application through HTTPS.  

5. [Install](install-client.md) the plugin and authenticate it.

6. [Add](../actions.md) Lightrun actions into the relevant lines of code, on-the-fly. Lightrun actions include: 

    - Logs 
    - Metrics 
    - Snapshots - virtual breakpoints that don't stop the app
    
7. When user actions are received, the Lightrun Management Server sends the request to the agent. The agent checks the requested actions through our proprietary sandbox, and once integrity, stability and security are verified, it adds instrumentation to your application during runtime, immediately. 

8. [View the output](../plugin.md#piping) and [exceptions](../exceptions/ide.md) directly from the IDE - or from our app in the browser.




Watch this video for more information: 


<iframe src="https://player.vimeo.com/video/431163367" width="640" height="360" frameborder="0" class="vimeo_edit" allow="autoplay; fullscreen" allowfullscreen></iframe></p>
