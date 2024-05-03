---
title : "Giới thiệu"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---

## Docker
#### Tổng quan
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
## Kubernetes
#### Tổng quan
Kubernetes là một nền tảng nguồn mở, có thể mở rộng, di động để quản lý khối lượng công việc và dịch vụ được đóng gói, tạo điều kiện thuận lợi cho cả cấu hình khai báo và tự động hóa. Nó có một hệ sinh thái rộng lớn và phát triển nhanh chóng. Các dịch vụ, hỗ trợ và công cụ của Kubernetes có sẵn rộng rãi.

#### Kiến trúc cụm Kubernetes
**Cluster**: Kubernetes Cluster bao gồm một tập hợp các worker node, được gọi là node, chạy các ứng dụng được đóng gói. Mỗi cụm có ít nhất một worker node. 

**Control Plane**: Control Plane quản lý các worker node và Pod trong Cluster. Trong môi trường sản phẩm, Control Plane thường hoạt động trên nhiều máy chủ và một cluster thường có nhiều node để đảm bảo tính sẵn sàng và khả nằng chịu lỗi cao.

**Worker Nodes**: Work Node chứa các Pods là các thành phần của khối lượng công việc ứng dụng.

**kube-api-server**: The API server là một thành phần của Kubernetes control plane mà hiển thị Kubernetes API. Máy chủ API là giao diện cho Kubernetes control plane.

**etcd**: Bộ lưu trữ key-value nhất quán và khả dụng cao được sử dụng như kho lưu trữ hổ trợ Kubernetes cho tất cả dữ liệu của Cluster.
**Scheduler**: Là thành phần của Control plane giám sát các Pod mới tạo chưa được chỉ định nào node nào, và sẽ chọn một node phù hợp để chúng triển khai trên.

**Controller Manager**: Là thành phần của Control plane chạy các quy trình quản lý. Một cách hợp lý, mỗi bộ điều khiển sẽ là một quy trình riêng biệt nhưng để giảm sự phức tạp, chúng thường được biên dịch thành một tện nhị phân duy nhất để chạy trên một quy trình duy nhất. Có nhiều loại bộ điều khiển khác nhau. Một số ví dụ như:
- Node controller: Chịu trách nhiệm nhận diện và phản hổi khi node không hoạt động.
- Job controller: Theo dõi các đối tượng Công việc đại diện cho các nhiệm vụ một lần, sau đó tạo các Pod để chạy các nhiệm vụ đó cho đến khi hoàn thành
- EndpointSlice controller: Điền vào các đối tượng EndpointSlice (để cung cấp liên kết giữa Service và Pod)
- ServiceAccount controller: Tạo ServiceAccounts mặc định cho một namespace mới.

*Trên đây không phải là danh sách đầy đủ.*

**kubelet**: Một agent chạy trên mỗi node trong cluster. It makes sure that containers are running in a Pod. Nó đảm bảo rằng các container đang chạy trong Pod.

**kube-proxy**: kube-proxy là một proxy mạng chạy trên mỗi node trong cluster của bạn, triển khai một phần khái niệm Service Kubernetes.

**pod**: là một phiên bản duy nhất của một ứng dụng và đối tượng nhỏ nhất mà bạn có thể tạo trong Kubernetes.

**Container Runtime Interface (CRI)**: Một thành phần cơ bản hỗ trợ Kubernetes chạy các container một cách hiệu quả. Nó chịu trách nhiệm quản lý việc thực thi và vòng đời của các container trong môi trường Kubernetes.

**cloud-control-manager**: Một thành phần Kubernetes control plane nhúng bộ điều khiển dành riêng cho đám mây. Trình quản lý bộ điều khiển đám mây cho phép bạn liên kết cụm của mình với API của nhà cung cấp đám mây và tách các thành phần tương tác với nền tảng đám mây đó khỏi các thành phần chỉ tương tác với cụm của bạn.

![Kiến trúc cụm Kubernetes](../../images/1.introduction/1.2.k8sarch.png?pc=90pt)

{{% notice info %}}
Truy cập [Kubernetes docs](https://kubernetes.io/docs) để thêm thông tin.
{{% /notice %}}


## Amazon EKS
#### Tổng quan
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
