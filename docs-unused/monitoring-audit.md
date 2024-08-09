# Monitoring Audit Logs
Lightrun maintains a record of your organization's Lightrun system usage, which is crucial for observing continuous compliance, performing system audits, and maintaining security.

The stored audit logs include data about activities related to the Management Portal, Lightrun plugins, and agents. With the Lightrun audit logs, you can answer questions such as:

- How is a specific user in your organization using Lightrun?
- What changes have been made to your organization’s account, and when?
- Who made a particular change, and when?
- Who created an agent or action, and when?

## Viewing audit logs
Lightrun captures all events made by every user associated with your organization and stores the event in Amazon S3 buckets in a Syslog file format. Please [contact our team](https://go.lightrun.com/contact-us) for access to your organization’s audit log Amazon S3 bucket.

You can also view a brief overview of all captured events in your Management portal. Follow the instructions [here](/audit-use/) for information on how to audit Lightrun system usage directly from your Lightrun Management Portal.

--8<-- "ux-reference/manager-role-only.md"

## Audit log retention

The audit logs S3 buckets are updated daily and have a default retention period of 24 months. Please [contact our support team](https://go.lightrun.com/contact-us) for more information on configuring your organization’s audit logs retention period.

## Audit log format

Lightrun Audit logs data are stored in Amazon S3 in a Syslog file format. The following code sample describes an example audit log for an agent-removed event.

```bash linenums="1"
1 2022-08-29T12:19:51Z 10.50.29.9 Lightrun 72850 
[actorId=d885cc7b-344f-44aa-a853-0a261a844d8d eventType=delete event=REMOVED_AGENT_SUCCESS outcome=success]
[runtime_environment=Java agent_id=d885cc7b-344f-44aa-a853-0a261a844d8d agent_name=shiran-Latitude-7410 (pid 72850) api_version=1.7 log_piping=BOTH agent_os=linux agent_pid=72850 agent_version=1.7.0-rc4.de87b07b3]
```

The Syslog message has the following format:

- [Header (Line 1)](#header)
- [Structured Data (Line 2)](#data)
- [Message (Line 3)](#message)

#### Header {#header}
The Header is the first part of the audit log data. The following table describes the data in the Header part of the audit log data.

|Data|Description|
|--|--|
|Version|Syslog protocol version|
|TimeStamp|The time when the audit log was created in an [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format.|
|HostName|The machine that sent the events data|
|PROCID|The log Process ID  which can be used to further identify the sender of the audit log.|
|MSGID| Audit log message ID.<br>- `authn`<br>- `creation`<br>- `access`<br>- `change`<br>- `deletion`|

#### Structured Data {#data}

The following table describes the data in the Structured Data part of the audit log.

|Data|Description|
|--|--|
|Actor type|Event actor, can be: <br>- `Agent`<br>- `System`<br>- `User`|
|Actor ID|Event actor ID. For example, User ID, Agent ID, or System ID.|
|Event| The event that created the audit log. See [Events Type](#events) below for a list of all events audited by Lightrun.|
|Event Type|Event type, can be: <br>- `authentication` <br>- `creation` <br>- `access` <br>- `change` <br>- `deletion`|
|Outcome|Event outcome, can be: <br>- `success` <br>- `failure` <br>- `unknown` |
|Target|Event target.|
|Details| Event details.|

#### Message {#message}

Events metadata. See [Events Type](#events) below for a list of all events audited by Lightrun and their metadata.

## Events Type {#events}
This section describes all events stored by Lightrun in the audit logs data and their corresponding metadata.

#### Authentication Events

|Event|Actor|Description|Metadata|
|--|--|--|--|
| `User login`|User|User has logged in successfully or failed login attempt due to an `error_message`.| User Metadata|
| `User logout`|User| User logged out.| User metadata|

#### Organization Management Events

|Event|Actor|Description|Metadata|
|--|--|--|--|
| `User creation`| User, System| New user was created successfully or failed due to an `error_message`.| User Metadata|
| `USERS_INVITED`| User| New user was invited successfully or failed due to an `error_message`. | User Metadata|
| `USERS_DELETED` | User | User was deleted successfully or failed due to an `error_message`. | User Metadata|
| `Renamed organization` | User | Organization was renamed successfully or failed due to an `error_message`. | User Metadata|
| `Changed plan` | User | Organization's plan was changed successfully or failed due to an `error_message`. | User Metadata|
| `Pro_TRIAL_START`| System | Organization started Lightrun PRO TRIAL. | User Metadata |
| `PRO trail ended` | System | Lightrun PRO TRIAL ended. | User Metadata |
| `Tag creation`| System | New METADATA TAG added to organization’s account.| User Metadata |

#### Agent Management Events

|Event|Actor|Description|Metadata|
|--|--|--|--|
| `Version update`| Agent | Agent version updated successfully or failed due to an `error_message`.| Agent Metadata|
| `REGISTERED`| Agent | New agent registered successfully or failed due to an `error_message`.| Agent Metadata|
| `DOWNLOADED`| Agent | Agent downloaded successfully or failed due to an `error_message`.| Agent Metadata|
| `REMOVED`| Agent | Agent deleted successfully or failed due to an `error_message`.| Agent Metadata|

#### Lightrun Action Events

**User actions**

|Event|Actor|Description|Metadata|
|--|--|--|--|
|`ADDED`|User| Action was added successfully by user or failed due to an `error_message`.| Action Metadata|
|`DISABLED`|User| Action was disabled successfully by user or failed due to an `error_message`.| Action Metadata|
|`REMOVED`|User|Action was deleted successfully by user or failed due to an `error_message`.| Action Metadata|
|`ENABLED`|User| Action was enabled successfully by user or failed due to an `error_message`.| Action Metadata|
|`HIT`|User| Action hit was captured successfully by user or failed due to an `error_message`.| Action Metadata|
|`LOAD`|User| Action was loaded successfully by user or failed due to an `error_message`.| Action Metadata|
|`SAVED`|User|Action was saved successfully by user or failed due to an `error_message`.| Action Metadata|
|`UPDATED`|User| Action was edited successfully by user or failed due to an `error_message`.| Action Metadata|

**Agent actions**

|Event|Actor|Description|Metadata|
|--|--|--|--|
|`ADDED`|Agent| Action was inserted successfully or failed due to an `error_message`. | - Action Metadata <br> - Agent Metadata <br> - User Metadata|
|`DISABLED`|Agent|Action was disabled successfully or failed due to an `error_message`. | - Action Metadata <br> - Agent Metadata <br> - User Metadata|
|`REMOVED`|Agent| Action was removed successfully or failed due to an `error_message`. | - Action Metadata <br> - Agent Metadata <br> - User Metadata|
|`ENABLED`|Agent|Action was enabled successfully or failed due to an `error_message`. | - Action Metadata <br> - Agent Metadata <br> - User Metadata|
|`HIT`|Agent|Action hit was captured successfully or failed due to an `error_message`. | - Action Metadata <br> - Agent Metadata <br> - User Metadata|
|`LOAD`|Agent|Action was loaded successfully or failed due to an `error_message`. | - Action Metadata <br> - Agent Metadata <br> - User Metadata|
|`SAVED`|Agent|Action was saved successfully or failed due to an `error_message`. | - Action Metadata <br> - Agent Metadata <br> - User Metadata|
|`UPDATED`|Agent|Action was updated successfully or failed due to an `error_message`. | - Action Metadata <br> - Agent Metadata <br> - User Metadata|

#### Service Configuration Events

|Event|Actor|Description|Metadata|
|--|--|--|--|
|`DATA_REDACTION_ADDED`|User|New data redaction was added successfully or failed due to an `error_message`.|User Metadata|
| `DATA_REDACTION_REMOVED`|User| Data redaction was removed successfully or failed due to an `error_message`.|User Metadata|
| `DATA_REDACTION_UPDATED`|User| Data redaction was updated successfully or failed due to an `error_message`.|User Metadata|
|`BLOCKLIST ADDED`|User| Blocklist was added successfully or failed due to an `error_message`.|User Metadata|
| `BLOCKLIST REMOVED`|User| Blocklist was removed successfully or failed due to an `error_message`.|User Metadata|

#### Integrations Events
|Event|Actor|Description|Metadata|
|--|--|--|--|
| `ENABLED`|User| New integration was added successfully or failed due to an `error_message`.  |User Metadata|
| `DISABLED`|User| Integration was disabled successfully or failed due to an `error_message`.|User Metadata|

### Events Metadata

#### User Metadata

The following table describes the data available in the User metadata.

|Data|Description|
|--|--|
| `user_id` | User ID value. |
| `user_name` | User name. |
| `user_types` | User type. |
| `user_group` | User group. |

#### Action Metadata

The following table describes the data available in the Action metadata.

|Data|Description|
|--|--|
| `action_type`| Action type: <br>- Log <br>- Metrics <br>- Snapshot |
| `action_id` | Action ID. |
| `condition` | Action conditions. |
| `expression` | Action expression. |
| `file_name, line` | Action filename and line. |
| `ignore_qouta` | Action `ignore_qouta` configuration. |
| `max_hit_count` | Action `max_hit_count` value. |

#### Agent Metadata

The following table describes the data available in the Agent metadata.

|Data|Description|
|--|--|
| `agent_api_version` | Agent API version.|
| `agent_ip` | Agent IP address. |
| `agent_id` | Agent ID value. |
| `agent_name` | Agent name. |
| `agent_os` | Agent OS. |
| `agent_pid` | Agent PID value. |
| `agent_version` | Agent version. |
| `runtime environment` | Runtime environment. |
| `log_piping` | Agent configured routing value. |
| `source` | Agent source. |