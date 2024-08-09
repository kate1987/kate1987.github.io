---
password: lightrun2024
---

# Lightrun On-premises deployment guide

This guide is intended for DevOps or network engineers who wish to deploy and maintain a local instance of the Lightrun Observability platform and describes step-by-step instructions on how to install the server on a Kubernetes cluster using a Helm chart provided by Lightrun. 

At a high level, the platform is composed of three main components - the Server, the agents, and the plugins. The agents and plugins are described briefly for context, though their installation and use are likely the responsibility of others. Such as the developers who will use Lightrun on a day-to-day basis. The focus is on the Lightrun Server installation, which is distributed as a set of containers. 

## Lightrun Architecture

The Lightrun platform comprises of these main components:

### Server

Along with management capabilities such as audit logs, authentication, access control, and configuration management, the Lightrun Server is the hub that coordinates all communication between Lightrun agents and IDE plugins, acting as a “middleman” between them. 
The management server is built of the following system components which should be deployed together, but can be scaled independently:

- **Frontend**: A web application that provides the web user interface through which administrators monitor and control the use of the system.
- **Backend**: The heart of the server, where all business logic is executed. The web frontend, developer IDE plugins, and monitoring agents all communicate with the backend to provide Lightrun’s end-to-end observability capabilities.
- **Keycloak**: A third-party open-source Identity and Access Management solution, Lightrun leverages Keycloak’s capabilities to manage authentication and authorization, and to enable Single Sign-on (SSO)via easy integration with the customer’s backing providers.
- **Redis**: Used for Lightrun application caching purposes.
- **MySQL**: The Lightrun Server Helm chart offers the option to deploy a dedicated instance of MySQL Server that will provide the system’s data storage for all configuration and ephemeral usage information.

### Agent

A Lightrun agent runs alongside each workload that is to be monitored. Developers or DevOps engineers integrate the agent with their code following language-specific directions. Integrating the agent with the application enables the use of Lightrun’s capabilities: adding logs, metrics, and snapshots at runtime, without application redeployment. Agent installation is described as part of the user account creation process in the Lightrun Management Server user interface. For more information, see [Lightrun agents](/introduction/agents/).

### Plugin

Lightrun plugins are IDE add-ons that provide observability capabilities directly in the IDE. By using the Lightrun plugin, developers can invoke Lightrun logs, metrics, and snapshots in running code, without redeployments, directly from their IDE. Developers install the Lightrun Plugin following the directions provided as part of the user account creation process in the Lightrun Server web user interface. For more information, see [Lightrun plugins](/introduction/plugins/).

## System Requirements

- Kubernetes version &ge; 1.23
- Docker Engine 20.10 or later
- Linux with `GLIBCXX_3.4.19` or later (Ubuntu 16+, Centos 7+ or equivalent)
- Kernel version &ge; 4.4

## Before you Begin

Before initiating the installation process, we recommend that your DevOps engineers review the Lightrun Helm chart and accompanying documentation. They should ensure they are comfortable with setting up suitable infrastructure that meets or exceeds the minimum recommendations mentioned in the chart. By planning ahead and coordinating with your Solution Engineer, we can ensure compatibility with your environment and provide guidance on how to adjust the Helm configuration to suit your needs.

1. **Set your endpoint and deployment credentials**

    The following setting should be set the in `values.yaml` prior to the installation. For more information, see [Appendix A](#appendixa).

   - `lightrun_endpoint`: Management Server URL.
   - `certificate`: Existing secret or base64 representation of the Management Server.
   - `license`: Your license provided by Lightrun.
  
2. **Enable system API keys**
   
    The system API keys feature requires that the server have an AES key which it uses to encrypt the API keys. The AES encryption key will be read from the initially empty file: `./keys/aes.key`

    a. Generate the key which should be of 128 bit length and hex encoded.

    ```shell
    openssl rand -hex 16 > ./keys/aes.key
    ```
        
    b. Add support for AES key management encryption to the `values.yaml` file.
            
    ```shell
    general:
        api_keys_encryption:
                enabled: false
                key_mount_path: "/keys"
    secrets:
        api_keys_encryption:
                aes_key: ""
    ```
3. **Deploy an MySQL database**

    Lightrun requires a `MySQL` (`InnoDB`) database to store configuration and application state. The Helm chart supports deploying an instance of our own database or connecting to an existing MySQL database, which should be pre-configured in accordance with the following: (1) Default database name `lightrunserver`, (2) name comparisons are not case-sensitive `lower_case_table_names=1`.  

4. **Set up external access to the services in a cluster**

    By default, the Lightrun Management Server exposes the services via an NGINX Ingress Controller, while three ingress objects are created by the chart separating client, server (agent), and management networks. For clusters with no Ingress Controller, the chart will create an nginx deployment as a LoadBalancer service. In OpenShift environments, external endpoints are exposed to the outside of the cluster through routers. 
   
5. **Deploy a metrics-server**

    For using Horizontal Pod Autoscaling functionality, deploy a [metrics-server](https://artifacthub.io/packages/helm/metrics-server/metrics-server). Deployment resource allocation is set in accordance with load specifications. These settings should be changed in `values.yaml` prior to the installation. For more information, see [Appendix A](#appendixa).


## Install the Lightrun server using Helm charts

1. Create a dedicated namespace to host the Lightrun server.

    ```shell
    kubectl create namespace lightrun
    ```
    
2. Navigate to the Lightrun Chart directory where the Lightrun Helm chart files are available (`values.yaml` and `Chart.yaml`).

3. Install the Lightrun server  in the previously created namespace using Helm.
   
    ```shell
    helm install lightrun-server . -n lightrun
    ```

4. Validate the status of the Pod. Confirm that all pods are up and running. This may take a few minutes for all pods to successfully deploy:

    ```shell
    kubectl get pods -n lightrun
    ```


## Get Started

Once the Helm chart is installed and all pods are up and running, you can access the Lightrun Management console by browsing to the `lightrun_endpoint` URL that you've specified in the `values.yaml` file.

![lightrun backend boot image -half](/assets/images/lightrun-backend-boot-image.png)

For the first login, you should use the default manager account.

- Username: `administrator@localhost.com`
- Password: The value of a Secret object `password`

Now, developers can register to the server and log in to the Lightrun Management console, download the Lightrun plugins or Lightrun CLI, and follow the instructions to install the Lightrun agent.


## Appendix A: Lightrun `values.yaml` Configuration file {#appendixa}

The Lightrun application has a dedicated `values.yaml` file with predefined parameters dictating the application. These parameters can be modified to meet your specific needs, offering flexibility in tailoring the application to your requirements.

### Database

- `db_local: true`: To create a new MySQL Server deployment inside k8s, as opposed to connecting to the existing one.
- `statefulset`: Relevant only to local DB in k8s.
- `db_endpoint`: Hostname of external DB. In case of local DB, the `db_endpoint` will be ignored and replaced with the appropriate deployment name.

![db local diagram](/assets/images/db-local-diagram.png)

### Message Queue

- `enabled: false`: Configure backend to use `message queue local: true.`  If set to `true`, will create statefulset with rabbitmq pod and service `mq_endpoint`. 
- When set to `local: false`, it will provide FQDN to connect to port. The port that will be used to connect to message queue. Default: `5672`.
- When set to `local: false`, all other properties of `mq` will be ignored.
For testing purposes, you can create a statefulset without a PVC (`PersistentVolumeClaim`)
In this case all data of `MQ` will be lost on `pod restart`.

    ```shell
    mq:
       storage: "0"
    ```

- `metrics: true`, Prometheus plugin will be enabled in the `RabbitMQ`.
Metrics will be exposed via the service on port `15692`
If you want to collect those metrics using Prometheus autodiscovery, you can provide annotations to that service in the deployments part of the values.

    ```shell
    deployments:
        rabbitmq:
            service:
                annotations:
                    prometheus.io/scrape: 'true'
                    prometheus.io/path: '/metrics'
                    prometheus.io/port: '15692'
    ```

    ![mq enabled diagram](/assets/images/mq-enabled-diagram.png)

### Ingress Controller

- `ingress_controller: true`:
If you have an existing Nginx ingress controller it can be utilized with ingress objects that will be created by this chart. Other ingress controllers may also be supported with adjustments to the annotations in `values.yaml`. Alternatively, the chart can be set to install a new Nginx pod as a Load balancer in place of an ingress controller.
- `ingress_class_name: nginx`:
Class name of the ingress controller that will be used to forward traffic to the deployment.
If there is no ingress controller (and a new one can't be installed), the chart will create an `nginx` deployment as a `LoadBalancer` service. For this setup to work k8s has to have some addon or any other way to serve external IP addresses for the load balancer, and to route traffic to it.
For more information, see [here](https://www.tkng.io/services/loadbalancer/).

    ```shell
    nginx_svc:
        type: LoadBalancer
    ```

- `ClusterIP` also supported for specific use cases, but only if port forwarding will be done on port 443:443.

    ```shell
    sudo kubectl port-forward service/<chart release name>-nginx 443:443
    ```

    ![Ingress controller diagram](/assets/images/ingress-controller-diagram.png)

### Network Policy
Refer to the `general.networkPolicy` key in `values.yaml` for a detailed explanation with examples.
for `networkPolicy.enabled: false`.
This setting determines whether network policy should be created as a part of the Helm chart installation. As stated in official Kubernetes documentation, in order to use this feature, a supported network plugin has to be installed in the cluster.
Otherwise, the creation of this object will have no effect.

!!! note

    The network policy applies to all pods within the namespace where the chart is installed.
    General flow control of a particular direction, either ingress or egress would look like:

![Network Policy diagram](/assets/images/network-policy-diagram.png)

The mandatory namespaces are:

- `namespace`: Where the chart is installed
- `kube-system`: `kube-system` is necessary to allow DNS communication. if the internal DNS resides on a different namespace then that namespace should be allowed from `values.yaml`.

### Internal TLS
By default, pods inside the cluster establish internal connections to each other without SSL encryption enabled, since SSL operations are computationally expensive. Therefore SSL is terminated on the client-facing load balancer.
In some cases, security policy requires that SSL encryption is used everywhere, including internal communication of the pods. Usually, such a requirement is handled by service mesh proxies, but in certain cases, it has to be done on the pod level.
For such cases we have introduced a new key internal_tls in `values.yaml` to enable encryption of the communication between the pods (backend -> keycloak, ingress -> frontend, etc).

!!! Note
        If internal TLS is enabled, we highly recommend adding more resources to allow servers to carry out SSL operations

#### Configure internal TLS

`Control` flag, setting to `true` will enable internal TLS

```shell
default value: false
enabled: true
```
    
There are 2 ways to provide certificates to pods:

```shell
certificates:
   source: "one of 2 options below"
```

```shell
generate_self_signed_certificates default option
```

Self-signed certificates for all pods (except backend and MySQL) will be generated using built-in capabilities of Helm. The common name of certificates will contain a service name. Certs are generated for 10 years. using this option will produce secrets of type: `kubernetes.io/tls` per pod's certificate.
Each secret will include these Helm hooks:

```shell
"helm.sh/hook": "pre-install"
"helm.sh/hook-delete-policy": "before-hook-creation"
```

So that those secrets won't be recreated during Helm upgrade.
!!! Note for ArgoCD users
    ArgoCD will still rotate those secrets on the "full sync" operation. This is due to the way ArgoCD works with Helm.
    This, however, will not cause an issue, as pods will not be redeployed on the certificate change.
    And when you trigger recreation of the pods for any reason, they'll get the new certificates on startup and continue to work as before.

    ```shell
    existing_certificates
    ```

You can provide the names of the k8s secrets with certificates created outside of this chart to be used for TLS.
Secrets should contain the following keys: `tls.crt`, `tls.key`
If the certificate's SAN has the DNS name of all services, it can be reused in all fields. The secrets have to be in the same namespace.

```shell
existing_certificates: 
   frontend: ""
   keycloak: ""
   redis: "" 
   rabbitmq: ""   
```

#### Certificate verification
By default, pods are configured to verify remote SSL certificates. This can be customised using the following control flag:

```shell
verification: "true"
```
By default, the pods will rely on the system's default well-known trusted CAs.
If you are using private CA, you can provide a secret with the CA certificate that was used to sign all other pods certificates (provided via `@param internal_tls.certificates.existing_certificates`)
This secret should contain the key: `ca.crt` should be in the same namespace.
 
 ```shell
    existing_ca_secret_name: some-ca-secret
```

#### Ingress configuration
If the `ingress_class_name` is nginx, the chart will automatically add an annotation to all ingress objects:

 ```shell
    nginx.ingress.kubernetes.io/backend-protocol: "HTTPS"
```
If you are using a different ingress controller, you'll need to add appropriate annotations via ingress values by yourself, or with the support of your Lightrun Solution Engineer.

The following diagram displays a visualized version of internal tls flow control.

![Internal tls diagram](/assets/images/internal-tls-diagram.png)

### Deployments
#### Backend
Amount of memory for `_JAVA_OPTIONS` is calculated from the memory limit of the pod
As of Lightrun version 1.14, the backend component requires connectivity to Lightrun's public S3 bucket for access to artifacts related to the IDE plugin.
For on-prem servers where access to an external S3 repository is not possible or desired, its use can be disabled with the following flag.
When disabled, IDE plugin installation and update will require additional manual intervention. Reach ot to Lightrun's customer support team to get guidance.

```shell
deployments:
    backend:
       artifacts:
            enable: false
```

### SecurityContext
Each deployment has these two parameters in order to control the `securityContext:`


```shell
podSecurityContext: {}
containerSecurityContext: {}
```

- On pod level, allow users to provide custom `SecurityContext`. The default is empty, except for the MySQL pod which has the default mandatory parameter `fsGroup: 10001`.

- On container level, each deployment has default parameters that cannot be overwritten, which are:

    ```shell
    runAsNonRoot: true
    seccompProfile:
        type: RuntimeDefault
    runAsUser: <custom_per_container>
    allowPrivilegeEscalation: false
    capabilities:
        drop:
        - "ALL"
    ```

- `containerSecurityContext`: If not empty then default values will be merged with `containerSecurityContext` from values using the following logic: non-overlapping fields will be added.
overlapping fields will be preserved from the default values. The purpose is to preserve the User id that will be used by the container for filesystem permissions.

#### Read-Only Root Filesystem
It is possible to control the mounted root filesystem for frontend, backend, and keycloak containers to be read-only. This is done by setting `general.readOnlyRootFilesystem: true`.

### Secrets
If `deploy_secrets: true` is set,  secrets will be deployed as part of this chart. If you don't want to store secrets in GitHub (Lightrun recommends that you don't), copy the `values.yaml` to a local folder and run helm with arguments `-f /path/to/file/values.yaml`.

#### Defaults
Some secrets are related to Lightrun integrations with various systems. They are configurable under:

```shell
secrets:
    Defaults:
```
#### Certificates
Lightrun uses certificates to ensure secure communication between the server and the developer's IDE plugin and between the server and the agents which it monitors. There is an option to use the existing certificate via e secret of type `kubernetes.io/tls`.


```shell
certificate:
   existing_cert: <name-of-the-secret>
```

Note that this secret has to be in the same namespace as the chart.


#### Deploying secrets outside of this chart

```shell
deploy_secrets: false
```

If you want to generate secrets and create them in k8s outside of this chart, you can copy the  `secrets.yaml` and put your own values in the fields that refer to helm values.
All the other secrets should remain the same.

The values that must be set are as follows:

```shell
general:
name: "client-name"   
lightrun_endpoint: "lightrun.example.com"
db_local: false
db_endpoint: "mysql.example.com" 
db_database: lightrunserver
ingress_controller: true
```

```shell
certificate:
    tls:
    crt: ""
    key: ""
    
secrets: <-- everything here
```

For a Production installation, consider providing more resources to `backend/frontend/keycloak` deployments.
