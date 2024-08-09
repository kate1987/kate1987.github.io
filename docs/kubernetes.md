# Installing Lightrun in Kubernetes

Since Lightrun works on the application level, there is no need for any extra configuration while installing Lightrun in Kubernetes - you can simply follow the [Docker container installation instructions](./docker.md) for the language your application is written in. 

Once your `Dockerfile` is ready, you can re-push the images into the relevant registry (like Docker hub), and Lightrun will work 
out-of-the-box.

### Lightrun Kubernetes Operator
The Lightrun Kubernetes (K8s) Operator is a Kubernetes operator provided by Lightrun to help install Lightrun agents in your Kubernetes workloads without having to change your docker or manifest files. You can find instructions on how to set up the Lightrun Kubernetes Operator [here](/kubernetes-operator/).

### Lightrun on a local Kubernetes cluster

If you'd like to get started using Lightrun in a local Kubernetes cluster, we offer a step-by-step tutorial for running [Lightrun on Minikube](minikube.md) - which might prove useful for experimentation purposes. 
