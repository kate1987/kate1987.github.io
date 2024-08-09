# About actions

Actions are any of the snapshots, dynamic logs or metrics that you request to add to your application directly from specific lines of its source code. 

Adding an action triggers a request that is sent to the agent. Once verified, the requested instrumentation is then added to the running application without interrupting any services.

!!! guard "Performance configurations"
     A system quota controls use of CPU, Networking, Memory, excessively long strings, too many instructions printing out, protection from infinite loops and the like. Users with the `IGNORE_QUOTA` role can customize these limits. 


--8<-- "ux-reference/action-output.md"






