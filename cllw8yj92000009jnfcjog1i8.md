---
title: "Exploring AWS Fundamentals: Automation, User Data, and IAM Basics"
datePublished: Tue Aug 29 2023 11:50:40 GMT+0000 (Coordinated Universal Time)
cuid: cllw8yj92000009jnfcjog1i8
slug: exploring-aws-fundamentals-automation-user-data-and-iam-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693307495670/064e5e44-5b97-4927-85e7-8c96ccf0a260.png
tags: cloud, aws, devops, 90daysofdevops, trainwithshubham

---

By this time you have created multiple EC2 instances, and post installation manually installed applications like Jenkins, docker etc. Now let's switch to little automation part. Sounds interesting??🤯

## AWS:

Amazon Web Services is one of the most popular Cloud Provider that has free tier too for students and Cloud enthutiasts for their Handson while learning (Create your free account today to explore more on it).

## User Data in AWS:

* When you launch an instance in Amazon EC2, you have the option of passing user data to the instance that can be used to perform common automated configuration tasks and even run scripts after the instance starts. You can pass two types of user data to Amazon EC2: shell scripts and cloud-init directives.
    
* You can also pass this data into the launch instance wizard as plain text, as a file (this is useful for launching instances using the command line tools), or as base64-encoded text (for API calls).
    
* This will save time and manual effort everytime you launch an instance and want to install any application on it like apache, docker, Jenkins etc.
    

## IAM:

AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources. With IAM, you can centrally manage permissions that control which AWS resources users can access. You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources.

### Task 1: **Launching EC2 Instance with Pre-installed Jenkins: Access and Verification**

* **Launch EC2 instance with already installed Jenkins on it. Once server shows up in console, hit the IP address in browser and you Jenkins page should be visible.**
    
* **Take screenshot of Userdata and Jenkins page, this will verify the task completion.**
    

1. Log in to your AWS Management Console.
    
2. Navigate to the EC2 Dashboard.
    
3. Click "Launch Instances" to start the process and choose Ubuntu image.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693307880401/c99806eb-dec1-4b90-b626-e74446b29a2f.png align="center")

1. Configure your instance details. Provide the suitable key pairs and security groups.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693307941672/7747268c-f55e-429d-8339-a081113dcdef.png align="center")

1. Select the advanced settings in the instance creation page.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693308027265/50688ae4-e32a-4d72-9b33-3873304b59c3.png align="center")

1. Navigate to User-data section and write a shell script to install Jenkins on the server.
    

```bash
#!/bin/bash
 sudo apt update
 sudo apt install openjdk-11-jre -y

 curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
   /usr/share/keyrings/jenkins-keyring.asc > /dev/null
 echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
   https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
   /etc/apt/sources.list.d/jenkins.list > /dev/null
 sudo apt-get update
 sudo apt-get install jenkins -y

  sudo systemctl enable jenkins
  sudo systemctl start jenkins
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693308283136/86a01507-fa98-42d6-b0f6-32ca9994d114.png align="center")

1. Include the port 8080 which is the Jenkins default port in the security group of the server.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693308204691/28fa7391-c3fa-4256-a201-ff44b334c8f5.png align="center")

1. Start the EC2 instance and using the public IP access the URL through port 8080.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693308432316/affae1b3-7b86-468e-9498-445474192cf3.png align="center")

### Task 2: **Exploring IAM Roles and Permissions in AWS**

**IAM Users:**

* IAM Users are individual AWS accounts within your AWS account.
    
* Each IAM user has their own username and password which is used to access AWS services.
    
* You can attach policies to IAM users to control what actions they can perform.
    
* IAM users are the most granular as you can attach specific policies to each individual user.
    

**IAM Groups:**

* IAM Groups allow you to assign policies to a group of IAM users.
    
* Rather than attaching policies to each individual user, you can attach them to a group and then add users to that group.
    
* This helps manage policies for multiple users in an organized way.
    
* Groups make it easier to manage permissions for many users at once.
    

**IAM Roles:**

* IAM Roles are similar to groups but are meant to be assigned to AWS resources instead of individual users.
    
* Roles allow you to assign permissions to resources like EC2 instances or Lambda functions, without needing individual credentials.
    
* When a resource assumes a role, it gets temporary security credentials that it can use to make API calls.
    
* This improves security since the temporary credentials are limited in scope and duration.
    
* Roles are useful for granting least privilege access to resources.
    

**In summary:**

* IAM Users represent individual humans who need access to your AWS account.
    
* IAM Groups allow you to organize users and assign policies to multiple users at once.
    
* IAM Roles are meant to be assigned to AWS resources (EC2 instances, Lambda functions, etc.) to assign them permissions.
    

**The hierarchy is:**

Roles &gt; Groups &gt; Users

Roles have the broadest scope of access, while Users have the most granular, specific access.

### **Creating IAM Roles: DevOps-User, Test-User, and Admin**

1. Log in to your AWS Management Console.
    
2. Navigate to the IAM service.
    
3. Click on "Roles" in the left navigation pane.
    
4. Click "Create role."
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693309047072/8bb589fd-2f57-4e5f-93a2-06d21be322ad.png align="center")

1. Choose the service that will use the role (e.g., EC2, Lambda, etc.).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693309128645/2662aee7-aa06-411c-ba29-16455fe8a41b.png align="center")

1. Select the appropriate permissions policies for the role. You can choose from existing policies or create a custom policy.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693309213884/639369bc-185d-4df3-8bc8-f76a296363a8.png align="center")

1. Enter a name for the role and click “**Create role**”.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693309288821/be934a90-94ce-42d7-b871-89525c90a82b.png align="center")

1. Repeat the above steps for each role you want to create: Test-User and Admin.
    
2. Create a “**Test-Users”** Role.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693309610698/861375af-6a4f-44c6-be52-a99510fc6a83.png align="center")

1. Create a “**Admin-User”** Role.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693309559355/e7e9a3a4-b6b5-48a4-9040-52acaa95be9b.png align="center")

1. Once the roles are created, you can assign them to individual IAM users or groups as needed, and control their access to AWS resources.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693309739451/34658e9c-70c5-4a06-ac81-026796a5421d.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.