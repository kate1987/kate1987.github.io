# Deploy Lightrun on AWS Lambda with container images

## Overview

To take advantage of Lightrun’s functionality in your AWS Lambda function, you must deploy Lightrun’s agent library with your project. One of the ways to import the additional code (frameworks, SDKs, libraries, and more) into a Lambda function is to package your Lambda function with the dependencies as a container image with [Docker](https://docs.docker.com/get-docker/) and then upload the image for hosting on [Amazon Elastic Container Registry (Amazon ECR)](https://aws.amazon.com/ecr/).

In this tutorial, you will learn how to package the Lightrun Node.js and your Lambda function into a container image with Docker. You will also learn how to upload the container image to Amazon ECR for deployment as a Lambda function.

## Prerequisites

This tutorial assumes that you have:

- A Lightrun account.
- [An AWS account.](https://aws.amazon.com/)
- Docker desktop or Docker engine installed and running on your local machine. See [docker.com](https://docs.docker.com/engine/install/) for Docker installation instructions.
- AWS CLI installed on your local machine. Follow the instructions [here](https://aws.amazon.com/cli/) to install and set up the AWS CLI on your local machine if you haven’t already.

## Configure your Lambda function source code to work with Lightrun

To configure your Lambda function code to work with Lightrun,

1. Wrap your Lambda function code with the `lightrun/lambda` module. The `lightrun/lambda` module ensures that the Lightrun agent is enabled before calling the serverless function, and also disables the Lightrun agent when the function call finishes so that it can properly handle the next call to the serverless function.

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
      Change `<lambda-function-name>` to your Lambda functions name.

  !!! important
      AWS Lambda functions are event-driven short-running programs with a maximum execution time of 15 minutes. To debug AWS Lamda functions with the Lightrun Node.js agent:

      1. Specify `lightrunWaitForInit: true` and `lightrunInitWaitTimeMs: 10000` in the Lightrun Node.js agent configuration. These two configuration parameters will block the lambda function execution till first time breakpoints are fetched from the Lightrun server and ensures that the Lightrun agent has time to communicate with the Lightrun server before the short-running application disconnects.

      2. Apply Metadata tags that include the name of your Lambda function - By default, a new Lightrun agent is created whenever the Lambda function is invoked. By adding our function’s name as a metadata tag, we can attach Lightrun actions to agents created whenever the Lambda function is invoked, even before the Lambda function is invoked. This is because an action bound to a metadata tag is implicitly attached to all agents possessing that tag.

2. Add Lightrun as a dependency in your `package.json` file.

	```json hl_lines="12"
	{
	"name": "docker_web_app",
	"version": "1.0.0",
	"description": "Node.js on Docker",
	"author": "Lightrun docker",
	"main": "server.js",
	"scripts": {
		"start": "node server.js"
	},
	"dependencies": {
		"express": "^4.18.2",
		"lightrun": "1.13.0"
	}
	}
	```



## Upload the Lambda function source code to AWS ECR

To deploy upload the Lambda function source code to AWS ECR.

1. Add a dockerfile to the functions folder.
	```bash
	touch .Dockerfile
	```
2. Add the following code sample to the dockerfile.
	```dockerfile
	FROM amazon/aws-lambda-nodejs:12
	COPY index.js package.json ./
	RUN npm install
	CMD [ "index.handler" ]
	```
3. Install the project dependencies.
	```js
	npm install .
	```
4. Create a repository for your Lambda function on ECR. Follow the instructions [here](https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-create.html) to create a private repository on AWS ECR.
5. Authenticate your Docker client to the Amazon ECR registry to which you intend to push your image.
	```bash
	aws ecr get-login-password --region region | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<region>.amazonaws.com
	```
6. Build the function's container image.
	```bash
	docker build -t <lambda_function_image_name> . --platform=linux/amd64
	```
7. Tag your container image name with the Amazon ECR repository.
	```bash
	docker tag <lambda_function_image_name>:latest <aws_account_id>.dkr.ecr.<region>.amazonaws.com/<ecr_repository_name>:latest
	```
8. Upload the container image to AWS ECR.
	```bash
	docker push <aws_account_id>.dkr.ecr.<region>.amazonaws.com/<ecr_repository_name>:latest
	```

!!! important
	Change `<lambda_function_image_name>` to your container image name, `<aws_account_id>` to your AWS account ID, `<region>` to your preferred AWS region, and `<ecr_repository_name>` to the name of the ECR repository that you created for the Lambda function.

## Verify things are working

To verify that a Lightrun agent has been installed added your Lambda function correctly,

1. Verify that a new agent with your Lambda function name is created anytime your Lambda function runs and dies immediately your Lambda function stops.
2. Verify that a tag with your Lambda function name has been added to your Lightrun account.