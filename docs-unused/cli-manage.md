# Administration from the CLI

From the Lightrun CLI, managers can [run administrator commands](#lightrun-cli).

--8<-- "ux-reference/manager-role-only.md"

!!! imp "Important"
     
	 If the file name and line number don't match the bytecode version of the app, Lightrun will behave inconsistently and will most likely fail. 

## Set up your CLI

--8<-- "ux-reference/cli-setup.md"

## Administrator commands {#lightrun-cli}

### `create-user`

#### Description

`create-user` creates a new user based on the specified details.

#### Synopsis

```bash
java -jar lightrunc.jar create-user <Username> <FirstName> <LastName> <Email> <Role1> <Role2>...-companyName <YOUR_COMPANY_NAME>
```

#### Options

| Option   | Description                                                  |
| -------- | ------------------------------------------------------------ |
| `Username` | A unique name for the user                                   |
| `Email`    | A valid and unique email address                             |
| `Role`     | Valid values: <br>`ROLE_ADMIN` <br>`ROLE_MANAGER`  <br>`ROLE_USER`  <br> `ROLE_SET_VALUE`<br> `ROLE_IGNORE_QUOTA` |

#### Output and examples

!!! example

     The following creates a new user with the **User** role for Dr. Dolittle with the user name dolittle when a Manager from the company DoctorCom runs the command.
    
     ```
     java -jar lightrunc.jar create-user dolittle Dr. Dolittle dolittle@doctor.com ROLE_USER
     ```
     
     When you press **Enter**, the terminal requests a password for the new user. 
     
     Enter a password, press **Enter** and the terminal prints: 
     
     `User successfully created in company DoctorCom`

### `delete-user`

#### Description

Delete a specified user.

!!! note
    The user must first be deactivated before they can be deleted. Deactivate directly from the Management Portal by navigating to Manager->User management.

#### Synopsis

```bash
java -jar lightrunc.jar delete-user <username>
```

#### Options

`username` - the email address associated with the user that is to be deleted

!!! warning
     Once deleted, the user cannot be restored.

#### Output and examples

!!! example

    ```bash
    java -jar lightrunc.jar delete-user SMITHJ@acme.com
    ```
    The following is printed to the terminal: `User Deleted`

### `clear-exceptions`

#### Description

Clear all exceptions from history.

#### Synopsis

`java -jar lightrunc clear-exceptions`

#### Options

None

#### Output and examples

The following output is printed to the terminal:

`Successfully cleared exceptions history from the server `
