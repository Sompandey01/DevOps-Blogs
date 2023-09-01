---
title: "Setting up an Application Load Balancer with AWS EC2 🚀"
datePublished: Fri Sep 01 2023 11:48:33 GMT+0000 (Coordinated Universal Time)
cuid: clm0j7dbt000u09l6h6w088ad
slug: setting-up-an-application-load-balancer-with-aws-ec2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693568870412/b1d886b1-2764-4d80-a2e5-958b02d00f05.png
tags: cloud, aws, devops, 90daysofdevops, trainwithshubham

---

Hi, I hope you had a great day yesterday learning about the launch template and instances in EC2. Today, we are going to dive into one of the most important concepts in EC2: Load Balancing.

## What is Load Balancing?

Load balancing is the distribution of workloads across multiple servers to ensure consistent and optimal resource utilization. It is an essential aspect of any large-scale and scalable computing system, as it helps you to improve the reliability and performance of your applications.

## What is Elastic Load Balancing ?

Elastic Load Balancing distributes incoming application traffic across multiple Amazon EC2 instances. It enables you to achieve fault tolerance, scalability and high availability for your applications.

**Types of load balancers:**

* **Classic Load Balancer -** Operates at the transport layer (Layer 4). Supports HTTP and HTTPS listeners.
    
* **Application Load Balancer -** Operates at the application layer (Layer 7). Supports HTTP/HTTPS and WebSockets.
    
* **Network Load Balancer -** Operates at the transport layer and is optimized for high performance.
    

In summary, Elastic Load Balancing enables you to distribute traffic across multiple EC2 instances. It provides benefits like fault tolerance, scalability, high availability and security. The different load balancer types give you options based on your performance and functionality requirements.

## Task 1: AWS EC2 Apache Server Setup with Custom Web Pages

* **Launch 2 EC2 instances with an Ubuntu AMI and use User Data to install the Apache Web Server.**
    

**Launch EC2 Instances:**

* Log in to your AWS Management Console.
    
* Navigate to the EC2 service.
    
* Click "Launch Instance."
    
* Choose an Ubuntu AMI from the available options.
    
* Select the instance type and configure other settings as needed.
    
* In the "User Data" field, you can add a script to install Apache.
    

Here's a sample User Data script:

```bash
#!/bin/bash
apt update -y
apt install apache2 -y
systemctl start apache2
systemctl enable apache2
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693558780546/416ba596-3538-4f54-af83-84f87e8316b0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693558838896/f3d2e5df-3019-4780-bb07-d80e5050a4fb.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693558953777/97b84cf1-c8c9-4562-bfc7-cb2fa57a0dc8.png align="center")

* Connect your ec2 instance.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693559022628/439c1f1b-b37c-45ac-b937-5f94be0a2bbb.png align="center")

Use the command below to check the status of Apache 2:

```bash
sudo systemctl status apache2
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693559174340/9cd2c808-17ad-4a52-91ba-7a640fe2ff7d.png align="center")

* **Modify the index.html file to include your name so that when your Apache server is hosted, it will display your name.**
    
* Go inside /var/www/html/ path and edit index.html file
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693560164429/ab56ddf1-1270-423b-8561-c49fe4c334a4.png align="center")

* Add html code below &lt;title&gt; tag to show your name.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693560131969/d740a9f2-2c90-416f-a3c9-2b7e3cd33d30.png align="center")

* Copy the public IP address and paste it into the address bar of a web browser.
    
* A webpage with details about your PHP installation ought to appear.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693560400670/ccb9babb-e8f3-4b4b-a72e-0a7681e22618.png align="center")

## Task 2: Setting Up AWS Application Load Balancer (ALB) and Target Groups for EC2 Instances

* **Create an Application Load Balancer (ALB) in EC2 using the AWS Management Console.**
    

**Create Target Groups:**

* In the EC2 dashboard, under "Load Balancing," click on "Target Groups."
    
* Click the "Create target group" button.
    
* Configure the target group settings, including the protocol (HTTP), port (80), and the health check settings.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693566899234/4c0c1795-81e7-4da2-b98d-9e9ed70db237.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693566880503/1dc800c5-cc19-419f-9579-02baacb49129.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693566944750/b026046c-b15a-4f75-915c-32eae4a77347.png align="center")

* You have to register targets instances to target group.
    
* Select the instances which you wanted to add.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693567052509/2e915215-f8dd-4ac9-9f02-5d0a0f130498.png align="center")

* Click on “Include as pending below”.
    
* Hit on the “Create target group”.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693567156668/678e9f8f-0abd-4c88-bcda-7e6fa5af51aa.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693567178639/a642c552-98ef-4db1-8344-8f586ae5e93c.png align="center")

* Now go back to your **"Load Balancer"** tab and click on the **refresh button** near the **"Default action"** and then you will see the new target group we just created.
    

**Create an Application Load Balancer (ALB):**

* Log in to your AWS Management Console.
    
* Navigate to the EC2 service.
    
* In the left sidebar, under "Load Balancing," click on "Load Balancers."
    
* Click the "Create Load Balancer" button.
    
* Choose "Application Load Balancer" and click "Create."
    
* Configure the ALB settings, including the VPC, availability zones, and listeners. Make sure to select HTTP (port 80) as a listener.
    
* Set up security groups and configure routing as needed.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693566399663/432ccbbc-ecc4-4bd4-904a-5fb497df5b9c.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693566420714/5f2d546c-9145-4bfb-9074-f4c005d3bb81.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693566504878/bae8cf71-4c97-4ec9-ae09-9871ce8df3b9.png align="left")

* Choose at least 2 subnet.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693567588078/e61d37ad-9963-4e33-9d69-59dc6917b4c0.png align="center")

* In the listener, section attaches the target group that you have created previously.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693567432776/8c950647-ac80-4944-8800-c78dc99d9cdf.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693567614920/dd73a10a-0bca-4bcd-a6e4-f4cdd04711e3.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693567657194/edb7fed0-490a-42e5-b5e7-2d354195c76b.png align="left")

* **Verify that the ALB is working properly by checking the health status of the target instances and testing the load balancing capabilities.**
    
* We’ll check the health status of the Target Group.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693567770271/3e50dfe4-dac9-4158-8ca2-a974d668c911.png align="center")

* Now let's check the status of Load balancer.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693567824319/060dfe50-7cd2-40f8-bb2d-3861364c2620.png align="center")

* Load balancer is successfully created in Active state.
    
* You can now copy the DNS of your load balancer and paste it into your browser to see different webpages
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693568602341/cbad76ee-3c62-4b89-adcb-43bccd2d9ebf.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.