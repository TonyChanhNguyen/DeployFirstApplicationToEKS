---
title : "Deploy application with Kubernetes POD by YAML manifest file"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 5.2 </b> "
---
In previous step, we will deploy the application on Kubernetes Deployment by imperative way. In this step, we will deploy the application on Kubernetes Deployment by declarative way.
1. Create a directory named **kube-manifest**.
```
mkdir kube-manifest
cd kube-manifest
```
2. Create a file named **01.mybasicapp-deployment.yaml**.
```
touch 01.mybasicapp-deployment.yaml
```
3. Open file **01.mybasicapp-deployment.yaml**.
4. Paste the code below and save.
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

![Deploy K8S Declarative](../../images/5.deployapptok8s/5.3.deployk8sdeclarative/5.3.1.deployk8sdeclarative.png?pc=90pt)

2. Create the file named **02.mybasicapp-service.yaml** and save those code below.
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
3. Apply those kubernetes file by command.
```
kubectl apply -f .
```

4. Then, check Deployment, Service and POD had been created by command.
```
kubectl get all
```
![Deploy K8S Declarative](../../images/5.deployapptok8s/5.3.deployk8sdeclarative/5.3.3.deployk8sdeclarative.png?pc=90pt)

5. Test your application.
```
curl http://<REPLACE-WITH-EXTERNAL-IP>:8080
```
![Deploy K8S Declarative](../../images/5.deployapptok8s/5.3.deployk8sdeclarative/5.3.4.deployk8sdeclarative.png?pc=90pt)

#### Congratulations, your application was deployed to Minikube using manifest file successfully.

11. To delete Deployment and Service created by declarative way, using below command.
```
kubectl delete -f .
```

12. Check Deployment and Service again to make sure that they were deleted.
```
kubectl get all
```

![Deploy K8S Declarative](../../images/5.deployapptok8s/5.3.deployk8sdeclarative/5.3.5.deployk8sdeclarative.png?pc=90pt)

13. Stop your Minikube Cluster to save the resource.
```
minikube stop
```

![Deploy K8S Declarative](../../images/5.deployapptok8s/5.3.deployk8sdeclarative/5.3.6.deployk8sdeclarative.png?pc=90pt)
