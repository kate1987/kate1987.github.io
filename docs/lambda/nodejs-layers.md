# Deploy Lightrun on AWS Lambda with Lambda layers

## Overview

To take advantage of Lightrun’s functionality in your AWS Lambda function, you must deploy Lightrun’s agent library with your project. One of the ways to import the additional code (frameworks, SDKs, libraries, and more) into a Lambda function is to bundle the function with an AWS Lambda Layer.

In this tutorial, you will learn how to package the Lightrun Node.js agent into a Lambda layer and integrate the packaged agent into your Node.js AWS Lambda function.

!!! note
	These instructions are valid only for AWS Lambda functions deployed as a .zip file archive.

## Prerequisites

This tutorial assumes that you have:

- A Lightrun account.
- [An AWS account.](https://aws.amazon.com/)

## Create a Lambda layer

An AWS Lambda Layer is a `.zip` file archive containing libraries, configuration files, dependencies, etc., that you can import into your Lambda function at runtime. 

To create an AWS Lambda layer for the Lightrun Node.js agent,

1. Compile the Lightrun Node.js agent into a `.zip` file archive.

  ??? info "Compile the Lightrun Node.js agent into a .zip archive"
      To compile the Lightrun Node.js into a zip file archive.

      1. Create a new directory that will be used to store the Lambda layer.
        ```bash
        mkdir lambda_layer
        cd lambda_layer
        ```
      2. Initialize NPM in the new directory. A `package.json` file will be generated for the directory.
        ```bash
        npm init -y
        ```
      3. Install Lightrun
        ```bash
        npm install lightrun
        ```
      4. Add the following build script to the generated `package.json` file.
        ```bash
        "scripts": {
        "build": "npm install && mkdir -p nodejs && cp -r node_modules nodejs/ && zip -r  layers.zip nodejs"
        }
        ```
      5. Generate your `.zip` file archive.
        ```bash
        npm run build 
        ```
      A `layers.zip` file will appear in the `lambda_layer` folder.

      !!! important
          Installed dependencies in a Node.js Lambda layer must be stored in a `nodejs/node_modules/{our libraries}` or `nodejs/<node-version>/node_modules/{our libraries}`  file path for the dependencies to be discovered by a Node.js Lambda function. You can learn more about Lambda layer paths [here](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html#configuration-layers-path.).

2. Create a Lambda layer with the `.zip` file archive. You can do this in two ways:
  
  - ??? info "Create a Lambda layer via the AWS console"
        To create an AWS Lambda layer from your AWS console.

        1. Navigate to the AWS Lambda console, and open the [Layers page](https://console.aws.amazon.com/lambda/home#/layers) of the console.
        2. Click **Create Layer**.
        3. Specify a name for the new Lambda Layer.
        4. Upload the generate `layers.zip` file.
        5. Select the compatible architecture and runtime for your `.zip` file (we will be using the  `x86_64` architecture and `nodejs14.x` as our preferred runtime environment).
        6. Click **Create**.

        The new Lambda Layer is now available to your Node.js Lambda functions.

  - ??? info "Create a Lambda layer with the AWS CLI"

        !!! important
            The following instructions assume that you have the AWS CLI installed on your local machine. Follow the instructions [here](https://aws.amazon.com/cli/) to install and set up the AWS CLI on your local machine if you haven’t already.

        To create an AWS Lambda layer with the AWS CLI, run the following command in your terminal.

        ```bash
        aws lambda --region us-east-1  publish-layer-version --layer-name 'Lightrun_Package_node' --compatible-runtimes 'nodejs14.x' --zip-file fileb://layers.zip
        ```

        Change `Lightrun_Package_node1` to your preferred layer name, change `us-east-1` to your preferred region, and `nodejs14.x` to your desired Node.js runtime environment. If the deployment is successful, you should get a response similar to the following in your terminal.

        ```json hl_lines="8"
        {
            "Content": {
                "Location": "<aws_location_key>",
                "CodeSha256": "DvW8+mrWOf9T5OAQkaekXpjpSVF4RbkFCiMo33o/BHA=",
                "CodeSize": 4430628
            },
            "LayerArn": "<layers_arn>",
            "LayerVersionArn": "<layers_version_arn>",
            "Description": "",
            "CreatedDate": "2022-06-16T12:13:50.087+0000",
            "Version": 1,
            "CompatibleRuntimes": [
                "nodejs14.x"
            ]
        }
        ```

        !!! note
            Note the `LayerVersionArn` key that was highlighted above, the key will be required for attaching the created Lambda layer to Lambda functions with the AWS CLI.

## Share the Lambda layer to your application

After compiling the Lightrun Node.js agent into a `.zip` file archive and uploading it to AWS as a Lambda layer, the next step is to add the Lambda layer to the Lambda functions. You can do this in two ways:

- [Deploy Lightrun on AWS Lambda with Lambda layers](#deploy-lightrun-on-aws-lambda-with-lambda-layers)
  - [Overview](#overview)
  - [Prerequisites](#prerequisites)
  - [Create a Lambda layer](#create-a-lambda-layer)
  - [Share the Lambda layer to your application](#share-the-lambda-layer-to-your-application)
    - [Add the Node.js agent Lambda layer to your application via the AWS Console](#add-the-nodejs-agent-lambda-layer-to-your-application-via-the-aws-console)
    - [Add the Node.js agent Lambda layer to your application from the AWS CLI](#add-the-nodejs-agent-lambda-layer-to-your-application-from-the-aws-cli)
  - [Verify things are working](#verify-things-are-working)


### Add the Node.js agent Lambda layer to your application via the AWS Console

If you have already deployed your Node.js function to AWS, you can easily attach the Lambda layer to the Lambda function in your AWS Console. To do that,

1. Open the [Functions page](https://us-east-1.console.aws.amazon.com/lambda/home?region=us-east-1#/functions) in your AWS Lambda console, and select the relevant Lambda function.

2. Navigate to **Configurations** > **Environment variables** > **Edit**.
3. Set the variable name to `LIGHTRUN_SECRET` and copy the value from your management portal.

  ![Environment variables](/assets/images/node-enviroment-variables.png)

  ![Environment variables](/assets/images/node-environment-variables1.png)

4. Wrap your Lambda function **Code source** with the `lightrun/lambda` module. The `lightrun/lambda` module ensures that the Lightrun agent is enabled before calling the serverless function, and also disables the Lightrun agent when the function call finishes so that it can properly handle the next call to the serverless function.

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

5. Click **Deploy** to update the code source.
6. Scroll down to the **Layers** section, and select **Add a layer**. 
7. Click **Custom layers** and select the appropriate layer from the drop-down list.
8. Pick a version and click **Add** to attach the layer to your Lambda function.

  ![Node layers](/assets/images/add-node-layer.png)


!!! important
    AWS Lambda functions are event-driven short-running programs with a maximum execution time of 15 minutes. To debug AWS Lamda functions with the Lightrun Node.js agent:

    1. Specify `lightrunWaitForInit: true` and `lightrunInitWaitTimeMs: 10000` in the Lightrun Node.js agent configuration. These two configuration parameters will block the lambda function execution till first time breakpoints are fetched from the Lightrun server and ensures that the Lightrun agent has time to communicate with the Lightrun server before the short-running application disconnects.

    2. Apply Metadata tags that include the name of your Lambda function - By default, a new Lightrun agent is created whenever the Lambda function is invoked. By adding our function’s name as a metadata tag, we can attach Lightrun actions to agents created whenever the Lambda function is invoked, even before the Lambda function is invoked. This is because an action bound to a metadata tag is implicitly attached to all agents possessing that tag.

### Add the Node.js agent Lambda layer to your application from the AWS CLI

!!! note
    - The following instructions assume that you have the AWS CLI installed on your local machine. Follow the instructions [here](https://aws.amazon.com/cli/) to install and set up the AWS CLI on your local machine if you haven’t already installed it
    - Ensure that you have configured all the permissions required to run an AWS Lambda function and created a role for the Lambda function. Learn more about the permissions needed to deploy a Lambda function [here](https://docs.aws.amazon.com/lambda/latest/dg/lambda-permissions.html). Follow the instructions [here](https://docs.aws.amazon.com/lambda/latest/dg/lambda-intro-execution-role.html) to create a Lambda execution role for your Lambda function.

If you haven’t deployed your Lambda function to AWS, you can attach the Lambda layer to your application during deployment with the AWS CLI. To deploy your Lambda function with the deployed Lambda layer.

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

2. Deploy the Lambda function with the AWS CLI. You can do this in two ways:

  - ??? info "Deploy the Lambda with .zip file archives."
        To deploy a Lambda function as a .zip file archive,

        1. Zip the function file.
          ```bash
          zip function.zip <lambda_function_file>.js
          ```
        2. Run the following command to deploy the .zip file archive.
          ```bash
          aws lambda create-function \
          --region us-east-1  \
          --function-name node3 \
          --zip-file fileb://function.zip \
          --role <lambda_execution_role_arn> \
          --handler index.handler \
          --runtime nodejs14.x --timeout 10 --memory-size 512 \
          --layers <LayerVersionArn> \
          --environment Variables="{LIGHTRUN_SECRET=<LIGHTRUN_KEY>}"
          ```
        
        !!! important
            Update the command with the following values:

            - `--function-name` - Lambda function name.
            - `--role` - Lambda execution role ARN. (Follow the instructions [here](https://docs.aws.amazon.com/lambda/latest/dg/lambda-intro-execution-role.html) to create a Lambda execution role for your Lambda function.)
            - `--runtime` - Preferred Node.js runtime environment.
            - `--layers` - Lambda layer Version ARN.
            - `--environment Variables` -  Lightrun secret Keys.
        
        You should get a response similar to the following if your deployment was successful.

        ```json
        {	
            "FunctionName": "node3",
            "FunctionArn": "arn:aws:lambda:us-east-1:<iam-user>:function:node3",
            "Runtime": "nodejs14.x",
            "Role": "arn:aws:iam::<iam-user>:role/lmb",
            "Handler": "index.handler",
            "CodeSize": 494,
            "Description": "",
            "Timeout": 100,
            "MemorySize": 512,
            "LastModified": "2022-06-20T08:22:44.022+0000",
            "CodeSha256": "d4hbbWI60FaCd0SfMLTCv+X2f33kM8sTzsC7lYp6LTc=",
            "Version": "$LATEST",
            "Environment": {
                "Variables": {
                    "LIGHTRUN_SECRET": <LIGHTRUN_KEY>
                }
            },
            "TracingConfig": {
                "Mode": "PassThrough"
            },
            "RevisionId": "f97c70b1-7ce7-48e6-92f5-3ba159cb2cf6",
            "Layers": [
                {
                    "Arn": "arn:aws:lambda:us-east-1:<iam-user>:layer:Lightrun_Package_node1:1",
                    "CodeSize": 4430628
                }
            ],
            "State": "Pending",
            "StateReason": "The function is being created.",
            "StateReasonCode": "Creating",
            "PackageType": "Zip",
            "Architectures": [
                "x86_64"
            ],
            "EphemeralStorage": {
                "Size": 512
            }
        ```
          

  - ??? info "Deploy the Lambda file as an AWS SAM application."

        !!! prerequisites
            The following instructions assume that you have the AWS SAM CLI and Docker installed on your local machine.

            - Follow the instructions [here](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install-mac.html) to install the AWS SAM CLI on your local machine. 
            - Follow the instructions [here](https://docs.docker.com/get-docker/) to setup Docker on your local machine.

        To deploy the Lambda function by packaging it as an AWS SAM template.

        1. Add a `template.yaml` file to the `node_lambda_function` folder.
          ```bash
          touch template.yaml
          ```
        2. Add the following yaml to the `template.yaml` file.
          ```yaml
          AWSTemplateFormatVersion : '2010-09-09'
          Transform: AWS::Serverless-2016-10-31
          Resources:
            NodeFunction:
              Type: AWS::Serverless::Function
              Properties:
                Handler: index.handler
                Runtime: nodejs14.x
                Role: <lambda_execution_role_arn>
                Layers:
                  - <LayerVersionArn>
                Environment:
                  Variables:
                    LIGHTRUN_SECRET: <LIGHTRUN_KEY>
          ```
        3. Run the following command to build the SAM template.
          ```bash
          sam build
          ```
        4. Run the following command to deploy the SAM template.
          ```bash
          sam deploy --guided
          ```

        !!! important
            Update the `template.yaml` file with the following values.

            - `NodeFunction` - change to your preferred Lambda function’s name.
            - `Role` - Lambda execution role ARN. (Follow the instructions [here](https://docs.aws.amazon.com/lambda/latest/dg/lambda-intro-execution-role.html) to create a Lambda execution role for your Lambda function.)
            - `Runtime` - Preferred Node.js runtime environment.
            - `Layers` - Lambda layer Version ARN 
            - `Environment/Variables` -  Lightrun secret Keys

## Verify things are working

To verify that a Lightrun agent has been installed added your Lambda function correctly,

1. Verify that a new agent with your Lambda function name is created anytime your Lambda function runs and dies immediately your Lambda function stops.
2. Verify that a tag with your Lambda function name has been added to your Lightrun account.