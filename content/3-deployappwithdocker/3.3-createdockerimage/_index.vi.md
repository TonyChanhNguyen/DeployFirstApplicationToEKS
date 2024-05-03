---
title : "Tạo container image"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3.3 </b> "
---
Bạn vừa tạo **Dockerfile** -  để hướng dẫn Docker cách thức xây dựng container image cho ứng dụng của bạn và **.dockerignore** - để thể hiện cho Docker biết tài nguyên nào không cần phải sao chép lên vùng làm việc. Giờ đây, chúng ta sẽ tiến hành xây dựng container image từ các tệp **Dockerfile** và **.dockerignore**.

Trước khi xây dựng container image. Hãy kiểm tra xem có image nào bên trong máy chủ, nhưng trước tiên hãy kiểm tra process đang chạy trước.

### Kiểm tra process
1. Nhập câu lệnh sau để liệt kê các process đang chạy.
```
docker ps
```
![Tạo Docker image](../../../images/3.deployappwithdocker/3.3.createdockerimage/3.3.1.createdockerimage.png?pc=90pt)
Không có process nào đang chạy bên trong máy chủ của bạn. Giờ chúng ta sẽ kiểm tra process nào tồn tại bên trong máy chủ.
2. Nhập câu lệnh sau để liệt kê các process tồn tại.
```
docker ps -a
```
![Tạo Docker image](../../../images/3.deployappwithdocker/3.3.createdockerimage/3.3.3.createdockerimage.png?pc=90pt)

Có 2 process đang tồn tại nhưng trạng thái là **Exited**. Nghĩa là các process này đã dừng. Hãy xóa chúng ra khỏi máy chủ.
3. Nhập ccâu lệnh sau để xóa tất cả process đang tồn tại.
```
docker rm $(docker ps -aq)
```
4. Kiểm tra lại lần nữa.
```
docker ps -a
```
![Tạo Docker image](../../../images/3.deployappwithdocker/3.3.createdockerimage/3.3.4.createdockerimage.png?pc=90pt)
Không còn process nào tồn tại
### Kiểm tra container image
1. Nhập câu lệnh sau để liệt kê các image bên trong máy chủ của bạn.
```
docker images
```
![Tạo Docker image](../../../images/3.deployappwithdocker/3.3.createdockerimage/3.3.1.createdockerimage.png?pc=90pt)

Có một container image tên **hello-world**. Đây là image được tải xuống khi bạn kiểm thử Docker Engine tại bước [3.1 Install Docker](../3.1-installdocker/) bằng câu lệnh ```sudo docker run hello-world```.

2. Giờ chúng ta sẽ xóa image này.
```
docker delete image hello-word
```
![Tạo Docker image](../../../images/3.deployappwithdocker/3.3.createdockerimage/3.3.5.createdockerimage.png?pc=90pt)

3. Liệt kê tất cả image một lần nữa.
```
docker images
```
![Tạo Docker image](../../../images/3.deployappwithdocker/3.3.createdockerimage/3.3.6.createdockerimage.png?pc=90pt)
Bây giờ không còn image nào bên trong máy chủ. Hãy xây dựng container image cho ứng dụng của bạn.

### Xây dựng container image
1. Thực thi câu lệnh này để xây dựng contianer image.
```
docker build -t fcj-application:v1 .
```
![Tạo Docker image](../../../images/3.deployappwithdocker/3.3.createdockerimage/3.3.7.createdockerimage.png?pc=90pt)

2. Bây giờ, hãy liệt kê tất cả image trong máy chủ.
```
docker images
```
![Tạo Docker image](../../../images/3.deployappwithdocker/3.3.createdockerimage/3.3.8.createdockerimage.png?pc=90pt)

Container image của ứng dụng của bạn đã được xây dựng thành công