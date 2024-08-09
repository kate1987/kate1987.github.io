# Manage groups with RBAC

A group represents a group of users in Lightrun. Using [RBAC (Role-Based Access Control)](rbac/overview.md), you can set up Lightrun groups to manage users that all need the same access and permissions to a particular resource, like an agent pool. For example, you can create a group for your DevOps team and grant privileged access to all DevOps-related agent pools to the group instead of adding permissions for each individual user.

When you create a Lightrun account, your organization is assigned a default group and agent pool. The default group has Standard role to the default agent pool and comprises every user in your organization. Users with a System admin role can create and assign users to groups. 

## What to know before working with groups

### Groups grant users access to agent pools

Before a user can access agents in an agent pool, the user must be part of a group with access to that agent pool. The amount of access the user has to the agent pool depends on the role assigned to the group. There are two roles in Lightrun.

- **Standard Role** - The standard role grants regular access to an agent pool. This includes creating Lightrun actions with the agents in the agent pool, full access to action data, etc. 

- **Privileged Role** - The privileged role grants a group the ability to ignore agent quota limitations in addition to the permissions granted by the Standard role. 

!!! note
	Lightrun roles are predefined and are not editable.

![Rbac example](../assets/images/rbac-example.png)

### Administrative levels enable the effective management of your Lightrun organization

Administrative levels are roles assigned to individual users for the effective management of your organization in Lightrun.

There are three administrative levels in Lightrun:

- System Administrator
- Group Administrator
- Member

The following table describes each administrative level and the amount of access and privileges they grant.

| Action type | System Administrator | Group Administrator | Member |
|-------------|----------------------|---------------------|--------|
| Invite users | &check; | &cross; | &cross; |
| Add or remove users from a group | &check; | &check; (Only for groups the group admin belongs to.) |  &cross; |
| Promote other members to group admins | &check; | &check; (Only for groups the group admin belongs to.) |  &cross; |
| Manage groups, role, and agent pools | &check; | &check; (Only for groups the group admin belongs to.) |  &cross; |
| Service Configuration | &check; | &cross; | &cross; |
| Audit Events | &check; | &cross; | &cross; |
| Logs Collector | &check; | &cross; | &cross; |
| Integrations | &check; | &cross; | &cross; |
| PII Redaction | &check; | &cross; | &cross; |
| Blocklist | &check; | &cross; | &cross; |
| Name and Plan editor |&check; | &cross; | &cross; |
| Email Configuration | &check; | &cross; | &cross; |

### Elevated Roles grant members of a group more access than others

In addition to the role assigned to a group, individual users can also be assigned elevated roles. Elevated roles grant group members more privileges than others. A DevOps group might have a standard role, but a single user can be granted an elevated privileged role. This elevated privileged role allows them to perform certain actions, like ignoring the preset agent quota limitations, which other group members cannot.

![Rbac example](../assets/images/rbac-example1.png)