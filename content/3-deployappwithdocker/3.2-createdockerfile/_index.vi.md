---
title : "Tạo Dockerfile"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 3.2 </b> "
---
Ở bước này, chúng ta sẽ tạo Dockerfile để hướng dẫn Docker làm thể nào để xây dựng container image cho ứng dụng.
1. Tạo tệp tên **Dockerfile**.
```
touch Dockerfile
```
![Tạo Dockerfile](../../../images/3.deployappwithdocker/3.2.createdockerfile/3.2.1.createdockerfile.png?pc=90pt)

2. Mở tệp **Dockerfile**.
![Tạo Dockerfile](../../../images/3.deployappwithdocker/3.2.createdockerfile/3.2.2.createdockerfile.png?pc=90pt)

3. Nhập đoạn code bên dưới.
```Dockerfile
FROM node:13-alpine

#configure working directory
WORKDIR /app

COPY package.json ./

RUN npm install

#bundle the source code

COPY . ./

EXPOSE 8080

CMD ["node","index.js"]


```
![Tạo Dockerfile](../../../images/3.deployappwithdocker/3.2.createdockerfile/3.2.3.createdockerfile.png?pc=90pt)

*Chú ý*: 
+ Tại bước **COPY package.json ./**, Docker sẽ sao chép tệp **package.json** tới vùng làm việc **/app**, sau đó thực thi bước **RUN npm install** để cài đặt tất cả các gói tin được định nghĩa trong tệp **package.json** và lưu chúng vào thư mục **node_modules**.

+ Tại bước **COPY . ./**, Docker sao chép tất cả các tài nguyên đến vùng làm việc **/app** - bao gồm thư mục **node_modules** và tệp **Dockerfile**. Các thư mục và tệp này không cần thiết phải sao chép lại lên vùng làm việc. Vì thế bạn có thể tạo một tệp **.dockerignore** để liệt kê các tệp hoặc thư mục không cần thiết được sao chép lên vùng làm việc.

4. Tạo tệp tên **.dockerignore**.
```
touch .dockerignore
```
![Tạo Dockerfile](../../../images/3.deployappwithdocker/3.2.createdockerfile/3.2.4.createdockerfile.png?pc=80pt)

Bạn sẽ không thấy **.dockerignore** ở đâu, vì Cloud9 nhận định **.dockerignore** là tệp ẩn.

5. Nhấn **Setting**.
6. Chọn **Show Hidden Files**.

![Create Dockerfile](../../../images/3.deployappwithdocker/3.2.createdockerfile/3.2.5.createdockerfile.png?pc=90pt)

7. Mở **.dockerignore** và nhập các giá trị.
```
node_modules
Dockerfile
```
![Tạo Dockerfile](../../../images/3.deployappwithdocker/3.2.createdockerfile/3.2.6.createdockerfile.png?pc=90pt)