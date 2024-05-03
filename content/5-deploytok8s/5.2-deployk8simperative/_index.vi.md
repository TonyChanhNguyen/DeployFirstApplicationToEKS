---
title : "Triển khai ứng dụng với Kubernetes POD bằng kubectl"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 5.2 </b> "
---
Ở bước trước đó, chúng ta đã cài đặt kubectl và minikube thành công. Tại bước này, chúng ta sẽ triển khai ứng dụng trên Kubernetes Deployment bằng mệnh lệnh (Imperative).

1. Liệt kê tất cả image trong máy chủ làm việc.
```
docker images
```
![Triển khai K8S Imperative](../../../images/5.deployapptok8s/5.2.deployk8simperative/5.2.1.deployk8simperative.png?pc=90pt)

2. Thực thi câu lệnh dưới đây để tạo Kubernetes Deployment trong Minikube Cluster với container image của ứng dụng của bạn.
```
kubectl create deployment mybasicapp --image=firstcloudjourneypcr/mybasicapp:v1
```
3. Liệt kê và kiểm tra Deployment tên **mybasicapp**.
```
kubectl get deployment
```
![Triển khai K8S Imperative](../../../images/5.deployapptok8s/5.2.deployk8simperative/5.2.2.deployk8simperative.png?pc=90pt)

4. Liệt kê POD được tạo bởi Deployment **mybasicapp**.
```
kubectl get pod
```
![Triển khai K8S Imperative](../../../images/5.deployapptok8s/5.2.deployk8simperative/5.2.3.deployk8simperative.png?pc=90pt)

Bây giờ, POD của ứng dụng đã được tạo nhưng không thể truy cập. Để truy cập POD, chúng ta cần tạo Service.

5. Thực thi câu lệnh này để tạo Service Load Balancer.
```
kubectl expose deployment mybasicapp --type=LoadBalancer --port=8080
```
6. Liệt kê và kiểm tra Service tên **mybasicapp**.
```
kubectl get service
```
![Triển khai K8S Imperative](../../../images/5.deployapptok8s/5.2.deployk8simperative/5.2.4.deployk8simperative.png?pc=90pt)

7. Tạo một đường dẫn để truy cập Load Balancer.
```
minikube tunnel
```
![Triển khai K8S Imperative](../../../images/5.deployapptok8s/5.2.deployk8simperative/5.2.5.deployk8simperative.png?pc=90pt)

8. Nhấn **Window**. Chọn **New Terminal** để tạo một cửa sổ lệnh riêng biệt.
![Triển khai K8S Imperative](../../../images/5.deployapptok8s/5.2.deployk8simperative/5.2.6.deployk8simperative.png?pc=90pt)

9. Liệt kê và kiểm tra Service tên **mybasicapp** lần nữa.
```
kubectl get service
```

![Triển khai K8S Imperative](../../../images/5.deployapptok8s/5.2.deployk8simperative/5.2.7.deployk8simperative.png?pc=90pt)

**EXTERNAL-IP** xuất hiện.

10. Bây giờ chúng ta kiểm thử ứng dụng bằng câu lệnh.
```
curl http://<REPLACE-WITH-EXTERNAL-IP>:8080
```
![Triển khai K8S Imperative](../../../images/5.deployapptok8s/5.2.deployk8simperative/5.2.8.deployk8simperative.png?pc=90pt)

#### Chúc mừng, ứng dụng của bạn đã được triển khai lên Minikube sử dụng kubectl thành công.

11. Xóa Deployment và Service của ứng dụng.
```
kubectl delete deployment mybasicapp
kubectl delete service mybasicapp
```

12. Kiểm tra Deployment và Service lần nữa để đảm bảo chúng đã được xóa.
```
kubectl get all
``` 