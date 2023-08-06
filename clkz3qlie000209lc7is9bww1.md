---
title: "Docker Cheat Sheet"
datePublished: Sun Aug 06 2023 07:08:08 GMT+0000 (Coordinated Universal Time)
cuid: clkz3qlie000209lc7is9bww1
slug: docker-cheat-sheet
tags: docker, devops, docker-command, 90daysofdevops, trainwithshubham

---

## Docker Commands:

### Image Management:

* `docker build`: Build a Docker image from a Dockerfile.
    
* `docker pull`: Pull an image from a registry (e.g., Docker Hub).
    
* `docker push`: Push an image to a registry (e.g., Docker Hub).
    
* `docker images`: List Docker images on the local machine.
    
* `docker rmi`: Remove one or more Docker images.
    
* `docker inspect`: Display detailed information about a Docker image.
    

### Container Management:

* `docker run`: Create and start a new container.
    
* `docker start`: Start one or more stopped containers.
    
* `docker stop`: Stop one or more running containers.
    
* `docker restart`: Restart one or more containers.
    
* `docker pause`: Pause processes in one or more containers.
    
* `docker unpause`: Unpause processes in one or more containers.
    
* `docker ps`: List running containers.
    
* `docker ps -a`: List all containers (including stopped ones).
    
* `docker rm`: Remove one or more containers.
    
* `docker exec`: Execute a command inside a running container.
    
* `docker logs`: View logs from a container.
    
* `docker stats`: Display a live stream of container resource usage.
    

### Docker Compose:

* `docker-compose up`: Create and start containers defined in a docker-compose.yml file.
    
* `docker-compose down`: Stop and remove containers, networks, and volumes defined in a docker-compose.yml file.
    
* `docker-compose build`: Build or rebuild services defined in a docker-compose.yml file.
    
* `docker-compose ps`: List containers defined in a docker-compose.yml file.
    
* `docker-compose logs`: View logs from containers defined in a docker-compose.yml file.
    

### Volume Management:

* `docker volume create`: Create a new named volume.
    
* `docker volume ls`: List available volumes.
    
* `docker volume inspect`: Display detailed volume information.
    
* `docker volume rm`: Remove one or more named volumes.
    
* `docker volume prune`: Remove all unused volumes.
    

### Network Management:

* `docker network create`: Create a new user-defined network.
    
* `docker network ls`: List available networks.
    
* `docker network inspect`: Display detailed network information.
    
* `docker network rm`: Remove one or more user-defined networks.
    
* `docker network prune`: Remove all unused networks.
    

### Registry/Login:

* `docker login`: Log in to a Docker registry (e.g., Docker Hub).
    
* `docker logout`: Log out from a Docker registry.
    

### **System Information:**

* `docker version`: Display Docker version information.
    
* `docker info`: Display Docker system-wide information.
    

These are some of the most commonly used Docker commands for various tasks related to image management, container management, Docker Compose, volume and network management, registry login/logout, and system information. Keep in mind that there are many other options and flags available for each command, and you can always refer to the Docker documentation for more details.

I hope you like my blog..!!

Stay Connected with me for more interesting articles on DevOps, if you like my blog follow me on **Hashnode** and **Linkedin** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)