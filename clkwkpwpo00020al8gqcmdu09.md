---
title: "Day 18: Docker for DevOps Engineers"
datePublished: Fri Aug 04 2023 12:40:11 GMT+0000 (Coordinated Universal Time)
cuid: clkwkpwpo00020al8gqcmdu09
slug: day-18-docker-for-devops-engineers
tags: docker, devops, docker-compose, 90daysofdevops, trainwithshubham

---

## Docker Compose

* Docker Compose is a tool that was developed to help define and share multi-container applications.
    
* With Compose, we can create a YAML file to define the services and with a single command, can spin everything up or tear it all down.
    

## Docker Compose Commands

Here's a list of common Docker Compose commands:

1. `docker-compose up`: Create and start containers.
    
2. `docker-compose down`: Stop and remove containers.
    
3. `docker-compose build`: Build or rebuild services.
    
4. `docker-compose start`: Start services.
    
5. `docker-compose stop`: Stop services.
    
6. `docker-compose restart`: Restart services.
    
7. `docker-compose logs`: View service logs.
    
8. `docker-compose ps`: List running containers.
    
9. `docker-compose exec`: Execute a command in a running container.
    

## What is YAML?

* YAML is a data serialization language that is often used for writing configuration files. Depending on whom you ask, YAML stands for yet another markup language or YAML ain’t markup language (a recursive acronym), which emphasizes that YAML is for data, not documents.
    
* YAML is a popular programming language because it is human-readable and easy to understand.
    
* YAML files use a .yml or .yaml extension.
    

### **Task 1: Learn how to use the docker-compose.yml file, to set up the environment, configure the services and links between different containers, and also to use environment variables in the docker-compose.yml file.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691150080362/8ffc97f2-8fac-4a7c-8e6a-423985a3e828.png align="center")

**Components of the above file:**

1. Version: Version is used to specify the version of the Docker Compose file format being used. It is always the first line in the `docker-compose.yml` file.
    
2. Services: Defines individual containers and their configurations.
    
3. Images: Specifies the Docker images used for each service.
    
4. Environment Variables: Sets environment variables for services.
    
5. Ports: Maps container ports to the host system.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691150986004/0dbdab9f-f314-4020-ac31-aa5ff7b9bde2.png align="center")

Checking the status of both servers:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691151110203/07105cf2-d207-498c-9340-5edd778a7aa0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691151347971/32dd40c2-36a5-49bb-933b-776d15332f0c.png align="center")

We have successfully created the services using docker-compose.yaml

### **Task 2: Pull a pre-existing Docker image from a public repository (e.g. Docker Hub) and run it on your local machine.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691151482436/499d0106-3750-411e-9eae-4f1b74602128.png align="center")

Run the container as a non-root user (Hint- Use `usermod` command to give user permission to docker). Make sure you reboot instance after giving permission to user.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691152215784/e72955f1-20e6-43ee-aa29-3ecbd9a1492e.png align="center")

Inspect the container's running processes and exposed ports using the docker inspect command.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691152264652/1f9d1feb-83e0-4a57-a39e-7903ed674ed3.png align="center")

Use the docker logs command to view the container's log output.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691152340504/da169bf8-c711-4055-aa40-3faa9de7c4ce.png align="center")

Use the docker stop and docker start commands to stop and start the container.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691152425142/6dc4a447-d2bd-4f71-b4a7-a377029e3d40.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691152465768/dbd09491-4a81-494f-8c61-ab3197f5382d.png align="center")

Use the docker rm command to remove the container when you're done.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691152573767/8c9f0193-27ce-4a41-97a0-bde633aa8602.png align="center")

## How to run Docker commands without sudo?

* Make sure docker is installed and system is updated (This is already been completed as a part of previous tasks):
    
* sudo usermod -a -G docker $USER
    
* Reboot the machine.
    

I hope you like my blog..!!

Stay Connected with me for more interesting articles on DevOps, if you like my blog follow me on **Hashnode** and **Linkedin** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)