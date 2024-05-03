---
title : "Dọn dẹp tài nguyên"
date :  "`r Sys.Date()`" 
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---

### Dọn dẹp EKS Cluster
1. Thực thi câu lệnh dưới đây để xóa EKS Cluster
```
eksctl delete cluster --name my-fcj-cluster --region ap-southeast-1
```

![Dọn dẹp tài nguyên](../../images/7.cleanup/7.1.cleanup.png?pc=90pt)

{{% notice info %}}
Sẽ mất khoảng 20 phút để xóa hoàn toàn EKS Cluster.
{{% /notice %}}

![Dọn dẹp tài nguyên](../../images/7.cleanup/7.2.cleanup.png?pc=90pt)

### Xóa môi trường Cloud9
1. Đi đến [Cloud9](https://ap-southeast-1.console.aws.amazon.com/cloud9control/home?region=ap-southeast-1#/).
2. Chọn **FCJ-Workspace**.
3. Nhấn **Delete**.

![Dọn dẹp tài nguyên](../../images/7.cleanup/7.3.cleanup.png?pc=90pt)

4. Nhập ```Delete``` để xác nhận.
5. Nhấn **Delete**.
![Dọn dẹp tài nguyên](../../images/7.cleanup/7.4.cleanup.png?pc=90pt)


### Xóa IAM Role.
1. Đi đến [IAM Role](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles).
2. Tìm kiếm IAM Role tên ```eksworkspace-administrator```.
3. Chọn IAM Role.
4. Nhấn **Delete**.
![Dọn dẹp tài nguyên](../../images/7.cleanup/7.5.cleanup.png?pc=90pt)

5. Nhập tên của IAM Role ```eksworkspace-administrator``` để xác nhận.
6. Nhấn **Delete**.
![Dọn dẹp tài nguyên](../../images/7.cleanup/7.6.cleanup.png?pc=90pt)