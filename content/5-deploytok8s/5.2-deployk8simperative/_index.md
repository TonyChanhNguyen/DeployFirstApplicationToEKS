---
title : "Deploy application with Kubernetes POD by kubectl"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 5.2 </b> "
---
In previous step, we had installed kubectl and minikube successfully. In this step, we will deploy the application on Kubernetes Deployment by imperative way.

1. List all images in your workspace machine.
```
docker images
```
![Deploy K8S Imperative](../../images/5.deployapptok8s/5.2.deployk8simperative/5.2.1.deployk8simperative.png?pc=90pt)

2. Execute those command to create a Kubernetes Deployment in Minikube Cluster with your application's container image.
```
kubectl create deployment mybasicapp --image=firstcloudjourneypcr/mybasicapp:v1
```
3. List and check the Deployment named **mybasicapp**.
```
kubectl get deployment
```
![Deploy K8S Imperative](../../images/5.deployapptok8s/5.2.deployk8simperative/5.2.2.deployk8simperative.png?pc=90pt)

4. List POD created by Deployment **mybasicapp**.
```
kubectl get pod
```
![Deploy K8S Imperative](../../images/5.deployapptok8s/5.2.deployk8simperative/5.2.3.deployk8simperative.png?pc=90pt)

Now, the POD of application was created but can not be accessed. To access to POD, we need to create the Service.

5. Execute the below command to create the Service Load Balancer.
```
kubectl expose deployment mybasicapp --type=LoadBalancer --port=8080
```
6. List and check the Service named **mybasicapp**.
```
kubectl get service
```
![Deploy K8S Imperative](../../images/5.deployapptok8s/5.2.deployk8simperative/5.2.4.deployk8simperative.png?pc=90pt)

7. Create the tunnel to access to your Load Balancer.
```
minikube tunnel
```
![Deploy K8S Imperative](../../images/5.deployapptok8s/5.2.deployk8simperative/5.2.5.deployk8simperative.png?pc=90pt)

8. Click on **Window**. Select **New Terminal** to create the separate terminal.
![Deploy K8S Imperative](../../images/5.deployapptok8s/5.2.deployk8simperative/5.2.6.deployk8simperative.png?pc=90pt)

9. List and check the Service named **mybasicapp** again.
```
kubectl get service
```

![Deploy K8S Imperative](../../images/5.deployapptok8s/5.2.deployk8simperative/5.2.7.deployk8simperative.png?pc=90pt)

The **EXTERNAL-IP** appeared.

10. Now we will test the application by command.
```
curl http://<REPLACE-WITH-EXTERNAL-IP>:8080
```
![Deploy K8S Imperative](../../images/5.deployapptok8s/5.2.deployk8simperative/5.2.8.deployk8simperative.png?pc=90pt)

#### Congratulations, your application was deployed to Minikube using kubectl successfully.

11. Delete Deployment and Service of your application.
```
kubectl delete deployment mybasicapp
kubectl delete service mybasicapp
```

12. Check Deployment and Service again to make sure they were deleted.
```
kubectl get all
``` 