# 2021-2022 Release Notes

Here's where you'll find Lightrun release notes for 2022, including the main highlights, enhancements and fixes made to each version as it is released.

To access the latest release notes, see [Lightrun release notes](/release_notes/lightrun-release-notes/).

## November 2022

### Version 1.8.3

Release Date: November 29, 2022 (SaaS)

#### Features & Changes

#### JetBrains Plugin

- We have increased the JetBrains plugin request timeout value. This increase will help to prevent client-side socket timeout errors thrown when a heavy snapshot hit is captured.

- The performance of the Jetbrains plugin Lightrun snapshot tool window has been improved. Snapshot hits load faster, and we have made it easier to navigate between hits in the improved tool window.

#### Node Agent

- We have fixed some security vulnerabilities found in the Node.js agent.
- We have fixed a bug in the Node.js agent lightrun serverless module that causes  AWS Lambda functions to crash.

#### Management Portal

- We have made UI improvements to the Management Portal registration page.
- Editing a user role in the Lightrun Management Portal no longer requests a password change.
- The `Max Snapshot Variables Depth` service configuration property has been removed from the management portal.

---

### Version 1.8

Release Date: November 6, 2022 (SaaS and On Premise)

#### Features & Changes

#### General

- We have added a new Lightrun action source option called Custom Sources. A Custom Source is a dynamic group of agents and tags defined by a set of conditions, like a shared property. Using a Custom Source, you can create a dynamic list of similar agents and tags depending on the set conditions and simultaneously apply Lightrun Logs, Metrics, and Snapshots to the list. For more information, see [Custom Sources](/actions/custom-sources/).

#### JetBrains Plugin

- We have made user interface improvements to the JetBrains plugin. Design enhancements have been made to the JetBrains plugin entry UI; you can now right-click on an error balloon to view more information about the error and search a Snapshot stack trace and variables.

#### VSCode Plugin

- We have implemented a filter only my actions feature that allows you to display only actions created by you, and snapshot data are now default sorted by recently hit.

#### JVM Agent

- We have added support for Invoke Dynamic to the Lightrun JVM agent. This feature, when enabled, allows a user to add expressions or conditions whose bytecode contains invokedynamic instruction to a Lightrun action. This includes Java expressions and conditions containing Lambda expressions and String concatenations using the ‘+’ character. For more information, see [Invokedynamic](/jvm/agent-configuration/#invokedynamic-support).

- The exception monitoring feature has been removed from the Lightrun JVM agent.
- The JVM agent is now compatible with custom log handlers like the [SLF4J](https://www.slf4j.org/) handler. For more information, see the [JVM agent configuration](/jvm/agent-configuration/#agent-flags).

#### Python Agent

- The Lightrun Python agent now supports Python 3.10.0 on Alpine Linux.
- We have added a new Python agent configuration property called `max_snapshot_buffer_size_in_bytes`. This property allows users to control the Lightrun Python agent snapshot buffer size. For more information, see [Python agent configuration](/python/agent-configuration/).

#### Node Agent

- We have added a Node.js agent module called lightrun_serverless for running Lightrun with Serverless Frameworks. The Lightrun serverless module wraps around serverless functions and ensures the Lightrun agent is enabled before starting the serverless function. It also disables the Lightrun agent when the function call finishes. For more information, see [Serverless Functions](/node/frameworks/serverless).

#### Management Portal

- UI/UX improvements for the Management portal.

- We have added a new Service configuration property called `Max Snapshot Variables Depth`. This property allows users with `ROLE_MANAGER `permissions to configure the amount of data displayed in snapshot variables directly from their Management Portal. For more information, see [Service configuration](/service-configuration/).

- We have added more events to the Lightrun audit logs. For more information, see [Audit System Use](/audit-use/).

- We have added the Lightrun Python agent Windows installation script to the On-Prem web UI.


#### Bug Fixes

- Fixed incorrect Typescript agent installation instructions in the Management Portal.
- Fixed clicking on a snapshot frame navigates users to a different class. 
- Fixed Java agent `lightrun_extra_class_path` configuration not working in windows.
- Fixed Python serverless decorator not working.
- Fixed error messages do not appear for expressions with errors in the VSCode plugin.
- Fixed Python agent snapshot containing variables from third-party packages.
- Fixed security vulnerabilities in the Lightrun server.
- Fixed Lightrun actions not default sorted by newer actions in plugins.

---

## August 2022

### Version 1.7.0

Release Date: August 29, 2022 (SaaS)

#### Features & Changes

#### General

* We have added a new Dynamic Logs and Metrics configuration property called `Target` that allows you to configure where you want to view your action output. There are two configuration options.
  - **Stdout** - action output is routed only to the application's standard output.
  - **Plugin** - action output appears in the Lightrun Console, Lightrun Management Portal, and configured integrations like Slack, Prometheus, etc.

  Also, the current agent routing option has been deprecated. For more information, see [action target routing](/actions/output-routing/).

*  The Lightrun Audit Log has been improved. The audit log format has been enhanced to include more system-level configuration-related actions, and events unrelated to auditing purposes have been removed from the audit logs. We have also added an option to export audit log events into an Amazon S3 bucket in a Syslog message format for further analysis.

* The JetBrains Lightrun Snapshot tool window and the VSCode Lightrun Console now display snapshot watch expressions before other variables. This change will make exploring your snapshot stack trace and variables in your IDE easier.

* UI/UX improvements for the new action forms.
  - Implement autofocus on the **Format** field.
  - Implement support for recently used agents and tags.

#### Management Portal

- UI/UX improvements for the Management portal.

- We have added a new Service configuration property called `Plugin send source full path`. This property enables users with `ROLE_MANAGER` permissions to enable or disable the Lightrun Plugin `Send Source Full Path` option directly in their Management Portal. For more information, see [Service configuration](/service-configuration/).

#### Python Agent

- The Lightrun Python agent now supports Python 3.10.0.

- The Lightrun Python agent now supports Windows OS! You can now create Lightrun actions (dynamic logs, metrics, and snapshots) using the Python agent directly on your Windows PC. For more information, see the Python agent [system requirements](/python/system-requirements/).

- We have added a new Python agent decorator called `lightrun_serverless` for running Lightrun with Serverless Frameworks like AWS Lambda. The Lightrun serverless decorator wraps around serverless functions and ensures that the Lightrun agent is enabled before starting the serverless function. It also disables the Lightrun agent when the function call finishes so that it can handle the next call to the serverless function. For more information, see [Serverless Functions](/python/frameworks/serverless/).

#### Node Agent

- Lightrun plugins now send the full path of a Javascript file to the Lightrun Node.js agent instead of the filename only. This option is enabled by default and helps to solve the Node.js agent `Multiple files match the path specified`. For more information, see the [Node.js agent troubleshooting guide](/troubleshooting/).

#### Bug Fixes

- Fixed Python agent crashes when creating or removing breakpoints.
- Fixed Node.js agent disappearing from up and running pods.
- Fixed Lightrun Server URL empty when VSCode plugin is downloaded from the VSCode marketplace.

---

## July 2022

### Version 1.6.0

Release Date: July 19, 2022 (SaaS and On Premise)

#### Features & Changes

#### Node Agent

- Previously, the Node.js agent quota had a default `MaxConditionCost` of `0.01` and a `MaxCPUCost` of `0.03`. The default values have now been increased to `1.0`  for  `MaxConditionCost` and `1.0` for `MaxCPUCost`. For more information, see [Node.js agent quota configuration](/node/agent-configuration/#quota). 

#### Python Agent

- Previously, the Python agent quota had a default `max_condition_cost` of `0.1` and a `max_log_cpu_cost` of `0.1`. The default values have now been increased to `1.0` for  `max_condition_cost` and `1.0` for `max_log_cpu_cost`. For more information, see [Python agent configuration parameters](/python/agent-configuration/#configuration-parameters).

- Lightrun plugins now send the full path of a Python file to the Lightrun Python agent instead of the filename only. This option is enabled by default and helps to solve the Python agent `Multiple modules matching %` error. For more information, see [Python agent troubleshooting guide](/troubleshooting/).

#### JVM Agent

- Previously, the JVM agent quota had a default `max_condition_cost` of `0.1` and a `max_log_cpu_cost` of `0.1`. The default values have now been increased to `1.0` for `max_condition_cost` and `1.0` for `max_log_cpu_cost`. For more information, see [JVM agent flags configuration](/jvm/agent-configuration/#agent-flags).

#### GitHub1s and GitHub.dev support

- The Lightrun VSCode.dev plugin now supports [GitHub1s](https://github.com/conwnet/github1s) and [GitHub.dev](https://github.com/github/dev) web editors. For more information, see [Lightrun for VSCode.dev](/vscode/vscode-dev/). 

#### Management Portal

- We have added a service configuration property called **Source Version Warnings Enabled** that allows users with `ROLE_MANAGER` permissions to disable IDE `source version warnings` to all users in their organization. For more information, see [Service configuration](/service-configuration/).

- UI/UX improvements to the Multi-tenant SSO user flows.

#### Bug Fixes

- Fixed VSCode plugin expired access token not automatically refreshing.
- Fixed new users are assigned different company IDs when they register with Google in their invite link.
- Fixed `lightrun.enable` not working when using the Python multiprocessing library in fork mode.

--

## June 2022

### Version 1.5.3

Release Date: June 19, 2022 (SaaS and On Premise)

#### Bug Fixes
- Fixed Windows OS Node.js agent installation instructions on the Management Portal.
- Fixed disabled metrics action in the Lightrun submenu when you right-click on the Lightrun action gutter icons in the JetBrains IDE.

---

## May 2022

### Version 1.5

Release Date: May 30, 2022 (SaaS and On Premise)

#### Features & Changes

#### Web IDEs

- Lightrun now supports web IDEs, including [VSCode for the web](https://vscode.dev), [VSCode code server](https://github.com/coder/code-server), and [JetBrains Projector](https://lp.jetbrains.com/projector/). See [Lightrun for vscode.dev](/vscode/vscode-dev/) and [Lightrun for code server](/vscode/code-server/) for more information.

#### JetBrains Plugin

- We have made user interface improvements to the JetBrains plugin. The Lightrun and Lightrun Snapshot tool windows have been redesigned to improve user engagement and stickiness. The new updates are currently in private beta and will gradually roll out over the next few weeks. See the new [New JetBrains plugin quick tour](/getting-around/) for more information.

#### Python Agent

- The python agent now supports Apple silicon macs. This means that you can now create Lightrun actions (dynamic logs, and snapshots) using the Python agent directly in your M1, M1 Pro, or M1 max MacBooks.  See the python agent [system requirements](/python/system-requirements/) for more information.
 
- We have added support for specifying `base_dir` parameters in the python agent configuration. Files in the directories specified in the python `base_dir` configuration parameter will have a higher priority in case of name conflicts. This parameter is very helpful in solving the python `Multiple modules matching %` error. See the [python agent configuration](/python/agent-configuration/) and [python troubleshooting guide](/troubleshooting/#common-error-messages_1) for more information.

#### JVM Agent

- The JVM agent now supports Apple silicon macs. This means that you can now create Lightrun actions (dynamic logs, snapshots, and metrics) using the JVM agent directly in your M1, M1 Pro, or M1 max MacBooks.  See the JVM agent [system requirements](/jvm/system-requirements/) for more information.

- Lightrun's JVM agent now supports ASM9 Java bytecode.

#### Management Portal

- We have added a service configuration property called **Default Piping** that can be used to configure an organization's default agent output routing in the Management portal. See [Service configuration](/service-configuration/) for more information.

- UI improvements for the Management portal.

#### Bug Fixes

- Fixed security vulnerabilities in Lightrun server.
- Fixed authentication issues in the JetBrains plugin.
- Improved agent performance under stress conditions (10,000 agents)
- Fixed absent gutter icon in VSCode IDE when an action FILENAME comprises the folder name, i.e., folder/filename, not the file name alone.

---

### Version 1.4.6

Release Date: May 3, 2022 (SaaS)

##### <span style="color: #1A3C5A;">Features & Changes</span>

**<span style="color: #1A3C5A;">Node Agent<span>**

Added the ability to insert Lightrun actions into Node.js Third-party modules. See [extraPaths](/node/agent-configuration/#extrapaths) for more information.

##### <span style="color: #1A3C5A;">Bug Fixes</span>

**<span style="color: #1A3C5A;">Node Agent</span>**

- Fixed wrong import syntax in Node.js agent package.

---

## April 2022

### Version 1.4.5

Release Date: April 5, 2022 (SaaS and On Premise)

**<span style="color: #1A3C5A;">General<span>**

- Fixes of Security vulnerabilities in Lightrun Server

---

## March 2022

### Version 1.4.4

Release Date: March 24, 2022 (SaaS)

##### <span style="color: #1A3C5A;">Bug Fixes</span>

**<span style="color: #1A3C5A;">JetBrains plugin</span>**

- Fixed Snapshot tab title is showing "Snapshot" instead of id+filename:line
- Fixed exception that occurs in some cases after user login
- Fixed pinned agent disappeared from tool window after insert tagged

**<span style="color: #1A3C5A;">Node Agent<span>**

- Fixed Security vulnerability in node agent

---

### Version 1.4.3

Release Date: March 15, 2022 (SaaS)

##### <span style="color: #1A3C5A;">Features & Changes</span>

**<span style="color: #1A3C5A;">Management Portal</span>**

UI enhancements 

**<span style="color: #1A3C5A;">General</span>**

- Fixes of Security vulnerabilities in Lightrun Server 
- Fixed log4j vulnerability in the Node.js agent

##### <span style="color: #1A3C5A;">Bug Fixes</span>
 
- Windows Agent: Does not work if there are spaces in the path

---

### Version 1.4.0

Release Date: March 02, 2022 (SaaS and On Premise)

##### <span style="color: #1A3C5A;">Features & Changes</span>

**<span style="color: #1A3C5A;">JVM Agent<span>**

- Windows Java agent is now GA!

**<span style="color: #1A3C5A;">Python Agent</span>**

- Python 2.7 MAC agent support

**<span style="color: #1A3C5A;">VSCode Plugin</span>**

- Lightrun VSCode extension is now GA!

**<span style="color: #1A3C5A;">Management Portal</span>**

- New UI design for the management portal
- Onboarding flow enhancements 

**<span style="color: #1A3C5A;">General</span>**

- Change agent default retention to 10 days (instead of 2 days).

##### <span style="color: #1A3C5A;">Bug Fixes</span>
 
- Multiple bug fixes and improvements for IntelliJ plug-in, Node & Python agents.
  
---

## January 2022

### Version 1.3.3

Release Date: January 19, 2022

#### Features & Changes

#### JVM Agent

- Java support for versions 14 to 17

#### Python Agent

- AWS lambda function support

#### Management Portal

- New successfully authenticated page when signing in from a plugin
- Mobile support for sign in & sign up pages
- Increased the character limit for PPI reduction
  
---

## December 2021

### Version 1.3.0

Release Date: December 28, 2021

#### Features & Changes

#### [NEW] VSCode Plugin

- Lightrun VSCode extension (beta) - initial release

#### JVM Agent

- Agent is removed faster when application exits

#### Python Agent

- `*.pyc` files support
- Agent is removed faster when application exits

#### Node.js Agent

- Agent is removed faster when application exits

#### General

- New audit event for user deletion

#### Bug Fixes

#### JetBrains plugin

- Fixed agents dropdown scroll when creating new action
- Fixed pinned agents minor bugs
- Tag removal from other sources is now reflected in the plugin

#### Management Portal

- Fixed Snapshots sorting

---

### Version 1.2.3

Release Date: December 13, 2021

#### Features & Changes

#### Python Agent

- Added `lightrun_class_path` configuration option to limit resource indexing
- Added the ability to change Lightrun default logger
- Added wait for Lightrun initialization option: `lightrun_wait_for_init` parameter allowing the agent sufficient time to spin up and get all actions before the code is executed

#### Node.js Agent

- AWS lambda function support
- Added wait for Lightrun initialization option: `lightrunWaitForInit` and `lightrunInitWaitTimeMs` parameters allowing the agent sufficient time to spin up and get all actions before the code is executed

#### General

- Increased the number of agents and seats for the Lightrun community version

#### Bug Fixes

#### JVM Agent

- Source version correlation fixed

#### Node.js Agent

- Performance improvements in active mode

#### JetBrains Plugin

- Last used agent/tag is set as default value
- An exception was thrown when tagged Snapshot action was clicked
- Agent/tag selection list scroll

#### Management Portal

- Fixed Snapshots sorting by date

---

## November 2021

### Version 1.2.2

Release Date: November 14, 2021

#### Features & Changes

#### Node.js Agent

- Performance improvements in idle mode

#### Bug Fixes

#### JetBrains Plugin

- Backward compatibility with v1.0 agents

#### General

- Detaching an agent threw an exception

## October 2021

### Version 1.2.0

Release Date: October 27, 2021

#### Features & Changes

#### JVM Agent

- Windows operating system support (preview)
- Show informative error when can't acquire JVM capabilities
- Extended expression now supports custom length through agent configuration

#### Python Agent

- Lightrun now supports Python applications, including Django, Flask and Apache Airflow frameworks. Add logs and snapshots to your Python application at runtime without the need for restarts or redeployments

#### Node.js Agent

- Lightrun now supports Node.js applications, including Express and Koa frameworks. Add logs and snapshots to your Node.js application at runtime without the need for restarts or redeployments

#### JetBrains Plugin

- JetBrains plugin now supports PyCharm IDE
- JetBrains plugin now supports WebStorm IDE
- Kotlin is now supported in IntelliJ IDE
- Allow log piping per action through Lightrun CLI
- Added pagination to agents list
- Max agents to display is configurable through settings
- Added support for .class files
- Improved performance
- JavaScript code completion when adding actions
- Add the option to test the server URL
- Primary agent/tag is selected when adding a new action
- Last used agent/tag is selected by default when adding a new action, if there is no pinned agent/tag
- Reduced the number of plugin refreshes
- Show "View only" agents after license limit is reached

#### Management Portal

- Added pagination to agents table
- PII redaction & blacklist pattern tester
- Minor styling upgrade
- Show "View only" agents after license limit is reached
- Show plan details - agents/seats count

#### General

- Support multiple Lightrun concurrent agents at large scale
- Improved Prometheus endpoint query time
- Server license validation
- CLI support for snapshot expressions
- Autofill user email for invited users
- Upgrade KeyCloak version to 13.0

#### Bug Fixes

#### JVM Agent

- Log failure when printing counter stats

#### JetBrains plugin

- Exceptions are shown only after second refresh
- Couldn't expand snapshot data
- Couldn't close embedded browser window
- Couldn't add action to programming languages that are not supported in source versioning
- Plugin disconnects when left-clicking the status button
- Snapshot tab is not selected when loading a snapshot from file
- Clicking 'only my logs' threw an exception
- IDE froze on logout when network is disconnected
- Actions were hidden when filtering agents

#### Management Portal

- Audit table sort
- Collect logs more than once throws an exception
- User was able to deactivate his own user
- Fix toggle button in edit user dialog
- Google translate was translating code instructions

#### General

- DB timestamps resolution
- PII redaction wasn't working in snapshot frames
- Agent with empty API Key threw an exception
- Agent was unable to get hostname from Alpine Docker

---

## April 2021

### Version 1.1.0

Release Date: April 18, 2021

#### Features & Changes

#### JVM Agent

- Improved resource indexing

#### JetBrains Plugin

- Added the ability to filter logs in the Lightrun console, based on agent ID
- Added copy log lines from Lightrun console to clipboard
- Minor design changes

#### Management Portal

- New login UI
- Added Lightrun Community version, supporting a single agent and a single seat
- Allow editing PII redaction patterns
- Added custom error pages
- Every user can see Entities pages in the Management Portal

#### General

- Added integration with Sentry
- Agents now report host's resources
- Added KeyCloak brute force protection
- Token is now stored in HTTP cookie instead of browser's local storage
- Agent reports data in batches to improve performance

#### Bug Fixes

- User couldn't change password when signing up with Google
- Authentication didn't redirect to the correct page
- User couldn't scroll error dialogs
- Default action expiration value was wrong
- Agent info dialog opened in a different IDE window
