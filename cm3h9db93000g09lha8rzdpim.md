---
title: "How to Host a Website Using an EC2 Instance, Route 53, and a Custom Domain"
datePublished: Thu Nov 14 2024 12:00:19 GMT+0000 (Coordinated Universal Time)
cuid: cm3h9db93000g09lha8rzdpim
slug: how-to-host-a-website-using-an-ec2-instance-route-53-and-a-custom-domain
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1731584919206/9d786422-82ab-4061-b686-a5a7c80012e3.png
tags: aws, projects, devops, devops-articles

---

Setting up a website with AWS Route 53 and EC2 makes hosting easy and adds powerful features like latency-based routing and health checks. This guide will show you how to connect a domain you’ve purchased to AWS, set up latency-based routing to make your site load faster for visitors from different locations, and add health checks to keep your site running smoothly all the time.

### Prerequisites

1. **An AWS Account**: If you don’t already have an AWS account, create one.
    
2. **A Purchased Domain**: Obtain a domain from a provider like Hostinger, GoDaddy, or Namecheap. For this guide, we'll assume the domain is managed by Hostinger.
    

### Step 1: Set Up Your EC2 Instance

1. **Launch an EC2 instance**: In the AWS Management Console, go to the EC2 dashboard and create a new instance.
    
    * Choose an Amazon Linux 2 AMI (or another OS of your choice).
        
    * Select instance type (t2.micro works well for small websites).
        
    * Configure security groups to allow HTTP traffic on port 80.
        
2. **Install HTTPD server**: Go to the advanced details and paste the script in user data.
    
    ```yaml
    #!/bin/bash
    sudo yum update -y
    
    # Install Apache web server (httpd)
    sudo yum install -y httpd
    sudo systemctl start httpd
    sudo systemctl enable httpd
    
    # Create a simple HTML file to verify the web server is running
    echo "<html><h1>Welcome to Apache Web Server from Mumbai</h1></html>" >/var/www/html/index.html
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731499272604/98069547-d04c-4ee2-ad5d-e455f9d93a57.png align="center")

### Step 2: Set Up Route 53 Hosted Zone

1. **Create a Hosted Zone**:
    
    * In the Route 53 console, create a new hosted zone.
        
    * Use your domain name (e.g., [`yourdomain.com`](http://yourdomain.com)) as the hosted zone name.
        
2. **Get the Name Servers**:
    
    * Once the hosted zone is created, AWS will provide a list of name servers. Copy these, as you’ll need them in the next step.
        
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731499051965/c78aa3ee-856e-4a80-837e-37ed367960e3.png align="left")
        

### Step 3: Configure Domain Settings in your Domain Provider

In my case, I’m using Hostinger for my domain.

1. **Update Name Servers**:
    
    * Log in to your Hostinger account and navigate to the DNS settings for your domain.
        
    * Replace the existing name servers with the ones provided by Route 53.
        
    * Save the changes; DNS updates can take 15-30 minutes to propagate fully.
        
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731499198232/16c9eeab-8fd3-4651-bbee-4f4bbf20db26.png align="left")
        

### Step 4: Add an A Record in Route 53

1. **Create an A Record**:
    
    * Go back to Route 53 and open your hosted zone.
        
    * Create an “A” record with simple routing, and paste the public IP address of your EC2 instance.
        
    * Save the record.
        
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731499317637/d1cffe9d-ba83-4287-8493-bfa93400485d.png align="left")
        

### Step 5: Access Your Website

After 40-50 minutes, your domain should direct you to your EC2 instance's HTTPD server. Enter your domain name in a browser, and you should see the webpage hosted on your EC2 instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731504075621/5279e363-e861-4901-9f1e-439bc11682e5.png align="center")

### Step 6: Add Latency-Based Routing for Multiple Regions

1. **Set Up an Additional EC2 Instance in a Different Region**
    
    * Repeat the above steps to set up a second EC2 instance in the N. Virginia region.
        
    * Configure this instance with the same files so it mirrors the Mumbai instance. *Change the script a little* instead of from Mumbai change it to from N. Virginia.
        
2. **Update Route 53 with Latency-Based Routing**
    
    * In your hosted zone, create a new A record but select **Latency Routing** instead of simple routing.
        
    * Add the IP address of each instance in its respective region (Mumbai and N. Virginia) and specify the regions.
        
    * Route 53 will direct users to the instance with the lowest latency based on their location.
        
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731504500011/86c1cf5c-689e-4f3a-84aa-f866c642f465.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731504665711/7bbeb14d-d2c4-47a4-9a95-a84bd4faed8b.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731504721678/ea7ed67d-d5ae-4292-999d-16cccb4e1497.png align="center")
        
        Use VPN to check the N. Virginia server. Now, we’ll use health checks in our server so I’m not using VPN right now.
        

### Step 7: Enable Health Checks for High Availability

To ensure visitors aren’t routed to an offline server, set up health checks:

1. **Create Health Checks for Both Instances**: In Route 53, configure health checks for each EC2 instance. Set the endpoint as the public IP address and choose HTTP as the protocol.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731506242361/ba06760a-7602-4b22-9a29-b03e45abebd1.png align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731506316714/fde5f3aa-847b-42fe-bf20-62d81d656b5b.png align="left")
    
2. **Associate Health Checks with Route 53 Records**: Link each A record to its corresponding health check. Now, Route 53 will monitor the instances, redirecting traffic to the healthy server if one instance goes down.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731506550172/276c21bb-3ae0-43a5-9d91-ad0a553afd2a.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731506593573/44c25dc7-943e-4fa9-aad4-a667094d5bf9.png align="center")
    
3. Check the health check whether your servers are healthy or not.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731506671591/153ad4f6-435e-4703-a6ac-47e2367f0308.png align="center")
    
4. Terminate the Mumbai server, wait a little and check the health check again.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731507037407/5c074738-0f98-4a38-b34e-956c110b7636.png align="center")
    
5. Since we terminated the Mumbai server health check now divert all the traffics to N. Virginia server or we can say the healthy server. Try to access your server and see the magic.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731507186987/8bde2a7a-7130-463e-8707-8af2d1dabac6.png align="left")
    

<mark>Security Tip</mark>: To keep your website safe, add an SSL/TLS certificate for HTTPS. This makes sure all data shared on your site is private and secure, building trust with your users.

### Summary

By following these steps, you have successfully hosted a website on AWS EC2, set up latency-based routing for optimal performance, and implemented health checks for high availability. This configuration ensures users from different regions experience minimal latency and uninterrupted service.