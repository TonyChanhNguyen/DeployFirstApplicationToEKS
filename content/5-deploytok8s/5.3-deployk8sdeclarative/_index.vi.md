---
title : "Triển khai ứng dụng với Kubernetes POD bằng YAML manifest"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 5.2 </b> "
---
Ở bước trước đó, chúng ta sẽ triển khai ứng dụng trên Kubernetes Deployment bằng mệnh lệnh (Imperative). Ở bước này, chúng ta sẽ tìm hiểu cách triển khai ứng dụng trên Kubernetes Deployment bằng tệp manifest YAML (Declarative)
1. Tạo một thư mục tên **kube-manifest**.
```
mkdir kube-manifest
cd kube-manifest
```
2. Tạo một tệp tên **01.mybasicapp-deployment.yaml**.
```
touch 01.mybasicapp-deployment.yaml
```
3. Mở tệp **01.mybasicapp-deployment.yaml**.
4. Dán đoạn mã code dưới đây và lưu lại.
```
apiVersion: apps/v1
kind: Deployment
metadata:
    name: mybasicapp-deployment
    labels:
        app: mybasicapp
spec:
    replicas: 1
    selector:
        matchLabels:
            app: mybasicapp
    template:
        metadata:
            labels:
                app: mybasicapp
        spec:
            containers:
            - name: mybasicapp
              image: firstcloudjourneypcr/mybasicapp:v1
              ports: 
              - containerPort: 8080
```

![Triển khai K8S Declarative](../../../images/5.deployapptok8s/5.3.deployk8sdeclarative/5.3.1.deployk8sdeclarative.png?pc=90pt)

2. Tạo một tệp tên **02.mybasicapp-service.yaml** và lưu đoạn mã code dưới đây.
```
apiVersion: v1
kind: Service
metadata:
    name: mybasicapp-service
    labels:
        app: mybasicapp
spec:
    selector:
        app: mybasicapp
    type: LoadBalancer
    ports:
    - port: 8080
      targetPort: 8080
```
3. Áp dụng các tệp Kubernetes.
```
kubectl apply -f .
```

4. Sau đó, kiểm tra Deployment, Service và POD vừa được tạo.
```
kubectl get all
```
![Triển khai K8S Declarative](../../../images/5.deployapptok8s/5.3.deployk8sdeclarative/5.3.3.deployk8sdeclarative.png?pc=90pt)

5. Kiểm tra ứng dụng.
```
curl http://<REPLACE-WITH-EXTERNAL-IP>:8080
```
![Triển khai K8S Declarative](../../../images/5.deployapptok8s/5.3.deployk8sdeclarative/5.3.4.deployk8sdeclarative.png?pc=90pt)

#### Chúc mừng, ứng dụng của bạn đã được triển khai trên Minikube sử dụng tệp manifest thành công.

11. Để xóa Deployment và Service được tạo ra bằng phương thức khai báo, sử dụng câu lệnh này.
```
kubectl delete -f .
```

12. Kiểm tra Deployment và Service lần nữa để đảm bảo rằng chúng đã được xóa.
```
kubectl get all
```

![Triển khai K8S Declarative](../../../images/5.deployapptok8s/5.3.deployk8sdeclarative/5.3.5.deployk8sdeclarative.png?pc=90pt)

13. Stop your Minikube Cluster to save the resource.
```
minikube stop
```

![Triển khai K8S Declarative](../../../images/5.deployapptok8s/5.3.deployk8sdeclarative/5.3.6.deployk8sdeclarative.png?pc=90pt)
