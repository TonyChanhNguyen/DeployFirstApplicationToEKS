---
title : "Pull image from DockerHub"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 4.3 </b> "
---
In previous step, we had pushed container image to DockerHub repository. In this step, we will pull container image to Workspace instance from DockerHub repository. To do that, we wil remove all images in workspace instance first. Then, we will perform pulling and running Docker container application from that image.
1. Let list all images in workspace instance. 
```
docker images
```
There are 2 container images in workspace instance.
2. Next, execute this command to delete them. Confirm **Y** when be asked.
```
docker image prune -a
```
3. List all images again to make sure they were deleted.
```
docker images
```
![Pull Container Image](../../images/4.dockerhub/4.3.pullimage/4.3.1.pullimage.png?pc=90pt)

4. Now we will pull the container image from DockerHub repository by command.
```
docker pull firstcloudjourneypcr/mybasicapp:v1
```

5. Then, list pulled container image
```
docker images
```
![Pull Container Image](../../images/4.dockerhub/4.3.pullimage/4.3.2.pullimage.png?pc=90pt)

We can see there is a container image hab been pulled successfully.

6. Now, we will deploy this image to Docker to run application for testing.
```
docker run --name demoapplication -d -p 8080:8080 firstcloudjourneypcr/mybasicapp:v1
```
7. Check running process in workspace instance.
```
docker ps
```
![Pull Container Image](../../images/4.dockerhub/4.3.pullimage/4.3.3.pullimage.png?pc=90pt)

The application had been deployed successfully.

8. Access to your application to see the result.
![Pull Container Image](../../images/4.dockerhub/4.3.pullimage/4.3.4.pullimage.png?pc=90pt)

#### Congratulations, you had pulled container image from Public Container Registry - DockerHub and deploy it to Docker successfully!