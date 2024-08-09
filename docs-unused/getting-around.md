
# JetBrains Plugin Quick Tour

<iframe width="560" height="315" src="https://www.youtube.com/embed/iesDKHbijZ8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The majority of the work you do with Lightrun, including troubleshooting, debugging, performance testing, and the like, is performed directly from either your IDE or the [Lightrun CLI](/cli/cli_reference/). When working from the IDE plugin, you can add Lightrun actions (logs, metrics, snapshots) to the relevant code line in the source code of your live app and then view the relevant output as well.

The remainder of this article describes:

- [The layout of Lightrun in IntelliJ](#layout)

- [How to search and filter dynamic logs and metrics](#search)

- [The Agents and Tags lists and their icons](#agents)

- [The Details window](#details) for additional action and agent details

## The plugin layout {#layout}

--8<-- "ux-reference/plugin-intellij-prereq.md"

Lightrun is part of the IntelliJ right-hand sidebar, and appears similarly to the following: 

![The Lightrun sidebar -quarter](assets/images/drawer.png)

 This sidebar displays all the running agents and their tags, as well as the actions that have been attached to them.

!!! note
     If these lists are completely empty or if you can only see a list of tags but not agents, the agents might all be down. Contact your manager for assistance.


This sidebar has two tabs: 

- **Agents** - lists all running agents and the dynamic logs you've attached to them from IntelliJ; this area of the sidebar is divided into [Tags](#tags) and [Agents](#agents)

    ![Agents and Tags -quarter](assets/images/agents-tags-exceptions.png)

- **Exceptions** - lists exceptions logged on running agents

Additionally, you can view dynamic logs in real time directly from the [Lightrun Console](#piping), located in the bottom sidebar.

## Search (filter) {#search}

From the dynamic search field, you can search for dynamic logs and snapshots from within specific agents. As you start typing, the list of agents updates dynamically.

![Login Dialog -quarter](assets/images/search.gif)

!!! tip
    This can be particularly helpful in finding specific dynamic logs when working with multiple agents.
	
## Agents and Tags list {#agents}

The **Tags** list appears similar to the following: 

![The Tags list -half](assets/images/tags.png)

The layout of the **Agents** list appears similar to the following:

![The Agents List -half](assets/images/agents.pn.png)

The panel at the top of each list contains the following information:

- An arrow to expand and collapse the list per tag or per agent.

- The name of the agent or list 

- In parenthesis, the total number of actions assigned to that tag or agent

- For Tags lists, the ![Status -icon](assets/images/i-tag.png) icon

- For Agents lists, the icons as described below

Most of the icons are relevant for both the **Agents** and the **Tags** lists:

![Agent Details -half](assets/images/agent-annotated.png)


The following table describes the actions you can leverage from both:

|      | Icon                                                         | Component           | Description                                                  |
| ---- | ------------------------------------------------------------ | ------------------- | ------------------------------------------------------------ |
| 1    | ![View details -icon](assets/images/i-details.png)           | [Details](#details) | Opens the information dialog box for the agent, the tag or for the action    |
| 2    | ![View/hide dynamic logs -icon](assets/images/i-eye.png)             | View/hide dynamic logs      | Toggle this button to hide/show dynamic logs in the editor. This applies to the hierarchy and can be toggled globally on the login button. |
| 3    | ![Pipe dynamic logs -icon](assets/images/i-pipe.png)                 | Pipe dynamic logs           | From the Agents list only, by default Lightrun dynamic logs print into the same logger that is used by your application. Following are the three options: `App Only` (the default), `Plugin Only` and `Both`. When set to `Plugin Only` or `Both` dynamic logs added to this agent also appear in the [Lightrun console](plugin.md#piping) of IntelliJ. |
| 4    | ![Delete -icon](assets/images/i-delete.png)                  | Delete action       | Delete any agent or tag actions. Only agent-activated actions can be deleted from the Agents list and tag-activated actions from the Tags list. |
| 5    | ![Go to line -icon](assets/images/i-goto.png)                | Go to line          | Jump to the source file and line number in the code that is associated with the action. |
| 6    | ![Status -icon](assets/images/i-toggle.png)                  | Toggle              | Toggle to disable or enable an action. Only agent-activated actions can be toggled from the Agents list and tag-activated actions from the Tags list. |
| 7    | ![Status -icon](assets/images/i-status.png)![Status -icon](assets/images/i-tag.png) | Status indicator    | Displays the current state of the action. One checks indicates the action was submitted to the server. Two checks indicate that it was received by the agent. Highlighted checks indicate that the agent accepted the action. From the Agents list, the tag icon indicates the action was activated with tags and not agents, and its status can be viewed from the Tags list. |
| 8    | ![Log level -icon](assets/images/i-loglevel.png)             | Log level indicator | Indicates the the level that was configured for the log (on log rows only): Info, Debug, Warn, Error. |

## Agent and Lightrun action details {#details}

To view details, click ![View details -icon](assets/images/i-details.png) from the relevant row. 

The **Details** dialog window pops up. 

For actions, the window appears similar to the following: 

![View action details -third](assets/images/details-action.png) 

The following table describes the information displayed in this window:

| Field           | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| ID              | The system-generated ID associated with this action item.    |
| Name            | The name assigned to the action when it was added.           |
| Type            | The type of action.                                          |
| Start Location  | The file and code line where the action starts following behavior. |
| End Location    | The file and code line where the action stops following behavior. |
| Create Time     | The time and day on which the action was created.            |
| Owner           | The user who created the action.                             |
| Quota in effect | The quota controls use of CPU, Networking, Memory, excessively long strings, too many instructions printing out, protection from infinite loops and the like. <br/>     Quota settings can be tuned in the agent.config file. |
| Log Message     | The message resulting from the action appears here, if relevant. |
| Error Message   | If any agent reports any errors for this action, they are documented here. |

For agents, the **Details** appear similar to the following, including details about location, versioning, associated tags and the piping mode:

![View agent details -third](assets/images/details-agents.png) 

The information in the agent **Details** window is as described in the following table: 

| Field         | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| Host          | The name of the machine where the agent is runnning.         |
| ID            | The unique identification number automatically generated for the action. |
| PID           | The process ID (for the machine where the agent is running). |
| Start Time    | The time at which the agent started running.                 |
| API Version   | The version of the API used by the agent.                    |
| Agent Version | The version of the agent.                                    |
| Piping Mode   | The configured [piping](#piping) method.    |
| Tags          | All tags that have been applied to this agent.               |

!!! note
     Read more about how to [view dynamic logs](logs.md), [metrics](metrics.md), and [the stacktrace](snapshots-plugin.md) based on the instrumentation you added. 

