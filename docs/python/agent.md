# Install the Lightrun Python agent

The Lightrun agent is at the core of the Lightrun platform. It's the component that communicates requests for runtime observability to your running code, and gathers and relays the requested data back to the Lightrun Server, and eventually the developer's IDE.

Before running the agent, it must be installed on the system where your code to be monitored is running, and its credentials must be declared either inside the application code, or in an `agent.config` file.

!!! reqs "Version Support"

    The instructions below apply to Python v3.8 to 3.11. If you're interested in support for other versions, please [reach out](mailto:info@lightrun.com) and let us know!

!!! reqs "System requirements"
    Please check the Python agent system requirements [here](system-requirements.md).

Lightrun can be installed both [directly](#direct-installation) and inside of a [Docker container](#docker-installation). 

### Direct installation

1. Install the python agent by running `python -m pip install lightrun`.

2. Import Lightrun inside your `main` function, by adding the following code at **the beginning** of the function.

   ```python
   try:
        import lightrun
        lightrun.enable(company_key="<COMPANY_SECRET>")
   except ImportError as e:
        print("Error importing Lightrun: ", e)
   ```

  !!! info "Getting Company Details"
      You can get your `<COMPANY_SECRET>` and `<server_url>` key by logging into the [Management Portal](https://app.lightrun.com) and inspecting the **Set up an agent** section.

  !!! note
      Other configuration parameters can also be passed here. For example, add the `server_url` parameter to the `lightrun.enable` command when using Lightrun on-prem.

      ```python
      try:
          import lightrun
          lightrun.enable(company_key="<COMPANY_SECRET>", com_lightrun_server="<server_url>")
      except ImportError as e:
          print("Error importing Lightrun: ", e)
      ```

3. Run the application as you normally would; for example, `python app.py`.

!!! imp "Important"
    - Lightrun actions in Python must only be applied to a function before the function is called. Actions inserted into a Python function while the function is currently executing will only take effect once the function is exited and called again. This also means that you can not use Lightrun actions in a Python program's `__main__` method as it is already running when the Lightrun agent initializes. 

    - If your Python program doesn’t have a `main()` method and all the code is in one scope, you will not be able to use Lightrun effectively. It is necessary to introduce a `main()` method that triggers the other methods that you want to debug with Lightrun.
    
        For example, you won't be able to debug with Lightrun in the following code:

        ```py
        def main():
            // code which does not include calls to other methods -- Lightrun actions won't work

            // ONLY code in methods which are called anew after the Lightrun action has been placed will have a chance to be observed

        if __name__ == '__main__':
            main()
        ```

        To use Lightrun, you need to have other methods that are triggered by the `main()` method.

        ```py
        def echo():
            //	some logic/algorithm
            // Lightrun actions will work in this method, for invocations of this method that happen AFTER the Lightrun action is created

        def main():
            // Lightrun actions won't work in this method
            echo()

        if __name__ == '__main__':
            main()
        ```

### Run as command line argument

You can also install a Lightrun agent to your application by specifying your Lightrun credentials as environment variables when you start your Python application from your command-line interface (CLI).

!!! note
    This option does not work for Gunicorn applications.

1. ​Open a terminal and change to the working directory where your project is located.
2. Install Lightrun in your application’s folder.

  ```shell
  python -m pip install lightrun
  ```

3. Run your application with your Lightrun credentials.

  ```shell
  python -m lightrun --com_lightrun_server=<server_url> --company_key=<COMPANY_SECRET> -- app.py
  ```

Change `<server_url>` to your Lightrun server URL, `app.py` to the name of your python file, and `<COMPANY_SECRET>` to your Lightrun company key.

!!! info "Getting Company Details"
     You can get your `<COMPANY_SECRET>` and `<server_url>` key by logging into the [Management Portal](https://app.lightrun.com) and inspecting the **Set up an agent** section.

### Docker installation

Docker containers are [ephemeral](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#general-guidelines-and-recommendations).

If you were to create a shell into a Docker container (by `docker exec -it <container-id>`, for example) and add the Lightrun files there, they would disappear the next time the container would spin up due to the ephemeral nature of that container.

Instead, we suggest you install Lightrun by adding it to the underlying Docker image directly, i.e. by "baking" the agent into the image.

This is an example `Dockerfile` that installs Lightrun with a simple dummy application, assuming the credentials were added to the **source code** of your application as shown above:

```dockerfile
FROM python:3.8
RUN pip install lightrun
COPY prime_main.py /app/prime_main.py
CMD ["python", "/app/prime_main.py"]
```

If you prefer passing the credentials via the command line, here's how to do it inside a `Dockerfile`:

```dockerfile
FROM python:3.8
RUN pip install lightrun
COPY prime_main.py /app/prime_main.py
CMD ["python", "-m", "lightrun", "--company_secret=<COMPANY_SECRET>", "--", "app/prime_main.py"]
```

**Note:** Add the `server_url` parameter when using Lightrun on-prem.

!!! imp "Important"
    Installing Lightrun in this fashion **does not** absolve you of the need to `import` Lightrun to your application. Please make sure to add Lightrun as an `import` to your application file.

### Lightrun in Alpine Linux

!!! imp "Prerequisites"

    Before installing the Lightrun Python agent on Alpine Linux, ensure that the following dependencies are installed.
    ```shell
    apk add --no-cache libstdc++ gcompat libgcc build-base py3-pybind11-dev abseil-cpp-dev re2-dev 
    ```
    [Optional]
    ```shell
    pip install google-re2==1.0
    ```

To install a Lightrun agent in Alpine Linux:

1. Create a Dockerfile. 

    Note that the following dockerfile serves as a sample file and should be adjusted to your envirorment. It should not be used in Production.


    ```dockerfile
    # Sample Dockerfile. Not to be used in Production.
    # Stage 0 - base alpine to create a .whl from requirements
    ARG PYTHON_BASE_REPO='python'
    ARG PYTHON_BASE_TAG='3.10-alpine3.19'

    FROM ${PYTHON_BASE_REPO}:${PYTHON_BASE_TAG} as build
    ARG LIGHTRUN_KEY='xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx2b'
    ARG SERVER_URL='https://app.lightrun.com'
    ARG INSTALL_SCRIPT='python-install-agent.sh'
    ARG COMPANY_ID='xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

    WORKDIR /wheel

    # Install all the build requirements and build the wheel files
    # Any dpenedncy requiring compilation will be built from source
    RUN apk add --update --no-cache \
            abseil-cpp-dev \
            build-base \
            curl\
            gcompat \
            libffi-dev \
            libgcc \
            libstdc++ \
            linux-headers \
            py3-pybind11-dev \
            re2-dev && \
        LIGHTRUN_KEY=${LIGHTRUN_KEY} sh -c "$(curl -k -L "${SERVER_URL}/public/download/company/${COMPANY_ID}/${INSTALL_SCRIPT}?platform=alpine")" && \
        whl_ver=`python --version | grep -oE [3]\.[[:digit:]]{1,3}\.[[:digit:]]{1,3} | cut -d. -f1,2 | tr -d '.'` && \
        whl_file=`basename agent/lightrun-*${whl_ver}*.whl` && \
        mkdir ./wheels && \
        cp -vfp agent/${whl_file} ./wheels && \
        python -m pip install --no-cache --upgrade pip johnnydep setuptools && \
        johnnydep ./wheels/${whl_file} --verbose 0 | tail -n +3 | grep -v lightrun | tr -cd '\11\12\15\40-\176' | awk '{print $1}' > requirements.txt && \
        python -m pip wheel -r requirements.txt --wheel-dir=/wheel/wheels

    # Copy wheels from the build stage and install Lightrun's agent
    # The agent's installation is done using the built wheels (and not from PyPI)
    FROM ${PYTHON_BASE_REPO}:${PYTHON_BASE_TAG}
    ARG ARG_USERNAME='lightrun'
    ARG ARG_UID=10001
    ARG ARG_GID=10002

    # Copy all the compiled wheel dependencies
    COPY --from=build --chown=$UID:0 --chmod=g=u,+x /wheel /wheel

    # Install C/ C++ libraries and create a user and a group
    RUN apk add --update --no-cache \
        libc6-compat \
        libstdc++ && \
      rm -rf /var/cache/apk/* && \
      addgroup -g ${ARG_GID} "${ARG_USERNAME}" && \
      adduser -h /home/${ARG_USERNAME} -u $ARG_UID -D -s /bin/false -G "${ARG_USERNAME}" ${ARG_USERNAME}

    WORKDIR /home/${ARG_USERNAME}
    RUN chown -R $UID:0 /home/${ARG_USERNAME}
    USER $ARG_UID

    # Create and activate a virtual environment, as a non-root user
    ENV VIRTUAL_ENV=/home/${ARG_USERNAME}/venv
    RUN python3 -m venv $VIRTUAL_ENV
    ENV PATH="$VIRTUAL_ENV/bin:$PATH"

    RUN python -m pip install --no-cache --upgrade \
            pip \
            setuptools && \
        python -m pip install --no-cache \
            --no-cache-dir \
            --no-index \
            --find-links=/wheel/wheels \
            /wheel/wheels/lightrun*.whl

    ENV PYTHONUNBUFFERED=1
    CMD ["python"]

    ```

2. Build the Dockerfile with the following command. 
        ```bash
           docker build \
                    --build-arg LIGHTRUN_KEY="<lightrun_secret_key>" \
                    --build-arg COMPANY_ID="<lightrun_company_id>" \
                    --build-arg PYTHON_BASE_TAG="<python_base_tag>" \
                    -t python-alpine-lightrun .
        ```

   - Change `<lightrun_secret_key>` to your Lightrun company key

   - Change `<lightrun_company_id>` to your Lightrun company ID

   - Change  `<python_base_tag>` to your preferred Python Alpine tag.

    **How to get your company details?** 

    a. You can get your `<COMPANY_SECRET>` (`<lightrun_secret_key>`) key by logging into the [Management Portal](https://app.lightrun.com) and inspecting the **Set up an agent** section.
        
    b. You can get your `<lightrun_company_id>` by inspecting your Management Portal dashboard URL. 
            ```bash
            https://app.lightrun.com/company/<lightrun_company_id>
            ```
                    
    c. Configure the `server_url` build arg when using Lightrun on-prem. 
            ```bash
            --build-arg server_url="<server_url>" \
            ```
            
3. Run the Docker container.
        ```bash
        docker run \
            --rm \
            -it \
            --name alpine-agent \
            python-alpine-lightrun \
            /bin/sh
        ```

4. Put your source code into the Docker container.
5. Add the Lightrun agent to your source code by following the instructions in your Lightrun Management Portal.

!!! note
    Installing the Lightrun agent is not required.

    ![Python Agent](/assets/images/py-agent.png)
