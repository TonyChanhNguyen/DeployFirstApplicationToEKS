---
title : "Push image to DockerHub"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 4.2 </b> "
---
In previous step, we created DockerHub account, public repository and login successfully. Now, we will perform to push container image to created repository.
1. Let list the container images in workspace instance again.
```
docker images
```
![Push Container Image](../../images/4.dockerhub/4.2.pushimage/4.2.1.pushimage.png?pc=90pt)

At you can see, we had only 1 image with **Repository** is **fcj-application**. To push container image to repository, **Repository** of your container image must match with repository format of DockerHub ```<YOUR_USER_NAME>/<YOUR_REPOSITORY_NAME>```. So now we need to use ``docker image tag`` command to copy and correct repository format of your container image in workspace instance.

2. Execute this command to tag your container image.
```
docker image tag fcj-application:v1 firstcloudjourneypcr/mybasicapp:v1
```
3. Then, let list container images in workspace instance again to see the result.
```
docker images
```
![Push Container Image](../../images/4.dockerhub/4.2.pushimage/4.2.2.pushimage.png?pc=90pt)

Now, there are 2 container images. The new one has repository named **firstcloudjourneypcr/mybasicapp** with tag is **v1**.
Next, let push this container image to DockerHub.

4. Execute this command to push your container image to DockerHub.
```
docker push firstcloudjourneypcr/mybasicapp:v1
```
![Push Container Image](../../images/4.dockerhub/4.2.pushimage/4.2.3.pushimage.png?pc=90pt)

5. Back to your Docker Hub repository to check the result. There is a image container had been pushed to.

![Push Container Image](../../images/4.dockerhub/4.2.pushimage/4.2.4.pushimage.png?pc=90pt)

