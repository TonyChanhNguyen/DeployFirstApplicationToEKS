---
title : "Deploy application with K8S"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

### Overview
Kubernetes is a portable, extensible, open source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.

#### Kubernetes cluster architecture
**Cluster**: A Kubernetes cluster consists of a set of worker machines, called nodes, that run containerized applications. Every cluster has at least one worker node.

**Control Plane**: The control plane manages the worker nodes and the Pods in the cluster. In production environments, the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault-tolerance and high availability.

**Worker Nodes**: The worker node(s) host the Pods that are the components of the application workload

**kube-api-server**: The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane.

**etcd**: Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.

**Scheduler**: Control plane component that watches for newly created Pods with no assigned node, and selects a node for them to run on.

**Controller Manager**: Control plane component that runs controller processes. Logically, each controller is a separate process, but to reduce complexity, they are all compiled into a single binary and run in a single process. There are many different types of controllers. Some examples of them are:
- Node controller: Responsible for noticing and responding when nodes go down.
- Job controller: Watches for Job objects that represent one-off tasks, then creates Pods to run those tasks to completion.
- EndpointSlice controller: Populates EndpointSlice objects (to provide a link between Services and Pods).
- ServiceAccount controller: Create default ServiceAccounts for new namespaces.

*The above is not an exhaustive list.*

**kubelet**: An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.

**kube-proxy**: kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept.

**pod**: is a single instance of an application and  the smallest object, that you can create in Kubernetes.

**Container Runtime Interface (CRI)**: A fundamental component that empowers Kubernetes to run containers effectively. It is responsible for managing the execution and lifecycle of containers within the Kubernetes environment.

**cloud-control-manager**: A Kubernetes control plane component that embeds cloud-specific control logic. The cloud controller manager lets you link your cluster into your cloud provider's API, and separates out the components that interact with that cloud platform from components that only interact with your cluster.

![Kubernetes Cluster Architecture](../images/1.introduction/1.2.k8sarch.png?pc=90pt)

{{% notice info %}}
Access to [Kubernetes docs](https://kubernetes.io/docs) for more detail.
{{% /notice %}}

### Content

+ 5.1 [Install Kubernetes](5-deploytok8s/5.1-installk8s/)
+ 5.2 [Deploy application with Kubernetes POD by kubectl](5-deploytok8s/5.2-deployk8simperative/)
+ 5.3 [Deploy application with Kubernetes POD by YAML manifest file](5-deploytok8s/5.3-deployk8sdeclarative/)