# Lightrun Manager CLI Commands

This reference describe the Lightrun CLI commands, options, and parameters available to Lightrun Administrators.

--8<-- "ux-reference/manager-role-only.md"

## Prerequisites

This tutorial assumes that you have:

- A Lightrun account.
- [Installed the Lightrun CLI on your local machine.](/cli/installation/)
- [Authenticated the Lightrun CLI](/cli/authentication/)

## `user`

### `create-user`

The `create-user` command creates a new user based on the specified details.

#### Synopsis

```bash
java -jar lightrunc.jar create-user <FirstName> <LastName> <Email> <Role1> <Role2>...-companyName <YOUR_COMPANY_NAME>
```

#### Options

| Option   | Description                                                  |
| -------- | ------------------------------------------------------------ |
| `Username` | A unique name for the user                                   |
| `Email`    | A valid and unique email address                             |
| `Role`     | Valid values: <br>`ROLE_ADMIN` <br>`ROLE_MANAGER`  <br>`ROLE_USER` ela na<br> `ROLE_IGNORE_QUOTA` |

#### Example

!!! Example

	 The following creates a new user with the **User** role for Dr. Dolittle with the user name dolittle when a Manager from the company DoctorCom runs the command.
    
     ```
     java -jar lightrunc.jar create-user dolittle Dr. Dolittle dolittle@doctor.com ROLE_USER
     ```
     
     When you press **Enter**, the terminal requests a password for the new user. 
     
     Enter a password, press **Enter** and the terminal prints: 
     
     `User successfully created in company DoctorCom`

### `delete-user`

The `delete-user` command deletes a specified user.

!!! warning
     A user cannot be restored once deleted.

!!! note
    The user must first be deactivated before they can be deleted. Deactivate directly from the Management Portal by navigating to Manager->User management.

#### Synopsis

```bash
java -jar lightrunc.jar delete-user <username>
```

#### Options

| Option   | Description                                                  |
| -------- | ------------------------------------------------------------ |
| `Username` | the email address associated with the user that is to be deleted             |


#### Example

!!! Example

    ```bash
    $ java -jar lightrunc.jar delete-user SMITHJ@acme.com
	User Deleted
    ```