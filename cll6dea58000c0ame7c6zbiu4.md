---
title: "Day 25: Complete Jenkins CI/CD Project - Continued with Documentation"
datePublished: Fri Aug 11 2023 09:12:53 GMT+0000 (Coordinated Universal Time)
cuid: cll6dea58000c0ame7c6zbiu4
slug: day-25-complete-jenkins-cicd-project-continued-with-documentation
tags: devops, jenkins, ci-cd, 90daysofdevops, trainwithshubham

---

## Task-01: Setting Up CI/CD with Jenkins and GitHub Webhooks: A Comprehensive Guide

* Document the process from cloning the repository to adding webhooks, and Deployment, etc. as a README , go through [this example](https://github.com/LondheShubham153/fynd-my-movie/blob/master/README.md)
    
* A well written readme file will help others to understand your project and you will understand how to use the project again without any problems.
    

### Introduction

Welcome to the comprehensive guide for setting up Continuous Integration and Continuous Deployment (CI/CD) using Jenkins and GitHub Webhooks. This README provides step-by-step instructions, from cloning the repository to configuring webhooks and deployment, ensuring a seamless and automated development workflow.

### Setting Up Jenkins

1. Install and configure Jenkins on your server. Ensure Jenkins is up and running.
    
2. Access the Jenkins dashboard using your web browser.
    
3. Create a new Jenkins job for your project:
    
    * Choose "New Item" from the dashboard.
        
    * Provide a name for your job and select the appropriate project type (e.g., Freestyle project).
        
    * Configure the source code management settings, typically using Git.
        
4. Install any necessary plugins to enable GitHub integration and Docker support, depending on your project's requirements.
    

### Configuring GitHub Webhooks

1. In your GitHub repository, navigate to "Settings" &gt; "Webhooks".
    
2. Click "Add webhook":
    

* Enter the Payload URL, which should be your Jenkins job's URL followed by "/github-webhook/" (e.g., [http://your-jenkins-server/job/your-job-name/github-webhook/](http://your-jenkins-server/job/your-job-name/github-webhook/)).
    
* Choose the content type as "application/json".
    
* Select the events that should trigger the webhook (e.g., "Push events").
    
* Optionally, add a secret for added security.
    

1. Save the webhook configuration.
    

### Install Docker and Docker Compose

1. Install Docker on your Jenkins server by following the official documentation.
    
2. Install Docker Compose using the official installation guide.
    

### Deployment Process

1. Configure your Jenkins job:
    

* In the job configuration, specify the GitHub repository URL.
    
* Set up build triggers to use the GitHub webhook you just created.
    

1. Set up your deployment steps in the Jenkins job:
    

* Depending on your project, you may use Docker Compose, scripts, or other tools.
    
* Ensure that the job builds, tests, and deploys your application.
    

1. When code changes are pushed to your GitHub repository, the webhook triggers your Jenkins job automatically.
    

### Troubleshooting

If you encounter any issues during setup or deployment, refer to the troubleshooting section in this repository or seek help from the community.

### Contributing

Contributions are welcome! If you find any improvements or fixes, please submit a pull request. Follow the project's guidelines for contributing.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691742513381/875072cb-711f-4475-92ec-163e9ba6ae4b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691742543152/3db2470f-d4f9-44f3-8cae-e08ab6759f87.png align="center")

## Task-02: Goal Planner

* Also, it's important to keep smaller goals, as it's a small task, think of a small Goal you can accomplish.
    
* Write about it using [**this template**](https://www.linkedin.com/posts/shubhamlondhe1996_taking-resolutions-and-having-goals-for-an-activity-7023858409762373632-s2J8?utm_source=share&utm_medium=member_desktop)
    
* Have small goals and strategies to achieve them, and also have a small reward for yourself.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691744542610/3e56e151-8da9-4368-9c2b-55a57b917fc5.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/) for the latest updates and discussions.