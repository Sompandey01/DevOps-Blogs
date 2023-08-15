---
title: "Jenkins Project"
datePublished: Tue Aug 15 2023 04:51:02 GMT+0000 (Coordinated Universal Time)
cuid: cllbtsxte000308l47zl91lzr
slug: jenkins-project
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692074985849/9da87220-fa59-4f96-b236-0038488b2933.png
tags: devops, jenkins, jenkins-devops, 90daysofdevops, trainwithshubham

---

## Day 28 Task: Jenkins Agents

# Jenkins Master (Server)

Jenkins’s server or master node holds all key configurations. Jenkins master server is like a control server that orchestrates all the workflow defined in the pipelines. For example, scheduling a job, monitoring the jobs, etc.

# Jenkins Agent

An agent is typically a machine or container that connects to a Jenkins master and this agent that actually execute all the steps mentioned in a Job. When you create a Jenkins job, you have to assign an agent to it. Every agent has a label as a unique identifier.

When you trigger a Jenkins job from the master, the actual execution happens on the agent node that is configured in the job.

A single, monolithic Jenkins installation can work great for a small team with a relatively small number of projects. As your needs grow, however, it often becomes necessary to scale up. Jenkins provides a way to do this called “master to agent connection.” Instead of serving the Jenkins UI and running build jobs all on a single system, you can provide Jenkins with agents to handle the execution of jobs while the master serves the Jenkins UI and acts as a control node.

[![](https://user-images.githubusercontent.com/115981550/215276859-fa140ab7-e905-41c9-8ae2-1eef577c5e72.png align="center")](https://user-images.githubusercontent.com/115981550/215276859-fa140ab7-e905-41c9-8ae2-1eef577c5e72.png)

## Pre-requisites

Let’s say we’re starting with a fresh Ubuntu 22.04 Linux installation. To get an agent working make sure you install Java ( same version as jenkins master server ) and Docker on it.

`Note:- While creating an agent, be sure to separate rights, permissions, and ownership for jenkins users.`

### **Deploy web app using Jenkins master and worker node.**

Here we will deploy a web app through Jenkins master to Jenkins worker node.

<mark>Step-1:</mark> Create 2 EC2 instances **Jenkins-master** & **Jenkins-agent.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692010307807/26268075-15ea-42c2-b068-cb604a2e689c.png align="center")

<mark>Step-2:</mark> Generate SSH keys on “Jenkins-master” by running “ssh-keygen”

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692010663721/6a078e68-f108-4024-8d1f-016f948a891b.png align="center")

<mark>Step-3:</mark> Now go to “.ssh” folder and there will be public and private key in Jenkins-server.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692010869001/81375092-f6dd-4854-9360-1ab38e2ea9b3.png align="center")

<mark>Step-4:</mark>  Add public key from “Jenkins-master” to “Jenkins-agent” under location “.ssh/authorized\_keys”

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692011005529/b29727dc-c0a1-4248-a5f2-29b81495ebe7.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692011200086/ec7770bb-c26c-4fc1-a324-7b7cbc8d3f7b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692011169064/6f5ceb12-69c3-4afa-be2c-2efa3d873a16.png align="center")

<mark>Step-5:</mark> Now, go to the Jenkins dashboard, click on “Manage Jenkins” and click on "Nodes and cloud".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692012762998/ff42ab51-eab6-4380-825d-7adbae93716c.png align="center")

<mark>Step-6:</mark>  Now, click on “+ New Node”

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692012886066/a4418062-d4d7-4638-a4df-488f2df64a68.png align="center")

<mark>Step-7:</mark> Add details of your second node, accordingly.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692069682388/85f4a87b-4b2b-43f0-93e9-7bef6f8d574f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692069701394/bfac7c33-a12f-4230-9284-45c85087dc2a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692069765469/e1100a0c-da6d-4aa4-9131-c0947328fd4a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692069780547/8cec3269-1340-4fd5-a991-2eb154745ff0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692069812810/7a70fa1b-bfed-44dd-a44d-cbd3e23f75f8.png align="center")

<mark>Step-8:</mark>   Now click on “Ok”, and the node will be connected and online.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692069891615/80897e55-607d-497c-b127-07ac800ea5c0.png align="center")

<mark>Step-9:</mark> Now, go to configurations in your task or project scheduled in Jenkins, and add the Label as same with the name of Node.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692073730699/f31138b6-6aad-4db6-bf63-1fb3ad66eccc.png align="center")

<mark>Step-10:</mark> Click on Save, and your project will be tied to Agent-01 and then build your project.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692073800864/74e1a6b0-2956-4d9a-bf62-1755a88f8e64.png align="center")

<mark>Step-11:</mark> Now, the web app will be up and running on “Jenkins-agent” and can be accessible via:

&lt;ip of Jenkins agent:8000&gt;

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692074291807/0d9920ae-c9f2-45f4-bd01-17ee056b2a21.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/) for the latest updates and discussions.