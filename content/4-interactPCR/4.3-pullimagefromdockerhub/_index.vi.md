---
title : "Kéo image về từ DockerHub"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 4.3 </b> "
---
Ở bước trước đó, chúng ta đã đẩy container image lên DockerHub repository.
Tại bước này, chúng ta sẽ kéo container image về máy chủ làm việc từ DockerHub repository. Để làm điều đó, trước tiên chúng ta cần xóa tất cả image trong máy chủ làm việc. Sau đó thực hiện việc kéo container image về và chạy ứng dụng từ image đó.
1. Hãy liệt kê tất cả các image trông máy chủ làm việc.
```
docker images
```
Có 2 container image trong máy chủ làm việc.
2. Kế tiếp, thực thi câu lệnh dưới để xóa chúng. Xác nhận **Y** khi được yêu cầu.
```
docker image prune -a
```
3. Liệt kê image một lần nữa để đảm bảo tất cả đã được xóa.
```
docker images
```
![Kéo image về từ DockerHub](../../../images/4.dockerhub/4.3.pullimage/4.3.1.pullimage.png?pc=90pt)

4. Bây giờ chúng ta sẽ kéo container image về từ DockerHub repository bằng câu lệnh.
```
docker pull firstcloudjourneypcr/mybasicapp:v1
```

5. Sau đó, liệt kê các image đã kéo về
```
docker images
```
![Kéo image về từ DockerHub](../../../images/4.dockerhub/4.3.pullimage/4.3.2.pullimage.png?pc=90pt)

Chúng ta thấy có 1 image vừa được kéo về thành công.

6. Bây giờ, chúng ta sẽ triển khai image này lên Docker để khởi chạy ứng dụng cho mục đích kiểm thử.
```
docker run --name demoapplication -d -p 8080:8080 firstcloudjourneypcr/mybasicapp:v1
```
7. Kiểm tra process đang chạy trong máy chủ làm việc.
```
docker ps
```
![Kéo image về từ DockerHub](../../../images/4.dockerhub/4.3.pullimage/4.3.3.pullimage.png?pc=90pt)

Ứng dụng đã được triển khai thành công.

8. Truy cập ứng dụng để kiểm tra kết quả.
![Kéo image về từ DockerHub](../../../images/4.dockerhub/4.3.pullimage/4.3.4.pullimage.png?pc=90pt)

#### Chúc mừng, bạn đã kéo container image về từ Public Container Registry - DockerHub và triển khai nó lên Docker thành công!