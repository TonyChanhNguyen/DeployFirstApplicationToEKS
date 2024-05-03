---
title : "Triển khai ứng dụng với Docker"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---
Trong phần này, chúng ta sẽ triển khai ứng dụng sử dụng Docker để hiểu được cách thức đóng gói và triển khai một ứng dụng.

### Tổng quan
Docker là một mã nguồn mở cho việc phát triển, di chuyển và triển khai ứng dụng. Docker cho phép bạn tách ứng dụng khỏi cơ sở hạ tầng để bạn có thể phân phối phần mềm nhanh chóng. Với Docker, bạn có thể quản lý hạ tầng như cách bạn quản lý ứng dụng. Bằng cách tận dụng các phương pháp của Docker để vận chuyển, kiểm thử và triển khai mã code, bạn có thể làm giảm đang kể độ trễ giữa việc viết mã code và triển khai nó trên môi trường sản phẩm.
#### Kiến trúc Docker
**The Docker daemon**: Docker daemon lắng nghe các yêu cầu Docker API và quản lý các đối tượng Docker như image, container, network và volume. Một daemon cũng giao tiếp với các daemon khác để quản lý các dịch vụ Docker.

**The Docker client**: Docker client là cách chính để nhiều người dùng Docker tương tác với Docker. Khi bạn sử dụng dòng lệnh, client gửi những dòng lệnh đó đến Docker daemon để thực hiện chúng. Dòng lệnh Docker sử dụng Docker API. Docker client có thể giao tiếp với một hoặc nhiều Docker daemon.

**Docker Desktop**: Docker Desktop là một ứng dụng dễ dàng cài đặt cho môi trường Mac, Windows hoặc Linux that enables you to build and share containerized applications and microservices. mà cho phép bạn xây dựng và chia sẻ các ứng dụng và microservice được đóng gói trong container.

**Docker registries**: Docker registry chứa Docker images. Docker Hub là một công cộng mà mọi người có thể dùng, và Docker mặc định tìm kiếm images trên Docker Hub. 

**Images**: Một image là một bản mẫu chỉ đọc với các hướng dẫn cho việc tạo một Docker container.

**Containers**: Container là một phiên bản có thể triển khai của image. Bạn có thể tạo, khởi chạy, dừng, di chuyển hoặc xóa một container bằng cách sử dụng Docker API hoặc CLI.

![Kiến trúc Docker](../../images/1.introduction/1.1.dockerarch.png?pc=90pt)

{{% notice info %}}
Truy cập [Docker docs](https://docs.docker.com/) để thêm thông tin.
{{% /notice %}}

### Nội dung
+ 3.1 [Cài đặt Docker](3.1-installdocker/)
+ 3.2 [Tạo Dockerfile cho ứng dụng](3.2-createdockerfile/)
+ 3.3 [Tạo container image cho ứng dụng](3.3-createdockerimage/)
+ 3.4 [Triển khai ứng dụng với Docker](3.4-deployapp/)