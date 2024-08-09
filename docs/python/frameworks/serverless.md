# Lightrun for Serverless Functions

To run a Serverless function with the Lightrun Python agent, follow these steps: 

1. Ensure that the Lightrun agent has been configured to work with your serverless function. For example, to use Lightrun with an AWS Lambda function, you must first package the Lightrun agent into an AWS Lambda Layer. *Follow the instructions [here](/lambda/python-layers/#create-a-lambda-layer) to setup a lambda layer for your Lightrun Python agent.*
2. Add the following to your function code.
	```py
	from lightrun.decorators import lightrun_serverless

	@lightrun_serverless(company_key = 'aaaaaa-bbbb-cccc-dddd-eeeeeeeeeee', lightrun_tags = ['tag1', 'tag2'])
	def serverless_func():
		"""Code"""
	```
3. Run your serverless function as normal.

!!! Note
	The Lightrun serverless decorator wraps around your serverless function and ensures that the Lightrun agent is enabled before calling the serverless function. It also disables the Lightrun agent when the function call finishes so that it can properly handle the next call to the serverless function.
