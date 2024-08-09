# Lightrun On-Premises Deployment Guide

## Overview

This guide is for DevOps or Network Engineers who wish to deploy and maintain a local instance of the Lightrun Observability platform. At a high level, the platform is composed of three main components, described below. This guide is aimed at the installation of the Lightrun Server, which is distributed as a set of containers. The other components - Agents and Plugins - are described briefly, for context, though their installation and use are likely the responsibility of others, such as the developers who will use Lightrun on a day-to-day basis. This document describes the server's installation to a Kubernetes cluster using a helm chart provided by Lightrun. Other options are available and described in other documents.

## Lightrun Architecture

**Server** - Along with management capabilities such as Audit logs, Authentication, Access Control, and Configuration management, the Lightrun Server is the hub that coordinates all communication between Lightrun Agents and IDE Plugins, acting as a "middleman" between them.

**Agent** - A Lightrun Agent runs alongside each workload that is to be monitored. Developers or DevOps engineers integrate the agent with their code following language-specific directions. Integrating the agent with the application enables the use of Lightrun's capabilities: adding logs, metrics, and snapshots at runtime, without application redeployment.

Agent installation is described as part of the user account creation process in the Lightrun Management Server user interface and documented as part of the Lightrun product documentation.

**Plugin** - Lightrun plugins are IDE add-ons that provide observability capabilities directly in the IDE. By using the Lightrun plugin, developers can invoke Lightrun logs, metrics, and snapshots in running code, without redeployments, directly from their IDE.

Developers install the Lightrun Plugin following the directions provided as part of the user account creation process in the Lightrun Server web user interface.

## System Components

The management server is built of the following components which should be deployed together but can be scaled independently:

- Frontend: a web application that provides the web user interface through which administrators monitor and control the use of the system. Beyond administration, "regular" users will interact with the frontend during their initial sign-up process. In general, the frontend does not experience heavy load and does not need to be scaled beyond a small number of instances for high availability.
  
- Backend: the heart of the server, where all business logic is executed. The web front end, developer IDE plugins, and monitoring agents all communicate with the backend to provide Lightrun’s end-to-end observability capabilities.
  
- Keycloak: a third-party open-source Identity and Access Management solution, Lightrun leverages Keycloak's capabilities to manage authentication and authorization, and to enable Single Sign-On via easy integration with the customer's backing providers.
  
- Redis: used for Lightrun application caching purposes
  
- MySQL: The Lightrun Server helm chart offers the option to deploy a dedicated instance of MySQL Server which will provide the system’s data storage for all configuration and ephemeral usage information. While this option is convenient, most customers choose instead to configure the Lightrun Server to leverage an external MySQL system instead, as most organizations have already deployed and are already monitoring and maintaining a MySQL server. 

## System Requirements

- Kubernetes version >= 1.23
- Docker Engine 20.10 or newer
- Linux with GLIBCXX_3.4.19 or newer (Ubuntu 16+, Centos 7+ or equivalent)
- Kernel version >= 4.4

## Minimal Resources Allocation

| Scale / Deployment   | Frontend | Backend             | Keycloak           | Redis              | MySQL             |
|----------------------|----------|---------------------|--------------------|--------------------|-------------------|
| Up to 1000 agents    | 1 replica | cpu: 1000m<br>memory: 2G | 2 replicas<br>cpu: 3000m<br>memory: 16G | 1 replica<br>cpu: 1000m<br>memory: 2G | 1 replica<br>cpu: 500m<br>memory: 512Mi<br>min 16GB storage |
| 1000-10000 agents    | 1 replica | cpu: 2000m<br>memory: 4G | 8 replicas<br>cpu: 4000m<br>memory: 16G | 1 replica<br>cpu: 2000m<br>memory: 8G | 1 replica<br>cpu: 1000m<br>memory: 1G<br>min 50GB storage |
| 10000-20000 agents   | 1 replica | cpu: 2000m<br>memory: 8G | 16 replicas<br>cpu: 4000m<br>memory: 16G | 1 replica<br>cpu: 2000m<br>memory: 8G | 1 replica<br>cpu: 1000m<br>memory: 1G<br>min 1000GB storage |
| More than 20000 agents | To be discussed | | | | |

*The deployment should be monitored by APM tools. The resources allocated to the deployment should be adapted and optimized to match the actual usage demands. This proactive approach ensures the system remains efficient, scalable, and capable of handling varying workloads.

## Deployment at a Glance

Please see Appendix I for the detailed explanation.

Prior to installation, we suggest that your DevOps engineers review the Lightrun Helm chart and accompanying documentation. They should ensure they are comfortable with setting up suitable infrastructure that meets or exceeds the minimum recommendations mentioned in the chart. By planning ahead and coordinating with your Solution Engineer, we can ensure compatibility with your environment and provide guidance on how to adjust the helm configuration to suit your needs.

External access to the services in a cluster. By default, Lightrun Management Server exposes the services via NGINX Ingress Controller, while 3 ingress objects are created by the chart separating client, server (agent), and management networks. For clusters with no Ingress Controller, the chart will create an nginx deployment as a LoadBalancer service. In OpenShift environments, external endpoints are exposed to the outside of the cluster through routers.

Lightrun requires a MySQL (InnoDB) database to store configuration and application state. The helm chart supports deploying an instance of our own database or connecting to an existing MySQL database, which should be pre-configured in accordance with the following: (1) Default database name lightrunserver, (2) name comparisons are not case-sensitive lower_case_table_names=1. For using Horizontal Pod Autoscaling functionality, metrics-server needs to be installed as a prerequisite. Deployment resource allocation is set in accordance with load specifications. These settings should be changed in values.yml prior to the installation. Please see Appendix I for detailed information.

- lightrun_endpoint - Management Server URL
- certificate - existing secret or base64 representation of the Management Server
- license - your license provided by Lightrun

## Getting Started

Once the helm chart is installed and all pods are up and running you can access the Lightrun Management console by browsing to lightrun_endpoint URL, you’ve specified in values.yml.

**Lightrun Backend Boot Image**

For the first login, you should use the default manager account.
- Username: manager@localhost.com
- Password: is the value of a Secret object KEYCLOAK_PASSWORD

Now, developers can register to the server and log in to the Lightrun Management console, download the Lightrun plugins or Lightrun CLI and follow the instructions to install an agent.

## Appendix I: Settings in values.yml Explained

### DB

- db_local: true - if you want to create a new MySQL Server deployment inside k8
