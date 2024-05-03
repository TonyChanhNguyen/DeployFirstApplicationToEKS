---
title : "Deploy application with Docker"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---
In this section, we will deploy the application using Docker to understand the way to containerize and run application.

### Overview
Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker's methodologies for shipping, testing, and deploying code, you can significantly reduce the delay between writing code and running it in production.

#### Docker architecture
**The Docker daemon**: The Docker daemon listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.

**The Docker client**: The Docker client is the primary way that many Docker users interact with Docker. When you use commands, the client sends these commands to Docker daemon, which carries them out. The docker command uses the Docker API. The Docker client can communicate with more than one daemon.

**Docker Desktop**: Docker Desktop is an easy-to-install application for your Mac, Windows or Linux environment that enables you to build and share containerized applications and microservices.

**Docker registries**: A Docker registry stores Docker images. Docker Hub is a public registry that anyone can use, and Docker looks for images on Docker Hub by default.

**Images**: An image is a read-only template with instructions for creating a Docker container.

**Containers**: A container is a runnable instance of an image. You can create, start, stop, move, or delete a container using the Docker API or CLI.

![Docker Architecture](../images/1.introduction/1.1.dockerarch.png?pc=90pt)

{{% notice info %}}
Access to [Docker docs](https://docs.docker.com/) for more detail.
{{% /notice %}}

### Content
+ 3.1 [Install Docker](3.1-installdocker/)
+ 3.2 [Create Dockerfile](3.2-createdockerfile/)
+ 3.3 [Create container image](3.3-createdockerimage/)
+ 3.4 [Deploy application](3.4-deployapp/)