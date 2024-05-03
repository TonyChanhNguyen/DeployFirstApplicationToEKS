---
title : "Cài đặt Docker"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 3.1 </b> "
---

Ở bước này, chúng ta sẽ kiểm tra phiên bản của Docker và cài đặt nếu nó không tồn tại.

### Kiểm tra phiên bản của Docker
1. Tại Cloud9 terminal, thực hiện dòng lệnh này để kiểm tra phiên bản của Docker.
```
docker version
```
![Cài đặt Docker](../../../images/3.deployappwithdocker/3.1.installdocker/3.1.1.installdocker.png?pc=90pt)

Bạn thấy, phiên bản Docker hiện là 25.0.3.

2. Chạy command này để kiểm tra Docker.
```
sudo docker run hello-world
```
![Cài đặt Docker](../../../images/3.deployappwithdocker/3.1.installdocker/3.1.2.installdocker.png?pc=90pt)


### Cài đặt Docker nếu nó chưa tồn tại.
1. Cập nhật máy chủ của bạn.
```
sudo yum update -y
```
2. Tải xuống gói Docker Community Edition.
```
sudo yum install -y docker
```

![Cài đặt Docker](../../../images/3.deployappwithdocker/3.1.installdocker/3.1.3.installdocker.png?pc=90pt)
3. Khởi chạy dịch vụ Docker.
```
sudo service docker start
```
4. Thêm ec2-user vào Docker Group để có thể thực thi các câu lệnh với Docker mà không cần sử dụng sudo.
```
sudo usermod -a -G docker ec2-user
```

5. Kiểm tra Docker.
```
sudo docker run hello-world
```
![Cài đặt Docker](../../../images/3.deployappwithdocker/3.1.installdocker/3.1.4.installdocker.png?pc=90pt)