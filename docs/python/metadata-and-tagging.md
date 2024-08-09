# Manage Lightrun Python agent metadata and tags

## Overview

Running agents with Python allows for two types of metadata to be specified, which can be included in either the metadata file or the application file, or entered as environment variables from the command line.

* DisplayName - identifies the deployment instance (for example, server name, company site)
* Tags - groups the agents according to context (for example, staging, production, server, QA)

## Agent tags

Tags are a powerful feature of the Lightrun agent. Applying tags enables you to group agents together with meaningful labels, typically based on common functionality. For example, you can use tags to identify the location and purpose of each agent: database servers, staging, QA, and so on. You can apply multiple tags to each agent, in any combination. Similarly, adding a single tag to multiple deployments of the same application allows you to add a log action to all of the instances at once.

By applying multiple tags, you can bind actions to an agent even before the application is launched, and you can apply actions to multiple applications regardless of where they are running. Once an action is bound to a tag, it is implicitly added to all agents that possess that tag.

Out-of-the-box, agents include a single **Production** tag. Users can:

- [Define and manage tags](#managing-tags)

- [View all tags](#view-tags)

## Managing tags

 Metadata and tags are specified within the code, in the `agent.metadata.json` file, or you can pass tags using an environment variable. Use one of the methods below to specify the agent's tags.

### Specifying agent tags within the code

You set agent tags by entering `metadata_registration_tags` argument in the `lightrun.enable()` call function. For example:

```python
lightrun.enable(company_key="<COMPANY_SECRET>", metadata_registration_tags='[{"name": "Production"},{"name": "EastUS"}]')
```

### Specifying agent tags using environment variable

You can use the `LIGHTRUN_TAGS` environment variable to set agent's tags dynamically. For example:

```bash
LIGHTRUN_TAGS=Production,Main,EastUS
```

### Specifying agent metadata and tags within a JSON file

1. From the relevant server where the agent is installed, create a file named `agent.metadata.json` file and open it.

2. Insert the following JSON (replace the dummy parameters and values as required):

   ```json
    {
      "registration": {
        "DisplayName": "<DISPLAY_NAME>",
        "tags": [
          {
            "name": "Tag1"
          },
          {
            "name": "Tag2"
          },
          {
            "name": "Tag3"
          }
        ]
      }
    }
   ```

  !!! info
  
       With no entered value, `displayName` will show the hostname of the machine running the application and the application's process identifier.

3. Open your application file (for example, main.py, app.py).

4. Within the `enable()` function, include a reference to the metadata JSON file.

   ```python
   try:
    import lightrun
    lightrun.enable(agent_config="/path/to/agent.config" , agent_regmetadata_file="/path/to/agent.metadata.json")
   except ImportError as e:
     print("Error importing Lightrun: ", e)
   ```

5. Restart the application.

  !!! imp "Important"
      Changes to the `agent.metadata.json` file do not take effect until the application is restarted.

**Example** 

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

## Viewing tags

Tags assigned to agents can be viewed from the Management Portal.

### To view tag details from the Management Portal {#view}

Log in to your Lightrun account and navigate to **Entities->Tags**.  
The **Tags** screen appears, similar to the following:

![Manage tags](../assets/images/app-tags.png)

The following details are displayed:

| Column  | Description                                               |
| ------- | --------------------------------------------------------- |
| Name    | The name of the tag.                                      |
| Actions | The list of actions currently attached to this tag.       |
| Agents  | The list of agents to which this tag has been associated. |
