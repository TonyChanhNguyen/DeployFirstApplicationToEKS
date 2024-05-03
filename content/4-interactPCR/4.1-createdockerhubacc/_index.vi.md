---
title : "Tạo tài khoản DockerHub"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 4.1 </b> "
---

1. Truy cập [DockerHub](https://www.docker.com/products/docker-hub/).
2. Nhấn **Sign up** để đăng ký tài khoản. Sau đó đăng nhập tài khoản của bạn.

![Tạo tài khoản DockerHub](../../../images/4.dockerhub/4.1.createaccount/4.1.1.createaccount.png?pc=90pt)

3. Sau khi đăng nhập, bạn sẽ được yêu cầu điền **Username**. Đây là giá trị duy nhất.
4. Sau đó, nhấn **Sign Up**.

![Tạo tài khoản DockerHub](../../../images/4.dockerhub/4.1.createaccount/4.1.2.createaccount.png?pc=90pt)

5. Tại mục **Repository**, nhấn **Create repository** để lưu trữ container image.
![Tạo tài khoản DockerHub](../../../images/4.dockerhub/4.1.createaccount/4.1.3.createaccount.png?pc=90pt)

6. Điền **Repository Name** với giá trị ```mybasicapp```.
7. Sau đó nhấn **Create**.

![Tạo tài khoản DockerHub](../../../images/4.dockerhub/4.1.createaccount/4.1.4.createaccount.png?pc=90pt)

Kế tiếp, chúng ta sẽ tạo Access Token được sử dụng để đăng nhập vào DockerHub từ máy chủ làm việc.

8. Nhấn vào tài khoản của bạn (Phía trên bên phải của trang).
9. Nhấn **My Account**.
10. Nhấn **Security**.
11. Cuối cùng, nhấn **New Access Token**.
![Tạo tài khoản DockerHub](../../../images/4.dockerhub/4.1.createaccount/4.1.5.createaccount.png?pc=90pt)

12. Điền **Access Token Description**.
13. Nhấn **Generate**.
![Tạo tài khoản DockerHub](../../../images/4.dockerhub/4.1.createaccount/4.1.6.createaccount.png?pc=90pt)

14. Lưu lại mã token.

![Tạo tài khoản DockerHub](../../../images/4.dockerhub/4.1.createaccount/4.1.7.createaccount.png?pc=90pt)

15. Trở lại cửa sổ lệnh của Cloud9. Nhập câu lệnh này để đăng nhập và cung cấp access token khi được yêu cầu.
```
docker login -u <REPLACE-YOUR-DOCKERHUB-USERNAME>
```
![Tạo tài khoản DockerHub](../../../images/4.dockerhub/4.1.createaccount/4.1.8.createaccount.png?pc=90pt)
