---
title: "S3 Programmatic access with AWS-CLI 💻"
datePublished: Sat Sep 09 2023 04:48:02 GMT+0000 (Coordinated Universal Time)
cuid: clmbjpdjs000109jqhyoreusq
slug: s3-programmatic-access-with-aws-cli
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694234782872/8e9af390-6724-491f-8e30-d8f963036504.jpeg
tags: cloud, aws, devops, 90daysofdevops, trainwithshubham

---

Hi, I hope you had a great day yesterday. Today as part of the #90DaysofDevOps Challenge we will be exploring most commonly used service in AWS i.e S3.

## What is AWS S3?

AWS S3 stands for Amazon Simple Storage Service. It is Amazon's cloud storage service for storing and retrieving any amount of data from the cloud.

**Some key points about AWS S3:**

* It is a simple object storage service, which means you store files as objects with a unique URL.
    
* It provides 11 9's of durability, meaning your data is extremely durable and unlikely to be lost.
    
* It offers high availability and scalability. It can scale to exabytes of data and to millions of requests per second.
    
* Data is stored across multiple Availability Zones for high availability.
    

**Some common use cases for S3 are:**

* Storing static websites
    
* Serving images/videos/files to applications
    
* Storing backups and archives
    
* Collecting logs from AWS services
    

## Task 1: AWS EC2 and S3 Interaction

* **Launch an EC2 instance using the AWS Management Console and connect to it using Secure Shell (SSH).**
    

1. **Log in to AWS Console:** Go to the AWS Management Console and log in to your AWS account.
    
2. **Launch an EC2 Instance:**
    
    * Navigate to the EC2 service.
        
    * Click on "Instances" in the left sidebar.
        
    * Click the "Launch Instances" button to create a new EC2 instance.
        
    * Follow the instance creation wizard, selecting an Amazon Machine Image (AMI), configuring instance details, adding storage, configuring security groups (allow SSH traffic), and reviewing your settings.
        
    * Launch the instance and create or select an existing key pair to use for SSH access.
        
3. **Connect to the EC2 Instance:**
    
    * Once your EC2 instance is running, select it in the EC2 dashboard.
        
    * Click the "Connect" button to view instructions for connecting via SSH. Use the provided SSH command, replacing `your-key.pem` with the path to your private key file.
        
    * **For example:**
        
        ```bash
        ssh -i /path/to/your-key.pem ec2-user@ec2-instance-public-ip
        ```
        

* **Create an S3 bucket and upload a file to it using the AWS Management Console.**
    
* Navigate to the S3 service in the AWS Management Console and Click the "Create bucket" button.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693739488034/9267f62b-6fb9-402c-8954-fcccc26faa28.png align="center")

* Choose a unique bucket name, select a region, and configure any additional settings as needed.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693739814512/db048fb9-ace5-40bd-b4b6-8f7fbea9e0f0.png align="center")

* Create the bucket.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693739644921/69fe51af-54aa-4540-989e-df15449f5f08.png align="center")

* The S3 bucket is created now.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693739842953/3660003a-6506-49b6-ae5b-da8d381489a0.png align="center")

**Upload a File to the S3 Bucket:**

* Inside your newly created S3 bucket, click the "Upload" button.
    
* Select the file you want to upload from your local machine and follow the upload wizard.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693740124299/e0e7d82f-6834-480e-8955-855569b17ea5.png align="center")

* The file is now uploaded to the S3 bucket.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693740181561/96b4a3ed-ff78-4c8d-b5ac-8483e1ea4c50.png align="center")

* **Access the file from the EC2 instance using the AWS Command Line Interface (AWS CLI).**
    

**Install AWS CLI on EC2:**

* If it's not already installed on your EC2 instance, you can install the AWS CLI by running:
    

```bash
sudo apt-get update
sudo apt-get install awscli -y
```

Once you installed AWS CLI use `aws --version` to check AWS CLI version.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694231020132/e05f00c8-ce5e-457b-bc8a-52eada6f9535.png align="center")

Now, configure your aws by using `aws configure` command and enter your AWS access key id and Secret access key.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694231169238/b07078ee-b6b0-4396-8c78-9541e04634a0.png align="center")

Now, list s3 bucket using `aws s3 ls` command:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694231258481/c4411e55-688e-4144-85f4-7b383059fb94.png align="center")

If you want to download the files present in your s3 bucket for that you can use `aws s3 cp` command to download the files.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694231592267/7e9d70e4-1525-452a-bcbd-dfcc71936106.png align="center")

## Task 2: EC2 Snapshot and S3 File Verification Task

**Create a snapshot of the EC2 instance and use it to launch a new EC2 instance.**

* Navigate to AWS EC2 service and click on “**Snapshots”**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694231836576/f7d3f75e-bc32-4ac7-88f7-0eee8be62052.png align="center")

* Now, click on "create snapshot"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694231886629/506e2a96-79fa-4152-82c0-b3cf59fd3cdc.png align="center")

* Select the EC2 instance that you want to create a snapshot.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694231967253/a0f31429-1073-4fa8-967d-0dfe453c5e9f.png align="center")

* Click on "create snapshot"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694232003489/aaebffc9-22a1-4d8f-a0be-7222c6b2d0d4.png align="center")

* Snapshot created.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694232034870/db79971c-3af0-4e1c-8ca0-16a9665e0a18.png align="center")

* Click on the "Actions" button present on the right side and choose "Create Image from snapshot" from the drop-down menu.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694232178497/be922462-c7b0-4853-8cf0-a7ca995e01df.png align="center")

* In the “Create Image from snapshot” window, enter a name and description for the image.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694232269049/59fd16f2-ec26-440b-a1c3-dae40346a2a4.png align="center")

* Now, click on "Create image"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694232327627/0a11571b-a021-4842-86bb-4b3e089be0b8.png align="center")

* Go to the "AMI" section on the EC2 dashboard and check if image is created or not.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694232494356/20b32760-841a-41f9-b6b6-1d8ba8565ac0.png align="left")

* Now click on "**Launch instances from AMI"**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694232749377/967fd1b3-fc22-4072-96c0-e770730e97be.png align="center")

* Connect to instance using SSH and use this command:
    

```bash
<aws s3 cp s3://bucket-name/file.txt .> - This command downloads a file from an S3 bucket to your local file system.
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694231592267/7e9d70e4-1525-452a-bcbd-dfcc71936106.png align="left")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.