

1. [Install the CLI](#install)

2. [Authenticate the CLI](#authenticate)

###### To use the Lightrun CLI {#install}

!!! reqs "Prerequisites"

     [Sign up](create-account.md) for your Lightrun account before getting started.
     
     The Lightrun CLI requires Java to be installed.


1. From a browser, log in to your Lightrun account and navigate to **Getting Started**. 

2. From the **Command Line Tool** section in the landing page, download `lightrunc.jar`. 

3. Open the terminal and navigate to where you downloaded the `lightrunc.jar` file.

4. [Authenticate](#authenticate) your CLI with your Lightrun account:

  1. Copy and run the first command line that appears in your browser. 
  
    !!! example
        ```
        java -jar lightrunc.jar login
        ```

    **Note:** Add `server-url <URL>` at the end of the command when using Lightrun on-prem.
    
  2. Copy and run the second command line that appears in your browser. 
  
    !!! example

        ```bash
        java -jar lightrunc.jar login myaccount@acme.com
        ```
    

5. To run any Lightrun command, add the following prefix: 

     ``` bash
     java -jar lightrunc.jar
     ```


###### Authenticate the CLI with Lightrun {#authenticate}

To use the CLI, first authenticate with your Lightrun account. You can authenticate directly from within the CLI or choose to redirect to the browser. 

``` bash
java -jar lightrunc.jar login <username/email address/password>
```

!!! example

    Log in directly from the CLI:

    ```bash
    java -jar lightrunc.jar login -email jane.doe@example.com -password secretpassword
    ```

!!! example

    Log in with a redirect to your browser:

    ```bash
    java -jar lightrunc.jar login myaccount@acme.com
    ```

