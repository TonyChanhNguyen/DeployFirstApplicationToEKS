---
title : "Đẩy image lên DockerHub"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 4.2 </b> "
---
Ở bước trước, chúng ta đã tạo tài khoản DockerHub, kho lưu trữ công cộng và đăng nhập thành công. Bây giờ, chúng ta sẽ thực hiện đẩy container image lên nơi lưu trữ.
1. Hãy liệt kê container images trong máy chủ làm việc.
```
docker images
```
![Đẩy Container Image](../../../images/4.dockerhub/4.2.pushimage/4.2.1.pushimage.png?pc=90pt)

Như bạn có thể thấy, chúng ta chỉ có duy nhất 1 image với **Repository** là **fcj-application**. Để đẩy container image lên repository, **Repository** của container image phải khớp với mẫu repository của DockerHub ```<YOUR_USER_NAME>/<YOUR_REPOSITORY_NAME>```. Vì thế chúng ta cần sử dụng câu lệnh ``docker image tag`` để sao chép và chuẩn hóa mẫu repository của container image trong máy chủ làm việc.

2. Thực thi câu lệnh này để gắn nhãn cho container image.
```
docker image tag fcj-application:v1 firstcloudjourneypcr/mybasicapp:v1
```
3. Sau đó, hãy liệt kê các container image trong máy chủ làm việc một lần nữa để kiểm tra kết quả.
```
docker images
```
![Đẩy Container Image](../../../images/4.dockerhub/4.2.pushimage/4.2.2.pushimage.png?pc=90pt)

Bây giờ, có 2 container image. Cái mới tạo có repository tên **firstcloudjourneypcr/mybasicapp** với nhãn **v1**.
Kế tiếp, hãy đẩy container image này lên DockerHub.

4. Thực thi câu lệnh để đẩy container image lên DockerHub.
```
docker push firstcloudjourneypcr/mybasicapp:v1
```
![Đẩy Container Image](../../../images/4.dockerhub/4.2.pushimage/4.2.3.pushimage.png?pc=90pt)

5. Trở về Docker Hub repository để kiểm tra kết quả. Có 1 image container đã được đẩy lên.

![Đẩy Container Image](../../../images/4.dockerhub/4.2.pushimage/4.2.4.pushimage.png?pc=90pt)

