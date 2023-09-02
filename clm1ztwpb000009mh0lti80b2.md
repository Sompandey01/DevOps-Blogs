---
title: "IAM Programmatic access and AWS CLI 🚀"
datePublished: Sat Sep 02 2023 12:21:45 GMT+0000 (Coordinated Universal Time)
cuid: clm1ztwpb000009mh0lti80b2
slug: iam-programmatic-access-and-aws-cli
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693657218208/cab3979e-e46c-4281-bc35-c01b953074d3.jpeg
tags: cloud, aws, devops, 90daysofdevops, tws

---

Today is more of a reading exercise and getting some programmatic access for your AWS account.

## IAM Programmatic access

IAM Programmatic access refers to accessing AWS services programmatically using the AWS APIs or SDKs. This is in contrast to the AWS Management Console which provides a graphical user interface.

When you use programmatic access, you will need to provide AWS credentials to authenticate the requests to the AWS APIs. These credentials can be:

* Access key ID and secret access key: These are long-term credentials for IAM users. They allow full access to all AWS services.
    
* Temporary security credentials: These are credentials that are generated for IAM roles. They provide temporary access and are useful for applications or EC2 instances to access AWS.
    
* AWS Security Token Service: STS can also be used to generate temporary security credentials.
    

## AWS CLI

The AWS Command Line Interface (AWS CLI) is a unified tool to manage your AWS services. With just one tool to download and configure, you can control multiple AWS services from the command line and automate them through scripts.

The AWS CLI v2 offers several new features including improved installers, new configuration options such as AWS IAM Identity Center (successor to AWS SSO), and various interactive features.

## Task-01: Create AWS\_ACCESS\_KEY\_ID and AWS\_SECRET\_ACCESS\_KEY from AWS Console.

1. **Log in to AWS**: Go to the AWS website and log in with your AWS account.
    
2. **Find IAM**: Look for "IAM" in the AWS dashboard, it's where you manage users and their permissions.
    
3. **Create a User**: If you don't have a user already, you can make one. This user will use the access keys. Just give the user a name and choose what they can do on AWS.
    
4. **Generate Access Keys**: Click on the user you created, and go to the "Security credentials" section. There, you can make access keys.
    
5. **Download the Keys**: Once you create the keys, you'll see them on your screen. Click to download them. It's a file with important secret codes.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693654826785/4056ed30-e513-4f9f-9954-18861c6c1e0f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693654881416/b7edbe84-9ef4-4f53-8648-52e8dc83f4ca.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693654932191/5737ff6e-59f9-457c-b4a3-12a122be8f34.png align="center")

* Click on the create access key.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693654989067/65593c6b-2fbf-4f76-846f-fb6f3b4ff2be.png align="center")

* Choose the CLI option or as per your requirement.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693655021632/762f86e0-f67d-4990-8c81-54ad4aaab9b6.png align="center")

* Now, create the access key.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693655166337/e6f843dc-4b54-42ce-a183-ae557b4cb528.png align="center")

* You can see two keys now which are the Access key and the Secret access key Save it.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693655267267/b951844d-b455-4f5b-932b-ab54df55e280.png align="center")

## Task 2: Setup and install AWS CLI and configure your account credentials.

Launch the EC2 instance with the script given below:

```bash
#!/bin/bash

sudo apt-get update
sudo apt-get install awscli -y
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693656061310/9199849f-35a3-4351-b798-b23686769883.png align="center")

Run the following command to verify the installation:

```bash
aws --version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693656362333/672829a8-adae-48ff-a420-b6c70fa6f9e5.png align="center")

Configure your AWS CLI Credentials

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693656628914/f4d63e4f-6325-4838-ac32-7fceff28a683.png align="left")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.