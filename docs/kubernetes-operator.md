# Lightrun Kubernetes Operator

The Lightrun Kubernetes (K8s) Operator is a Kubernetes operator provided by Lightrun to help install Lightrun agents in your Kubernetes workloads without having to change your docker or manifest files. 

The Lightrun Kubernetes operator project was initially scaffolded using [kubebuilder book](https://book.kubebuilder.io/) and [operator-sdk](https://sdk.operatorframework.io/), and the project aims to follow the [Kubernetes Operator pattern](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/). You can find the project’s GitHub repository [here](https://github.com/lightrun-platform/lightrun-k8s-operator).

## How does the Lightrun Kubernetes Operator work?

To add and debug with Lightrun agents in your Kubernetes cluster, you must:

1. Install a Lightrun agent into the cluster (with initContainers or with Persistent Volumes).
2. Instruct your application to start using the installed agent.

The Lightrun K8s Operator carries out these two steps automatically for you. You can learn more about how the Lightrun K8s Operator works by checking out the following [link](https://github.com/lightrun-platform/lightrun-k8s-operator/blob/main/docs/how.md).

!!! note
	[Read this before deploying the Lightrun K8s Operator to production](https://github.com/lightrun-platform/lightrun-k8s-operator/blob/main/docs/before_prod.md). 

## Setup the Lightrun Kubernetes Operator

### Prerequisites
This tutorial assumes that you are using Kubernetes version 1.25 or later.

### Install the Lightrun Kubernetes Operator

1. Create a namespace for the Lightrun Kubernetes Operator.
	```bash
	kubectl create namespace lightrun-operator
	```
2. Deploy the Lightrun Kubernetes Operator to the created namespace.
	```bash
	kubectl apply -f https://raw.githubusercontent.com/lightrun-platform/lightrun-k8s-operator/main/examples/operator.yaml -n lightrun-operator
	```
3. To show how the Lightrun operator works, we have created a test deployment for you. You can access the `deployment.yaml` file [here](https://raw.githubusercontent.com/lightrun-platform/lightrun-k8s-operator/main/examples/deployment.yaml).  Create a sample deployment namespace and deploy the `deployment.yaml` file to the created namespace.
	```bash
	$ kubectl create namespace lightrun-agent-test
	$ kubectl apply -f https://raw.githubusercontent.com/lightrun-platform/lightrun-k8s-operator/main/examples/deployment.yaml -n lightrun-agent-test
	```
4. Create a test folder.
	```bash
	mkdir lightrun_operator_test
	```
5. Download the Lightrun K8s Operator agent configuration file into the test folder.
	```bash
	curl https://raw.githubusercontent.com/lightrun-platform/lightrun-k8s-operator/main/examples/lightrunjavaagent.yaml > agent.yaml
	```
	An `agent.yaml` file will appear in the test folder.

6. Open the `agent.yaml` file in your preferred code editor and edit the following configuration options.

   - `serverHostname`: The `serverHostname` value is your Lightrun server url. For SaaS, the value is `app.lightrun.com`, while on-prem users will have to use their own hostname.

   - `lightrun_key`: Your Lightrun secret key.

   - `pinned_cert_hash`: You can get this value by navigating to `https://<serverHostname>/api/getPinnedServerCert`. *Note - you have to be authenticated to the Lightrun server to view the key*.

7. Create the agent Custom resource.
	```bash
	kubectl apply -f agent.yaml -n lightrun-agent-test
	```
8. Login to your Lightrun management portal to confirm if the new agent was registered.

### Install the Lightrun Kubernetes Operator with Helm Chart

1. Add the Lightrun K8s Operator repository to your Helm repository list.
	```bash
	helm repo add lightrun-k8s-operator https://lightrun-platform.github.io/lightrun-k8s-operator
	```
2. Install the Helm chart repository using one of these methods:

   - Install using default values.
	```bash
	helm install lightrun-k8s-operator/lightrun-k8s-operator  -n lightrun-operator --create-namespace
	```

   - Install using a custom values file.
	```bash
	helm install lightrun-k8s-operator/lightrun-k8s-operator  -f <values file>  -n lightrun-operator --create-namespace
	```

3. To uninstall the Helm chart.
	```bash
	helm delete lightrun-k8s-operator
	```

!!! note 
	- `helm upgrade --install` or `helm install --dry-run` may not work properly due to limitations of how Helm work with CRDs. You can find more info [here](https://helm.sh/docs/chart_best_practices/custom_resource_definitions/).

	- CRDs will not be deleted due to Helm CRDs limitations. You can learn more about the limitations [here](https://helm.sh/docs/topics/charts/#limitations-on-crds).

#### Chart version vs controller version

For the sake of simplicity, we are keeping the convention of the same version for both the controller image and the Helm chart. This helps to ensure that controller actions are aligned with CRDs preventing failed resource validation errors.

## Lightrun Kubernetes Operator Limitations

1. If an application has [JDWR](https://en.wikipedia.org/wiki/Java_Debug_Wire_Protocol) enabled, it will cause a conflict with the Lightrun agent installed by the Lightrun K8s operator.
2. You must install the correct init container for your application’s container platform. For example, `lightruncom/k8s-operator-init-java-agent-linux:1.7.0-init.0`.

	Supported platforms:

   - Linux

   - Alpine

   K8s type of deployment:

   - Deployment

   Supported languages:

   - Java