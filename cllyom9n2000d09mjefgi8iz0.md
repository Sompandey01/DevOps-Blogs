---
title: "AWS EC2 Automation"
datePublished: Thu Aug 31 2023 04:44:34 GMT+0000 (Coordinated Universal Time)
cuid: cllyom9n2000d09mjefgi8iz0
slug: aws-ec2-automation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693456974801/5b7df0cb-95bc-4f11-b4b1-d1afb4736cca.jpeg
tags: cloud, aws, devops, 90daysofdevops, tws

---

## Automation in EC2

Amazon EC2 allows you to automate many routine tasks to improve efficiency and reduce manual operations and maintenance costs. Some tasks you can automate in EC2 are:

• **Instance launching -** You can write scripts or use AWS services like CloudFormation to automatically launch new EC2 instances based on templates. This ensures consistency and repeatability.

• **Instance termination -** You can set up auto scaling policies or write scripts to automatically terminate idle or unused instances to save costs.

• **Backup and snapshotting -** You can automate the creation of EBS volume snapshots on a schedule to ensure your data is regularly backed up.

• **Security updates -** You can automate the installation of OS and software security updates on your EC2 instances to keep them patched and secure.

• **Scaling -** You can set up auto-scaling groups that automatically scale your EC2 fleet up or down based on metrics or schedules. This helps handle fluctuations in demand.

• **Configuration management -** You can use tools like Chef, Puppet or Ansible to automate and standardize the configuration of your EC2 instances.

• **Monitoring -** You can configure CloudWatch alarms to trigger automated actions when certain thresholds are met, like terminating unhealthy instances.

Automating routine tasks in EC2 helps improve reliability, security and cost efficiency. It reduces the need for manual operations and human error. Automation also enables a more dynamic and scalable infrastructure that can quickly respond to changes in demand.

## Launch template in AWS EC2

* You can make a launch template with the configuration information you need to start an instance. You can save launch parameters in launch templates so you don't have to type them in every time you start a new instance.
    
* For example, a launch template can have the AMI ID, instance type, and network settings that you usually use to launch instances.
    
* You can tell the Amazon EC2 console to use a certain launch template when you start an instance.
    

## Instance Types

Amazon EC2 has a large number of instance types that are optimised for different uses. The different combinations of CPU, memory, storage and networking capacity in instance types give you the freedom to choose the right mix of resources for your apps. Each instance type comes with one or more instance sizes, so you can adjust your resources to meet the needs of the workload you want to run.

## AMI

An Amazon Machine Image (AMI) is an image that AWS supports and keeps up to date. It contains the information needed to start an instance. When you launch an instance, you must choose an AMI. When you need multiple instances with the same configuration, you can launch them from a single AMI.

## Task 1: **Creating a Launch Template, Launching Instances, and Setting Up an Auto Scaling Group in AWS EC2**

* **Create a launch template with Amazon Linux 2 AMI and t2.micro instance type with Jenkins and Docker setup (You can use the Day 39 User data script for installing the required tools.**
    

**<mark>Step 1:</mark> Create a Launch Template**

1. **Navigate to the EC2 Dashboard:** Go to your AWS Management Console, then under the "Compute" section, click on "EC2".
    
2. **Create a Launch Template:** In the EC2 Dashboard, click on "Launch Templates" in the left navigation pane, and then click the "Create launch template" button.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693454400715/ce842f23-1040-4c88-a224-7167c785e3b3.png align="center")

**Configure Template Details:**

* Provide a name and description for the launch template.
    
* For "AMI ID," select the Ubuntu AMI.
    
* For "Instance type," select t2.micro.
    
* Under "Advanced Details," provide your user data script that installs Jenkins and Docker (you mentioned using Day 39 User data script).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693454607389/5d717b53-5328-429d-a234-37df3dfea703.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693454650342/1cfc4b23-680d-4491-b94b-5881d05a61ad.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693454694762/393d4bb4-74c2-4626-a099-e653d8962d7b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693454793763/384561f0-9e39-4cf6-92cc-085b6986b865.png align="center")

In the “**Advanced Details**” section, paste the user data script for installing Jenkins and Docker in the “**User data**” field.

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

 sudo apt-get update
 sudo apt-get install docker.io -y
 sudo systemctl start docker
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693454867263/226e5e53-ba04-45b1-b939-a779b2984102.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693454885977/320eda3b-7624-425a-acda-5db9f79c2894.png align="center")

Choose “**Create launch template**”. below you can see template is created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693455076274/a833248e-d044-49d5-b02d-565bbac534cf.png align="center")

**Create 3 Instances using Launch Template, there must be an option that shows number of instances to be launched.**

**<mark>Step 2:</mark> Launch Instances using the Launch Template**

1. **Navigate to Launch Instances:** In the EC2 Dashboard, click on "Instances" in the left navigation pane, and then click the "Launch Instances" button.
    
2. **Select Launch Template:** Choose the "My launch template" tab and select the launch template you created in the previous step.
    
3. **Configure Instance Details:** Configure settings like instance count, network settings, IAM role, etc.
    
4. **Add Storage:** Configure the storage settings as needed.
    
5. **Configure Security Group:** Configure security group settings as needed.
    
6. **Review and Launch:** Review your settings and click the "Launch" button.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693455696018/ac2e2082-5d78-4bf9-8552-8f9023ade2b8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693455751481/43245d00-4ed9-4dfd-a1ff-33f2864aa291.png align="center")

You can see three instances created from template.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693455821335/8cdd3744-960f-4e95-87f1-a8bc222d4678.png align="center")

## Task 2: Create an Auto Scaling Group

Creating an Auto Scaling Group will automatically manage the number of instances running based on certain conditions like CPU utilization, network traffic, etc.

1. **Navigate to Auto Scaling Groups:** In the EC2 Dashboard, click on "Auto Scaling Groups" in the left navigation pane, and then click the "Create Auto Scaling group" button.
    
2. **Configure Group Details:**
    
    * Choose the launch template you created earlier.
        
    * Configure the group size settings, such as desired, minimum, and maximum instances.
        
3. **Configure Scaling Policies:** Set up scaling policies based on conditions like CPU utilization.
    
4. **Configure Notifications and Tags (Optional):** Configure notifications and add tags if needed.
    
5. **Review and Create:** Review your settings and click the "Create Auto Scaling group" button.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693456016483/54b8d4c6-6485-4786-bf0f-f5c5c1055092.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693456078827/da8e0ffe-aa15-4ba9-ab36-560b9f5bd66a.png align="center")

For “**Network**”, choose the VPC and subnet you want the instances to launch in.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693456184488/0e873062-e08e-4398-9cb8-06176662e9e9.png align="center")

For “**Load balancing**”, choose any option as per your requirement.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693456234264/a32ea924-f5e2-4313-b7b6-07111b94194e.png align="center")

In the “**Group Size**” page, enter the desired capacity for the auto-scaling group, such as 2.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693456334101/5a95edd1-28e4-4565-8c29-a93c583067e6.png align="center")

* Review the details and click on **"Create Auto Scaling group"** to create the group.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693456438439/06a3c034-2351-43da-9dea-76947bf4a624.png align="center")

Autoscaling group is created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693456592851/67b7e0a0-de45-4bc3-9161-02f2fbbc8e4b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693456761993/c2d9a66a-f627-4782-95fa-7169a1b4849e.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.