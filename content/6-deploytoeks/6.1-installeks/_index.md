---
title : "Install Amazon EKS"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 6.1 </b> "
---
eksctl is a simple command line utility for creating and managing Kubernetes clusters on Amazon EKS.
1. At Cloud9 terminal, execute those command to install Amazon EKS.
+ Download and extract the latest release of eksctl with the following command.
```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
```

+ Move the extracted binary to /usr/local/bin.
```
sudo mv /tmp/eksctl /usr/local/bin
```

+ Test that your installation was successful with the following command
```
eksctl version
```
![Install Amazon EKS](../../images/6.deployapptoeks/6.1.installeks/6.1.1.installeks.png?pc=90pt)