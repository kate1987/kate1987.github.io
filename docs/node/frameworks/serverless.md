# Lightrun for Serverless Functions

To run a Serverless function with the Lightrun Node.js agent,

1. Wrap your serverless function source code with the `lightrun/lambda` module.

  ```js
  const lightrun = require("lightrun/lambda");

  exports.handler = lightrun.wrap( async (event, context) => {
        <lambda function source code here>
      }, {
        lightrunSecret: process.env.LIGHTRUN_SECRET,
        agentLog: {
          logsPath: "",
          level: "debug"
        },
        lightrunWaitForInit: true, 
        lightrunInitWaitTimeMs: 10000,
        metadata: {
          registration: {
              displayName: "<lambda_function_name>",
              tags: ['<lamda_function_name>']
          }
        }
      }
  );

  ```

  !!! note
	  The `lightrun/lambda` module wraps around your serverless function and ensures that the Lightrun agent is enabled before calling the serverless function. It also disables the Lightrun agent when the function call finishes so that it can properly handle the next call to the serverless function.

2. Package and deploy your serverless function with the Lightrun agent. For example, to deploy a Lightrun agent with an AWS Lambda function, you must package the Lightrun agent into a [Lambda layer for use by the Lambda function](/lambda/nodejs-layers/) or package the Lightrun agent and Lambda function together into a [container image for deployment on Amazon ECR](/lambda/nodejs-containers/).
