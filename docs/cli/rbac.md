# Lightrun RBAC CLI Commands

This reference describe the Lightrun CLI commands, options, and parameters available to Lightrun Administrators.

## Prerequisites

This tutorial assumes that you have:

- [Created your Lightrun account.](https://app.lightrun.com/)
- [Installed the Lightrun CLI on your local machine.](/cli/installation/)
- [Authenticated the Lightrun CLI](/cli/authentication/)

## Before your begin

- The commands in this reference are for managing users with the Lightrun Role-based access control (RBAC) feature.
- The Lightrun Role-based access control feature is only available to users on our Enterprise plan; please contact our [support team](https://go.lightrun.com/contact-us)  for more information.
- Make sure to read the [User management concepts](/rbac/concepts/) guide before starting this tutorial to have a basic understanding of how user management works in Lightrun.

## `groups & access`

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

     - run `java -jar lightrunc.jar add-group-members <GroupId> email1, email2` to add multiple users to a group.

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

     - run `java -jar lightrunc.jar remove-group-members <GroupId> email1, email2` to add multiple users to a group.

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

     - run `java -jar lightrunc.jar promote-to-group-admins <GroupId> email1, email2` to promote multiple users to group admin.

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

     - run `java -jar lightrunc.jar demote-from-group-admins <GroupId> email1, email2` to remove multiple users as group admins.

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
     		```bash
			$ java -jar lightrunc delete-agent-pool 2f60469f-787b-41a0-8f39-5b4ae01c8495
			```

## `roles`
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