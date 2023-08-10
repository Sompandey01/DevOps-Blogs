---
title: "Day 24: Complete Jenkins CI/CD Project"
datePublished: Thu Aug 10 2023 15:09:57 GMT+0000 (Coordinated Universal Time)
cuid: cll5apmbn000f0al52eljchvc
slug: day-24-complete-jenkins-cicd-project
tags: devops, jenkins, 90daysofdevops, trainwithshubham, tws

---

Let's make a beautiful CI/CD Pipeline for your Node JS Application 😍

### **Task-01: Setting Up Jenkins with GitHub for CI/CD using GiHub webhooks**

**Step-1:** Fork this repository: [**https://github.com/LondheShubham153/node-todo-cicd.git**](https://github.com/LondheShubham153/node-todo-cicd.git)

**Step-2:** Create a connection to your Jenkins job and your GitHub Repository via GitHub Integration using git webhook. Add the git url of your project:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691668963346/10180d2e-e45a-4c55-b72f-fdf4d64a55e9.png align="center")

Now, Select "**GitHub hook trigger for GITScm polling"** in Jenkins:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691669340802/c65c9961-fdd4-4238-8ede-d6fd72e7bc12.png align="center")

Add the build steps

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691670103811/12b0a559-e3bb-481f-ad87-48935a4dec1d.png align="center")

**Configure GitHub Webhook**

1. Open your GitHub repository in your browser.
    
2. Go to the repository's "Settings" tab.
    
3. Select "Webhooks" from the left-hand menu.
    
4. Click on the "Add webhook" button.
    
5. In the "Payload URL" field, enter the Jenkins job URL you noted down earlier.
    
6. For "Content type," choose "application/json."
    
7. Select the events that you want to trigger the webhook. The most common event is "push," which triggers when code is pushed to the repository.
    
8. Click "Add webhook" to save the webhook configuration.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691670327211/91c5743d-c36c-4ba4-9245-6afa05fdb735.png align="center")

To test the webhook, make a small code change in your GitHub repository and commit it:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691670632762/e7ed1c4f-4516-4cfa-a408-bb7236999f6d.png align="center")

Now, whenever you push code to your GitHub repository, the webhook will send a request to the Jenkins job's URL. This will trigger the Jenkins job automatically, running your specified build and deployment steps.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691670736632/16d7835c-f61b-4e6c-9fd3-3ac73d55a4fb.png align="center")

Checking on port 8000

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691670816710/20c65495-9777-4b77-9c43-d0b15dbe465c.png align="center")

### **Task-02: Seamless Application Deployment with Webhooks and Docker Compose**

In the Execute shell run the application using Docker compose

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691673217404/09f5db14-5e88-424a-a08a-2fb942822fc6.png align="center")

Make a Docker Compose file for this Project

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691673251916/0cacd2c2-8e10-48ee-8190-cbc4f78fa32e.png align="center")

To test the webhook, make a small code change in your GitHub repository and commit it

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691680052778/e32accfe-2d8d-414b-9589-6b8c8f59fcda.png align="center")

It's working perfectly.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691679993671/72d393f2-0184-4f50-bed7-728735c142ec.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/) for the latest updates and discussions.