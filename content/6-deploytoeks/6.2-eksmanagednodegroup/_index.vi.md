---
title : "Triển khai ứng dụng lên EKS Cluster Managed Nodegroup"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 6.2 </b> "
---

Một Kubernetes node mà một máy chạy các ứng dụng được đóng gói theo phương thức container. Mỗi node có các thành phần sau:
+ **Container runtime** – Phần mềm có trách nhiệm cho việc khởi chạy container.
+ **kubelet** – Đảm bảo rằng các container hoạt động tốt và chạy trong Pod được liên kết của chúng.
+ **kube-proxy** – Duy trì các quy tắc mạng cho phép liên lạc với Pod của bạn

Amazon EKS cung cấp các loại node chính sau:
- **AWS Fargate**: Fargate là công cụ điện toán serverless dành cho vùng chứa giúp loại bỏ nhu cầu quản lý các phiên bản cơ bản. Với Fargate, bạn chỉ định nhu cầu tài nguyên của ứng dụng và AWS sẽ tự động cung cấp, thay đổi quy mô và duy trì cơ sở hạ tầng. Tùy chọn này lý tưởng cho những người dùng ưu tiên tính dễ sử dụng và muốn tập trung vào phát triển và triển khai ứng dụng thay vì quản lý cơ sở hạ tầng.
- **Karpenter**: Karpenter là một công cụ tự động chia tỷ lệ Kubernetes Cluster linh hoạt, hiệu suất cao, giúp cải thiện tính khả dụng của ứng dụng và hiệu quả của cụm. Karpenter khởi chạy các tài nguyên điện toán có kích thước phù hợp để đáp ứng nhu cầu tải ứng dụng thay đổi. Tùy chọn này có thể cung cấp tài nguyên điện toán kịp thời đáp ứng yêu cầu khối lượng công việc của bạn.
- **Managed node groups**: Managed node groups là sự kết hợp giữa tự động hóa và tùy chỉnh để quản lý tập hợp phiên bản Amazon EC2 trong Amazon EKS cluster. AWS đảm nhiệm các nhiệm vụ như vá lỗi, cập nhật và thay đổi quy mô node, giúp đơn giản hóa các khía cạnh vận hành. Song song đó, các đối số kubelet tùy chỉnh được hỗ trợ, mở ra khả năng cho các chính sách quản lý bộ nhớ và CPU nâng cao. ơn nữa, chúng còn tăng cường bảo mật thông qua vai trò AWS Identity and Access Management (IAM) cho các tài khoản dịch vụ, đồng thời hạn chế nhu cầu về các quyền riêng biệt cho mỗi cluster.
- **Self-managed nodes**: Self-managed nodes cung cấp toàn quyền kiểm soát các phiên bản Amazon EC2 của bạn trong Amazon EKS cluster. Bạn chịu trách nhiệm quản lý, mở rộng quy mô và duy trì các node, mang lại cho bạn toàn quyền kiểm soát cơ sở hạ tầng cơ bản. Tùy chọn này phù hợp với những người dùng cần kiểm soát và tùy chỉnh chi tiết các node của họ và sẵn sàng đầu tư thời gian vào việc quản lý và duy trì cơ sở hạ tầng của họ.

**Nhưng trong bài thực hành này, chúng ta sẽ chỉ tập trung vào việc triển khai ứng dụng trên Amazon EKS Cluster Managed Nodegroup.**
### Tạo EKS Cluster
1. Tại cửa sổ lệnh Cloud9, thực thi câu lệnh dưới để tạo EKS Cluster.
```
eksctl create cluster --name=my-fcj-cluster --region=ap-southeast-1 --zones=ap-southeast-1a,ap-southeast-1b --managed --nodegroup-name=my-fcj-node --nodes=2 --node-type=t3.micro
```
![Amazon EKS Managed NodeGroup](../../../images/6.deployapptoeks/6.2.managednodegroup/6.2.1.managednodegroup.png?pc=90pt)
{{% notice info %}}
Sẽ mất khoảng 20 phút để hoàn tất. 
{{% /notice %}}
![Amazon EKS Managed NodeGroup](../../../images/6.deployapptoeks/6.2.managednodegroup/6.2.2.managednodegroup.png?pc=90pt)
2. Sau khi quá trình tạo Cluster hoàn tất, liệt kê cluster của bạn trong máy chủ làm việc.
```
eksctl get cluster
```
![Amazon EKS Managed NodeGroup](../../../images/6.deployapptoeks/6.2.managednodegroup/6.2.3.managednodegroup.png?pc=90pt)

3. Liệt kê các Node trong Cluster.
```
kubectl get node
```
![Amazon EKS Managed NodeGroup](../../../images/6.deployapptoeks/6.2.managednodegroup/6.2.4.managednodegroup.png?pc=89pt)

Có 2 node được liệt kê trong EKS Cluster.

4. Di chuyển đến [EC2 Instance](https://ap-southeast-1.console.aws.amazon.com/ec2/home?region=ap-southeast-1#Instances:instanceState=running;tag:alpha.eksctl.io/nodegroup-name=my-fcj-node;v=3;$case=tags:true%5C,client:false;$regex=tags:false%5C,client:false) để thấy các máy chủ kết nối với Node Group.
![Amazon EKS Managed NodeGroup](../../../images/6.deployapptoeks/6.2.managednodegroup/6.2.5.managednodegroup.png?pc=90pt)

Có 2 máy chủ được tạo (khớp với **--nodes=2** trong **câu lệnh eksctl**) với tên là **my-fcj-cluster-my-fcj-node-Node** (định dạng `<Cluster-Name>-<NodeGroup-Name>-Node`), loại **t3.micro** (khớp với **--node-type=t3.micro** trong **câu lệnh eksctl**) và Availability Zone là **ap-southeast-1a** và **ap-southeast-1b** (khớp với **--zones=ap-southeast-1a,ap-southeast-1b** trong **câu lệnh eksctl**).


### Khám phá EKS Cluster
1. Đi đến [CloudFormation](https://ap-southeast-1.console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks), chúng ta sẽ thấy có 2 stack được tạo - 1 cho việc tạo EKS Cluster và 1 cho EKS NodeGroup.
![Amazon EKS Managed NodeGroup](../../../images/6.deployapptoeks/6.2.managednodegroup/6.2.6.managednodegroup.png?pc=90pt)

2. Đi đến [Amazon EKS](https://ap-southeast-1.console.aws.amazon.com/eks/home?region=ap-southeast-1), chúng ta sẽ thấy có 1 EKS Cluster tên **my-fcj-cluster**. Nhấn vào nó.
![Amazon EKS Managed NodeGroup](../../../images/6.deployapptoeks/6.2.managednodegroup/6.2.7.managednodegroup.png?pc=90pt)

3. Chuyển đến mục **Compute**.
4. Chúng ta sẽ thấy node group tên **my-fcj-node** với **Desired size** là 2 liên kết với EKS Cluster tại mục **Node groups**.
![Amazon EKS Managed NodeGroup](../../../images/6.deployapptoeks/6.2.managednodegroup/6.2.8.managednodegroup.png?pc=90pt)

### Triển khai ứng dụng lên EKS Cluster
1. Tại thư mục **kube-manifest**, thực thi câu lệnh sau để triển khai ứng dụng lên EKS Cluster.
```
kubectl apply -f .
```

2. Liệt kê các Service được tạo ra.
```
kubectl get svc
```
hoặc
```
kubectl get service
```
![Amazon EKS Managed NodeGroup](../../../images/6.deployapptoeks/6.2.managednodegroup/6.2.9.managednodegroup.png?pc=90pt)

3. Truy cập **LoadBalancer HostName** để kiểm tra kết quả. Thay thế **EXTERNAL-IP** dịch vụ của bạn trong ```http://<REPLACE-YOUR-EXTERNAL-IP>:8080```.

*Example:* Trường hợp này Hostname sẽ là http://a6d733c6da3c1499f9ac945a665aa815-1253515241.ap-southeast-1.elb.amazonaws.com:8080
![Amazon EKS Managed NodeGroup](../../../images/6.deployapptoeks/6.2.managednodegroup/6.2.10.managednodegroup.png?pc=90pt)


#### Chúc mừng, bạn đã triển khai ứng dụng lên EKS CLuster Managed Node Group thành công.

### Dọn dẹp.
1. Tại cửa sổ lệnh Cloud9, để xóa hết tất cả tài nguyên đã tạo. Thực thi câu lệnh bên dưới.
```
kubectl delete -f .
```
![Amazon EKS Managed NodeGroup](../../../images/6.deployapptoeks/6.2.managednodegroup/6.2.11.managednodegroup.png?pc=90pt)

2. Liệt kê tất cả tài nguyên để đảm bảo chúng đã bị xóa hoàn toàn.
```
kubectl get all
```
![Amazon EKS Managed NodeGroup](../../../images/6.deployapptoeks/6.2.managednodegroup/6.2.12.managednodegroup.png?pc=90pt)

