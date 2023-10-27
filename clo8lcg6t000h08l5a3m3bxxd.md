---
title: "Terraform with AWS"
datePublished: Fri Oct 27 2023 12:30:04 GMT+0000 (Coordinated Universal Time)
cuid: clo8lcg6t000h08l5a3m3bxxd
slug: terraform-with-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698409756202/26401d45-8e8e-44a2-8823-e1678b96052c.png
tags: aws, devops, terraform, 90daysofdevops, trainwithshubham

---

Provisioning on AWS is quite easy and straightforward with Terraform.

## Prerequisites:

### AWS CLI installed

The AWS Command Line Interface (AWS CLI) is a unified tool to manage your AWS services. With just one tool to download and configure, you can control multiple AWS services from the command line and automate them through scripts.

* Install AWS CLI on the Ubuntu server.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698406607587/0a5ec91f-675f-4b83-b5dc-044f36d12c4c.png align="center")

### AWS IAM user

IAM (Identity Access Management) AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources. You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources.

*In order to connect your AWS account and Terraform, you need the access keys and secret access keys exported to your machine.*

```yaml
export AWS_ACCESS_KEY_ID=<access key>
export AWS_SECRET_ACCESS_KEY=<secret access key>
```

* Create an IAM user with suitable permissions.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698406883860/09289b83-59ee-4d49-9d21-3c208a31694a.png align="center")

* Now, click on the Create access key and select CLI.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698406975612/0a284210-06be-406f-a883-3340f5f9bd78.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698407006744/077bc285-2e76-4970-b22b-d5b51ca54ec5.png align="center")

* The access key and Secret access key are created. Now, export the access keys to configure the aws console to the terminal through awscli.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698408143354/546c88e6-6475-402c-b229-40aa9d9da776.png align="center")

### Install required providers

```yaml
terraform {
 required_providers {
        aws = {
        source  = "hashicorp/aws"
        version = "~> 4.16"
}
}
        required_version = ">= 1.2.0"
}
```

Add the region where you want your instances to be

```yaml
provider "aws" {
region = "ap-south-1"
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698408348372/d451280c-c571-42c2-ace6-7fbbcfb16fed.png align="center")

## Task-01: Provision an AWS EC2 instance using Terraform

```yaml
resource "aws_instance" "aws_ec2_test" {
        count = 4
        ami = "ami-08c40ec9ead489470"
        instance_type = "t2.micro"
        tags = {
     Name = "TerraformTestServerInstance"
  }
}
```

Let's add this inside main.tf file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698408475115/291dc4d1-59a9-459e-aad8-788cef553568.png align="center")

* Initialise the terraform in the servers to download the required providers.
    

```yaml
terraform init
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698408552557/591d27cf-079e-4e5e-b33b-5111a67041d8.png align="center")

* View the plan of Terraform to check the servers spin up with given configurations.
    

```yaml
terraform plan
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698409038647/abb81902-7c0f-4daf-bd13-fe5053090e53.png align="center")

* Now, apply the terraform file to create the servers.
    

```yaml
terraform apply
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698409097443/62fa032e-80f4-41a3-a1cc-297369883e33.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698409150782/1d692426-cf89-410e-a275-cae8b6acb20c.png align="center")

Let’s check the console.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698409527919/05f55eb0-c755-404b-85c1-53f0170d2e19.png align="center")

---

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.