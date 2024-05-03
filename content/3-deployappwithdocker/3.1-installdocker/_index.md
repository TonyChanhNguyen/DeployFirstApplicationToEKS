---
title : "Install Docker"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 3.1 </b> "
---
In this step, we will check the version of Docker and install if it is not existing.

### Check the version of Docker
1. At the Cloud9 terminal, execute this command to check the version of docker.
```
docker version
```
![Install Docker](../../images/3.deployappwithdocker/3.1.installdocker/3.1.1.installdocker.png?pc=90pt)

At you see, the version of Docker now is 25.0.3.

2. Run this command to test with Docker.
```
sudo docker run hello-world
```
![Install Docker](../../images/3.deployappwithdocker/3.1.installdocker/3.1.2.installdocker.png?pc=90pt)


### Install Docker if it is not existing.
1. Update the installed packages and package cache on your instance.
```
sudo yum update -y
```
2. Install the most recent Docker Community Edition package.
```
sudo yum install -y docker
```

![Install Docker](../../images/3.deployappwithdocker/3.1.installdocker/3.1.3.installdocker.png?pc=90pt)
3. Start the Docker service.
```
sudo service docker start
```
4. Add the ec2-user to the docker group so you can execute Docker commands without using sudo.
```
sudo usermod -a -G docker ec2-user
```

5. Run this command to test with Docker.
```
sudo docker run hello-world
```
![Install Docker](../../images/3.deployappwithdocker/3.1.installdocker/3.1.4.installdocker.png?pc=90pt)