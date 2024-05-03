---
title : "Cài đặt Amazon EKS"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 6.1 </b> "
---
eksctl là một câu lệnh đơn giản giúp ích cho việc tạo và quản lý Kubernetes clusters trên Amazon EKS.
1. Tại cửa sổ lệnh Cloud9, thực thi câu lệnh dưới đây để cài đặt Amazon EKS.
+ Tải và trích xuất bản phát hành mới nhất của eksctl bằng lệnh sau.
```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
```

+ Di chuyển nhị phân được trích xuất thành /usr/local/bin.
```
sudo mv /tmp/eksctl /usr/local/bin
```

+ Kiểm tra cài đặt.
```
eksctl version
```
![Cài đặt Amazon EKS](../../../images/6.deployapptoeks/6.1.installeks/6.1.1.installeks.png?pc=90pt)