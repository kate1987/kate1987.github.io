# Lightrun Agents

The Lightrun agent is at the core of the Lightrun platform. It runs alongside your application and inserts Lightrun actions(Logs, Metrics, and Snapshot) added through Lightrun IDE plugins into the application at runtime.

## Differences between Agents, Tags, and Custom Sources.

|Agents|Tags|Custom Sources|
|------|---|---------------|
| Agents are the core of the Lightrun platform.  Lightrun agents run alongside your application and insert Lightrun actions(Logs, Metrics, and Snapshot) added through Lightrun IDE plugins into the application at runtime.| Tagging allows you to group agents using a meaningful name, typically based on a common functionality.|Custom Source is a dynamic group of agents and tags defined by a chosen set of conditions, like a shared property (tag or hostname). |
|When you insert a Lightrun action (dynamic log, snapshot, and metrics) into an agent, the action is tied to the agent's lifetime. Once the agent stops running, the action is deleted. | When you add an action to a tag, the action outlives any individual agent.  The action is tied to the tag, and as agents come and go, they pick up the actions assigned to the tag.|Depending on the custom source conditions, a dynamic list of agents and tags is created when you create a custom source. Lightrun actions added to a custom source are simultaneously applied to every agent and tag in the list. |

## More on Agents

To get started, pick your programming language or check out our deployment examples:

**Programming Languages**

- [Node.js](/node/agent/)
- [Java](/jvm/agent/)
- [Python](/python/agent/)

**Deployment Options**

- [AWS Lambda](/lambda/introduction/)
- [Docker](/docker/)
- [Kubernetes](/kubernetes/)
