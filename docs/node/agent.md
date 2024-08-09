# Install the Lightrun Node.js agent

The Lightrun agent is at the core of the Lightrun platform. It's the component that communicates requests for runtime observability to your running code, and gathers and relays the requested data back to the Lightrun Server, and eventually the developer's IDE.

Before running the agent, it must be installed on the system where your code to be monitored is running, and its credentials must be declared either inside the application code, as environment variables, or in an `agent.config` file.

!!! reqs "Version Support"
    The instructions below apply to Node.js v10 and higher. If you require support for earlier versions, please [reach out](mailto:info@lightrun.com) and let us know!

!!! reqs "System requirements"
    Please check the Node.js agent system requirements [here](system-requirements.md).


Lightrun can be installed both [directly](#direct-installation) and inside of a [Docker container](#docker-installation). 

### Direct installation

1. Open a terminal and change to the working directory where your project is located.
2. Install the Node agent by entering `npm install lightrun`.
3. Open your application file (for example, `app.js`) and add the following code at the beginning of the file.

   ```javascript
   require('lightrun').start({
     lightrunSecret: '<LIGHTRUN_SECRET>',
     metadata: {
        filename: <FULL_PATH_TO_METADATA_FILE>
     }
   });
   ```

  !!! info "Getting Company Details"
      To get your `<LIGHTRUN_SECRET>` key, log into the [Management Portal](https://app.lightrun.com) and inspect the **Set Up An Agent** section, under **Getting Started**.
   
  !!! note

      The `metadata` block with the `filename` parameter is **optional**; the agent runs perfectly well without them. Using metadata nevertheless provides substantial benefits when managing your agents. See [here](/node/metadata-and-tagging/) for details, with examples, on constructing the metadata file.

4. Enter the parameter values for `lightrunSecret` and (optionally) the `metadata_file`.

5. Save and close the application file.

6. From a terminal, enter the command to run your application (for example, `node index.js` or `npm start`).

### Alternative method - Providing agent credentials as environment variables

!!! note
    This method works only for Linux and MacOS.

!!! info
    Although using this method allows you to avoid hard-coding your credentials into the source code, you must enter them in the run command every time your application is launched with the agent.

**Instructions**

1. Open a terminal and change to the working directory where your project is located.

2. Install the Node agent by entering `npm install lightrun`.

3. Open your application file (for example, `app.js`) and add the following code to the beginning of the file:

   ```javascript
    require('lightrun').start();
   ```

4. Save and close the application file.

5. From a terminal, enter the command to run your application, with the environment variables declared _before_ the `node` command.

   ```javascript
   LIGHTRUN_SECRET=<LIGHTRUN_SECRET> node --require lightrun/start app.js
   ```

--8<-- "ux-reference/node-typescript.md"

!!! important
    Unless you are working within a TypeScript framework, such as [Express or Koa](#running-the-agent-with-express-or-koa), for the above procedure, you must compile the TypeScript application file.

    ```bash
    tsc index.ts
    ```
    
    Following compilation, another file is created that has the same name as your TypeScript application, but with the ```.js``` extension.

!!! tip
    You can choose to provide the agent's credentials as environment variables, when running your application from the command line, instead of inserting them in the application file, as explained [above](#alternative-method-providing-agent-credentials-as-environment-variables) (**note** this does not work in MS Windows).

### Docker installation

Docker containers are [ephemeral](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#general-guidelines-and-recommendations).

If you were to create a shell into a Docker container (by `docker exec -it <container-id>`, for example) and add the Lightrun files there, they would disappear the next time the container would spin up due to the ephemeral nature of that container.

Instead, we suggest you install Lightrun by adding it to the underlying Docker image directly, i.e. by "baking" the agent into the image.

This is an example `Dockerfile` that installs Lightrun with a simple dummy application:

```dockerfile
FROM node:17.5.0
RUN npm install lightrun
COPY prime_main.js /app/prime_main.js
CMD ["node", "prime_main.js"]
```

If you prefer passing the credentials via the command line, here's how to do it inside a `Dockerfile`:

```dockerfile
FROM node:17.5.0
RUN npm install lightrun
COPY prime_main.js /app/prime_main.js
CMD ["LIGHTRUN_SECRET=<LIGHTRUN_SECRET>", "node", "--require", "lightrun/start", "prime_main.js"]
```


!!! imp "Important"
    Installing Lightrun in this fashion **does not** absolve you of the need to `require` Lightrun in your application. Please make sure to add Lightrun as an `require` to your application file.
### Running the agent with Express or Koa

If you are using Express or Koa frameworks in your application, refer to the instructions linked below:

* [Express](/node/frameworks/express)
* [Koa](/node/frameworks/koa)
