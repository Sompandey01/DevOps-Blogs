---
title: "Your CI/CD pipeline on AWS - Part-1 🚀 ☁"
datePublished: Sun Sep 24 2023 11:44:50 GMT+0000 (Coordinated Universal Time)
cuid: clmxe75ut000g0amphugg7ei9
slug: your-cicd-pipeline-on-aws-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695555838689/df7facc5-69b8-4eb2-9c34-1d3342c5e240.png
tags: cloud, aws, devops, 90daysofdevops, trainwithshubham

---

What if I tell you, in next 4 days, you'll be making a CI/CD pipeline on AWS with these tools.

* CodeCommit
    
* CodeBuild
    
* CodeDeploy
    
* CodePipeline
    
* S3
    

## What is CodeCommit?

CodeCommit is a managed source control service by AWS that allows users to store, manage, and version their source code and artefacts securely and at scale. It supports Git, integrates with other AWS services, enables collaboration through branch and merge workflows, and provides audit logs and compliance reports to meet regulatory requirements and track changes. Overall, CodeCommit provides developers with a reliable and efficient way to manage their codebase and set up a CI/CD pipeline for their software development projects.

## Task 1: Configuring GitCredentials for CodeCommit and Cloning a Repository

**\- Set up a code repository on CodeCommit and clone it on your local.**

**\- You need to set up GitCredentials in your AWS IAM.**

**\- Use those credentials in your local and then clone the repository from CodeCommit.**

* Login and Open the AWS Management Console and navigate to the CodeCommit service.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695535855537/c9a1731b-697a-4a7a-b9dc-5a4cdb625846.png align="center")

* Create a repository by clicking on the “**Create repository**” button.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695535972743/b367bc10-6ba9-49a1-a85f-4bd4b0120352.png align="center")

* Enter a name for your repository give description, default branch name, and repository visibility.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695536057141/9f7b536e-9640-49d8-800a-9b320a64d304.png align="center")

* demo-repo Successfully Created.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695536103921/6f372817-d72e-42d1-8211-90473c9b9f84.png align="center")

**Now,** **Configure Git Credentials in AWS IAM:**

* Go to the IAM console.
    
* Click on Users in the left-hand menu, and then click on your username.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695536319224/5923216e-c9c8-4876-8e7c-5125098d679e.png align="center")

* In permissions, Add permissions for git access for IAM user.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695536390794/0aebceb4-a4cc-4a7c-a5d1-03f2595f86f1.png align="center")

* Search and select “**AWSCodeCommitFullAccess**” and “**AWSCodeCommitPowerUser**”.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695536727896/a44815b0-4a8a-4812-b953-e6fb4f8e4edc.png align="center")

* Now, In **Security credentials** section scroll down to the “**HTTPS Git credentials for AWS CodeCommit**”, click on “**Generate credentials**”.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695536883291/5bcb8af8-acd4-4abf-84ba-fffff9d92165.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695536931053/14c209ac-f152-486f-b9d5-0267c2897d80.png align="center")

* Now, Navigate to the repository we created earlier and let's add a file there.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695537621742/aeea7fd1-42f8-46f1-926d-932061c019b6.png align="center")

* Click on "Create file" and give the info.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695537496413/71c31b5c-0dc3-4063-bedd-2f89612f543f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695537568221/22214cb3-c4e3-4457-a54f-eb3455cef824.png align="center")

* Copy the repository url.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695537674089/52a5a87c-37e6-4ab9-a5ed-6a216a1e47a4.png align="center")

* Open the server terminal and use the git clone command to clone the repository from CodeCommit to the server.
    

```bash
git clone <your-codecommit-repo-clone-https-url>
```

* You will be prompted to enter your Git credentials. Enter the username and password that you downloaded earlier.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695538121664/c5d357d1-0ef7-4ce5-980f-ad3670c32ec8.png align="center")

## Task 2: Adding and Pushing Changes to a CodeCommit Repository

**\- Add a new file from local and commit to your local branch**

* Create a new file.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695554453211/5fbb65c3-de6a-4d98-b817-b210739989b3.png align="center")

* Check status using command “git status”.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695554499960/63e6be24-a85f-4f5f-a2cb-8287dc7f1eb7.png align="center")

* Now, Add the file using `git add` command and commit the changes.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695554677331/70661fd9-4eed-4242-bc4e-45edca8089fe.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695554687326/29948668-f6cd-46c3-a695-6a0f9a46b1a4.png align="center")

**\- Push the local changes to CodeCommit repository.**

* To push the local changes to CodeCommit repository simply use the command given below:
    

```bash
git push origin <branch name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695554943809/b02dce3f-74b7-4321-b560-359d6486926b.png align="center")

* Verify that the changes have been pushed to the CodeCommit repository:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695554979349/863ace96-ab96-40e0-af43-ad409dd20c4b.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.