---
title : "Create container image"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3.3 </b> "
---
You had created **Dockerfile** - to guide Docker the way to build container image for your application and **.dockerignore** - to show to Docker know which resources do not need to copy to working directory. Now, we will perform to build container image from those **Dockerfile** and **.dockerignore** file.

Before build container image. Let check there is any image in your machine, but let check which process is running in your machine first.

### Check process
1. Enter this command to list running process in your machine.
```
docker ps
```
![Create Docker image](../../images/3.deployappwithdocker/3.3.createdockerimage/3.3.1.createdockerimage.png?pc=90pt)
There is no running process in your machine. Now we will check which process is existing in your machine.
2. Enter this command to list existing process in your machine.
```
docker ps -a
```
![Create Docker image](../../images/3.deployappwithdocker/3.3.createdockerimage/3.3.3.createdockerimage.png?pc=90pt)

There are 2 processes are existing in machine but status is **Exited**. It means those processes had been stopped. Let remove them into your machine.
3. Enter this command to remove all existing process.
```
docker rm $(docker ps -aq)
```
4. Let check existing process again.
```
docker ps -a
```
![Create Docker image](../../images/3.deployappwithdocker/3.3.createdockerimage/3.3.4.createdockerimage.png?pc=90pt)
There are no existing process in machine.
### Check container image
1. Enter this command to list all container images in your machine.
```
docker images
```
![Create Docker image](../../images/3.deployappwithdocker/3.3.createdockerimage/3.3.1.createdockerimage.png?pc=90pt)

There is a container image named **hello-world**. This image was pulled to your machine when you test Docker Engine at step [3.1 Install Docker](../3.1-installdocker/) by command ```sudo docker run hello-world```.

2. Now we will delete this image by command.
```
docker delete image hello-word
```
![Create Docker image](../../images/3.deployappwithdocker/3.3.createdockerimage/3.3.5.createdockerimage.png?pc=90pt)

3. Let list images again.
```
docker images
```
![Create Docker image](../../images/3.deployappwithdocker/3.3.createdockerimage/3.3.6.createdockerimage.png?pc=90pt)
Now, there are no images in your machine. Let build container image for your application.

### Build container image
1. Execute this command to build container image for your application.
```
docker build -t fcj-application:v1 .
```
![Create Docker image](../../images/3.deployappwithdocker/3.3.createdockerimage/3.3.7.createdockerimage.png?pc=90pt)

2. Now, let list all images in your machine.
```
docker images
```
![Create Docker image](../../images/3.deployappwithdocker/3.3.createdockerimage/3.3.8.createdockerimage.png?pc=90pt)

The container image of your application had been built successfully.