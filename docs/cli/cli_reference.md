# Lightrun CLI Commands

This reference describe the Lightrun CLI commands, options, and parameters.

## Prerequisites

This tutorial assumes that you have:

- A Lightrun account.
- [Installed the Lightrun CLI on your local machine.](/cli/installation/)
- [Authenticated the Lightrun CLI](/cli/authentication/)

## Synopsis

```bash
java -jar lightrunc.jar <command> <options>

```

Add the `-v` command when running any command to enable the verbose mode. For exammple, 

```bash
java -jar lightrunc.jar <command> <options> -v

```

Use `java -jar lightrunc.jar help` to view a list of all available commands and options in your terminal.

!!! example

     ```bash
     $ java -jar lightrunc.jar help
     Usage: LightrunC [OPTIONS]
     Command line interface to Lightrun
          list-agents                 List the agents
          list-tags                   List the tags
          list-agents-by-tag <Tag>    List the agents by given tag
          list-actions <AgentId>      List the actions for the given agent id
          log <AgentId> <Filename>:<LineNumber> <Format> [-ignoreQuota] [-pipe 
          enable/disable/client]
                                   Insert a log to the given agent at the given
                                        file/line with the format (text of the log)
          clog <AgentId> <Filename>:<LineNumber> <Format> [-condition <Condition>] 
          [-expireSec <ExpireSec>] [-ignoreQuota] [-pipe enable/disable/client]
                                   Insert a conditional log to the given agent
                                        at the given file/line with the format
                                        (text of the log)
          snapshot <AgentId> <Filename>:<LineNumber> [-condition <Condition>] 
          [-watch <Expression>] [-expireSec <ExpireSec>] [-maxHitCount 
          <MaxHitCount>] [-ignoreQuota] [-pipe enable/disable/client]
                                   Insert a snapshot to the given agent at the
                                        given file/line
          counter <AgentId> <FileName>:<LineNumber> <CounterName> [-condition 
          <Condition>] [-expireSec <ExpireSec>] [-aggregateBy <Aggregate By 
          Prefix>] [ignoreQuota] [-pipe enable/disable/client]
                                   Count the number of times each thread hits
                                        the requested line.
                                   This option is currently supported only for
                                        Java agents.
          customMetric <AgentId> <FileName>:<LineNumber> <MetricName> 
          <MetricExpression> [-condition <Condition>] [-expireSec <ExpireSec>] 
          [-ignoreQuota] [-pipe enable/disable/client]
                                   Get metrics for the value given by the
                                        expression.
                                   This option is currently supported only for
                                        Java agents.
          snapshot-data <AgentId> <SnapshotId> [<output-file>]
                                   Prints the accumulated data for a snapshot or
                                        saves it to <output-file>
          rm <AgentId> <ActionId>     Removes an action from the given agent
          rm-tag <tagName>            Removes a tag from the server
          status                      Prints the current status of the backend
          detach <on|off>             Disconnects all agents and disables lightrun
                                        instantly (when on) until it's turned off
                                        again
          print-logs <AgentId> [<ActionId>] [-range <StartTimestamp-EndTimestamp 
          (milliseconds)>]
                                   Print all logs for the given agent. Limited
                                        to 1000 most recent results. Optionally,
                                        you can specify the range via the 'range'
                                        argument
          print-all-logs              Print all logs for all agents. Limited to
                                        1000 most recent results. Optionally, you
                                        can specify the range via the 'range'
                                        argument
          enable-piping <AgentId>     Logs/Counters/TicTocs for this agent id will
                                        be piped to Lightrun's backend and printed
                                        on the server! Logs are available with the
                                        print-logs command.
          client-piping <AgentId>     Logs/Counters/TicTocs for this agent id will
                                        be piped to Lightrun's backend and hidden
                                        in the server! Logs are available with the
                                        print-logs command
          disable-piping <AgentId>    Logs/Counters/TicTocs for this agent id will
                                        only be printed on the server! (this
                                        doesn't stop the action)
          server-url <ServerURL>      Sets the server URL for the command line
          login                       Log in the server. The login will supply a
                                        URL for further authentication. Optionally,
                                        you can specify the user name and password
                                        via the 'email' and 'password' arguments.
          logout                      Logs out the currently logged in user on this
                                        machine
          version                     Prints the version of Lightrun CLI and the
                                        backend server
          listen                      Listens to agent/log registration events and
                                        prints them out
          -v, verbose                 Verbose mode
          user                        Prints the details on the server for the
                                        currently logged in user
          help                        Print help details
          toggle-action [AgentId] <ActionId>
                                   Enable/Disable an action
          add-certificate <Certificate>
                                   Add a server certificate
          show-certificates           Show all the server certificates
          rm-certificate <Certificate>
                                   Remove a server certificate
          enable-pinning-status       Enable certificate pinning
          disable-pinning-status      Disable certificate pinning
          get-pinning-status          Get certificate pinning
          clear-exceptions            Clear all exceptions from history by Admin /
                                        Manager
          ignoreQuota, -ignoreQuota   Add this argument when submitting a new
                                        action in order to disable the quota limits
                                        on that action. This operation can
                                        seriously impact your performance and is
                                        only available for users with the ignore
                                        quota permission
          -pipe enable/disable/client Set Piping for action.
                                   enable - enables piping in the backend.
                                   disable - Stops tracking action in the
                                        backend/client
                                   client - Action will be piped to the backend
                                        and hidden in the server
     ```

## `listen`

The `listen` command prints out events (agent/actions events) from the server as they occur.

#### Synopsis

`java -jar lightrunc.jar listen`

#### Example

!!! note
     Use ++ctrl+c++ to exit listen mode.

!!! example

     run `java -jar lightrunc.jar listen`

     ```bash
     $ java -jar lightrunc.jar listen
     Connecting to server
     Listening for events
     {"eventType":"CONNECTED","status":{"status":"OK","statusCode":"STATUS_OK"}}
     {"eventType":"SESSION_DETAILS","metadata":{"sessionId":"ecf32a4b-43da-ea93-bce0-18ef235e962a"},"status":{"status":"OK","statusCode":"STATUS_OK"}}
     {"agentDisplayName":"","eventType":"AUTHENTICATED","status":{"status":"OK","statusCode":"STATUS_OK"}}
     {"actionType":"LOG","agentDisplayName":"erezk-Latitude-7400 (pid 30554)","agentId":"f4b0d260-ec00-4459-a9ed-b8ef7d4ffcf7","eventType":"LOG_DATA_ADDED","status":{"status":"OK","statusCode":"STATUS_OK"}}
     {"actionType":"LOG","agentDisplayName":"erezk-Latitude-7400 (pid 30554)","agentId":"f4b0d260-ec00-4459-a9ed-b8ef7d4ffcf7","eventType":"LOG_DATA_ADDED","status":{"status":"OK","statusCode":"STATUS_OK"}}
     {"actionType":"LOG","agentDisplayName":"erezk-Latitude-7400 (pid 30554)","agentId":"f4b0d260-ec00-4459-a9ed-b8ef7d4ffcf7","eventType":"LOG_DATA_ADDED","status":{"status":"OK","statusCode":"STATUS_OK"}}
     {"actionType":"LOG","agentDisplayName":"erezk-Latitude-7400 (pid 30554)","agentId":"f4b0d260-ec00-4459-a9ed-b8ef7d4ffcf7","eventType":"LOG_DATA_ADDED","status":{"status":"OK","statusCode":"STATUS_OK"}}
     {"actionType":"LOG","agentDisplayName":"erezk-Latitude-7400 (pid 30554)","agentId":"f4b0d260-ec00-4459-a9ed-b8ef7d4ffcf7","eventType":"LOG_DATA_ADDED","status":{"status":"OK","statusCode":"STATUS_OK"}}
     ```


## `version`

The `version` command outputs information about your current CLI version and Lightrun server version.

#### Synopsis

`java -jar lightrunc.jar version`

#### Example

!!! example

     run `java -jar lightrunc.jar version`

     ```bash
     $ java -jar lightrunc.jar version
     CLI Client Version: 1.4
     Server Version: 1.6
     ```

## `user`

The `user` command outputs all relevant information about the current logged-in user.

#### Synopsis

`java -jar lightrunc.jar user`

#### Example

!!! example

     run `java -jar lightrunc.jar user`

     ```bash
     $ java -jar lightrunc.jar user
     class UserDTO {
         activated: true
         authorities: <permissions>
         company: class CompanyDTO {
             agentAPIKey: <agent-api-key>
             agentsEnabled: true
             certificatePinningEnabled: false
             displayName: null
             dontStorePluginToken: false
             id: <id>
             inviteKey: <invite-key>
             licenseExpiry: <liscense-expiry>
             licensedAgents: 1000
             licensedUsers: 1000
             managerId: null
             managerLogin: null
             name: <name>
             subscriptionStatus: STANDARD
             uniquifier: <uniquifier>
             users: []
         }
         companyName: <company-name>
         createdBy: <accout-created-by>
         createdDate: <created-date>
         email: <email>
         firstName: <first-name>
         id: <id>
         imageUrl: null
         langKey: en
         lastModifiedBy: <account-last-modified-by>
         lastModifiedDate: <last-modified-date>
         lastName: <last-name>
         password: null
         passwordHash: null
         passwordSet: false
         registerMethod: <register-method>
         subscriptionStatus: <subscription-status>
     }
     ```

## `status`

The `status` command outputs the current status of the Lightrun Management server, including licensing information about the agent and other relevant details.

#### Synopsis

`java -jar lightrunc.jar status`

#### Example

!!! example

     run `java -jar lightrunc.jar status`

     ```bash
     $ java -jar lightrunc.jar status
     Lightrun CLI Client
     ----------
     Server URL: https://app.lightrun.com
     Company Name: <company-name
     Version: 1.4
     Backend Version: 1.6
     User: <user-email>
     Licenced Agents: 1000
     Licence Expiry: <liscence-expiry>
     Exception Daily Limit: Not Reached
     ```

## `detach`

When experiencing any issues on the server, you might want to disable Lightrun in order to rule it out when troubleshooting.

The `detach` command allows you to disable all Lightrun agents on the specified server and re-enable the agents at will.


#### Synopsis

`java -jar lightrunc.jar detach on/off`

#### Options

| Option   | Description                         |
| -------- | ----------------------------------- |
| `on`| Disable all Lightrun agents on your server. |
| `off` | Enable detached agents. |

#### Examples

!!! example

     run `java -jar lightrunc.jar detach on` to disable all Lightrun agents

     ```bash
     $ java -jar lightrunc.jar detach on
     Agents are now detached
     ```

     run `java -jar lightrunc.jar detach off` to enable all Lightrun agents

     ```bash
     $ java -jar lightrunc.jar detach off
     Agents are now re-enabled
     ```

## `logout`

The `logout` logs out the currently logged in user from the Lightrun CLI.

#### Synopsis

`java -jar lightrunc.jar logout`

#### Example

!!! example

     run `java -jar lightrunc.jar logout`

     ```bash
     Logged out successfully!
     ```

## `agents`, `tags`, `and` `custom sources`

### `list-agents`

The `list-agents` command outputs all agents and their associated actions.

#### Synopsis

`java -jar lightrunc.jar list-agents`

#### Example

!!! Example
     run `java -jar lightrunc.jar list-agents`

     ```bash
     $ java -jar lightrunc.jar list-agents
     0 : ID e93fccd1-9f76-46ae-b703-056e25b8092e HOST ip-172-31-50-47 PID 14507 UPDATE 1/21/21, 9:16 AM
        ACTION 4261257f-fbc0-4fc5-8fe7-e8dbf3944eb7 FILE PrimeMainMR.java LINE 10 TYPE TICTOC
        ACTION 99e8e7b0-9248-4d89-8f6f-2d3c5fa9aebc FILE PrimeMainMR.java LINE 15 TYPE LOG Hello world {java expression}gg
        ACTION b383e31b-8749-419f-a492-85a919cc0da8 FILE PrimeMainMR.java LINE 22 TYPE TICTOC
        ACTION c3f863e6-ba7d-4480-83c0-ef4a278ecddb FILE PrimeMainMR.java LINE 15 TYPE COUNTER
        ACTION e5790c99-f763-4d26-8d3f-2714c89c0fad FILE PrimeMainMR.java LINE 10 TYPE BREAKPOINT
     1 : ID f93fccd1-9f75-46ae-b703-456e25b8092e HOST ip-172-31-50-47 PID 14508 UPDATE 1/21/21, 9:16 AM
        ACTION 5261257f-fbc0-4fc5-8fe7-e8dbf3944eb7 FILE PrimeMainMR.java LINE 10 TYPE TICTOC
        ACTION 49e8e7b0-9248-4d89-8f6f-2d3c5fa9aebc FILE PrimeMainMR.java LINE 15 TYPE LOG Hello world {java expression}gg
        ACTION g383e31b-8749-419f-a492-85a919cc0da8 FILE PrimeMainMR.java LINE 22 TYPE TICTOC
        ACTION a3f863e6-ba7d-4480-83c0-ef4a278ecddb FILE PrimeMainMR.java LINE 15 TYPE BREAKPOINT
        ACTION l5790c99-f763-4d26-8d3f-2714c89c0fad FILE PrimeMainMR.java LINE 10 TYPE BREAKPOINT
     ```

### `list-agents-by-tag`

The `list-agents-by-tag` command outputs all agents and actions related to the specified tag.

#### Synopsis

`java -jar lightrunc.jar list-agents-by-tag Production`

#### Options

| Option | Description                                            |
| ------ | ------------------------------------------------------ |
| Tag    | The name of the relevant tag. For example, Production. |

#### Example

!!! Example
     run `java -jar lightrunc.jar list-agents-by-tag Production` to list all agents associated to the Production tag.
    
     ```bash
     $ java -jar lightrunc.jar list-agents-by-tag Production
     0 : ID <user-id> HOST <host> PID 10 UPDATE 7/26/22, 8:08 PM TAGS [Production]
      downloads % java -jar lightrunc.jar list-agents-by-tag Production
     0 : ID <user-id> HOST <host> PID 10 UPDATE 7/26/22, 8:13 PM TAGS [Production]
      ACTION 1ecff847-db90-46f8-9493-bdac3518809b FILE PrimeMainMR.java LINE 30 TYPE LOG Hello world {expression}
      ACTION 275cae4c-ece9-4f6c-8950-594cd3ccc7fd FILE PrimeMainMR.java LINE 59 TYPE COUNTER 
      ACTION 5eaeeca1-4861-473b-8d55-b39b29af26ad FILE PrimeMainMR.java LINE 20 TYPE TICTOC ERROR Collision in breakpoint location on the same tree
      ACTION 758a36b8-50be-472c-8a6e-891eb3d31747 FILE PrimeMainMR.java LINE 78 TYPE BREAKPOINT 
      ACTION a214a929-6bc8-44ff-92f1-5c0140084038 FILE PrimeMainMR.java LINE 33 TYPE LOG Hello world {expression}
     ```
### `list-tags`

The `list-tags` command lists all tags and their actions.

#### Synopsis

`java -jar lightrunc.jar list-tags`

#### Example

!!! Example
     run `java -jar lightrunc.jar list-tags`

     ```bash
     $ java -jar lightrunc.jar list-tags
     Tag: Production
        ACTION 4f6f8e67-2252-4093-bcf2-9a5254f074ef FILE PrimeMainMR.java LINE 50 TYPE LOG Hello world {java expression}
        ACTION 99e8e7b0-9248-4d89-8f6f-2d3c5fa9aebc FILE PrimeMainMR.java LINE 15 TYPE LOG Hello world {java expression}gg
        ACTION e5790c99-f763-4d26-8d3f-2714c89c0fad FILE PrimeMainMR.java LINE 10 TYPE BREAKPOINT
     Tag: Staging
        ACTION b383e31b-8749-419f-a492-85a919cc0da8 FILE PrimeMainMR.java LINE 22 TYPE TICTOC
        ACTION c3f863e6-ba7d-4480-83c0-ef4a278ecddb FILE PrimeMainMR.java LINE 15 TYPE COUNTER
     ```

### `list-custom-sources`

The `list-custom-sources` command outputs all available custom sources.

#### Synopsis

`java -jar lightrunc.jar list-custom-sources`

#### Example

!!! Example
     run `java -jar lightrunc.jar list-custom-sources`
     ```bash
     $ java -jar lightrunc.jar list-custom-sources
     Custom Source: Production (86ba64eb-89a7-445d-a3f3-e273645594b6)
     ```

### `list-agents-by-custom-source-name`

The `list-agents-by-custom-source-name` command lists all agents associated with a custom source.

#### Synopsis

`java -jar lightrunc.jar list-agents-by-custom-source-name <CustomSource>`

#### Options

| Option   | Description                         |
| -------- | ----------------------------------- |
| Custom Source | Custom source name. |

#### Examples

!!! Example
     run  `java -jar lightrunc.jar list-agents-by-custom-source-name <CustomSource>`
     ```bash
     $ java -jar lightrunc.jar list-agents-by-custom-source-name Staging   
     0 : ID a7324611-3ab0-4ea1-8cad-bbc9fcfe3e4a HOST 6f4d43f85e53 PID 14 UPDATE 2/1/23, 7:37 AM TAGS [Production]
     ```

### `list-actions`

The `list-actions` command lists all actions associated with a specified agent or tag.

#### Synopsis

`java -jar lightrunc.jar list-actions <AgentId>`

#### Options

| Option   | Description                         |
| -------- | ----------------------------------- |
| Agent-ID | Enter the ID of the relevant agent. |
| Tag | Enter the relevant tag instead of an agent ID. |

#### Examples

!!! Example
     run  `java -jar lightrunc.jar list-actions <AgentId>` to list all actions associated with the specified agent.
     ```bash
     $ java -jar lightrunc.jar list-actions 7b5a1f54216b  
     There are no actions to agent 7b5a1f54216b
     ```

     run `java -jar lightrunc.jar list-actions tag:<tagName>` to list all actions associated with the specified tag.

     ```bash
     $  java -jar lightrunc.jar list-actions tag:Production
     There are no actions to agent tag:Production
     ```



### `client-piping`

The `client-piping` command pipes Log, Metrics, Counters, and Tic Toc data to the Lightrun Console, Management Portal, and any other configured logging tool.

#### Synopsis

`java -jar lightrunc.jar client-piping <Agent-ID>`

#### Options

| Option   | Description                         |
| -------- | ----------------------------------- |
| Agent-ID | Enter the ID of the relevant agent. |

#### Example

!!! Example
     run `java -jar lightrunc.jar client-piping <Agent-ID>`

     ```bash
     $ java -jar lightrunc.jar client-piping da0c440b-ae8e-4011-9f61-93a07405baa2
     Log tracking in progress, use print-logs to view the output
     ```


### `enable-piping`

The `enable-piping` command pipes Log, Metrics, Counters, and Tic Toc data to the Lightrun Console, Management Portal, and any other configured logging tool.

#### Synopsis

`java -jar lightrunc.jar enable-piping <Agent-ID>`

#### Options

| Option   | Description                         |
| -------- | ----------------------------------- |
| Agent-ID | Enter the ID of the relevant agent. |

#### Example

!!! Example
     run `java -jar lightrunc.jar enable-piping <Agent-ID>`

     ```bash
     $ java -jar lightrunc.jar enable-piping da0c440b-ae8e-4011-9f61-93a07405baa2
     Log tracking in progress, use print-logs to view the output
     ```

### `disable-piping`

The `disable-piping` command disables all output piping for the specified agent.

#### Synopsis

`java -jar lightrunc.jar disable-piping <Agent-ID>`

#### Options

| Option   | Description                         |
| -------- | ----------------------------------- |
| Agent-ID | Enter the ID of the relevant agent. |

#### Example

!!! Example
     run `java -jar lightrunc.jar disable-piping <Agent-ID>`

     ```bash
     $ java -jar lightrunc.jar disable-piping da0c440b-ae8e-4011-9f61-93a07405baa2 
     Log tracking is disabled
     ```


## `actions`

### `toggle-action`

The `toggle-action` command enables or disables an action.

#### Synopsis

`java -jar lightrunc.jar toggle-action <Agent-ID> <ActionId>`

#### Options

| Option    | Description                          |
| --------- | ------------------------------------ |
| Agent-ID | Enter the ID of the relevant agent. |
| Action-ID | Enter the ID of the relevant action. |

#### Examples

!!! Example
     run `java -jar lightrunc.jar toggle-action <Agent-ID> <ActionId>` on an active action to disable the action.

     ```bash
     $ java -jar lightrunc.jar toggle-action da0c440b-ae8e-4011-9f61-93a07405baa2  b5f20e04-5ab1-4c14-887b-1386ee96ce1b
     Action b5f20e04-5ab1-4c14-887b-1386ee96ce1b was successfully disabled
     ```
     
     run `java -jar lightrunc.jar toggle-action <Agent-ID> <ActionId>` on a disabled action to enable the action.

     ```bash
     $ java -jar lightrunc.jar toggle-action da0c440b-ae8e-4011-9f61-93a07405baa2  b5f20e04-5ab1-4c14-887b-1386ee96ce1b
     Action b5f20e04-5ab1-4c14-887b-1386ee96ce1b was successfully enabled
     ```

### `log`

The `log` command inserts a log to the given agent at the given file/line with the format (text of the log).

#### Synopsis

`java -jar lightrunc.jar log <AgentId> <Filename>:<LineNumber> <Format> -expireSec <ExpireSec> [-ignoreQuota]`

!!! imp "Important"
     
	 If the file name and line number don't match the bytecode version of the app, Lightrun will behave inconsistently and will most likely fail. 

#### Options

| Option       | Description                         |
| ------------ | ----------------------------------- |
| Agent-ID     | The ID of the relevant agent. <br>*Change `AgentID` to tag:`tagName` to insert the action into a tag.* |
| Filename     | The name of the file, including the suffix   |
| LineNumber   | The number of the line of code in the referenced file.           |
| Format       | The text to appear in your logs.    |
| expireSec   | The amount of time for which this log should run. <br>*Dynamic logs timeout after 1 hour by default if you don't insert an expiry time.*  |
| ignoreQuota | When set, the quota limit configured for running Lightrun actions is overridden and this log will continue to run even if it reaches the quota. <br>*Only users with the Ignore Quota role can use this option.*  |

#### Example

!!! Example
     - run `java -jar lightrunc.jar log <AgentId> <Filename>:<LineNumber> <Format> -expireSec <ExpireSec> [-ignoreQuota]` to add a log to an agent.
       ```bash
       $ java -jar lightrunc.jar log 00e5ab81-2d63-404f-9c27-2f7ee9a0bfb8 request.js:11 Hello-world  -expireSec 360 
       The log was submitted
       ```
     - run `java -jar lightrunc.jar log tag:<tagName> <Filename>:<LineNumber> <Format> -expireSec <ExpireSec> [-ignoreQuota]` to add a log to a set of agents identified by a tag.
       ```bash
       $ java -jar lightrunc.jar log tag:Production request.js:11 Hello-world  -expireSec 360 
       The log was submitted
       ```
     

### `print-logs`

The `print-logs` command outputs all logs for the given agent.

#### Synopsis

`java -jar lightrunc.jar print-logs <AgentId> [<ActionId>] [-range <StartTimestamp-EndTimestamp (milliseconds)>]`

!!! note
    - Piping must be enabled (`enable-piping` command) for the `print-logs` to be able to output.
    - The `print-logs` output is limited to 1000 most recent results.

#### Options

| Option   | Description                                                  |
| -------- | ------------------------------------------------------------ |
| AgentId  | The ID of the relevant agent.                          |
| ActionId | The ID of the action for which you want to view all logs. You can run 'list-actions' to view a list of action IDs. |
| range    | Specify a time range to view dynamic logs for only that period of time. Use 13 digit epoch time when specifying a range. |

#### Example

!!! Example
      run `java -jar lightrunc.jar print-logs <AgentId> [<ActionId>] [-range <StartTimestamp-EndTimestamp (milliseconds)>]`

      ```bash
      $ java -jar lightrunc.jar print-logs 0 0 -range 1615391135824-1615391135924
      INFO: LOGPOINT: 197581639 is a prime number
      INFO: LOGPOINT: 197581649 is a prime number
      INFO: LOGPOINT: 197581651 is a prime number
      INFO: LOGPOINT: 197581673 is a prime number
      INFO: LOGPOINT: 197581687 is a prime number
      INFO: LOGPOINT: 197581697 is a prime number
      INFO: LOGPOINT: 197581717 is a prime number
      INFO: LOGPOINT: breakpointId: [f188655e-7dab-42a1-acad-ce53a16a85dc]: Logpoint is paused due to high call rate until log quota is restored
      ```



### `print-all-logs`

The `print-all-logs` command prints all logs for all agents.

#### Synopsis

`java -jar lightrunc.jar print-all-logs`

!!! note
    - Piping must be enabled (`enable-piping` command) for the `print-all-logs` to be able to output.
    - The `print-all-logs` output is limited to 1000 most recent results.

#### Example

!!! Example
     run `java -jar lightrunc.jar print-all-logs`

     ```bash
     $ java -jar lightrunc.jar print-all-logs
     INFO: LOGPOINT: breakpointId: [786e3a7e-a60b-4e48-884e-2c126c4da8e3]: Logpoint is paused due to high call rate until log quota is restored
     INFO: LOGPOINT: Hello world 24373299
     INFO: LOGPOINT: Hello world 24373300
     INFO: LOGPOINT: Hello world 24373301
     INFO: LOGPOINT: Hello world 24373298
     INFO: LOGPOINT: Hello world 24373307
     INFO: LOGPOINT: Hello world 24373308
     INFO: LOGPOINT: Hello world 24373309
     INFO: LOGPOINT: Hello world 24373310
     INFO: LOGPOINT: Hello world 24373312
     ```


### `clog`

The `clog` command inserts a conditional log for the given agent in the given file and line.

#### Synopsis

`java -jar lightrunc.jar clog <AgentId> <Filename>:<LineNumber> <Format> [-condition <Condition>] [-expireSec <ExpireSec>] [-ignoreQuota]`

!!! imp "Important"
     
	 If the file name and line number don't match the bytecode version of the app, Lightrun will behave inconsistently and will most likely fail. 

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Agent-ID    | The ID of the relevant agent. <br>*Change `AgentID` to tag:`tagName` to insert the action into a tag.* |
| FileName    | The name of the file containing the code in which to add the metric, including the extension. For example: MyJavaFile.java |
| LineNumber  | The line number within the code file.                        |
| Format      | The text to appear in your dynamic logs for this metric.    |
| Condition   | Any valid Java expression that does not change the state of the code.    |
| ExpireSec   | The amount of time for which this log should run.       |
| ignoreQuota | When set, the quota limit configured for running Lightrun actions is overridden and this log will continue to run even if it reaches the quota. <br>*Only users with the Ignore Quota role can use this option.*  |

#### Example

!!! Example
     - run `java -jar lightrunc.jar clog <AgentId> <Filename>:<LineNumber> <Format> [-condition <Condition>] [-expireSec <ExpireSec>] [-ignoreQuota]` to add the clog to an agent.
       ```bash
       java -jar lightrunc.jar clog 5c6e9cdef4e833279ee286a1 Main.java:10 "Array size {arr.length}" -condition "i % 10 == 0""
       ```
       The log will be printed when the expression `i % 10 == 0` evaluates to true.
     - run `java -jar lightrunc.jar clog tag:<tagName> <Filename>:<LineNumber> <Format> [-condition <Condition>] [-expireSec <ExpireSec>] [-ignoreQuota]` to add a clog to a set of agents identified by a tag.
       ```bash
       java -jar lightrunc.jar clog tag:Production Main.java:10 "Array size {arr.length}" -condition "i % 10 == 0""
       ```
       The log will be printed when the expression `i % 10 == 0` evaluates to true.


### `snapshot`

The `snapshot` command inserts a snapshot to the specified agent at the given file/line.

#### Synopsis

`java -jar lightrunc.jar snapshot <AgentId> <Filename>:<LineNumber> [-condition <Condition>] [-expireSec <ExpireSec>] [-maxHitCount <MaxHitCount>] [-ignoreQuota]`

!!! imp "Important"
     
	 If the file name and line number don't match the bytecode version of the app, Lightrun will behave inconsistently and will most likely fail. 

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Agent-ID    | The ID of the relevant agent. <br>*Change `AgentID` to tag:`tagName` to insert the action into a tag.*  |
| FileName    | The name of the file containing the code in which to add the metric, including the extension. For example: MyJavaFile.java |
| LineNumber  | The line number within the code file.                        |
| Condition   | Any valid Java expression that does not change the state of the code.     |
| ExpireSec   | The amount of time for which this action should run.       |
| MaxHitCount | The maximum number of times to take this snapshot during the valid period of this action; default = 1                    |
| ignoreQuota | When set, the quota limit configured for running Lightrun actions is overridden and this action will continue to run even if it reaches the quota. <br>*Only users with the Ignore Quota role can use this option.*  |

#### Example

!!! Example
     - run `java -jar lightrunc.jar snapshot <AgentId> <Filename>:<LineNumber> [-condition <Condition>] [-expireSec <ExpireSec>] [-maxHitCount <MaxHitCount>] [-ignoreQuota]` to add a snapshot to an agent.
       ```bash
       $ java -jar lightrunc.jar snapshot da0c440b-ae8e-4011-9f61-93a07405baa2 PrimeMainMR.java:42 
       The breakpoint was submitted
       ```
     - run `java -jar lightrunc.jar snapshot tag:<tagName> <Filename>:<LineNumber> [-condition <Condition>] [-expireSec <ExpireSec>] [-maxHitCount <MaxHitCount>] [-ignoreQuota]` to add a snapshot to a set of agents identified by a tag.
       ```bash
       $ java -jar lightrunc.jar snapshot tag:Production PrimeMainMR.java:42 
       The breakpoint was submitted
       ```
### `snapshot-data`

The `snapshot-data` command prints out the accumulated data for a snapshot, or save the data into a specified output file.

#### Synopsis

`java -jar lightrunc.jar snapshot-data <AgentId> <SnapshotId>[<output-file>]`

#### Options

| Option     | Description                                                  |
| ---------- | ------------------------------------------------------------ |
| Agent-ID   | The ID of the relevant agent.                          |
| SnapshotId | The ID of the snapshot for which to print the existing data. |

#### Example

!!! Example
     run `java -jar lightrunc.jar snapshot-data <AgentId> <SnapshotId>[<output-file>]`

     ```bash
     $ java -jar lightrunc snapshot-data e178578f-14da-476f-a084-bc460d6ec2b0 eb5abb0a-4677-4bed-9999-ea0b76c4efd2

     [class BreakpointDataDTO {
      actionId: eb5abb0a-4677-4bed-9999-ea0b76c4efd2
      agentId: e178578f-14da-476f-a084-bc460d6ec2b0
      createTime: class TimeDTO {
          nanos: 696685698
          seconds: 1611590801
      }
      dataId: 72f81a80-c415-4f00-a43d-83523a735230
      evaluatedExpressions: null
      stackFrames: [class AgentStackFrameDTO {
          arguments: [class WatchEntryDTO {
              members: null
              name: args
              status: null
              type: null
              value: null
              varTableIndex: 1
          }]
          function: PrimeMain.main
          locals: [class WatchEntryDTO {
              members: null
              name: i
              status: null
              type: int
              value: 30514481
              varTableIndex: null
          }]
          location: class LocationDTO {
              column: 0
              endOfLine: false
              line: 20
              path: PrimeMain.java
          }
      }]
      variableTable: [class WatchEntryDTO {
          members: null
          name: null
          status: class BreakpointStatusDTO {
              description: class BreakpointStatusDescriptionDTO {
                  format: Buffer full. Use an expression to see more data
                  parameters: null
              }
              isAccepted: false
              isError: true
              refersTo: VARIABLE_VALUE
          }
          type: null
          value: null
          varTableIndex: null
      }, class WatchEntryDTO {
          members: [class WatchEntryDTO {
              members: null
              name: length
              status: null
              type: int
              value: 0
              varTableIndex: null
          }]
          name: null
          status: null
          type: java.lang.String[]
          value: null
          varTableIndex: null
          }]
     }]

     ```

!!! tip
    You may use agent/action indexes instead of an ID.
    For example:

    ```bash
    java -jar lightrunc.jar snapshot-data 0 0 will output the first snapshot of the first agent
    ```

!!! tip
    The output file is saved in JSON format, and can be manipulated by other tools.

### `customMetric`

The `customMetric` command creates a custom metric based on specified expressions and values 

!!! note
     - This command is currently supported only for Java agents.
     
     - Always use quotes when setting a condition ("num>3") in order to avoid shell output redirection to file descriptor 3.

#### Synopsis

`java -jar lightrunc.jar customMetric <AgentId> <FileName>:<LineNumber> <MetricName> <MetricExpression> [-condition <Condition>] [-expireSec <ExpireSec>] [-ignoreQuota]`

!!! imp "Important"
     
	 If the file name and line number don't match the bytecode version of the app, Lightrun will behave inconsistently and will most likely fail. 

#### Options


| Option           | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| ignoreQuota      | When set, the quota limit configured for running Lightrun actions is overridden and this custom metric will continue to run even if it reaches the quota. The quota controls use of CPU, Networking, Memory, excessively long strings, too many instructions printing out, protection from infinite loops and the like. <br> *Only administrators with the Ignore Quota role can use this option.*  |
| Agent-ID         | The ID of the relevant agent. *Change `AgentID` to tag:`tagName` to insert the action into a tag.* |
| FileName         | The name of the file containing the code in which to add the metric, including the extension. For example: MyJavaFile.java |
| LineNumber       | The line number within the code file.                        |
| MetricName       | Assign a unique name to this metric.   |
| MetricExpression | Configure any valid Java expression that does not change the state of the code.  |
| Condition        | Any valid Java expression that does not change the state of the code.  |
| ExpireSec        | Configure the duration that this metric should run in seconds.                                                             |

#### Example

!!! Example
     - run `java -jar lightrunc.jar customMetric <AgentId> <FileName>:<LineNumber> <MetricName> <MetricExpression> [-condition <Condition>] [-expireSec <ExpireSec>] [-ignoreQuota]` to add a customMetric to an agent.
			```bash
			$ java -jar lightrunc.jar customMetric 0 PrimeMain.java:14 MyPrimeMetric num -condition "num>3"
			INFO: 10 Mar 2021, 11:59:26 CustomMetric Stats:
			{
				"MyPrimeMetric" :
				{"count" : 55106,"max" : 675526339,"mean" : 6.731275234790297E8,"min" : 629652109,"p50" : 6.73885867E8,"p75" : 6.74822641E8,"p95" : 6.75395141E8,"p98" : 6.75455779E8,"p99" : 6.75491381E8,"p999" : 6.75526339E8,"stddev" : 2424070.6627122667  }
			}
			```
     - run `java -jar lightrunc.jar customMetric tag:<tagName> <FileName>:<LineNumber> <MetricName> <MetricExpression> [-condition <Condition>] [-expireSec <ExpireSec>] [-ignoreQuota]` to add a customMetric to a set of agents identified by a tag.
			```bash
			$ java -jar lightrunc.jar customMetric tag:Production PrimeMain.java:14 MyPrimeMetric num -condition "num>3"
			INFO: 10 Mar 2021, 11:59:26 CustomMetric Stats:
			{
				"MyPrimeMetric" :
				{"count" : 55106,"max" : 675526339,"mean" : 6.731275234790297E8,"min" : 629652109,"p50" : 6.73885867E8,"p75" : 6.74822641E8,"p95" : 6.75395141E8,"p98" : 6.75455779E8,"p99" : 6.75491381E8,"p999" : 6.75526339E8,"stddev" : 2424070.6627122667  }
			}
			```		

### `counter`

The `counter` command returns the number of times each thread hit a specified code line.

!!! note
     - This command is currently supported only for Java agents.

#### Synopsis

`java -jar lightrunc.jar counter <AgentId> <FileName>:<LineNumber> <CounterName> [-condition <Condition>] [-expireSec <ExpireSec>] [-aggregateBy <Aggregate By Prefix>] [ignoreQuota]`

!!! imp "Important"
     
	 If the file name and line number don't match the bytecode version of the app, Lightrun will behave inconsistently and will most likely fail. 

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Agent-ID    | The ID of the relevant agent.  *Change `AgentID` to tag:`tagName` to insert the action into a tag.*  |
| FileName    | The name of the file containing the code in which to add the metric, including the extension. For example: MyJavaFile.java |
| LineNumber  | The line number within the code file.                        |
| CounterName | The name of the counter - the text to appear in your dynamic logs for this metric.    |
| Condition   | Any valid Java expression that does not change the state of the code.     |
| ExpireSec   | The amount of time for which this counter should run.  |
| aggregateBy | Collect and aggregate data for the specified string only.    |
| ignoreQuota | Only users with the Ignore Quota role can use this option. When set, the quota limit configured for running Lightrun actions is overridden and this counter will continue to run even if it reaches the quota.  |

#### Example

!!! Example
     - run `java -jar lightrunc.jar counter <AgentId> <FileName>:<LineNumber> <CounterName> [-condition <Condition>] [-expireSec <ExpireSec>] [-aggregateBy <Aggregate By Prefix>] [ignoreQuota]` to add a counter to an agent.
			```bash
			$ java -jar lightrunc counter e178578f-14da-476f-a084-bc460d6ec2b0 PrimeMain.java:20 myCounter
			The counter was submitted
			```
     - run `java -jar lightrunc.jar counter tag:<tagName> <FileName>:<LineNumber> <CounterName> [-condition <Condition>] [-expireSec <ExpireSec>] [-aggregateBy <Aggregate By Prefix>] [ignoreQuota]` to add a counter to a set of agents identified by a tag.
			```bash
			$ java -jar lightrunc counter tag:Production PrimeMain.java:20 myCounter
			The counter was submitted
			```

## `pii redaction`

### `create-pii-redaction-template`

The `create-pii-redaction-template` command adds a new PII Redaction template to the Lightrun server.


#### Synopsis

`java -jar lightrunc.jar create-pii-redaction-template <Name>`


#### Options

| Option | Description |
| -------- | ----------------------------------- |
| Name|  Enter the name of the relevant PII Redaction template. |


#### Example

!!! Example

     - run `java -jar lightrunc.jar create-pii-redaction-template`
      
          ```bash
          $ java -jar lightrunc.jar create-pii-redaction-template piiAP15 pii-redaction-agentpool-15
          PII redaction template 'piiAP15' successfully created
          ```
### `update-pii-redaction-template`

The `update-pii-redaction-template` command modifies and updates an existing template.

#### Synopsis

`java -jar lightrunc.jar update-pii-redaction-template <Name> -name TEMPLATE_NEW_NAME -description`

#### Options

| Option | Description |
| -------- | ----------------------------------- |
| Name | Enter the name of the relevant PII redaction template. |
| Description|  Enter a description for the template. |


#### Example

!!! Example
     - run `java -jar lightrunc.jar update-pii-redaction-template <Name> -name TEMPLATE_NEW_NAME -description`
               ```bash
               java -jar lightrunc.jar update-pii-redaction-template piiAP15 -name demo
                PII redaction template 'demo' successfully updated
               ```
### `list-pii-redaction-templates`

The `list-pii-redaction-templates` command lists all available PII Redaction templates.

#### Synopsis

`java -jar lightrunc.jar list-pii-redaction-templates`

#### Example

!!! Example

         - run `java -jar lightrunc.jar list-pii-redaction-templates`
           
          ```bash
          java -jar lightrunc.jar list-pii-redaction-templates
          ID 1 NAME Default DESCRIPTION This PII Redaction template will be applied to all agent pools by default
          ID 134 NAME demo DESCRIPTION pii-redaction-agentpool-15
          ID 135 NAME demo - 2023-09-06T08-18-06_529147516Z DESCRIPTION pii-redaction-agentpool-15
          ```
### `delete-pii-redaction-template`

The `delete-pii-redaction-template` command deletes an existing PII Redaction template.

#### Synopsis


`java -jar lightrunc.jar delete-pii-redaction-template <Name>`


#### Options


| Option | Description |
| -------- | ----------------------------------- |
| Name | Enter the name of the relevant PII Redaction template. |


#### Example

!!! Example

         - run `java -jar lightrunc.jar delete-pii-redaction-template <Name>`

          ```bash
          $ java -jar lightrunc.jar delete-pii-redaction-template demo
          PII redaction template 'demo' successfully deleted
          ```


### `clone-pii-redaction-template`

The `clone-pii-redaction-template` command duplicates the PII Redaction template and provides a new name.

#### Synopsis


`java -jar lightrunc.jar clone-pii-redaction-template <Name>`


#### Options

| Option | Description |
| -------- | ----------------------------------- |
| Name | Enter the name of the source PII Redaction template you want to clone. |


#### Example


!!! Example
        - run `java -jar lightrunc.jar clone-pii-redaction-template <Name>`
          ```bash
          $java -jar lightrunc.jar clone-pii-redaction-template demo
          PII redaction template 'demo - 2023-09-06T08-18-06_527147516Z' successfully created
          ```
### `add-pii-redaction-pattern`

The `add-pii-redaction-pattern` command adds new patterns to an existing PII Redaction template.

#### Synopsis

`java -jar lightrunc.jar add-pii-redaction-pattern <TemplateName> <PatternName> <Pattern> [BY_NAME|BY_VALUE]`


#### Options


| Option | Description |
| -------- | ----------------------------------- |
| TemplateName | Enter the name of the relevant PII redaction template. |
| PatternName | Enter the name of the relevant pattern. |
| PATTERN | Enter the pattern. PATTERN is a regex, and indicates the data matching the regex to be redacted. |
| BY_NAME | Indicate that data will be redacted based on the variable name. |
| BY_VALUE | Indicate that the data will be redacted based on the variable value. |


#### Example
 

!!! Example

          run `java -jar lightrunc.jar clone-pii-redaction-template <Name>`
          ```bash
          $java java -jar lightrunc.jar add-pii-redaction-pattern demo Tickets com.sales.tickets BY_VALUE
          Successfully added pattern to template 'demo'
          ```


### `list-pii-redaction-pattern`

The `list-pii-redaction-patterns` command lists all the patterns configured on the specific PII Redaction template.


#### Synopsis


`java -jar lightrunc.jar list-pii-redaction-patterns <TemplateName>`


#### Options

| Option | Description |
| -------- | ----------------------------------- |
| TemplateName | Enter the name of the relevant PII Redaction template.|


#### Example


!!! Example
     - run `java -jar lightrunc.jar list-pii-redaction-patterns
       <TemplateName>`

     ```bash
     java -jar lightrunc.jar list-pii-redaction-patterns demo
     NAME: Tickets TYPE: BY_VALUE PATTERN: com.sales.tickets CASE-INSENSITIVE: false
     ```

### `delete-pii-redaction-pattern`

The `delete-pii-redaction-pattern` command deletes an existing pattern set on a specific PII Redaction template.


#### Synopsis


`java -jar lightrunc.jar delete-pii-redaction-pattern <TemplateName> <PatternName>`


#### Options


| Option | Description |
| -------- | ----------------------------------- |
| TemplateName | Enter the name of the relevant PII Redaction template. |
| PatternName | Enter the name of the relevant pattern. |


#### Example


!!! Example
        - run `java -jar lightrunc.jar delete-pii-redaction-pattern <TemplateName> <PatternName>`

         ```bash
         $ java -jar lightrunc.jar delete-pii-redaction-pattern demo Tickets
         PII redaction pattern 'Tickets' successfully deleted
         ```

## `certificates`

### `show-certificates`

The `show-certificates` command outputs all certificates present in your Lightrun server.

#### Synopsis

`java -jar lightrunc.jar show-certificates`

#### Example

!!! Example
     run `java -jar lightrunc.jar show-certificates`

     ```bash
     $ java -jar lightrunc.jar show-certificates
     ee80811b38e7e6c2dc4cc372cbea86bd86b446b012e427f2e19bf094afba5d12 (PRECONFIGURED)
     ```
### `add-certificate`

The `add-certificate` command adds a new certificate to the Lightrun server.

#### Synopsis

`java -jar lightrunc.jar add-certificate <certificate-sha256-public-key>`

#### Options

| Option      | Description         |
| ----------- | ------------------- |
| `<certificate-sha256-public-key>` | sha256 of the public key of the certificate |

#### Example

!!! Example
     run `java -jar lightrunc.jar add-certificate <certificate-sha256-public-key>` to add a new certificate.

     ```bash
     $ java -jar lightrunc.jar add-certificate <certificate-sha256-public-key>
     Successfully added certificate.
     ```

### `rm-certificate`

The `rm-certificate` command removes a certificate from the Lightrun server.

#### Synopsis

`java -jar lightrunc.jar rm-certificate <certificate-sha256-public-key>`

#### Options

| Option      | Description         |
| ----------- | ------------------- |
| `<certificate-sha256-public-key>` | sha256 of the public key of the certificate |

#### Example

!!! Example
     run `java -jar lightrunc.jar rm-certificate <certificate-sha256-public-key>` to remove a cerficate from the Lightrun server.

     ```bash
     $ lightrunc.jar rm-certificate <certificate-sha256-public-key>
     Successfully removed certificate <certificate-sha256-public-key>

     ```

### `get-pinning-status`

The `get-pinning-status` command returns the Lightrun server certificate pinning status.

#### Synopsis

`java -jar lightrunc.jar get-pinning-status`

#### Example

!!! Example
     run `java -jar lightrunc.jar get-pinning-status`.

     ```bash
     $ java -jar lightrunc.jar get-pinning-status
     Pinning status is disabled
     ```

### `enable-pinning-status`

The `enable-pinning-status` command enables certificate pinning.

#### Synopsis

`java -jar lightrunc.jar enable-pinning-status`

#### Example

!!! Example
     run `java -jar lightrunc.jar enable-pinning-status`

     ```bash
     $ java -jar lightrunc.jar enable-pinning-status
     Certificate pinning is now enabled
     ```

### `disable-pinning-status`

The `disable-pinning-status` command disables certificate pinning.

#### Synopsis

`java -jar lightrunc.jar disable-pinning-status`

#### Example

!!! Example
     run `java -jar lightrunc.jar disable-pinning-status`

     ```bash
     $ java -jar lightrunc.jar disable-pinning-status
     Certificate pinning is now disabled
     ```

## `groups & access`

- The commands in this section are for managing users with the Lightrun Role-based access control (RBAC) feature.
- The Lightrun Role-based access control feature is only available to users on our Enterprise plan; please contact our [support team](https://go.lightrun.com/contact-us)  for more information.


### `create-group`

The `create-group` command creates a group of users.

#### Synopsis

`java -jar lightrunc.jar create-group <Name>`

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Name | The name of the group. |


#### Example

!!! Example
     - run `java -jar lightrunc.jar create-group sysadmins` to create a new group named `sysadmins`.
          ```bash
          $ java -jar lightrunc create-group sysadmins                       
          Group 'sysadmins' (id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b) successfully created
          ```

### `update-group-name`

The `update-group-name` command updates the name of a group.

#### Synopsis

`java -jar lightrunc.jar update-group-name <GroupId> <Name>`

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Group ID | The ID of the relevant group. |
| Name | The group’s new name.|

#### Example

!!! Example
     - run `java -jar lightrunc.jar update-group-name <group id> <new_name>` to update the name of a group.
          ```bash
          $ java -jar lightrunc update-group-name  5f8881b7-3e04-48ab-9bba-b2d1b9870a8b sys-managers
          Group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated
          ```  

### `list-groups`

The `list-groups` command returns a list of all groups available to the current user.

!!! note 
     The `list-groups` command will return all groups in the Lightrun organization if the user is a System Administrator.

#### Synopsis

`java -jar lightrunc.jar list-groups`

#### Example

!!! Example
     - run `java -jar lightrunc.jar list-groups`.
          ```bash
          $ java -jar lightrunc list-groups          
          ID 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b NAME sysadmins USERS COUNT 0 GROUP ADMINS N/A
          ID b1603a77-661c-44c6-89de-dfd1d126f0c9 NAME 664379ed-7b49-472b-9d08-19d2ab3b0c84 USERS COUNT 1 GROUP ADMINS N/A
          Page 1 of 1
          ```

### `list-accesses`

The `list-accesses` command returns the role, elevated users, and agent pools associated with a group.

#### Synopsis

`java -jar lightrunc.jar list-accesses <GroupId>`

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Group ID | The ID of the relevant group. |

#### Example

!!! Example
     - run `java -jar lightrunc.jar list-accesses <GroupId>`.
          ```bash
          $ java -jar lightrunc list-accesses  5f8881b7-3e04-48ab-9bba-b2d1b9870a8b
		  Group "5f8881b7-3e04-48ab-9bba-b2d1b9870a8b" has access to agent-pools [Default Agent Pool] with role "Standard"
          ```

### `update-group-role`

The `update-group-role` command updates the role assigned to a group. 

#### Synopsis
`java -jar lightrunc.jar update-group-role <GroupId> <RoleName>`

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Group ID | The ID of the relevant group. |
| Role Name| The role that should be assigned to the group. A group can be assigned one of the following roles.<br>- Standard<br>- Privileged |

#### Example

!!! Example
     - run `java -jar lightrunc.jar update-group-role <GroupId> <RoleName>`.
          ```bash
          $ java -jar lightrunc update-group-role  5f8881b7-3e04-48ab-9bba-b2d1b9870a8b privileged
          Access to group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated
          ```

### `add-group-members`

The `add-group-members` adds users to a group.

#### Synopsis

`java -jar lightrunc.jar add-group-members <GroupId> [email...]`

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Group ID | The ID of the relevant group. |
| email | The email address of the relevant user. |

#### Example

!!! Example
     - run `java -jar lightrunc.jar add-group-members <GroupId> <email> ` to add a user to a group.

          ```bash
          $ java -jar lightrunc add-group-members 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b user@email.com
          Group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated
          ```

     - run `java -jar lightrunc.jar add-group-members <GroupId> email1 email2` to add multiple users to a group.

          ```bash
          $ java -jar lightrunc add-group-members 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b user1@email.com user2@email.com 
          Group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated
          ``` 


### `remove-group-members`

The `remove-group-members` removes users from a group.

#### Synopsis

`java -jar lightrunc.jar remove-group-members <GroupId> [email...]`

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Group ID | The ID of the relevant group. |
| email | The email address of the relevant user. |

#### Example

!!! Example
     - run `java -jar lightrunc.jar remove-group-members <GroupId> <email> ` to add a user to a group.

          ```bash
          $ java -jar lightrunc remove-group-members 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b user@email.com
          Group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated
          ```

     - run `java -jar lightrunc.jar remove-group-members <GroupId> email1 email2` to add multiple users to a group.

          ```bash
          $ java -jar lightrunc remove-group-members 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b user1@email.com user2@email.com 
          Group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated
          ``` 

### `promote-to-group-admins`

The `promote-to-group-admins` command promotes a user to a group admin role.

#### Synopsis

`java -jar lightrunc.jar promote-to-group-admins <GroupId> [email...]`

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Group ID | The ID of the relevant group. |
| email | The email address of the relevant user. |

#### Example

!!! Example
     - run `java -jar lightrunc.jar promote-to-group-admins <GroupId> <email> ` to promote a user to a group admin.

          ```bash
          $ java -jar lightrunc promote-to-group-admins 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b user@email.com
          Group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated
          ```

     - run `java -jar lightrunc.jar promote-to-group-admins <GroupId> email1 email2` to promote multiple users to group admin.

          ```bash
          $ java -jar lightrunc promote-to-group-admins 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b user1@email.com user2@email.com 
          Group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated
          ```

### `demote-from-group-admins`

The `demote-from-group-admins` command removes a user as a group admin.

#### Synopsis

`java -jar lightrunc.jar demote-from-group-admins <GroupId> [email...]`

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Group ID | The ID of the relevant group. |
| email | The email address of the relevant user. |

#### Example

!!! Example
     - run `java -jar lightrunc.jar demote-from-group-admins <GroupId> <email>` to remove a user as a group admin.

          ```bash
          $ java -jar lightrunc demote-from-group-admins 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b user@email.com
          Group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated
          ```

     - run `java -jar lightrunc.jar demote-from-group-admins <GroupId> email1 email2` to remove multiple users as group admins.

          ```bash
          $ java -jar lightrunc demote-from-group-admins 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b user1@email.com user2@email.com 
          Group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated
          ```

### `duplicate-group`

The `duplicate-group` command duplicates a group of users.

#### Synopsis

`java -jar lightrunc.jar duplicate-group <GroupId> <Name>`

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Group ID | The ID of the group to be duplicated. |
| Name | The name of the duplicate group. |

#### Example

!!! Example
     - run `java -jar lightrunc.jar duplicate-group <GroupId> <Name>`
          ```bash
          $ java -jar lightrunc duplicate-group 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b newgroupname
          Group 'newgroupname' (id: 2d71546a-6f5f-47d4-9754-73ee9ccfc959) successfully created  
          ``` 

### `add-access-to-pools`

The `add-access-to-pools` command grants a group access to an agent pool.

#### Synopsis

`java -jar lightrunc.jar add-access-to-pools <GroupId> <PoolName1> [PoolName1...]`

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Group ID | The ID of the relevant group. |
| PoolName | Agent pool names. |

#### Example

!!! Example
     - run `java -jar lightrunc.jar add-access-to-pools <GroupId> <PoolName1>` to grant access to an agent pool.

          ```bash
          $ java -jar lightrunc add-access-to-pools 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b agentPool1 
          Group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated   
          ``` 
               
     - run `java -jar lightrunc.jar add-access-to-pools <GroupId> <PoolName1> <PoolName2` to grant access to multiple agent pools.

          ```bash
          $ java -jar lightrunc add-access-to-pools 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b agentPool1 agentPool2
          Access to group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated
          ```

### `remove-access-to-pools`

The `remove-access-to-pools` command removes the access that a group has to an agent pool.

#### Synopsis

`java -jar lightrunc.jar remove-access-to-pools <GroupId> <PoolName1> [PoolName2...]`

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Group ID | The ID of the relevant group. |
| PoolName | Agent pool names. |

#### Example

!!! Example
     - run `java -jar lightrunc.jar remove-access-to-pools <GroupId> <PoolName1>` to remove access to an agent pool.

          ```bash
          $ java -jar lightrunc remove-access-to-pools 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b agentPool1 
          Group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated   
          ``` 
               
     - run `java -jar lightrunc.jar remove-access-to-pools <GroupId> <PoolName1> <PoolName2` remove access to multiple agent pools.

          ```bash
          $ java -jar lightrunc remove-access-to-pools 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b agentPool1 agentPool2
          Access to group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated
          ```

### `delete-group`

The `delete-group` command deletes a group.

!!! warning
     A group cannot be restored once deleted.


#### Synopsis

`java -jar lightrunc.jar delete-group <Name>`

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Name | The name of the group. |

#### Example

!!! Example
     - run `java -jar lightrunc.jar delete-group <Name>`
     		```bash
			$ java -jar lightrunc delete-group  8986ca74-7044-438b-840e-2e3a1ae8898f
            Group (id: 8986ca74-7044-438b-840e-2e3a1ae8898f) successfully deleted
			```

## `agent-pool`
- The commands in this section are for managing users with the Lightrun Role-based access control (RBAC) feature.
- The Lightrun Role-based access control feature is only available to users on our Enterprise plan; please contact our [support team](https://go.lightrun.com/contact-us) for more information.

### `create-agent-pool`

The `create-agent-pool` command creates a new agent pool.

#### Synopsis

`java -jar lightrunc.jar create-agent-pool <Name> [Description]`

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Name | The name of the new agent pool. |
| email | Agent pool description. |

#### Example

!!! Example
     - run `java -jar lightrunc.jar create-agent-pool <Name> [Description]`.
     		```bash
			$ java -jar lightrunc create-agent-pool agentPool1 new-agent-pool         
               Agent pool 'agentPool1' (id: 77eb44fc-e2e7-4358-b43d-ad1942b0b7f6) successfully created
			```

### `agent-pool`
The `agent-pool` command specifies the agent pool to be used by the command line. 

#### Synopsis

`java -jar lightrunc.jar agent-pool <AgentPoolId>`

!!! note
     After setting an agent pool with the `agent-pool` command, all results returned by the command line will only be relevant to that agent pool. To run a command for another agent pool, add the `--agent-pool` flag to the command.

     ```bash
     `java -jar lightrunc.jar <current_command> --agent-pool <AgentPoolId>`
     ```

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Agent Pool ID | The ID of the relevant agent pool. |


#### Example

!!! Example
     - run `java -jar lightrunc.jar agent-pool <AgentPoolId>`
     		```bash
			$ java -jar lightrunc agent-pool 77eb44fc-e2e7-4358-b43d-ad1942b0b7f6
               Agent pool set to (id: 77eb44fc-e2e7-4358-b43d-ad1942b0b7f6) successfully. All following commands will use this agent pool.
			```
### `update-agent-pool`

The  `update-agent-pool`  command updates the name or description of the agent pool.

#### Synopsis

`java -jar lightrunc.jar update-agent-pool <AgentPoolId> [Name] [Description]`

#### Options

| Option | Description |
| -------- | ----------------------------------- |
| AgentPoolId | The ID of the relevant agent pool. |
| Name | Enter the new name for the relevant agent pool. |
| Description | Enter the new description. |

#### Example

!!! Example
     - run `java -jar lightrunc.jar update-agent-pool 385ee7e7-c526-41e6-9e70-ec4aee16abe3 Demo "New description"`
  
               $ java -jar lightrunc.jar update-agent-pool <AgentPoolId> [Name] [Description]
               
### `delete-agent-pool`

The `delete-agent-pool` command deletes an agent pool.

!!! warning
     An agent pool cannot be restored once deleted.

#### Synopsis

`java -jar lightrunc.jar delete-agent-pool <AgentPoolId>`

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Agent Pool ID | The ID of the relevant agent pool. |

#### Example

!!! Example
     - run `java -jar lightrunc.jar delete-agent-pool <AgentPoolId>`
     		
               
			$ java -jar lightrunc delete-agent-pool 2f60469f-787b-41a0-8f39-5b4ae01c8495
               
	
### `assign-pii-redaction-to-agent-pool`

The  `assign-pii-redaction-to-agent-pool` assigns an PII redaction template to an agent pool.

#### Synopsis

`java -jar lightrunc.jar assign-pii-redaction-to-agent-pool <AgentPoolId> <PIIRedactionName>`

#### Options


| Option | Description |
| -------- | ----------------------------------- |
| AgentPoolId | The ID of the relevant agent pool. |
| PIIRedactionName | Enter the name of the PII redaction template. |


#### Example


!!! Example
     - run `java -jar lightrunc.jar assign-pii-redaction-to-agent-pool <AgentPoolId> <PIIRedactionName>`
          ```bash
          java -jar lightrunc.jar assign-pii-redaction-to-agent-pool 6245f7aa-3132-4799-98a0-020bc9b606ab demo
          Agent pool (id: 6245f7cc-3132-4799-98a0-030bc9b606ab) successfully updated
          ```
### `get-agent-pool-key` 

This `get-agent-pool-key` command gets the agent API key associated with the given
agent pool. By default, it prints asterisks and copies the key to clipboard. To print
the key to stdout, use `-o text`.

#### Synopsis

`java -jar lightrunc.jar get-agent-pool-key <PoolId>`

#### Options


| Option | Description |
| -------- | ----------------------------------- |
| PoolId | The ID of the relevant agent pool. |


#### Example


!!! Example
     - run `java -jar lightrunc.jar get-agent-pool-key <PoolId>`

                     ```bash
                     $ java -jar lightrunc.jar get-agent-pool-key 823007b4-8782-11ed-8e17-0a666cdc13c9
                                  *********************************72b (Copied to clipboard)
                     ```



## `roles`
- The commands in this section are for managing users with the Lightrun Role-based access control (RBAC) feature.
- The Lightrun Role-based access control feature is only available to users on our Enterprise plan; please contact our [support team](https://go.lightrun.com/contact-us) for more information.
### `list-roles`

The `list-roles` command outputs all roles and their permissions.

#### Synopsis

`java -jar lightrunc.jar list-roles`

#### Example 

!!! Example
     - run `java -jar lightrunc.jar list-roles`
     		```bash
			$ java -jar lightrunc list-roles                            
            ID 5ad5a113-05d1-4033-9dba-20346dee2477 NAME Standard PERMISSIONS [STANDARD]
            ID d5e25064-7321-4f37-824d-369430a205b3 NAME Privileged PERMISSIONS [STANDARD, IGNORE_QUOTA]
			```

### `add-elevated-roles`
The `add-elevated-roles` command grants a user an elevated role.

#### Synopsis

`java -jar lightrunc.jar add-elevated-roles <GroupId> <Email>:<RoleName> [Email:RoleName...]`

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Group ID | The ID of the relevant group. |
| Email | The email of the relevant user. |
| RoleName | The new role to be assigned to the user |

#### Example 

!!! Example
     - run `java -jar lightrunc.jar add-elevated-roles <GroupId> <Email>:<RoleName>` to grant a user an elevated role.

          ```bash
          $ java -jar lightrunc add-elevated-roles 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b user@email.com:Privileged 
          Access to group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated  
          ``` 
               
     - run `java -jar lightrunc.jar add-elevated-roles <GroupId> <Email>:<RoleName> [Email:RoleName...]` to grant multiple users in a group elevated roles.

          ```bash
          $ java -jar lightrunc add-elevated-roles 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b user@email.com:Privileged  user1@email:Privileged
          Access to group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated
          ```

### `remove-elevated-roles`

The `remove-elevated-roles` command removes the elevated role assigned to a user.

#### Synopsis

`java -jar lightrunc.jar remove-elevated-roles <GroupId> <Email1> [Email2...]`

#### Options

| Option      | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| Group ID | The ID of the relevant group. |
| Email | The email of the relevant user. |

#### Example 

!!! Example
     - run `java -jar lightrunc.jar remove-elevated-roles <GroupId> <Email>` to remove the elevated role granted to a user.

          ```bash
          $ java -jar lightrunc remove-elevated-roles 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b user@email.com
          Access to group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated  
          ``` 
               
     - run `java -jar lightrunc.jar remove-elevated-roles <GroupId> <Email> [Email..]` to remove the elevated role granted to multiple users.

          ```bash
          $ java -jar lightrunc remove-elevated-roles 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b user@email user1@email
          Access to group with id: 5f8881b7-3e04-48ab-9bba-b2d1b9870a8b successfully updated
          ```