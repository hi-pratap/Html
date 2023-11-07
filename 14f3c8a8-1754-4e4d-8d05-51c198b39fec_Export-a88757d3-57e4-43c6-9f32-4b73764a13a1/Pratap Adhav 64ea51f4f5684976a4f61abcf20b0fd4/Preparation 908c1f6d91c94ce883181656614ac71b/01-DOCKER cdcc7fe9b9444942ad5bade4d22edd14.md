# 01-DOCKER

ID: DOPS-5
Created: July 31, 2023 4:17 PM
Files & media: https://drive.google.com/file/d/1lAW5phx1bjnsVl0f8kcsCd5wHfQUvS6F/view?usp=drive_link
Select: devops
Date: November 30, 2023
Days Left: 📅 23 days left
Status: In progress
URL: https://iz-my.sharepoint.com/:f:/g/personal/pratap_adhav_intelizign_com/ElTNMyk537VMhJ8yG_XPuOEBw4EVJG6eSFgSZIb5bL1R7Q?e=mj42ij

- [x]  lecture 1
- [x]  lecture 4 ?—name and -modes
- [ ]  lecture 7
- [ ]  lecture 10
- [ ]  lecture 13
- [ ]  lecture 16
- [ ]  lecture 19

- [x]  lecture 2
- [ ]  lecture 5
- [ ]  lecture 8
- [ ]  lecture 11
- [ ]  lecture 14
- [ ]  lecture 17
- [ ]  lecture 20

- [x]  lecture 3
- [ ]  lecture 6
- [ ]  lecture 9
- [ ]  lecture 12
- [ ]  lecture 15
- [ ]  lecture 18

1. Docker Notes: Docker & Kubernetes (4 weeks)

# 1. Docker Introduction:

- Docker container is an isolated area used for deploying applications.
- It allows for easy and cost-effective deployment with high performance.
- Docker containers are lightweight and efficient virtualization units.

> It is isolated area
> 

> It is For only deploying applications Very easily
> 

> With low cast
> 

> With high performance
> 

![Untitled](01-DOCKER%20cdcc7fe9b9444942ad5bade4d22edd14/Untitled.png)

## a. AWS Servers:

- **To create an AWS server, follow these steps:**
    1. Create an **AWS account** and **log in.**
    2. Choose the **EC2 service**.
    3. Configure the instance details, such as the **instance count** and type (e.g., **t2.micro**).
    4. Select an **Ubuntu Linux AMI (Amazon Machine Image)** as the operating system.
    5. Configure security settings, including SSH and HTTP access.
    6. Choose an EBS root volume for storage.
    7. Launch the instance to create the server.
    
    ![Untitled](01-DOCKER%20cdcc7fe9b9444942ad5bade4d22edd14/Untitled%201.png)
    

![Untitled](01-DOCKER%20cdcc7fe9b9444942ad5bade4d22edd14/Untitled%202.png)

### 1. Connecting to AWS Server:

How to connect to aws server?

1. Install git on laptop
2. By using git bash , pem file we can connect

`$ sudo -i`

> switch to Root user
> 

`#apt-get update`

> To Get Update{ Initially we have to do this}
> 

`#curl -fsSL [https://get.docker.com](https://get.docker.com/) -o [install-docker.sh](http://install-docker.sh/)`

> To Get Docker install Script on our Linux Machine
> 

`#sudo sh [install-docker.sh](http://install-docker.sh/)`

> We have to Run this script to install docker on linux
> 

WE NEED TO CHECK IF DOCKER IS INSTALLED

`#docker --version`

> To check Docker Version
> 

`#docker run --name myc1 -d -p 8081:80 nginx`

> Docker run = search image + download image + create container
> 

```java
1. This Command will Search image first in local registry, means in docker deamon, then if not found it will search on docker hub registry
2. Download image 
3. And create Container
```

`#docker ps`

> Docker ps is for checking running containers
> 

`#docker images`

> Docker images is for checking the available images in local registry
> 

`#docker rm <container name/container id> -f`

> docker rm delete the container and -f here is used to forcefully delete.
> 

`#docker rmi <image name/ image id>`

> Docker RMI delete the image from local Repository
> 

`#docker ps -a -q`

> docker ps -a -q is for getting all docker container with there container id.
> 

```java
1. -a={"this is used to get all images."}
2. -q={"this is used to get container id from container list"}
```

`#docker images -q`

> Docker images -q is used to get image id from images list
> 

`#docker rm $(docker ps -a -q) -f`

> this command is used to delete all the docker container at once
> 

`#docker rmi $(docker images -q)`

> this command is used to delete all the docker images at once
> 

`#docker inspect <container_name_or_id>`

> The **`docker inspect`** command is used to obtain detailed information about a specific Docker container. It provides a comprehensive `JSON representation` of the container's configuration and runtime details
> 

`# docker search <image name>`

> The **`docker search`** command is used to search for Docker images available in the Docker Hub registry or any other container registry specified in your Docker configuration.
> 

`# docker pull <image name>`

> The **`docker pull`** command is used to download Docker images from a container registry, such as Docker Hub, to your local system.
> 

`#docker stop <container name/ id>`

> The **`docker stop`** command is used to gracefully stop a running Docker container.
> 

`#docker ps -a`

> The **`docker ps`** command is used to display information about the running containers on your system. However, when you add the **`-a`** (or **`--all`**) flag, it shows information about all containers, including both running and stopped ones. This command is useful for checking the status of containers, viewing container details, and identifying stopped containers that you may want to remove.
> 

`#docker rm <container name/ id>`

> The **`docker rm`** command is used to remove one or more stopped Docker containers from your system. When you stop a container using **`docker stop`**, it remains on your system as a stopped container until you explicitly remove it with **`docker rm`**.
> 

> `Docker run = search image + download image + create container`
> 

## b. Docker ARK:

![Untitled](01-DOCKER%20cdcc7fe9b9444942ad5bade4d22edd14/Untitled%203.png)

Docker run itself is docker client

Docker App is Docker Demon

Docker Hub is Docker Registry

## c. Docker Lifecycle:

- The Docker container lifecycle involves several stages, including creating, starting, stopping, and removing containers.

> Before deleting we should stop docker container.
> 
- To stop docker container use `docker stop <container_id/container_name>`
- to check if it stopped use `docker ps` which shows only running container
- <to check stopped container user `docker ps -a {which shows all the containers}`>

![Untitled](01-DOCKER%20cdcc7fe9b9444942ad5bade4d22edd14/Untitled%204.png)

## c. Docker Modes:

### 1. **Docker Attach: Without the `-d` flag** :

When creating the container, container is attached to the terminal. When the terminal is closed, the container automatically stops.
Example: `docker run nginx`

### 2. **Docker Detach: With the `-d` flag,**

When creating the container, container is detached from the terminal, and it continues running even when the terminal is closed.
Example: `docker run -d nginx`

### 3. **Docker Interact: With the `it` flag:**

After creation of the container, by using interact mode , we can get into the
container.

Example: `docker exec -it <container name> /bin/bash`

## d. How Docker Containers Work:

- Docker containers run on top of the host OS, using shared kernel features to achieve isolation.
- They are built from images that contain the application and its dependencies.
- Docker containers are portable and can be easily moved and executed on different systems.

## e. Port Forwarding:

- Port forwarding, specified using the `p` flag in `docker run`, allows mapping ports between the host and the container.
- For example, `docker run -p 8081:80 nginx` maps port 80 of the container to port 8081 on the host. This allows accessing the web server running inside the container from the internet.

# 2 Docker Commands 🚢

### 1. Get root User

`$ sudo -i`

> switch to Root user
> 

### 2. Get Update

`#apt-get update`

> To Get Update{ Initially we have to do this}
> 

### 3. Get docker scripts

`#curl -fsSL [https://get.docker.com](https://get.docker.com/) -o [install-docker.sh](http://install-docker.sh/)`

> To Get Docker install Script on our Linux Machine
> 

### 4. Install the Docker Script

`#sudo sh [install-docker.sh](http://install-docker.sh/)`

> We have to Run this script to install docker on linux
> 

### 5. Check Docker version

`#docker --version`

> To check Docker Version
> 

### 6. Docker Create Container

`#docker run --name myc1 -d -p 8081:80 nginx`

> Docker run = search image + download image + create container
> 

```java
1. This Command will Search image first in local registry, means in docker deamon, then if not found it will search on docker hub registry
2. Download image 
3. And create Container
```

### 7. Docker check Running Container

`#docker ps`

> Docker ps is for checking running containers
> 

### 8. Docker Check images

`#docker images`

> Docker images is for checking the available images in local registry
> 

### 9. Docker Delete The Container

`#docker rm <container name/container id> -f`

> docker rm delete the container and -f here is used to forcefully delete.
> 

### 10. Docker delete the Image

`#docker rmi <image name/ image id>`

> Docker RMI delete the image from local Repository
> 

### 11. Docker get All Container Id

`#docker ps -a -q`

> docker ps -a -q is for getting all docker container with there container id.
> 

```java
1. -a={"this is used to get all images."}
2. -q={"this is used to get container id from container list"}
```

### 12. Docker Get Images Id

`#docker images -q`

> Docker images -q is used to get image id from images list
> 

### 13. Docker Delete All the Container

`#docker rm $(docker ps -a -q) -f`

> this command is used to delete all the docker container at once
> 

### 14. Docker Delete All the Images

`#docker rmi $(docker images -q)`

> this command is used to delete all the docker images at once
> 

### 15. Docker Check All The Details

`#docker inspect <container_name_or_id>`

> The **`docker inspect`** command is used to obtain detailed information about a specific Docker container. It provides a comprehensive `JSON representation` of the container's configuration and runtime details
> 

### 16. Docker Search Image

`# docker search <image name>`

> The **`docker search`** command is used to search for Docker images available in the Docker Hub registry or any other container registry specified in your Docker configuration.
> 

### 17. Docker Pull Images

`# docker pull <image name>`

> The **`docker pull`** command is used to download Docker images from a container registry, such as Docker Hub, to your local system.
> 

### 18. Docker Stop Container

`#docker stop <container name/ id>`

> The **`docker stop`** command is used to gracefully stop a running Docker container.
> 

### 19. Docker Check all the running Container

`#docker ps -a`

> The **`docker ps`** command is used to display information about the running containers on your system. However, when you add the **`-a`** (or **`--all`**) flag, it shows information about all containers, including both running and stopped ones. This command is useful for checking the status of containers, viewing container details, and identifying stopped containers that you may want to remove.
> 

### 20. Docker Delete container.

`#docker rm <container name/ id>`

> The **`docker rm`** command is used to remove one or more stopped Docker containers from your system. When you stop a container using **`docker stop`**, it remains on your system as a stopped container until you explicitly remove it with **`docker rm`**.
> 

> `**Docker run = search image + download image + create container**`
> 

# 3. Image👍

1. create Image
2. Build Image
3. Create Container

{ Docker File is simple plain text format }

> 1) Create Docker File name should be exactly `Dockerfile`
> 

```java
FROM ubuntu:22.04 // this is base image
MAINTAINER pratap // this is optional
RUN apt-get update // this run while image building
CMD ["echo","This is my First Container"] // only this command executing container above three were executed while building 
```

> 2) Now Build Docker Image using a command
> 

`docker build -t myImage:1`

> 3) Create Container
> 

`docker run myImage:1` 

### Tomcat

![Untitled](01-DOCKER%20cdcc7fe9b9444942ad5bade4d22edd14/Untitled%205.png)

## Deploy Java Application

#vi Dockerfile `{For Editing File}`

```docker
FROM tomcat:8.5.37-jre8
MAINTAINER maha
RUN apt-get update
COPY mahaLogin.war /usr/local/tomcat/webapps
EXPOSE 8080
CMD[”catalina.sh”, ”run”] 
```