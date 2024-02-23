---
title: "DevOps Project-3"
datePublished: Fri Feb 23 2024 11:37:21 GMT+0000 (Coordinated Universal Time)
cuid: clsykv0sv00050akz92v97m5p
slug: devops-project-3
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1708688152670/1cf576ed-6422-4668-80f4-50d496d27649.jpeg
tags: docker, projects, devops, 90daysofdevops, trainwithshubham

---

## Project Description

The project aims to deploy a web application using Docker Swarm, a container orchestration tool that allows for easy management and scaling of containerized applications. The project will utilize Docker Swarm's production-ready features such as load balancing, rolling updates, and service discovery to ensure high availability and reliability of the web application. The project will involve creating a Dockerfile to package the application into a container and then deploying it onto a Swarm cluster. The Swarm cluster will be configured to provide automated failover, load balancing, and horizontal scaling to the application. The goal of the project is to demonstrate the benefits of Docker Swarm for deploying and managing containerized applications in production environments.

## Prerequisites

Let’s Get Started with AWS First thing, head over to the AWS portal and create three new instances with specific names:

Swarm-manager,

Swarm-worker1,

Swarm-worker2.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708602948111/b259e791-15d3-4370-8303-ceb2c59bff45.png align="center")

Now, Install docker on all three servers.

Initialise the docker swarm in the manager node.

To add a worker to this swarm, run the following command as displayed after the "docker swarm init" :

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708603484085/99fe3a21-4a09-416d-a814-6fb074a7d678.png align="center")

Now Copy and paste this token in your worker nodes

docker swarm join --token SWMTKN-1-0mh89i4vg81rjc5qk3x4lw6rqntvrecepucmk7rrslfwpdm69n-7dtesuyur6sct1w4bske7ktv7 172.31.33.94:2377

* Open port **2377** in the security group for all the servers.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708604001310/b90a7673-fa49-43a1-8fe6-3e1a7bb07522.png align="center")

We can check the docker swarm status to check the connected worker nodes o manager nodes using "docker node ls"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708604200379/1123e0da-cccb-4b10-a136-e34adc9b7a46.png align="center")

Let's take an image from my repository to deploy the application on the docker swarm servers.

[https://hub.docker.com/repository/docker/sompandey/notes-app/general](https://hub.docker.com/repository/docker/sompandey/notes-app/general)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708605129916/a4357ed9-f9f2-411e-b484-8b81eb81d2ad.png align="center")

Create a service in the docker manager node server to install the application through the docker image from the docker hub.

```yaml
sudo docker service create --name notesApp --replicas 3 --publish 8000:8000 sompandey/notes-app:latest
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708687892492/d21be18d-a851-415c-8bc2-868f26ae9749.png align="center")

We can check the service that is created in the manager node server.

Also, check the docker logs in the worker node servers for running docker containers.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708605633384/b140cc42-f702-4031-aa38-dda3a78606ff.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708605648744/c9868b47-5274-4b16-a4c4-c679803ae60b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708605690342/c0f8ee1c-a6d6-4baf-80d9-3b384e14093b.png align="center")

Open the port 8000 which is required to run the application.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708687939751/77724a0c-7796-4a2d-9d0d-7f12d66bac3e.png align="center")

Let's check the web-app in both the swarm node servers.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708687980223/49200c1f-16e4-43c6-8151-e7d6c96b8712.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708688007734/10c6edef-4957-4e25-b717-c2986a83ab9f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708688036875/0e1a4e83-c461-4fdf-8226-6f2d2b797033.png align="center")

The application is running in both Master and Worker node.

---

Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.