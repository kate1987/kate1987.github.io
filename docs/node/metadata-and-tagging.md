# Manage the Node.js agent metadata and tagging

## Overview

Metadata and tags allow you to locate agents more easily; for instance, agents performing the same type of task or running on the same server, or company site. Tags also allow you to group agents with labels for bulk actions across multiple applications (running on the same server, or even on different servers).

Running agents with Node.js allows for two types of metadata to be specified, which can be included in either the metadata file or the application file, or entered as environment variables from the command line.

* `displayName` - identifies the application instance (for example, server name, company site)
* `tags` - groups the agents according to context (for example, staging, production, server, QA)

## Agent tags

Tags are a powerful feature of the Lightrun agent. Applying tags enables you to group agents together with meaningful labels, typically based on common functionality.

For example, you can use tags to identify the location and purpose of each agent: database servers, staging, QA, and so on. You can apply multiple tags to each agent, in any combination. Similarly, adding a single tag to multiple deployments of the same application allows you to add a log action to all of the instances at once.

By applying multiple tags, you can bind actions to an agent even before the agent is launched, and you can apply actions to multiple applications regardless of where they are running. Once an action is bound to a tag, it is implicitly added to all agents that possess that tag.

!!! example

    * Create a tag named **Integration**.
    * Add that tag to relevant agents where you're running your application for integration testing.
    * Set integration tests to execute with the **Integration** tag in order to debug an integration test failure.
    * You can now filter all agents in the plugin and display only those with the **Integration** tag.  
    The output lists all actions you inserted for integration testing across all of your agents.

Out-of-the-box, agents include a single **Production** tag. You can:

* [Create and manage tags](#managing-tags)

* [View all tags](#view-tags)

* View tags and their details [from the CLI](#view-tags)

## Managing tags

Metadata and tags are specified within the code or in the `agent.metadata.json` file.

### Specifying agent metadata and tags within the code

The metadata properties can be declared in the `start` method, as follows.

```js
require('lightrun').start({
    company: '<COMPANY_NAME>',
    lightrunSecret: '<LIGHTRUN_SECRET>',
    metadata: {
        registration: {
            displayName: "Pilot site",
            tags: ['Production', 'Main', 'EastUS']
        }
    }
}
```

### Specifying agent tags using environment variable

You can use the `LIGHTRUN_TAGS` environment variable to set agent's tags dynamically.

For example,

```bash
LIGHTRUN_TAGS=Production,Main,EastUS
```

### Specifying agent metadata and tags within a JSON file

1. From the relevant server where the agent is installed, go to the `agent.metadata.json` file (see a typical example [here](https://github.com/lightrun-platform/lightrun/blob/main/examples/Node/agent.metadata.json)) and open it.  

1. Insert the following JSON (replace the dummy parameters and values as required):

   ```json
    {
      "registration": {
        "displayName": "<DISPLAY_NAME>",
        "tags": [
          {
            "name": "<Tag1>"
          },
          {
            "name": "<Tag2>"
          },
          {
            "name": "<Tag3>"
          }
        ]
      }
    }
   ```

1. Open your application file (for example, `app.js`).

1. At the top of the file, within the `start` method, include a reference to the metadata JSON file.

   ```javascript
   require('lightrun').start({
        company: '<COMPANY_NAME>',
        lightrunSecret: '<LIGHTRUN_SECRET>',
        metadata: {
            filename: '<FULL_PATH_TO_METADATA_FILE>'
        }
   });
   ```

1. Restart the application.

  !!! imp "Important"
      Changes to the `agent.metadata.json` file do not take effect until the application is restarted.

Alternatively, you can use the environment variable `LIGHTRUN_METADATA_FILE` to pass the path for the metadata json file.

### Example

The following JSON provides to the `displayName` parameter a value that indicates a pilot site deployment. Tag labels are included for Production, main, and East US.

```json
{
    "registration": {
      "displayName": "Pilot site",
      "tags": [
        {
          "name": "Production"
        },
        {
          "name": "Main"
        },
        {
          "name": "EastUS"
        }
      ]
    }
}
```

Additional metadata configuration examples can be found [here](https://github.com/lightrun-platform/lightrun/blob/main/examples/Node).

## Viewing tags

Tags assigned to agents can be viewed from the Management Portal.

#### To view tag details from the Management Portal {#view}

Log in to your Lightrun account and navigate to **Entities->Tags**.
The **Tags** screen appears, similar to the following:

![Manage tags](../assets/images/app-tags.png)

The following details are displayed:

| Column  | Description                                               |
| ------- | --------------------------------------------------------- |
| Name    | The name of the tag.                                      |
| Actions | The list of actions currently attached to this tag.       |
| Agents  | The list of agents to which this tag has been associated. |
