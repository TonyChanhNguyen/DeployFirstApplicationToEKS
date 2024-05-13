---
title : "Triển khai ứng dụng lên EKS Cluster"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---
### Tổng quan
Amazon Elastic Kubernetes Service (Amazon EKS) là một dịch vụ được quản lý giúp loại bỏ sự cần thiết của việc cài đặt, vận hành và duy trì Kubernetes control plane của bạn trên Amazon Web Services (AWS).

#### Kiến trúc Amazon EKS

Amazon EKS đảm bảo mỗi cluster đều có Kubernetes control plane riêng biệt. Thiết kế này giữ cho cơ sở hạ tầng của mỗi cụm tách biệt, không trùng lập giữa các Cluster hoặc tài khoản AWS. Việc thiết lập bao gồm:
- **Các thành phần phân tán**: Control plane chứa ít nhất 2 phiên bản máy chủ API (API server) và 3 phiên bản etcd giữa 3 AWS Availability Zone trong một AWS Region.
- **Tối ưu hiệu suất**: Amazon EKS giám sát chủ động và điều chỉnh các phiên bản Control plane để duy trì hiệu năng cao nhất.
- **Khả năng phục hồi**: Nếu một phiên bản Control plane không hoạt động, Amazon EKS nhanh chóng thay thế nó, sử dụng Availability Zone khác nếu cần thiết.
- **Thời gian hoạt động ổn định**: Bằng việc triển khai các Cluster giữa các Availability Zone, đạt được tính khả dụng của điểm cuối máy chủ API (SLA) đáng tin cậy.

Amazon EKS sử dụng Amazon Virtual Private Cloud (Amazon VPC) để giới hạn lưu lượng giữa các thành phần Control plane bên trong một Cluster. Các thành phần Cluster không thể nhìn thấy hoặc nhận giap tiếp từ các Cluster hoặc tài khoản AWS khác, ngoại trừ khi được xác thực bởi quy tắc Kubernetes role-based access control (RBAC).

Ngoài Control plane, một Amazon EKS cluster còn có một tập các worker machines gọi là node. Việc lựa chọn lại Amazon EKS cluster node thích hợp là rất quan trọng để đáp ứng các yêu cầu cụ thể của bạn và tối ưu hóa việc sử dụng tài nguyên. Amazon EKS cung cấp các loại node chính sau:
- **AWS Fargate**: Fargate là công cụ điện toán serverless dành cho vùng chứa giúp loại bỏ nhu cầu quản lý các phiên bản cơ bản. Với Fargate, bạn chỉ định nhu cầu tài nguyên của ứng dụng và AWS sẽ tự động cung cấp, thay đổi quy mô và duy trì cơ sở hạ tầng. Tùy chọn này lý tưởng cho những người dùng ưu tiên tính dễ sử dụng và muốn tập trung vào phát triển và triển khai ứng dụng thay vì quản lý cơ sở hạ tầng.
- **Karpenter**: Karpenter là một công cụ tự động chia tỷ lệ Kubernetes Cluster linh hoạt, hiệu suất cao, giúp cải thiện tính khả dụng của ứng dụng và hiệu quả của cụm. Karpenter khởi chạy các tài nguyên điện toán có kích thước phù hợp để đáp ứng nhu cầu tải ứng dụng thay đổi. Tùy chọn này có thể cung cấp tài nguyên điện toán kịp thời đáp ứng yêu cầu khối lượng công việc của bạn.
- **Managed node groups**: Managed node groups là sự kết hợp giữa tự động hóa và tùy chỉnh để quản lý tập hợp phiên bản Amazon EC2 trong Amazon EKS cluster. AWS đảm nhiệm các nhiệm vụ như vá lỗi, cập nhật và thay đổi quy mô node, giúp đơn giản hóa các khía cạnh vận hành. Song song đó, các đối số kubelet tùy chỉnh được hỗ trợ, mở ra khả năng cho các chính sách quản lý bộ nhớ và CPU nâng cao. ơn nữa, chúng còn tăng cường bảo mật thông qua vai trò AWS Identity and Access Management (IAM) cho các tài khoản dịch vụ, đồng thời hạn chế nhu cầu về các quyền riêng biệt cho mỗi cluster.
- **Self-managed nodes**: Self-managed nodes cung cấp toàn quyền kiểm soát các phiên bản Amazon EC2 của bạn trong Amazon EKS cluster. Bạn chịu trách nhiệm quản lý, mở rộng quy mô và duy trì các node, mang lại cho bạn toàn quyền kiểm soát cơ sở hạ tầng cơ bản. Tùy chọn này phù hợp với những người dùng cần kiểm soát và tùy chỉnh chi tiết các node của họ và sẵn sàng đầu tư thời gian vào việc quản lý và duy trì cơ sở hạ tầng của họ.
![Kiến trúc Amazon EKS](../../images/1.introduction/1.3.eksarch.png?pc=90pt)

{{% notice info %}}
Truy cập [Amazon EKS docs](https://docs.aws.amazon.com/eks/latest/userguide/) để thêm thông tin.
{{% /notice %}}

**Trong bài thực hành này, chúng ta chỉ sẽ tập trung vào việc làm thế nào để triển khai ứng dụng với EKS Cluster Managed node groups and Fargate Profile.**

### Nội dung
+ 6.1 [Cài đặt eksclt](6.1-installeks/)
+ 6.2 [Triển khai ứng dụng bằng EKS Cluster Managed nodegroup](6.2-eksmanagednodegroup/)
+ 6.3 [Triển khai ứng dụng bằng EKS Cluster Fargate Profile](6-deploytoeks/6.3-eksfargate/)