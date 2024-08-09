# Manage users and roles

--8<-- "ux-reference/manager-role-only.md"

!!! tip
     You can also manage users directly from the agent.config file or from the terminal. See [the CLI reference](/cli/manager_cli_reference/) for more details.

Administrators can manage users and their permissions as follows:

- [Onboard new users and view pending invitations](#onboard)

- [Manage existing users](#permissions)

###### To navigate to Users management in the Management Portal {#navigate}

1. Log in to your Lightrun account.
2. Click **Settings** located at the bottom left corner of your Management Portal.
3. Select **Users** under **Identity and Access Management**.
The **Users Management** screen loads and appears similar to the following:

![User management](assets/images/users-management.png)

## Onboard new users {#onboard}
To onboard new users to Lightrun, you need to invite them first. Once they join the organization's account, you can give them the relevant permissions. 
######  To invite new users to your Lightrun account

1. Log in to your Lightrun account.
2. Click **Invite member** located at the bottom left corner of your Management Portal.
    The **Invite member** screen loads and appears similar to the following:
    ![Invite users -half](assets/images/invite-users.png)
    The Invite member page offers two ways to invite users:

  - **Invite new users**
  - **Pending Invites**

3. To invite users, you can: 
   - Copy and send the invite link to the users in a secure manner of your choice. 
     If you cannot see this option, check that the **Self Service** feature is enabled in the **Identity and Access Management** > **Identity Configuration** page.
   - Enter the intended email addresses separated by commas and then click **Send**

Once the user receives the invitation, by mail or through the invite link, they will be redirected to a registration page. They can create their account, and log in to access their Management Portal.

Invited users who have registered their accounts can be seen on the **Users Management** page. The list of your pending invitations can be seen in the **Pending Invites** section.

## Manage existing users {#permissions}

Administrators can create, edit, and remove users. Administrators can also assign users roles that can help the user perform specific actions. The following table describes the available roles and their permitted actions:

| Roles    | Permissions                                             |
| --------- | ------------------------------------------------------------ |
| `role_manager` | Additional capabilities enabling server and user management, such as creating and removing users, clearing exceptions, managing integrations, etc.|
|`role_ignore_quota` | Permissions to ignore the system quota; the quota controls use of CPU, Networking, Memory, excessively long strings, too many instructions printing out, protection from infinite loops, etc. |
|`role_user`  | Standard permissions to insert actions and view resulting data. |

###### To create a new user

1. [Navigate](#navigate) to the User Management screen. 
2. Click **Create new user**.
   The **Edit User** window pops up with empty fields.
3. Complete the fields with relevant details. 
  ![Create user -quarter](assets/images/create-user.png)
4. To enable the user immediately, toggle the **Activated** button to green. 
5. Add [permissions](#permissions) from the **User Roles** window: click on the relevant role. To add multiple roles, press `CTRL` or `command` on mac, and click on the relevant roles.

###### To view user details

You can view the permissions and details that were entered for a user when created or modified, as well as the creation and modification details. 

1. [Navigate](#navigate) to the **User Management** screen. 
2. From the row for the relevant user click the ![View user](assets/images/eye.png){: style="height:25px;width:30px"} **View Icon**.
    The **User** details window pops up.  

###### To edit existing users 

1. [Navigate](#navigate) to the User Management screen. 
2. From the row for the relevant user click ![Edit user](assets/images/pencil.png){: style="height:25px;width:25px"} **Edit Icon**.
    The **Edit User** window pops up with empty fields.
3. Complete the fields with relevant details. 
	![Create user -quarter](assets/images/create-user.png)
4. To activate or deactivate the user, toggle the **Activated** button to green. 
5. Add or remove [permissions](#permissions) from the **User Roles** window: click on the relevant role to add or remove it. To add multiple roles, press `CTRL`, and then click on the relevant roles.

###### To remove a user 

1. [Navigate](#navigate) to the User Management screen. 

2. From the row for the relevant user, toggle the Active button to grey.

    The **Delete** icon now appears on the row.

3. Click ![Delete user](assets/images/delete.png){: style="height:25px;width:25px"}.

    The **Confirm** window pops up:

    ![Delete user -third](assets/images/confirm-delete.png)

4. When prompted, click **Delete** to remove the user.
