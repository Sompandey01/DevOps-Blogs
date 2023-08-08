---
title: "Getting Started with Jenkins 😃"
datePublished: Tue Aug 08 2023 14:27:06 GMT+0000 (Coordinated Universal Time)
cuid: cll2easw1000509l8e6t9go1u
slug: getting-started-with-jenkins
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691504745216/a8681996-0b0e-4db4-817a-081925edf8a6.png
tags: devops, jenkins, jenkins-devops, 90daysofdevops, trainwithshubham

---

## What is Jenkins?

* Jenkins is an open source continuous integration-continuous delivery and deployment (CI/CD) automation software DevOps tool written in the Java programming language. It is used to implement CI/CD workflows, called pipelines.
    
* Jenkins is a tool that is used for automation, and it is an open-source server that allows all the developers to build, test and deploy software. It works or runs on java as it is written in java. By using Jenkins we can make a continuous integration of projects(jobs) or end-to-endpoint automation.
    
* Jenkins achieves Continuous Integration with the help of plugins. Plugins allow the integration of Various DevOps stages. If you want to integrate a particular tool, you need to install the plugins for that tool. For example Git, Maven 2 project, Amazon EC2, HTML publisher etc.
    

### Task-1: **What you understood in Jenkin, write a small article in your own words**

Jenkins is an open-source tool written in Java that runs on Windows, macOS and other Unix- like systems. It is free to use, it automates the entire software development life cycle. It helps us to enable the CI/CD process which compiles, builds and test code for us.

### Task-2: **Create a freestyle pipeline to print "Hello World!!**

**Step 1: Install Jenkins**

If you haven't already, you need to install and set up Jenkins on your system. You can follow the official Jenkins installation guide for your operating system: [**Jenkins Installation**](https://www.jenkins.io/doc/book/installing/)

**Step 2: Create a New Freestyle Project**

Open your Jenkins dashboard after installation and click on "Create a job" on the right-hand side menu.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691503539668/d0ea315b-a3cb-4ca0-bb27-dae865104341.png align="center")

Enter a name for your project, e.g., "HelloWorldPipeline" and Select "Freestyle project" and click "OK".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691503549888/9a75dcca-7ad7-4fd8-80cc-afdeb699cc82.png align="center")

Add a simple description

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691503379541/a7e4da09-9c68-45c7-b23e-331ebcc89d72.png align="center")

**Step 3: Configure the Freestyle Project**

In the project configuration page, scroll down to the "Build" section. Click on the "Add build step" dropdown and select "Execute shell" (assuming you're using a Unix-like system) or "Execute Windows batch command" (for Windows).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691503735540/02d9119a-2392-464f-b2a4-5c4eaf0bd74a.png align="center")

In the command box, simply enter the command to print "Hello World!!". For Unix-like systems, you can use:

Save your configuration by clicking "Save" at the bottom of the page.

**Step 4: Run the Pipeline**

Go back to your Jenkins dashboard and find your "HelloWorldPipeline" project and click on it and then click on "Build Now" to manually trigger a build.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691504215662/cf6c2569-f088-416f-84dc-33d0a453a4a9.png align="center")

Now, Click on #1

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691504274606/ef49e50a-9d41-46a8-940a-21439d38c00b.png align="center")

Now, Click on "Console Output" It should display "Hello World!!"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691504467284/c8970aa8-e550-4a5d-9315-938a4dfec8c5.png align="center")

Congratulations! You've created a simple Freestyle Jenkins pipeline that prints "Hello World!!"

I hope you like my blog..!!

Stay Connected with me for more interesting articles on DevOps, if you like my blog follow me on **Hashnode** and **Linkedin** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)