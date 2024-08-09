# Lightrun for AWS Lambda

Nowadays, FaaS (Function as a Service) is the default choice for individual developers and mature software vendors seeking low-cost, effortless, and scalable deployment solutions. While providing overall significant benefits like reduced costs, improved scalability, improved application resiliency, etc., using a FaaS platform like AWS Lambda also provides its limitations and challenges.

One of the biggest challenges faced with FaaS applications is the lack of remote debugging options in a serverless environment. Due to the stateless nature of FaaS applications, developers often face a number of challenges when collecting data needed to detect and fix bugs when debugging cloud applications.

Lightrun address these challenges by allowing dynamic data collection from your AWS Lambda function without code redeployment. With Lightrun, you can add logs, receive a stack trace, or monitor metrics data directly in your IDE without having to remove the FaaS application from its production environment.

If you'd like to get started using Lightrun in your Lambda function product environment, you can add a Lightrun agent to your AWS Lambda function with the following tutorials. 

- [Lightrun on Node.js AWS Lambda](/lambda/nodejs-layers/)
- [Lightrun on Python AWS Lambda](/lambda/python-layers/)

!!! note
	We currently do not support debugging AWS Lambda functions with the Lightrun Java agent.