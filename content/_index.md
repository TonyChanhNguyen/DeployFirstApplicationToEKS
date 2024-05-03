---
title : "Deploy first application on Amazon EKS"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# Deploy first application on Amazon EKS

### Overview

In this hands-on lab, we will learn fundamental knowledge and how can deploy a basic application on Docker, Kubernetes and Amazon EKS. 

![DockerandK8SandEKS](images/DockerK8SEKS.png?pc=90pt)

### Content
1. [Introduction](1-introduce/)
2. [Prerequisites](2-prerequiste/)
    + 2.1 [Create Cloud9 workspace](2-prerequiste/2.1-createcloud9workspace/)
    + 2.2 [Modify IAM Role](2-prerequiste/2.2-modifyiamrole/)
    + 2.3 [Installation](2-prerequiste/2.3-installation/)
    + 2.4 [Create basic application](2-prerequiste/2.4-createbasicapp/)
3. [Deploy application with Docker](3-deployappwithdocker/)
    + 3.1 [Install Docker](3-deployappwithdocker/3.1-installdocker/)
    + 3.2 [Create Dockerfile](3-deployappwithdocker/3.2-createdockerfile/)
    + 3.3 [Create container image](3-deployappwithdocker/3.3-createdockerimage/)
    + 3.4 [Deploy application](3-deployappwithdocker/3.4-deployapp/)
4. [Interact with Public Container Registry](4-interactpcr/)
    + 4.1 [Create DockerHub account](4-interactpcr/4.1-createdockerhubacc/)
    + 4.2 [Push container image to DockerHub](4-interactpcr/4.2-pushimagetodockerhub/)
    + 4.3 [Pull container image from DockerHub](4-interactpcr/4.3-pullimagefromdockerhub/)
5. [Deploy application to Kubernetes](5-deploytok8s/)
    + 5.1 [Install Kubernetes](5-deploytok8s/5.1-installk8s/)
    + 5.2 [Deploy application with Kubernetes POD by kubectl](5-deploytok8s/5.2-deployk8simperative/)
    + 5.3 [Deploy application with Kubernetes POD by YAML manifest file](5-deploytok8s/5.3-deployk8sdeclarative/)
6. [Deploy applicaiton with Amazon EKS](6-deploytoeks/)
    + 6.1 [Install eksclt](6-deploytoeks/6.1-installeks/)
    + 6.2 [Deploy application by EKS Cluster Managed nodegroup](6-deploytoeks/6.2-eksmanagednodegroup/)
7. [Cleanup resources](/7-cleanup/)
