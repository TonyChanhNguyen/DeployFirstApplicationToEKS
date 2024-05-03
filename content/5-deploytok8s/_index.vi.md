---
title : "Triển khai ứng dụng với K8S"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

### Tổng quan
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

### Nội dung
+ 5.1 [Cài đặt Kubernetes](5.1-installk8s/)
+ 5.2 [Triển khai ứng dụng với Kubernetes POD bằng kubectl](5.2-deployk8simperative/)
+ 5.3 [Triển khai ứng dụng với kubernetes POD bằng YAML manifest file](5.3-deployk8sdeclarative/)