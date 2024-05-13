---
title : "Triển khai ứng dụng bằng EKS Cluster Fargate Profile"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 6.3 </b> "
---

### Triển khai ứng dụng
1. Tại cửa sổ lệnh Cloud9, tạo các thư mục **01.fargate-profile** và **02.application**.
```
mkdir 01.fargate-profile 02.application
ls
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.1.fargateprofile.png?pc=90pt)

2. Di chuyển 2 tệp manifest tới thư mục **02.application**.
```
mv 01.mybasicapp-deployment.yaml 02.application/
mv 02.mybasicapp-service.yaml 02.application/
ls 02.application/
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.2.fargateprofile.png?pc=90pt)
3. Bây giờ, hãy liệt kê tất cả các tệp và thư mục trong **kube-manifest**.
```
ls
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.3.fargateprofile.png?pc=90pt)
Bao gồm 2 thư mục **01.fargate-profile** và **02.application**. 2 tệp manifest **01.mybasicapp-deployment.yaml** và **02.mybasicapp-service.yaml** bên trong **02.application**.

4. Tạo một tệp tên **fargate-profiles.yaml** trong **01.fargate-profile**.
```
touch 01.fargate-profile/fargate-profiles.yaml
ls 01.fargate-profile
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.4.fargateprofile.png?pc=90pt)

5. Tạo một tệp tên **00.namespace.yaml** trong **02.application**.
```
touch 02.application/00.namespace.yaml
ls 02.application
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.5.fargateprofile.png?pc=90pt)

6. Mở tệp **fargate-profiles.yaml** dán đoạn mã code bên dưới. Sau đó lưu lại.
```
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig
metadata:
  name: my-fcj-cluster  # Name of the EKS Cluster
  region: ap-southeast-1
fargateProfiles:
  - name: fp-fcj
    selectors:
      # All workloads in the "ns-fcj" Kubernetes namespace will be
      # scheduled onto Fargate:      
      - namespace: ns-fcj
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.6.fargateprofile.png?pc=90pt)

7. Mở tệp **00.namespace.yaml** dán đoạn mã code bên dưới. Sau đó lưu lại.
```
apiVersion: v1
kind: Namespace
metadata: 
  name: ns-fcj
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.9.fargateprofile.png?pc=90pt)

Bây giờ, chúng ta cần thêm thành phần **Namespace** trong **Deployment** và **Service** của tệp manifest.

8. Mở tệp **01.mybasicapp-deployment.yaml**, thêm ```namespace: ns-fcj``` bên trong **metadata** và bên dưới **name** và **labels**. Sau đó lưu lại.
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.7.fargateprofile.png?pc=90pt)

9. Mở tệp **02.mybasicapp-service.yaml**, thêm ```namespace: ns-fcj``` bên trong **metadata** và bên dưới **name** và **labels** và thay thế **Type** từ **LoadBalancer** thành **NodePort**. Sau đó lưu lại.
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.8.fargateprofile.png?pc=90pt)

10. Tại thư mục **kube-manifest**, thực thi câu lệnh bên dưới để tạo Fargate Profile.
```
eksctl create fargateprofile -f 01.fargate-profile/fargate-profiles.yaml
``` 
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.10.fargateprofile.png?pc=90pt)

11. Liệt kê Fargate Profile.
```
eksctl get fargateprofile --cluster my-fcj-cluster
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.11.fargateprofile.png?pc=90pt)

12. Tại thư mục **kube-manifest**, thực thi câu lệnh bên dưới để triển khai ứng dụng lên EKS Cluster.
```
kubectl apply -Rf 02.application
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.12.fargateprofile.png?pc=90pt)
13. Liệt kê tất cả tài nguyên.
```
kubectl get all -n ns-fcj
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.13.fargateprofile.png?pc=90pt)

14. Liệt kê Node.
```
kubectl get nodes -o wide
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.14.fargateprofile.png?pc=90pt)


Có một máy chủ Fargate xuất hiện, nhưng nó không có **EXTERNAL-IP**. Bởi vì máy chủ Fargate nằm ở Private Subnet, vì thế bạn không truy cập tới ứng dụng một cách trực tiếp. Vì thế nếu bạn muốn truy cập tới ứng dụng trên máy chủ Fargate, hãy tạo một  Ephemeral Pod với Curl image để kiểm tra ứng dụng.

15. Chúng ta cần lấy Private IP Address của Pod ứng dụng trong mục IP.
```
kubectl describe pod <Pod-NAME> -n ns-fcj
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.15.fargateprofile.png?pc=90pt)

Trong trường hợp này, Private IP Address của Pod ứng dụng là **192.168.78.227**.

16. Chạy câu lệnh bên dưới để triển khai một Curl Ephemeral Pod.
```
kubectl run mycurlpod -n ns-fcj --image=curlimages/curl -i --tty -- sh
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.16.fargateprofile.png?pc=90pt)
17. Sử dụng câu lệnh Curl để truy cập tới ứng dụng. Thay thế với Private IP Address của Pod.
```
curl http://<REPLACE-WITH-PRIVATE-IP>:8080
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.17.fargateprofile.png?pc=90pt)

Curl Ephemeral Pod đã lấy được nội dung của ứng dụng.

18. Nhập câu lệnh ```exit``` để thoát.
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.18.fargateprofile.png?pc=90pt)

19. Liệt kê tất cả Pod đã tạo.
```
kubectl get pod -n ns-fcj
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.19.fargateprofile.png?pc=90pt)

20. Xóa Ephemeral Pod.
```
kubectl delete pod mycurlpod -n ns-fcj
kubectl get pod -n ns-fcj
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.20.fargateprofile.png?pc=90pt)

Curl Ephemeral Pod đã bị xóa.

### Dọn dẹp
1. Xóa tất cả tài nguyên đã tạo.
```
kubectl delete -Rf 02.application
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.21.fargateprofile.png?pc=90pt)

2. Liệt kê tất cả tài nguyên.
```
kubectl get all -n ns-fcj
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.22.fargateprofile.png?pc=90pt)

3. Xóa Fargate Profile.
```
eksctl delete fargateprofile --cluster my-fcj-cluster --name fp-fcj --region ap-southeast-1 --wait
```
![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.23.fargateprofile.png?pc=90pt)

4. Sẽ mất khoảng 5 phút để xóa Fargate Profile thành công.

![Amazon EKS Cluster Fargate Profile](../../../images/6.deployapptoeks/6.3.fargateprofile/6.3.24.fargateprofile.png?pc=90pt)