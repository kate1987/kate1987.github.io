# Authenticating the Lightrun CLI

Before you can start debugging with Lightrun from your CLI, you must first authenticate with your Lightrun account.

## Prerequisites

This tutorial assumes that you have:

- A Lightrun account.
- [Installed the Lightrun CLI on your local machine.](/cli/installation/)

## Authenticate in your CLI

1. Navigate to the folder where your downloaded CLI `lightrunc.jar` file stored in your terminal.
2. Run the following command. `java -jar lightrunc.jar login`.

	You will be redirected to your browser for authentication.

	```bash
	$ java -jar lightrunc.jar login
	Redirecting to your login URL: 
	https://app.lightrun.com/auth/realms/lightrun/protocol/openid-connect/auth?client_id=web_app&response_mode=fragment&response_type=code&redirect_uri=https://app.lightrun.com/device/<>
	Press Enter to open URL in browser
	
	Logged in successfully!
	```
 
3. Alternatively, you can chose authenticate the Lightrun CLI directly in your terminal.

	```bash
	java -jar lightrunc.jar login -email <jane.doe@example.com> -password <secretpassword>
	```

	Change `jane.doe@example.com` to your account **username/email** and change `<secretpassword>` to your **password**. 
