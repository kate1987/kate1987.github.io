# Tags

Tagging allows you to group agents using a meaningful name, typically based on a common functionality.  For example, you can use tags to identify the location and purpose of each agent: Database servers, Staging, and so forth. Additionally, you can apply to each agent multiple tags in any combination.

Using tags, you can bind actions to an agent before the agent has been launched and apply actions to applications across different sectors. Once an action is attached to a tag, it is implicitly added to all agents possessing that tag.

## Common Use Cases

### Debug Serverless Functions
Serverless functions are stateless programmatical functions written for a single purpose. They are hosted on managed infrastructure by cloud computing companies who maintain the infrastructure and code base of the serverless function.

Serverless functions are short-running functions. Suppose a Lightrun action is added directly to an agent created when the serverless function is started. In that case, the action will be deleted when the serverless function disconnects, and you will have to insert the action again when the serverless function restarts. 

You can solve this problem by attaching the Lightrun actions to tags instead. Lightrun actions attached to a tag outlive any individual agent. The action is implicitly attached to every agent created whenever the serverless function is started and persists even after the short-running function disconnects. 

### Debug Multiple Deployment Environments
Nowadays, most software companies have multiple deployment environments to enable teams to build and test software in isolation and ultimately deliver a high-quality product to production. Lightrun makes it easy to debug each deployment environment with tags. 

Imagine a scenario with three deployment environments in your system.

- Development
- Staging
- Production environments

You can add configuration for each environment as a tag in your agent config and apply Lightrun actions to each section by adding to the tag.

```json
"registration": {
   "DisplayName" : "<display-name>"
   "tags": [
     {
       "name": "Development"
     },
     {
       "name": "Staging"
     },
     {
       "name": "Production" 
     }
   ]
 }
```

Suppose you are experiencing a problem in the Production environment but not in any other environment. In that case, you can target that environment with Lightrun actions by applying the actions to the Production tag. A good tagging system can help you target just the set of agents relevant to your investigation.

## More on Tagging

To get started, pick your programming language.

**Programming Languages**

- [Node.js](/node/metadata-and-tagging/)
- [Java](/jvm/tagging/)
- [Python](/python/metadata-and-tagging/)