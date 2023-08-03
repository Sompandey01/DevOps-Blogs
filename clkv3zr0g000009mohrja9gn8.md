---
title: "Day 17: Docker Project for DevOps Engineers."
datePublished: Thu Aug 03 2023 12:04:11 GMT+0000 (Coordinated Universal Time)
cuid: clkv3zr0g000009mohrja9gn8
slug: day-17-docker-project-for-devops-engineers
tags: docker, opensource, devops, 90daysofdevops, trainwithshubham

---

## Dockerfile

Docker is a tool that makes it easy to run applications in containers. Containers are like small packages that hold everything an application needs to run. To create these containers, developers use something called a Dockerfile.

A Dockerfile is like a set of instructions for making a container. It tells Docker what base image to use, what commands to run, and what files to include. For example, if you were making a container for a website, the Dockerfile might tell Docker to use an official web server image, copy the files for your website into the container, and start the web server when the container starts.

## Dockerfile Commands:

Here's a more concise and specific list of common Dockerfile commands:

1. `FROM`: Specifies the base image to build upon.
    
2. `COPY` or `ADD`: Copies files from the host machine to the image.
    
3. `RUN`: Executes commands during the image build process.
    
4. `CMD`: Sets the default command to run when the container starts.
    
5. `ENTRYPOINT`: Sets the main executable for the container.
    
6. `ENV`: Sets environment variables inside the container.
    
7. `EXPOSE`: Informs Docker about the ports the container will listen on.
    
8. `VOLUME`: Creates a mount point for data persistence.
    
9. `WORKDIR`: Sets the working directory for the image.
    
10. `USER`: Specifies the user context for the container.
    

### Task 1: Create a Dockerfile for a simple web application (e.g. a Node.js or Python app)

We have a project with Django here, let's clone it

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691064143201/493d8141-0ad5-4536-9793-a9c643bd0f27.png align="center")

Let's make the dockerfile:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691061690161/04a96257-2df1-4f2c-9a7f-edea8f78f5c3.png align="center")

### Task 2: Build the image using the Dockerfile and run the container

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691061816866/7d290fcc-9c60-4eb7-8f58-a6f83da2c1f3.png align="center")

To check whether the image is build or not simply use:

```plaintext
docker images
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691061999550/fffc681a-2a1f-4131-bbf2-faa650674b1f.png align="center")

### Task 3: Verify that the application is working as expected by accessing it in a web browser

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691062150581/389368e8-4351-4352-81a5-3b99a70ed8cb.png align="center")

### Task 4: Push the image to a public or private repository (e.g. Docker Hub )

Create a repository on Docker Hub

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691063479167/b7660c03-7b78-4643-b2c6-b1c17a3ee55a.png align="center")

Login into your docker registry using `docker login` command:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691063592116/1f6e0842-5f7e-4f0d-af74-bf98d9263c3e.png align="center")

Tag the image according to the repository you have created:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691063518959/6e0a2a9c-e49c-49f9-a537-d0e7f81f4f5c.png align="center")

Push the image:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691063546265/408656e7-1ac4-47e6-95aa-cba7e5f5a7e8.png align="center")

Check on the docker hub website if the image is uploaded or not.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691063340910/7c34a7fc-dd11-406f-a150-3215944dd256.png align="center")

I hope you like my blog..!!

Stay Connected with me for more interesting articles on DevOps, if you like my blog follow me on **Hashnode** and **Linkedin** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)