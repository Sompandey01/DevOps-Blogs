---
title: "Getting Started with AWS Basics☁"
datePublished: Mon Aug 28 2023 02:59:34 GMT+0000 (Coordinated Universal Time)
cuid: clluajock000009l9atsl0v1y
slug: getting-started-with-aws-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693191498743/96693780-7f0b-4c42-a25b-61ce58a991b0.jpeg
tags: ec2, aws, devops, 90daysofdevops, trainwithshubham

---

Congratulations!!!! You have come so far. Don't let your excuses break your consistency. Let's begin our new Journey with Cloud☁. By this time you have created multiple EC2 instances, if not let's begin the journey:

## What is AWS ??

AWS or Amazon Web Services is a comprehensive, evolving cloud computing platform provided by [**Amazon.com**](http://Amazon.com). It offers a variety of infrastructure as a service products including:

* **EC2 (Elastic Compute Cloud)** - virtual servers in the cloud
    
* **S3 (Simple Storage Service)** - cloud storage
    
* **VPC (Virtual Private Cloud)** - virtual networking in the cloud
    
* **RDS (Relational Database Service)** - managed relational databases in the cloud
    
* **Lambda** - serverless compute
    
* **ElastiCache** - in-memory cache
    
* **CloudFront** - content delivery network (CDN)
    

With AWS, you pay only for the cloud resources you actually use. You have no upfront infrastructure costs and you can scale up or down your usage based on your requirements.

**Some key benefits of AWS are:**

1. **Scalability** - The ability to rapidly scale up or down your resources based on demand.
    
2. **Reliability** - AWS has a very high uptime and reliability record due to its multiple availability zones.
    
3. **Cost Efficiency** - You only pay for what you use, so it can be more cost efficient than maintaining your own infrastructure.
    
4. **Flexibility** - AWS offers a wide variety of services and configuration options to meet your needs.
    
5. **Speed** - You can quickly provision new resources as needed in minutes.
    

**Some common use cases for AWS are:**

* Hosting web applications
    
* Running big data workloads
    
* Scaling e-commerce sites during sales events
    
* Serving as a disaster recovery site
    

In summary, AWS provides a suite of cloud computing services that let you scale and adjust your infrastructure as needed, paying only for the resources you consume. It aims to reduce the cost and complexity of maintaining your own physical hardware and data centres.

## What is IAM ??

AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources. With IAM, you can centrally manage permissions that control which AWS resources users can access. You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources.

Get to know IAM more deeply [Click Here!!](https://www.youtube.com/watch?v=ORB4eY8EydA)

### Task 1: **Creating IAM User, Launching EC2 Instance, and Installing Jenkins and Docker via Shell Script**

* **Create an IAM user with username of your own wish and grant EC2 Access. Launch your Linux instance through the IAM user that you created now and install jenkins and docker on your machine via single Shell Script.**
    

**<mark>Step 1:</mark> Create IAM User**

Log in to your AWS Management Console and search for **IAM** Service.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693135070884/7ae33ffc-cbaf-48e4-ba68-42261bea37ab.png align="center")

Open it and Click on "Users" in the left navigation pane.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693135406015/e001ee6e-9994-432a-9684-1740fc33cf3c.png align="center")

Click "Add user."

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693135741342/c6df3671-6028-4295-bcff-371ce8a84424.png align="center")

Enter a username of your choice. Select **“Programmatic access”** and click **“Next”.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693135844047/966381d5-53e2-4c1b-bd69-f2b3840460b9.png align="center")

Select “Attach existing policies directly” and select the policy **“AmazonEC2FullAccess”.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693136114174/89c111a3-387f-4d01-becd-27d160039e58.png align="center")

Click “Next” until you reach the end, Review configurations then click **“Create user”.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693136176852/06435bed-07ca-4f1e-bc47-0e62fa78c049.png align="center")

Take note of the **username and password,** as you will need these to authenticate your IAM user when launching instances.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693136219903/a6a98a1f-7734-4591-b52d-d6c0b5a0e3d0.png align="center")

Note down **Account ID** for login credentials.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693136405943/57793bda-525b-4a06-b9aa-1534ff6a7454.png align="center")

**<mark>Step 2:</mark> Launch EC2 Instance**

Log in to the AWS Management Console with the IAM user credentials you just created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693137553905/ea59036b-871b-42e9-9070-172d8096b6b5.png align="center")

Go to the EC2 service and click on **“Launch instance”.**

Choose a **Linux** **Ubntu OS**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693137629141/15636b53-c61c-4a52-92bb-82f43c2b2d72.png align="center")

Select Instance type **“t2.micro”** Create new key pair and download it. I have used my previously created key pair.

Click on **“Launch Instance”.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693137686603/6dbbad5d-3237-4817-a5a3-0edd77533e0f.png align="center")

Select **the instance** and click on **connect**. Select the **Connect to instance** with **SSH client** and copy the **SSH link.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693137846179/372ebb15-890d-40e0-b8ac-8ffc48405d16.png align="center")

Go to th folder where you downloaded the **.pem key pair** file

Click on the top directory bar and type cmd in the bar then cmd will start.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693138220867/1a00e0ed-13d3-4104-9ea7-c03f0db8685e.png align="center")

In the cmd paste the copied **ssh url** to connect remote server.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693138389024/1ce8971a-8bf1-43f3-aa3c-6b158dcbd9bc.png align="center")

**<mark>Step 3:</mark> Shell Script for Jenkins and Docker Installation**

Create a shell script (e.g., `install_jenkins_docker.sh`) with the following content:

```bash
#!/bin/bash

#installing java
sudo apt update
java -version
sudo apt install default-jre
javac -version

#installing jenkins
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
            /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
            https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
                /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install jenkins
sudo systemctl start jenkins.service
sudo systemctl status jenkins

#installing docker
sudo apt-get update
sudo apt-get install docker.io -y
sudo systemctl start docker
sudo systemctl status docker
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693139100784/c3c74c07-f496-4c4a-af31-779fb19eb53c.png align="center")

**<mark>Step 4:</mark> Run the Shell Script**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693138727502/5d59c1b7-d18e-4010-b13f-efcbfac50863.png align="center")

Check **docker** and **Jenkins** version

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693139185576/8aaadee9-94ad-4ab4-bdfa-b1f18280bbd7.png align="center")

### Task 2: Creating an Avengers DevOps Team: IAM Users, Groups, and Policies

In this task you need to prepare a devops team of avengers. Create 3 IAM users of avengers and assign them in devops groups with IAM policy.

**<mark>Step 1:</mark> Create 3 IAM Users\\**

1. Log in to your AWS Management Console.
    
2. Navigate to the IAM service.
    
3. Click on "Users" in the left navigation pane.
    
4. Click "Add user."
    
5. Enter the usernames for the three IAM users (e.g., `ironman`, `thor`, `hawkeye`).
    
6. Select "Programmatic access" and "AWS Management Console access" as access types.
    
7. Choose "Autogenerated password" or "Custom password" to set initial passwords.
    
8. Uncheck the "User must create a new password at next sign-in" option (if you set a custom password).
    
9. Choose "Add user to group" and select the "DevOps" group (which we'll create in the next step).
    
10. Review and create the users.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693190424469/0f563b5c-68f4-434d-9c82-fbd21ea0055a.png align="center")

**<mark>Step 2:</mark> Create DevOps Group**

1. In the IAM console, click on "Groups" in the left navigation pane.
    
2. Click "Create new group."
    
3. Enter a group name (e.g., `Avengers`).
    
4. Click "Next Step."
    
5. Search for and attach relevant policies to the group. For DevOps access, you might attach policies like "AmazonEC2FullAccess," "AmazonS3FullAccess," "AmazonRDSFullAccess," etc.
    
6. Review and create the group.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693190539955/59ce62d0-4a5c-48f5-bd80-c13608f2e905.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693190892095/854c9073-661c-4e41-8348-31392dd2459e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693190921684/8ef318f1-7537-42cd-8b00-4cfa602a485c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693190949048/f00725c5-c376-40a7-ba3c-9a779ecd1448.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693191075607/c3908460-375f-4070-9796-b99c1c43d5cb.png align="center")

Now, **each user** is associated with a specific DevOps group with the necessary **IAM policies**. You can add more users by clicking **“Add users”.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693191326247/b2a66853-4937-4f1a-97ca-77b6f16da963.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693191338689/ac92dbd8-53c6-4136-9e41-dc0d37b5a562.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.