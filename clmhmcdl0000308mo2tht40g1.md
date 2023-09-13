---
title: "Test Knowledge on aws 💻"
datePublished: Wed Sep 13 2023 10:48:31 GMT+0000 (Coordinated Universal Time)
cuid: clmhmcdl0000308mo2tht40g1
slug: test-knowledge-on-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694601963305/c69a5d6f-212e-49c7-84d3-f4f9bb823ba9.png
tags: cloud, aws, devops, 90daysofdevops, trainwithshubham

---

Today, we will be test the aws knowledge on services in AWS, as part of the 90 Days of DevOps Challenge.

## Task-01: Deploy, Monitor, and Troubleshoot a Web Server on AWS EC2

* **Launch an EC2 instance using the AWS Management Console and connect to it using SSH.**
    
* **Install a web server on the EC2 instance and deploy a simple web application.**
    
* **Monitor the EC2 instance using Amazon CloudWatch and troubleshoot any issues that arise**.
    

**Launch EC2 Instance:**

* Access the AWS Management Console.
    
* Navigate to the EC2 service.
    
* Launch a new EC2 instance as we have seen in our previous blogs.
    
* Select free tier t2 micro.
    
* Configure the instance details, such as instance type, VPC, subnet, and security group settings.
    
* Create or use an existing key pair to enable SSH access to the instance.
    
* Launch the instance.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694595410327/61179e82-90ed-4221-a4d3-9ac72df1d1ed.png align="center")

**Connect to EC2 Instance:**

* Once the instance is running, connect to it using SSH from your local machine.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694595495709/7150ddec-2987-4112-a882-f0f2a797b988.png align="center")

**Install Web Server:**

* Update the package manager on the EC2 instance: `sudo apt update -y`
    
* Install the Apache Web Server on the EC2 instance: `sudo apt install apache2 -y`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694595758748/62530bc7-71da-4353-8b29-b1ec1b837bb7.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694596575956/896be396-92a4-42c1-a376-61a46749a689.png align="center")

**Deploy a Simple Web Application:**

* Edit the index.html file using vi or nano editor
    
* Insert the basic web page html css code into index file
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694597758016/874d1843-f6d9-4d57-909f-40fbdea89449.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694597767351/a42750dc-da71-4d9b-b5ff-c3f81fd6a1f7.png align="center")

**Monitor EC2 Instance with Amazon CloudWatch:**

* Go to the AWS CloudWatch service in the AWS Management Console.
    
* Click on "**Create alarm"**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694597978592/7cb21297-d8b1-4e0e-bb53-2cb790b0cdb8.png align="center")

* On **Specify metric and conditions** page click on **Select metric.**
    
* Select the EC2 metric to monitor, such as CPU utilization or network traffic.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694598180795/337ebab6-f041-4ee9-bb73-d9314cd425cc.png align="center")

* Configure conditions and click “Next” button.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694598263369/3520a533-bb9e-44c1-bf11-f0fdf3a42224.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694598290722/eb2c5766-ceb4-4148-a239-fa8ed290616a.png align="center")

* Set up alarm parameters of notification settings.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694598397320/b4854240-ed17-4c1b-96bc-989a90a2295c.png align="center")

* Give name for alarm and click on next then preview the page and click on “Create alarm”.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694598444878/13b72039-c070-49e8-86cd-4da5cf8f9721.png align="center")

* Alarm for CPU utilization is created successfully.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694598497160/fb3aa5f5-5371-4670-a529-acb387517f38.png align="center")

## Task-02: Auto Scaling and Monitoring with AWS Console and CLI

* **Create an Auto Scaling group using the AWS Management Console and configure it to launch EC2 instances in response to changes in demand.**
    
* **Use Amazon CloudWatch to monitor the performance of the Auto Scaling group and the EC2 instances and troubleshoot any issues that arise.**
    
* **Use the AWS CLI to view the state of the Auto Scaling group and the EC2 instances and verify that the correct number of instances are running.**
    

**Create template from instance:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694599244034/1ff6ab61-7085-487b-8589-e92eb5a13a67.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694599400443/0054be99-0a12-43c4-a793-b519ee7ebda3.png align="center")

**Create an Auto Scaling Group (ASG) using the AWS Management Console:**

1. Log in to your AWS Management Console.
    
2. Navigate to the Auto Scaling service.
    
3. Create a new Auto Scaling group.
    
4. Configure the launch template or configuration for the instances in the group.
    
5. Set up the scaling policies, including minimum and maximum instances.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694599472372/9757aade-6d36-4f8f-9feb-b6c5929c61e6.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694599506821/5a745720-6ac5-4a29-92ec-cb3b30d790ad.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694599566232/e70e5d3e-baea-4e71-aeac-65b41658bd33.png align="center")

* Now provide Desired Capacity, Minimum and Maximum Capacity.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694599649543/4412cafd-89c2-46ce-8ff8-dfaa141750f0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694599685114/1a55355e-f50e-4fcb-96dd-c89e9454e8b0.png align="center")

* Take a Review of Configuration and Hit the “Create Auto Scaling Group” Button.
    
* The Auto-scaling group is now created.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694599751927/2c564198-dc44-4937-a5e0-3c1dd25c9d7f.png align="center")

**Monitor the ASG and EC2 Instances using Amazon CloudWatch:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694600356131/d73f3602-64aa-4ee7-a2b2-b4361d5a6b68.png align="center")

* You can add the same to the already created dashboard in AWS CloudWatch.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694600456056/9e1735d7-528b-464f-a557-0f2eabb8d283.png align="center")

* Same can be setup to trigger an e-mail by setting a CloudWatch alarm which we have in above task for instance monitoring.
    

**Verify ASG State Using AWS CLI:**

1. Install and configure the AWS CLI on your local machine.
    
2. Use AWS CLI commands to view information about the Auto Scaling group and instances.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694600609350/ffbc4755-dc11-42de-847c-3692e150d682.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694600714107/edbd6763-f580-4ceb-8e34-d301328ac2f0.png align="center")

* Provide Access Key ID, Secret Access Key, Region Name and Output Format.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694601068645/7d687696-3e63-4380-ab64-943712ab0c04.png align="center")

* You can verify the running Auto-scaling group with the AWS CLI command.
    

```bash
aws autoscaling describe-auto-scaling-groups
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694601142355/1e7954cb-0f26-4109-a6c8-3e4575bd62d1.png align="center")

* To verify EC2 instance use this command:
    

```bash
aws autoscaling describe-auto-scaling-instances
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694601276393/fdad9777-2ea9-4d2e-a037-a95003f5c888.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.