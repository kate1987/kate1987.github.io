# .NET: Metadata and Tags

## Overview

Running agents with .NET allow for two types of metadata to be specified: 

- `DisplayName` - identifies the application instance (for example, server name, company site)
- `Tags` - groups the agents according to context (for example, staging, production, server, QA)

The two properties can be specified either in your code with the `Lightrun.Start` command or in an `agent.metadata.json` file.

### Specifying agent tags within the code

The metadata properties can be declared in the `Lightrun.Start` command, as follows: 

``` 
LightrunAgent.Start(new AgentOptions {
    Secret = "<LIGHTRUN_SECRET>",
    DisplayName = "<agent_display_name>",
    Tags = new[] {"Production", "Main", "EastUS"}
});
```


### Specifying agent metadata and tags within a JSON file

1. Create an `agent.metadata.json` file in your project’s repository.
2. Insert your tag and display name into the `agent.metadata.json` file in the following format:
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
3. Add the path to the `agent.metadata.json` file to your `Lightrun.Start` command.

    ```
    LightrunAgent.Start(new AgentOptions {
        Secret = "<LIGHTRUN_SECRET>",
        RegistrationMetadataFile = "<full-path-to-agent.metadata.json-file>"
    });
    ```

