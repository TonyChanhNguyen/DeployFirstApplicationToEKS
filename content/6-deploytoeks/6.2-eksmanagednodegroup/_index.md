---
title : "Deploy application to EKS Cluster Managed Nodegroup"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 6.2 </b> "
---

### Create EKS Cluster
1. At Cloud9 terminal, execute command below to create EKS Cluster.
```
eksctl create cluster --name=my-fcj-cluster --region=ap-southeast-1 --zones=ap-southeast-1a,ap-southeast-1b --managed --nodegroup-name=my-fcj-node --nodes=2 --node-type=t3.micro
```
![Amazon EKS Managed NodeGroup](../../images/6.deployapptoeks/6.2.managednodegroup/6.2.1.managednodegroup.png?pc=90pt)
{{% notice info %}}
It will take you about 20 minutes to finish. 
{{% /notice %}}
![Amazon EKS Managed NodeGroup](../../images/6.deployapptoeks/6.2.managednodegroup/6.2.2.managednodegroup.png?pc=90pt)
2. After Cluster creation process finish, list your cluster on workspace machine.
```
eksctl get cluster
```
![Amazon EKS Managed NodeGroup](../../images/6.deployapptoeks/6.2.managednodegroup/6.2.3.managednodegroup.png?pc=90pt)

3. List Nodes in Cluster.
```
kubectl get node
```
![Amazon EKS Managed NodeGroup](../../images/6.deployapptoeks/6.2.managednodegroup/6.2.4.managednodegroup.png?pc=89pt)

There are 2 nodes listed in EKS Cluster.

4. Let go to [EC2 Instance](https://ap-southeast-1.console.aws.amazon.com/ec2/home?region=ap-southeast-1#Instances:instanceState=running;tag:alpha.eksctl.io/nodegroup-name=my-fcj-node;v=3;$case=tags:true%5C,client:false;$regex=tags:false%5C,client:false) to see the instance associated to Node Group.
![Amazon EKS Managed NodeGroup](../../images/6.deployapptoeks/6.2.managednodegroup/6.2.5.managednodegroup.png?pc=90pt)

There are 2 instances created (match with **--nodes=2** on **eksctl command**) with name is **my-fcj-cluster-my-fcj-node-Node** (format `<Cluster-Name>-<NodeGroup-Name>-Node`), type is **t3.micro** (match with **--node-type=t3.micro** on **eksctl command**) and Availability Zone is **ap-southeast-1a** and **ap-southeast-1b** (match with **--zones=ap-southeast-1a,ap-southeast-1b** on **eksctl command**).


### Explore EKS Cluster
1. Go to [CloudFormation](https://ap-southeast-1.console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks), we will see there are 2 stacks created - 1 for creating EKS Cluster and 1 for EKS NodeGroup.
![Amazon EKS Managed NodeGroup](../../images/6.deployapptoeks/6.2.managednodegroup/6.2.6.managednodegroup.png?pc=90pt)

2. Go to [Amazon EKS](https://ap-southeast-1.console.aws.amazon.com/eks/home?region=ap-southeast-1), we will see there is a EKS Cluster named **my-fcj-cluster**. Click on it.
![Amazon EKS Managed NodeGroup](../../images/6.deployapptoeks/6.2.managednodegroup/6.2.7.managednodegroup.png?pc=90pt)

3. Navigate to **Compute** tab.
4. We will see the node group named **my-fcj-node** with **Desired size** is 2 associated to EKS Cluster at **Node groups** field.
![Amazon EKS Managed NodeGroup](../../images/6.deployapptoeks/6.2.managednodegroup/6.2.8.managednodegroup.png?pc=90pt)

### Deploy application to EKS Cluster
1. At **kube-manifest** directory, execute those command to deploy application to EKS Cluster.
```
kubectl apply -f .
```

2. List the service created.
```
kubectl get svc
```
or
```
kubectl get service
```
![Amazon EKS Managed NodeGroup](../../images/6.deployapptoeks/6.2.managednodegroup/6.2.9.managednodegroup.png?pc=90pt)

3. Access to **LoadBalancer HostName** to see the result. Replace your service's **EXTERNAL-IP** on ```http://<REPLACE-YOUR-EXTERNAL-IP>:8080```.

*Example:* In my case the host name will be http://a6d733c6da3c1499f9ac945a665aa815-1253515241.ap-southeast-1.elb.amazonaws.com:8080
![Amazon EKS Managed NodeGroup](../../images/6.deployapptoeks/6.2.managednodegroup/6.2.10.managednodegroup.png?pc=90pt)


#### Congratulations, you had deployed your application to EKS CLuster Managed Node Group successfully.

### Clean up.
1. At Cloud9 terminal, to delete all resources created. Execute command below.
```
kubectl delete -f .
```
![Amazon EKS Managed NodeGroup](../../images/6.deployapptoeks/6.2.managednodegroup/6.2.11.managednodegroup.png?pc=90pt)

2. List all resources to make sure that they are deleted totally.
```
kubectl get all
```
![Amazon EKS Managed NodeGroup](../../images/6.deployapptoeks/6.2.managednodegroup/6.2.12.managednodegroup.png?pc=90pt)

3. Delete your node group.
```
eksctl delete nodegroup --cluster my-fcj-cluster --name my-fcj-node --region ap-southeast-1 --drain=false
```
![Amazon EKS Managed NodeGroup](../../images/6.deployapptoeks/6.2.managednodegroup/6.2.13.managednodegroup.png?pc=90pt)

4. After about 10 minutes, list node on your cluster to confirm they are deleted.
```
kubectl get node
```
![Amazon EKS Managed NodeGroup](../../images/6.deployapptoeks/6.2.managednodegroup/6.2.14.managednodegroup.png?pc=90pt)