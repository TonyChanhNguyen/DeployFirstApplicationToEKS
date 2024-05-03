---
title : "Cài đặt công cụ Kubernetes"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 5.1 </b> "
---

Đầu tiên, chúng ta cần cài đặt Kubernetes (Minikube) lên máy chủ làm việc. **Minikube** mà một công cụ mà cho phép bạn chạy một Kubernetes cluster node đơn trong máy tính cá nhân hoặc máy chủ EC2 để bạn có thể thử nghiệm Kubernetes.

Minikube là một bộ cài đặt Kubernetes (K8) gọn nhẹ, có thể tạo một Virtual Machine (VM) trên máy chủ nội bộ hoặc máy chủ đám mấy, triển khai một cluster đơn giản mà chỉ chứa 1 node.

Nhưng để cài đặt kubectl và minikube trong máy chủ làm việc, dung lượng lưu trữ phải dư thừa. Vì thế đầu tiên, chúng ta cần mở rộng dung lượng lưu trữ của máy chủ làm việc.

### Mở rộng dung lượng lưu trữ lên 50GB.
1. Đi đến **EC2 instance** của máy chủ làm việc.
![Cài đặt K8S](../../../images/5.deployapptok8s/5.1.installkubectl/5.1.5.installkubectl.png?pc=90pt)

2. Chuyển đến mục **Storage**.
3. Nhấn **Volume ID**.
![Cài đặt K8S](../../../images/5.deployapptok8s/5.1.installkubectl/5.1.6.installkubectl.png?pc=90pt)

Dung lượng lưu trữ hiện tại là 10GB. Chúng ta sẽ nâng cấp nó lên 50GB.

4. Chọn **EBS volume**.
5. Nhấn **Action**. Sau đó chọn **Modify volume**.
![Cài đặt K8S](../../../images/5.deployapptok8s/5.1.installkubectl/5.1.7.installkubectl.png?pc=90pt)
6. Đổi từ **10** lên **50** tại mục **Size (GiB)**.
7. Nhấn **Modify**.
![Cài đặt K8S](../../../images/5.deployapptok8s/5.1.installkubectl/5.1.8.installkubectl.png?pc=90pt)

8. Sau đó, nhấn **Modify** để xác nhận.
![Cài đặt K8S](../../../images/5.deployapptok8s/5.1.installkubectl/5.1.9.installkubectl.png?pc=90pt)

9. Trở lại cửa sổ lệnh Cloud9, thực thi câu lệnh dưới đây để khởi động lại máy chủ làm việc.
```
sudo reboot
```
![Cài đặt K8S](../../../images/5.deployapptok8s/5.1.installkubectl/5.1.10.installkubectl.png?pc=90pt)

10. Sau khi khởi động thành công. Kiểm tra kết quả.
```
df -h
```
Có một bộ lưu trữ được gắn thêm vào máy chủ của bạn với dung lượng là 43GB.
![Cài đặt K8S](../../../images/5.deployapptok8s/5.1.installkubectl/5.1.11.installkubectl.png?pc=90pt)


### Cài đặt kubectl
1. Tại **Cửa sổ lệnh Cloud9**, thực thi câu lệnh dưới đây để cài đặt **kubectl**.
+ Cập nhật máy chủ.
```bash
sudo yum update
```
+ Cài đặt kubectl.
```bash
curl -LO https://dl.k8s.io/release/v1.30.0/bin/linux/amd64/kubectl
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```
2. Kiểm tra phiên bản **kubectl**.
```
kubectl version --client
```

![Cài đặt K8S](../../../images/5.deployapptok8s/5.1.installkubectl/5.1.3.installkubectl.png?pc=90pt)


### Cài đặt minikube
1. Tại **Cửa sổ lệnh Cloud9**, thực thi câu lệnh dưới đây để cài đặt **minikube**.
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
```
2. Khởi chạy Kubernetes Cluster với **minikube**.
```
minikube start
```
3. Kiểm tra phiên bản.
```
minikube version
```
![Cài đặt K8S](../../../images/5.deployapptok8s/5.1.installkubectl/5.1.12.installkubectl.png?pc=90pt)


