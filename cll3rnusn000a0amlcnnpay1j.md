---
title: "Day 23: Jenkins Freestyle Project for DevOps Engineers."
datePublished: Wed Aug 09 2023 13:28:56 GMT+0000 (Coordinated Universal Time)
cuid: cll3rnusn000a0amlcnnpay1j
slug: day-23-jenkins-freestyle-project-for-devops-engineers
tags: devops, jenkins, 90daysofdevops, trainwithshubham, tws

---

## What is CI/CD?

* CI or Continuous Integration is the practice of automating the integration of code changes from multiple developers into a single codebase. It is a software development practice where the developers commit their work frequently into the central code repository (Github or Stash). Then there are automated tools that build the newly committed code and do a code review, etc as required upon integration. The key goals of Continuous Integration are to find and address bugs quicker, make the process of integrating code across a team of developers easier, improve software quality and reduce the time it takes to release new feature updates.
    
* CD or Continuous Delivery is carried out after Continuous Integration to make sure that we can release new changes to our customers quickly in an error-free way. This includes running integration and regression tests in the staging area (similar to the production environment) so that the final release is not broken in production. It ensures to automate the release process so that we have a release-ready product at all times and we can deploy our application at any point in time.
    

## What Is a Build Job?

A Jenkins build job contains the configuration for automating a specific task or step in the application building process. These tasks include gathering dependencies, compiling, archiving, or transforming code, and testing and deploying code in different environments.

Jenkins supports several types of build jobs, such as freestyle projects, pipelines, multi-configuration projects, folders, multibranch pipelines, and organization folders.

## What is Freestyle Projects ?? 🤔

A freestyle project in Jenkins is a type of project that allows you to build, test, and deploy software using a variety of different options and configurations. Here are a few tasks that you could complete when working with a freestyle project in Jenkins:

### Task-01: Create an agent for your app. ( which you deployed from docker in the earlier task)

Click on "Set up an agent"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691557754545/dc6f03f7-c702-4d10-bd88-589cc186a23a.png align="center")

Now, Give a node name and select "Permanent Agent"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691557890713/ac3bf49f-7e0f-4383-b582-a3ff3af3b637.png align="center")

Add details

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691558042039/16723060-4be2-4d9c-af32-d1d806325f37.png align="center")

Select "Use WebSocket" and Save

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691558083198/269c6daa-9efb-4964-9600-ca0d38182122.png align="center")

Now, Your node is ready

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691558242677/60fcb7bf-f383-4e31-8ea5-d53c9e89631d.png align="center")

### Create a new Jenkins freestyle project for your app.

Open your Jenkins dashboard and click on "Create a job" on the right-hand side menu. Enter a name for your project, e.g., "Todo-dev" and Select "Freestyle project" and click "OK".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691558999488/b1f6b2c8-c55a-4e10-87c1-67b6588c0dd8.png align="center")

### In the "Build" section of the project, add a build step to run the "docker build" command to build the image for the container. Add a second step to run the "docker run" command to start a container.

Add the GitHub path where your docker file is present.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691580859570/b381de5d-fca6-40aa-bb01-2e901bdfd480.png align="center")

In "Source Code Management" Click on "Git" and add your repository link and branch

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691583216744/851856f0-f1c1-48cf-8bc6-f3640cb92f38.png align="center")

Select "Execute shell" and add commands to execute and save it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691560311309/9cc852f8-878c-48d1-afa6-582b4a000f49.png align="center")

Now click on "Build Now" then click on #1 and check "Console Output"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691583164814/7ab5d6f6-7404-4618-9d82-5a864c27eca5.png align="center")

Use `docker ps` command to check whether the container is running or not

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691583396534/94eabf99-2359-4382-9121-18c6a9963e24.png align="center")

Checking port 8000

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691583612856/ed2c2813-1636-4944-b606-9c9582241fe3.png align="center")

### Task-02: Create Jenkins project to run "docker-compose up -d" command to start the multiple containers defined in the compose file

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691583827458/d02af1c2-68b4-4f72-9743-ca072b39356e.png align="center")

Again, add a GitHub path where your file is present

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691585641955/9f09bf89-67d5-471f-b203-c5b736eac2ea.png align="center")

Add this command to start the container

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691587421252/af69bdaa-f1fc-40c8-8489-0d697f9d2b99.png align="center")

Successfully built.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691586741025/87f835ea-feea-4360-990a-cc8ef4af0b8e.png align="center")

Use `docker ps` command to check

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691586942412/8586ce77-f9b6-40b4-a5b3-0317450e9006.png align="center")

The website is working on port 8001

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691587037836/5c41a811-cdd0-42ac-9fb9-424989e20aec.png align="center")

### Set up a cleanup step in the Jenkins project to run the "docker-compose down" command to stop and remove the containers defined in the compose file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691587258855/185d8635-c468-453c-b5d4-7a0509d8b96f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691587297415/ea7a3b1a-2ce1-42dc-aa0c-c44fe3aa2ca5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691587372360/d4ca8fbc-be6f-4eca-84e9-1082e98feed3.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/) for the latest updates and discussions.