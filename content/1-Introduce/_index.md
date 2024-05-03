---
title : "Introduction"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
## Docker
#### Overview
Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker's methodologies for shipping, testing, and deploying code, you can significantly reduce the delay between writing code and running it in production.

#### Docker architecture
**The Docker daemon**: The Docker daemon listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.

**The Docker client**: The Docker client is the primary way that many Docker users interact with Docker. When you use commands, the client sends these commands to Docker daemon, which carries them out. The docker command uses the Docker API. The Docker client can communicate with more than one daemon.

**Docker Desktop**: Docker Desktop is an easy-to-install application for your Mac, Windows or Linux environment that enables you to build and share containerized applications and microservices.

**Docker registries**: A Docker registry stores Docker images. Docker Hub is a public registry that anyone can use, and Docker looks for images on Docker Hub by default.

**Images**: An image is a read-only template with instructions for creating a Docker container.

**Containers**: A container is a runnable instance of an image. You can create, start, stop, move, or delete a container using the Docker API or CLI.

![Docker Architecture](../images/1.introduction/1.1.dockerarch.png?pc=90pt)

{{% notice info %}}
Access to [Docker docs](https://docs.docker.com/) for more detail.
{{% /notice %}}
## Kubernetes
#### Overview
Kubernetes is a portable, extensible, open source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.

#### Kubernetes cluster architecture
**Cluster**: A Kubernetes cluster consists of a set of worker machines, called nodes, that run containerized applications. Every cluster has at least one worker node.

**Control Plane**: The control plane manages the worker nodes and the Pods in the cluster. In production environments, the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault-tolerance and high availability.

**Worker Nodes**: The worker node(s) host the Pods that are the components of the application workload

**kube-api-server**: The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane.

**etcd**: Consistent and highly-available key value store used as Kubernetes backing store for all cluster data.

**Scheduler**: Control plane component that watches for newly created Pods with no assigned node, and selects a node for them to run on.

**Controller Manager**: Control plane component that runs controller processes. Logically, each controller is a separate process, but to reduce complexity, they are all compiled into a single binary and run in a single process. There are many different types of controllers. Some examples of them are:
- Node controller: Responsible for noticing and responding when nodes go down.
- Job controller: Watches for Job objects that represent one-off tasks, then creates Pods to run those tasks to completion.
- EndpointSlice controller: Populates EndpointSlice objects (to provide a link between Services and Pods).
- ServiceAccount controller: Create default ServiceAccounts for new namespaces.

*The above is not an exhaustive list.*

**kubelet**: An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.

**kube-proxy**: kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept.

**pod**: is a single instance of an application and the smallest object, that you can create in Kubernetes.

**Container Runtime Interface (CRI)**: A fundamental component that empowers Kubernetes to run containers effectively. It is responsible for managing the execution and lifecycle of containers within the Kubernetes environment.

**cloud-control-manager**: A Kubernetes control plane component that embeds cloud-specific control logic. The cloud controller manager lets you link your cluster into your cloud provider's API, and separates out the components that interact with that cloud platform from components that only interact with your cluster.

![Kubernetes Cluster Architecture](../images/1.introduction/1.2.k8sarch.png?pc=90pt)

{{% notice info %}}
Access to [Kubernetes docs](https://kubernetes.io/docs) for more detail.
{{% /notice %}}

## Amazon EKS
#### Overview
Amazon Elastic Kubernetes Service (Amazon EKS) is a managed service that eliminates the need to install, operate, and maintain your own Kubernetes control plane on Amazon Web Services (AWS)

#### Amazon EKS architecture

Amazon EKS ensures every cluster has its own unique Kubernetes control plane. This design keeps each cluster's infrastructure separate, with no overlaps between clusters or AWS accounts. The setup includes:
- **Distributed components**: The control plane positions at least two API server instances and three etcd instances across three AWS Availability Zones within an AWS Region.
- **Optimal performance**: Amazon EKS actively monitors and adjusts control plane instances to maintain peak performance.
- **Resilience**: If a control plane instance falters, Amazon EKS quickly replaces it, using different Availability Zone if needed.
- **Consistent uptime**: By running clusters across multiple Availability Zones, a reliable API server endpoint availability Service Level Agreement (SLA) is achieved.

Amazon EKS uses Amazon Virtual Private Cloud (Amazon VPC) to limit traffic between control plane components within a single cluster. Cluster components can't view or receive communication from other clusters or AWS accounts, except when authorized by Kubernetes role-based access control (RBAC) policies.

In addition to the control plane, an Amazon EKS cluster has a set of worker machines called nodes. Selecting the appropriate Amazon EKS cluster node type is crucial for meeting your specific requirements and optimizing resource utilization. Amazon EKS offers the following primary node types:
- **AWS Fargate**: Fargate is a serverless compute engine for containers that eliminates the need to manage the underlying instances. With Fargate, you specify your application's resource needs, and AWS automatically provisions, scales, and maintains the infrastructure. This option is ideal for users who prioritize ease-of-use and want to concentrate on application development and deployment rather than managing infrastructure.
- **Karpenter**: Karpenter is a flexible, high-performance Kubernetes cluster autoscaler that helps improve application availability and cluster efficiency. Karpenter launches right-sized compute resources in response to changing application load. This option can provision just-in-time compute resources that meet the requirements of your workload.
- **Managed node groups**: Managed node groups are a blend of automation and customization for managing a collection of Amazon EC2 instances within an Amazon EKS cluster. AWS takes care of tasks like patching, updating, and scaling nodes, easing operational aspects. In parallel, custom kubelet arguments are supported, opening up possibilities for advanced CPU and memory management policies. Moreover, they enhance security via AWS Identity and Access Management (IAM) roles for service accounts, while curbing the need for separate permissions per cluster.
- **Self-managed nodes**: Self-managed nodes offer full control over your Amazon EC2 instances within an Amazon EKS cluster. You are in charge of managing, scaling, and maintaining the nodes, giving you total control over the underlying infrastructure. This option is suitable for users who need granular control and customization of their nodes and are ready to invest time in managing and maintaining their infrastructure.
![Amazon EKS Architecture](../images/1.introduction/1.3.eksarch.png?pc=90pt)

{{% notice info %}}
Access to [Amazon EKS docs](https://docs.aws.amazon.com/eks/latest/userguide/) for more detail.
{{% /notice %}}
