# Jetbrains Plugin Quick Tour

<iframe width="560" height="315" src="https://www.youtube.com/embed/iesDKHbijZ8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The majority of the work you do with Lightrun, including troubleshooting, debugging, performance testing, and the like, is performed directly from either your IDE or the [Lightrun CLI](cli.md). When working from the IDE plugin, you can add Lightrun actions (logs, metrics, snapshots) to the relevant code line in the source code of your live app and then view the relevant output as well.

## The plugin layout {#layout}

--8<-- "ux-reference/plugin-intellij-prereq.md"

Lightrun is part of the IntelliJ right-hand sidebar, and appears similarly to the following: 

![The Lightrun sidebar -third](assets/images/intellij-new.png)

The Lightrun sidebar has two tabs: 

- [**Agents**](#agents)
- [**Tags**](#tags)

!!! note
     Please note that the **Agent** and **Tag** tabs display only actively running agents and tags in your IDE. If both tabs are empty or only the agent tab is empty, please contact your manager for assistance.

## Agents tab {#agents}

The Agents tab displays a list of all active agents currently attached to your Jetbrains IDE and all the actions associated with each agent. You can search for agents, view and configure agent details, view action details or delete actions, and configure agent output piping in the Agents tab. 

###### To search for an agent
1. Enter the agent's name or PID value into the search bar.
2. Click the Search button. 
	
	The agent lists should appear similar to the following image 
	![The Lightrun sidebar -half](assets/images/intellij-agent1.png)

3. Click the drop-left icon ![Drop left -icon](assets/images/drop-left.png) on the left-hand side of an agent to display a list of all actions associated with that agent.
	![The Lightrun sidebar -half](assets/images/intellij-agents2.png)

The following table describes the icons present in the agents and action lists and the functions of each icon.

|      | Icon                                                         | Function                                                  |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1    | ![View details -icon](assets/images/i-details.png)           | Opens the information dialog box for the agent, tag, or action  |
| 2    | ![View/hide dynamic logs -icon](assets/images/i-eye.png)             | Toggle this button to hide/show dynamic logs in the editor. This applies to the hierarchy and can be toggled globally on the login button. |
| 3    | ![Pipe dynamic logs -icon](assets/images/i-pipe.png)                 | Use this icon to configure an agent output piping. See [Viewing action output](#piping) for more details.  |
| 4    | ![Delete -icon](assets/images/i-delete.png)                  | Delete agent or tag actions. Only agent-activated actions can be deleted from the Agents list and tag-activated actions from the Tags list. |
| 5    | ![Go to line -icon](assets/images/i-goto.png)                | Jump to the source file and line number in the code that is associated with the action. |
| 6    | ![Status -icon](assets/images/i-toggle.png)                  | Toggle to disable or enable an action. Only agent-activated actions can be toggled from the Agents list and tag-activated actions from the Tags list. |
| 7    | ![Status -icon](assets/images/i-status.png)![Status -icon](assets/images/i-tag.png) | Displays the current state of the action.<br/>- One checks indicates the action was submitted to the server.<br/>- Two checks indicate that it was received by the agent.<br/>- Highlighted checks indicate that the agent accepted the action.<br/>From the Agents list, the tag icon indicates the action was activated with tags and not agents, and its status can be viewed from the Tags list. |
| 8    | ![Log level -icon](assets/images/i-loglevel.png)         | Indicates the the level that was configured for the log (on log rows only): Info, Debug, Warn, Error. |

###### To view more information about an agent or Lightrun action {#details}

Click the information icon ![View details -icon](assets/images/i-details.png) on the right side of the agent or action. A dialog box will appear on your screen, showing more details about the agent/action.

The agent details dialog box should appear similar to the following image.

![View details -half](assets/images/intellij-agents3.png)

The following table describes the information present in the dialog box.

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

The action details dialog box should appear similar to the following image.

![View details -half](assets/images/action-details1.png)

The following table describes the information present in the dialog box.

| Field           | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| ID              | The system-generated ID associated with this action item.    |
| Type            | The type of action.                                          |
| Location  | The file and code line where the action starts following behavior. |
| Create Time     | The time and day on which the action was created.            |
| Owner           | The user who created the action.                             |
| Quota in effect | The quota controls use of CPU, Networking, Memory, excessively long strings, too many instructions printing out, protection from infinite loops and the like. <br/>     Quota settings can be tuned in the agent.config file. |
| Log Message     | The message resulting from the action appears here, if relevant. |
| Error Message   | If any agent reports any errors for this action, they are documented here. |

### Viewing action output {#piping}

Lightrun allows you to specify where you would like your agent’s action output to be displayed.

###### To configure Lightrun action output routing

1. From your Jetbrains IDE, click the Lightrun tab on the top right-hand corner of your IDE to display the Lightrun sidebar.
2. Click the agent tab to display a list of all active agents.
3. From the relevant agent, click ![Sidebar -icon](assets/images/i-pipe.png) to open the **Piping** menu.
	![View details -ten](assets/images/intellij-piping.png)
4. Select the relevant configuration. See the table below for more information. 

| Configuration |  Description   |
|--------|----------|
| **App/Stdout** | Output appears only in the application's standard output. 
|
| **Plugin** | Output appears in the Lightrun Management Portal, Jetbrains IDE( Lightrun Console and Lightrun Snapshot), and other third-party integrations. |
| **Both** | Output appears in the Lightrun Management Portal, Lightrun console, integrations, and standard output. |


## Tags tab {#tags}

The Tags tab displays a list of all active tags currently attached to Lightrun actions running in your Jetbrains IDE.

###### TO SEARCH FOR A TAG

1. Enter the tag’s into the search bar.
2. Click the Search button.

	The tag list should appear similar to the following image.
	![The Lightrun sidebar -half](assets/images/intellij-tags1.png)

3. Click the drop-left icon ![Drop left -icon](assets/images/drop-left.png) on the left-hand side of the tag listing to display a listing of all actions associated with that tag.
	![The Lightrun sidebar -half](assets/images/intellij-tags2.png)

The following table describes the icons present in the tags and action listing and the functions of each icon.

|      | Icon                                                         | Function                                                  |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1    | ![View details -icon](assets/images/i-details.png)           | Opens the information dialog box for the agent, tag, or action.    |
| 2    | ![Delete -icon](assets/images/i-delete.png)                  | Delete any agent or tag actions. Only agent-activated actions can be deleted from the Agents list and tag-activated actions from the Tags list. |
| 3    | ![Go to line -icon](assets/images/i-goto.png)                | Jump to the source file and line number in the code that is associated with the action. |
| 4    | ![Status -icon](assets/images/i-toggle.png)                  | Toggle to disable or enable an action. Only agent-activated actions can be toggled from the Agents list and tag-activated actions from the Tags list. |
| 5    | ![Status -icon](assets/images/i-status.png)![Status -icon](assets/images/i-tag.png) | Displays the current state of the action.<br/>- One checks indicates the action was submitted to the server.<br/>- Two checks indicate that it was received by the agent.<br/>- Highlighted checks indicate that the agent accepted the action.<br/>From the Agents list, the tag icon indicates the action was activated with tags and not agents, and its status can be viewed from the Tags list. |
| 6    | ![Log level -icon](assets/images/i-loglevel.png)         | Indicates the the level that was configured for the log (on log rows only): Info, Debug, Warn, Error. |
