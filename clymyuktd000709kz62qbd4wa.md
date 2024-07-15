---
title: "DevOps Project 10 Mounting S3 Bucket on EC2 Linux using S3FS"
datePublished: Mon Jul 15 2024 12:33:54 GMT+0000 (Coordinated Universal Time)
cuid: clymyuktd000709kz62qbd4wa
slug: devops-project-10-mounting-s3-bucket-on-ec2-linux-using-s3fs
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1721046791321/7aa47783-df3d-4b86-a905-bbf6dfb843c7.jpeg
tags: linux, aws, devops, devops-articles, 90daysofdevops

---

## **Project Description**

In this AWS Mini Project, you will learn how to Mount an AWS S3 Bucket on an Amazon EC2 Linux instance using S3FS. The project provides a hands-on experience with Amazon Web Services (AWS) and covers key components such as AWS S3, Amazon EC2, and S3FS.

Through practical implementation, you will gain valuable insights into securely integrating AWS services, managing data storage in S3, and leveraging S3FS to enable seamless access and interaction between EC2 instances and S3 buckets.

### **Step 1: Create a New IAM User**

Begin by creating a new IAM user in the AWS console. Go to the IAM service, click on "Users," and then "Add user." Enter the name of the new user and proceed to the next step.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721046191336/ff6cb795-1d88-4487-a24e-60da95c72876.png align="center")

Set permissions for the user. For this project, you can create a policy or use an existing one that allows S3 access. Review and create the user. Make sure to save the user's access key and secret access key, as you'll need these later.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721046355700/887d512a-eace-41bc-ab96-4c77bfb215aa.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721046376211/f48c66fe-f2aa-44b8-b544-dd939f1cd18e.png align="center")

### **Step 2: Create EC2 Instance**

Create a new `t2.micro` instance on AWS EC2

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721045253767/23e3527e-a1f0-4215-a473-c4d181ab6e18.png align="center")

Install the AWS Command Line Interface (aws-cli) if not already installed.

```yaml
 curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721045411754/73d0f7f0-53b6-470b-87f2-9fa29f6738cc.png align="center")

### **Step 3: Install S3FS**

After installing AWS CLI, proceed to install S3FS on the EC2 instance.

```yaml
sudo apt install s3fs -y
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721045557811/68e59080-155c-4f8c-a2cf-9c847e1a8c29.png align="center")

### **Step 4: Create a Folder and Add Files**

Create a folder named "bucket" at a location `/home/ubuntu` on the EC2 instance. Add 1–2 files to this folder.

```yaml
mkdir bucket
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721045640209/4c4935a9-5548-4698-967e-a0457f9ae300.png align="center")

```yaml
touch test1.txt test2.txt 
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721045679771/e79b1b44-8eea-4bb7-a908-b4d0dead2d32.png align="center")

### **Step 5: Create S3 Bucket**

In the AWS console, create an S3 bucket with a suitable name.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721045768144/5c326369-c7a5-4954-893a-58caa5a0b094.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721045793810/f8ba99ac-b036-424f-96e2-d972eeefc3f7.png align="center")

### **Step 6: Configure AWS CLI**

On the EC2 instance, configure the AWS CLI by running the command `aws configure` and providing the Access Key and Secret Key obtained earlier.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721045875082/4a784493-15b6-41b6-9152-e79fb261b4f6.png align="center")

### **Step 7: Sync Files to S3 Bucket**

Run the below command to sync the files from the given location on the EC2 instance to the S3 bucket.

```yaml
aws s3 sync /home/ubuntu/bucket s3://day89-s3bucket
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721045953712/d29f9b37-e3be-4fd6-a500-3caf41f93b76.png align="center")

### **Step 8: Verify the Sync**

Refresh the objects inside the S3 bucket to confirm that all the files from the EC2 instance are successfully uploaded to the S3 bucket.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721045988365/cc9df6ae-c3a5-4e9e-bc5b-de7fc38fe9b6.png align="center")

**Congratulations on completing Day 89 of the #90DaysOfDevOps Challenge!**

Today, you successfully mounted an AWS S3 bucket on an EC2 Linux instance using S3FS. This achievement has deepened your expertise in AWS, S3, EC2, and S3FS.

Stay tuned for tomorrow as we conclude this incredible journey with the final day of the challenge. Keep up the great work!