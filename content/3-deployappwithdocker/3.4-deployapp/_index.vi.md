---
title : "Triển khai ứng dụng"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 3.4 </b> "
---
Ở bước trước đó, bạn đã xây dựng container image cho ứng dụng của bạn. Bây giờ, chứng ta sẽ triển khai nó lên Docker.

### Triển khai ứng dụng lên Docker sử dụng container image
1. Thực thi câu lệnh này để khởi chạy ứng dụng của bạn với Docker.
```
docker run -d --name my-docker-deployment -p 8080:8080 fcj-application:v1 
```
2. Kiểm tra process đang chạy bên trong máy chủ.
```
docker ps -a
```
![Triển khai ứng dụng](../../../images/3.deployappwithdocker/3.4.deployapp/3.4.1.deployapp.png?pc=90pt)

3. Truy cập URL ```http://<YOUR_IP_ADDRESS>:8080``` để kiểm tra kết quả.
![Triển khai ứng dụng](../../../images/3.deployappwithdocker/3.4.deployapp/3.4.2.deployapp.png?pc=90pt)

#### Chúc mừng, bạn vừa triển khai ứng dụng lên Docker thành công.

### Xóa process.
1. Đầu tiên, chúng ta cần dừng process đang chạy.
```
docker stop my-docker-deployment
```
2. Sau đó, sử dụng câu lệnh này để xóa process.
```
docker rm my-docker-deployment
```
3. Kiểm tra các process tồn tại trên máy của bạn lần nữa.
```
docker ps -a
```
![Triển khai ứng dụng](../../../images/3.deployappwithdocker/3.4.deployapp/3.4.3.deployapp.png?pc=90pt)