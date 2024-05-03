---
title : "Deploy application to EKS Cluster"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---
### Overview
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

### Content
+ 6.1 [Install eksclt](6-deploytoeks/6.1-installeks/)
+ 6.2 [Deploy application by EKS Cluster Managed nodegroup](6-deploytoeks/6.2-eksmanagednodegroup/)