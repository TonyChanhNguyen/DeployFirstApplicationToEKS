---
title : "Install Kubernetes tools"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 5.1 </b> "
---

First, we need to install Kubernetes tool (Minikube) to your workspace instance. **Minikube** is a tool that lets you run a single-node Kubernetes cluster on your personal computer or in EC2 instance so that you can try out Kubernetes.

Minikube is a lightweight Kubernetes (K8) installation, which can create a Virtual Machine (VM) on your local instance or in a cloud instance, which deploys a simple cluster containing only one node.

But to install kubectl and minikube on your workspace instance, its storage capacity must be redundant. So first, we need to expand the storage capacity of workspace instance.

### Expand storage capacity to 50GB.
1. Go to EC2 instance of your workspace instance.
![Install K8S](../../images/5.deployapptok8s/5.1.installkubectl/5.1.5.installkubectl.png?pc=90pt)

2. Navigate to **Storage** tab.
3. Click on **Volume ID**.
![Install K8S](../../images/5.deployapptok8s/5.1.installkubectl/5.1.6.installkubectl.png?pc=90pt)

Your storage capacity now is 10GB. We will upgrade it to 50GB.
4. Select your EBS volume.
5. Click on **Action**. Then select **Modify volume**.
![Install K8S](../../images/5.deployapptok8s/5.1.installkubectl/5.1.7.installkubectl.png?pc=90pt)
6. Change from **10** to **50** at **Size (GiB)** field.
7. Click on **Modify**.
![Install K8S](../../images/5.deployapptok8s/5.1.installkubectl/5.1.8.installkubectl.png?pc=90pt)

8. Then, click on **Modify** to confirm.
![Install K8S](../../images/5.deployapptok8s/5.1.installkubectl/5.1.9.installkubectl.png?pc=90pt)

9. Go back to Cloud9 terminal, execute the below command to reboot your workspace instance.
```
sudo reboot
```
![Install K8S](../../images/5.deployapptok8s/5.1.installkubectl/5.1.10.installkubectl.png?pc=90pt)

10. After workspace instance reboot successfully. Check the result.
```
df -h
```
There is a volume mounted to your workspace instance with capacity is 43GB.
![Install K8S](../../images/5.deployapptok8s/5.1.installkubectl/5.1.11.installkubectl.png?pc=90pt)


### Install kubectl
1. At **Cloud9 Terminal**, execute those command to install **kubectl**.
+ Update the instance packages.
```bash
sudo yum update
```
+ Install kubectl.
```bash
curl -LO https://dl.k8s.io/release/v1.30.0/bin/linux/amd64/kubectl
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```
2. Check version of **kubectl**.
```
kubectl version --client
```

![Install K8S](../../images/5.deployapptok8s/5.1.installkubectl/5.1.3.installkubectl.png?pc=90pt)


### Install minikube
1. At **Cloud9 Terminal**, execute those command to install **minikube**.
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
```
2. Start Kubernetes Cluster with **minikube**.
```
minikube start
```
3. Check the version.
```
minikube version
```
![Install K8S](../../images/5.deployapptok8s/5.1.installkubectl/5.1.12.installkubectl.png?pc=90pt)


