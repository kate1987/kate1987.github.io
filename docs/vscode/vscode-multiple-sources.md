# Working with Multiple Sources

## Overview

Lightrun allows you to select multiple agents and tags as a single source when creating an action directly from your IDE. This option lets you simultaneously apply an action to a custom group of agents and tags.

## Selecting multiple Sources

###### TO ADD AN ACTION TO MULTIPLE SOURCES IN YOUR VSCODE IDE

1. Open the **Insert an Action** form. For instructions on how to open the **Insert a Log** form, see [Dynamic Logs](/vscode/vscode-plugin-dynamic-logs/); for the **Insert a metric** form, see [Metrics](/vscode/vscode-plugin-metrics/); for the **Insert a Snapshot** form, see [Snapshot](/vscode/vscode-plugin-snapshots/).
2. Click the ![Menu --icon](../assets/images/vscode/vscode-custom-source-menu.png) icon next to the **SOURCE** field to select your preferred condition. 
  ![Custom Source --quarter](../assets/images/vscode/vscode-custom-source.png)

  !!! note
      You can select one of two conditions:
      
      - **Match Any** - The action will be added to an agent if the agent is associated with any of the tags or custom sources selected in the SOURCE field.
      - **Match All** -  The action will be added to every agent, tag, and custom source selected in the SOURCE field.

3. Select the agents and tags to be added in the **SOURCE** field.
4. Click **Create** to create the action. 
  The action will be added to the selected sources.