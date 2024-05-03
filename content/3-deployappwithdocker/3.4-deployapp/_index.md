---
title : "Deploy application"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 3.4 </b> "
---
In previous step, you had built container image for your application. Now, we will deploy it to Docker.

### Deploy application to Docker using container image
1. Execute this command to run your application with Docker.
```
docker run -d --name my-docker-deployment -p 8080:8080 fcj-application:v1 
```
2. Check which process is running in your machine.
```
docker ps -a
```
![Create Application](../../images/3.deployappwithdocker/3.4.deployapp/3.4.1.deployapp.png?pc=90pt)

3. Access to URL ```http://<YOUR_IP_ADDRESS>:8080``` to see the result.
![Create Application](../../images/3.deployappwithdocker/3.4.deployapp/3.4.2.deployapp.png?pc=90pt)

#### Congratulations, you had deployed your application to Docker successfully.

### Delete process.
1. First, you need to stop your process by command.
```
docker stop my-docker-deployment
```
2. Then, use this command to remove your process.
```
docker rm my-docker-deployment
```
3. Let check existing process in your machine again.
```
docker ps -a
```
![Create Application](../../images/3.deployappwithdocker/3.4.deployapp/3.4.3.deployapp.png?pc=90pt)