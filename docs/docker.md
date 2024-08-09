## Installing Lightrun inside a Docker container

Docker containers are [ephemeral](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#general-guidelines-and-recommendations).

If you were to create a shell into a Docker container (by `docker exec -it <container-id>`, for example) and add the Lightrun files there, they would disappear the next time the container would spin up due to the ephemeral nature of that container.

Instead, we suggest you install Lightrun by adding it to the underlying Docker image directly, i.e. by "baking" the agent into the image.

Instructions for each language we support are provided inside the "Install an Agent" section for the language:

- [Installing Lightrun for the JVM inside a Docker container](jvm/agent.md#docker-installation)
- [Installing Lightrun for Node.js inside a Docker container](node/agent.md#docker-installation)
- [Installing Lightrun for Python inside a Docker container](python/agent.md#docker-installation)
