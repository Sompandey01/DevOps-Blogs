---
title: "Meta-Arguments in Terraform"
datePublished: Sat Nov 04 2023 12:56:43 GMT+0000 (Coordinated Universal Time)
cuid: clok1tjuf000009jsbw5bf94h
slug: meta-arguments-in-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699102564950/3bc97aed-d5d2-4d3d-9c6d-ec671283d98b.png
tags: aws, cloud-computing, devops, terraform, 90daysofdevops

---

When you define a resource block in Terraform, by default, this specifies one resource that will be created. To manage several of the same resources, you can use either count or for\_each, which removes the need to write a separate block of code for each one. Using these options reduces overhead and makes your code neater.

Count is what is known as a ‘meta-argument’ defined by the Terraform language. Meta-arguments help achieve certain requirements within the resource block.

## Count

The count meta-argument accepts a whole number and creates the number of instances of the resource specified.

When each instance is created, it has its own distinct infrastructure object associated with it, so each can be managed separately. When the configuration is applied, each object can be created, destroyed, or updated as appropriate.

eg.

```yaml
terraform {
required_providers {
aws = {
source = "hashicorp/aws"
version = "~> 4.16"
}
}
required_version = ">= 1.2.0"
}
provider "aws" {
region = "ap-south-1"
}
resource "aws_instance" "server" {
count = 4
ami = "ami-053b0d53c279acc90"
instance_type = "t2.micro"
tags = {
Name = "Server ${count.index}"
}
}
```

## for\_each

Like the count argument, the for\_each meta-argument creates multiple instances of a module or resource block. However, instead of specifying the number of resources, the for\_each meta-argument accepts a map or a set of strings. This is useful when multiple resources are required that have different values. Consider our Active Directory groups example, with each group requiring a different owner.

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

provider "aws" {
  region = "us-east-1"
}

locals {
  ami_ids = toset([
    "ami-0889a44b331db0194",
    "ami-007855ac798b5175e",
  ])
}

resource "aws_instance" "server" {
  for_each = local.ami_ids
  ami           = each.key
  instance_type = "t2.micro"
  tags = {
    Name = "Server ${each.key}"
  }
}
```

## Task: Create the above Infrastructure as code and demonstrate the use of Count and for\_each.

### Count:

Copy the code written at the count block and paste it into the main.tf file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699101203729/b496eaf2-27fb-4804-87d7-10038a20928d.png align="center")

Now, run terraform init, plan and apply.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699101361335/915fb9f5-733e-47c1-9b80-33f60380dfdf.png align="center")

Let’s check our output.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699101394748/5d90f21e-9d59-48d0-bdb4-ceacfee6c62f.png align="center")

### for\_each:

Copy the code written at the for\_each block and paste it into the main.tf file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699102227189/4fd7d476-9c51-4de8-93de-f82d819eb213.png align="center")

Now, run terraform init, plan and apply.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699102343226/6a72656c-814b-4ba5-bac6-5c9e6fd7d0ef.png align="center")

Let’s check our output.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699102375927/595585e2-6d48-4d0f-a640-373d6f4131aa.png align="center")

---

Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.