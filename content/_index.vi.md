---
title : "Triển khai ứng dụng đầu tiên trên Amazon EKS"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# Triển khai ứng dụng đầu tiên trên Amazon EKS

### Tổng quan
Trong bài thực hành này, chúng ta sẽ cùng tìm hiểu các khái niệm cơ bản và cách thức triển khai một ứng dụng đơn giản trên Docker, Kubernetes và Amazon EKS.

![DockerandK8SandEKS](../images/DockerK8SEKS.png?pc=90pt)

### Nội dung

1. [Giới thiệu](1-introduce/)
2. [Các bước chuẩn bị](2-Prerequiste/)
    + 2.1 [Tạo môi trường Cloud9](2-prerequiste/2.1-createcloud9workspace/)
    + 2.2 [Cấu hình IAM Role](2-prerequiste/2.2-modifyiamrole/)
    + 2.3 [Cài đặt ứng dụng](2-prerequiste/2.3-installation/)
    + 2.4 [Tạo ứng dụng cơ bản](2-prerequiste/2.4-createbasicapp/)
3. [Triển khai ứng dụng với Docker](3-deployappwithdocker/)
    + 3.1 [Cài đặt Docker](3-deployappwithdocker/3.1-installdocker/)
    + 3.2 [Tạo Dockerfile cho ứng dụng](3-deployappwithdocker/3.2-createdockerfile/)
    + 3.3 [Tạo container image cho ứng dụng](3-deployappwithdocker/3.3-createdockerimage/)
    + 3.4 [Triển khai ứng dụng với Docker](3-deployappwithdocker/3.4-deployapp/)
4. [Thao tác với Public Container Registry](4-interactpcr/)
    + 4.1 [Tạo tài khoản DockerHub](4-interactpcr/4.1-createdockerhubacc/)
    + 4.2 [Đẩy container image lên DockerHub](4-interactpcr/4.2-pushimagetodockerhub/)
    + 4.3 [Tải container image từ Docker](4-interactpcr/4.3-pullimagefromdockerhub/)
5. [Triển khai ứng dụng với Kubernetes](5-deploytok8s/)
    + 5.1 [Cài đặt Kubernetes](5-deploytok8s/5.1-installk8s/)
    + 5.2 [Triển khai ứng dụng với Kubernetes POD bằng kubectl](5-deploytok8s/5.2-deployk8simperative/)
    + 5.3 [Triển khai ứng dụng với kubernetes POD bằng YAML manifest file](5-deploytok8s/5.3-deployk8sdeclarative/)
6. [Triển khai ứng dụng với EKS](6-deploytoeks/)
    + 6.1 [Cài đặt eksclt](6-deploytoeks/6.1-installeks/)
    + 6.2 [Triển khai ứng dụng bằng EKS Cluster Managed nodegroup](6-deploytoeks/6.2-eksmanagednodegroup/)
7. [Dọn dẹp tài nguyên](/7-cleanup/)

