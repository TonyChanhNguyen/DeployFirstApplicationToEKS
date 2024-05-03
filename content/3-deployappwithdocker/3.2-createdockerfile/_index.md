---
title : "Create Dockerfile"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 3.2 </b> "
---
In this step, we will create a Dockerfile to guide Docker how to build container image of your application.
1. Create a file named **Dockerfile**.
```
touch Dockerfile
```
![Create Dockerfile](../../images/3.deployappwithdocker/3.2.createdockerfile/3.2.1.createdockerfile.png?pc=90pt)

2. Open the **Dockerfile**.
![Create Dockerfile](../../images/3.deployappwithdocker/3.2.createdockerfile/3.2.2.createdockerfile.png?pc=90pt)

3. Enter the code below.
```Dockerfile
FROM node:13-alpine

#configure working directory
WORKDIR /app

COPY package.json ./

RUN npm install

#bundle the source code

COPY . ./

EXPOSE 8080

CMD ["node","index.js"]


```
![Create Dockerfile](../../images/3.deployappwithdocker/3.2.createdockerfile/3.2.3.createdockerfile.png?pc=90pt)

*Note*: 
+ At step **COPY package.json ./**, Docker will copy **package.json** file to working directory **/app**, then process step **RUN npm install** to install all dependencies were defined in **package.json** file and save them to **node_modules** folder.

+ At step **COPY . ./**, Docker will copy all resource to working directory **/app** - include **node_modules** folder and **Dockerfile** file. Those folder and file are not necessary to copy again to working directory. So you can create **.dockerignore** to list which file or folder do not need to copy to working directory.

4. Create file named **.dockerignore** by command.
```
touch .dockerignore
```
![Create Dockerfile](../../images/3.deployappwithdocker/3.2.createdockerfile/3.2.4.createdockerfile.png?pc=80pt)

You will not see where **.dockerignore** is, since Cloud9 recognize **.dockerignore** is hidden file.

5. Click on **Setting**.
6. Select **Show Hidden Files**.

![Create Dockerfile](../../images/3.deployappwithdocker/3.2.createdockerfile/3.2.5.createdockerfile.png?pc=90pt)

7. Open **.dockerignore** and enter those values.
```
node_modules
Dockerfile
```
![Create Dockerfile](../../images/3.deployappwithdocker/3.2.createdockerfile/3.2.6.createdockerfile.png?pc=90pt)