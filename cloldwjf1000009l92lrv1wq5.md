---
title: "Terraform Modules"
datePublished: Sun Nov 05 2023 11:22:44 GMT+0000 (Coordinated Universal Time)
cuid: cloldwjf1000009l92lrv1wq5
slug: terraform-modules
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699183258354/5ab4b980-180c-4f68-a3a9-7c2ed7d157f0.jpeg
tags: cloud-computing, devops, terraform, 90daysofdevops, trainwithshubham

---

## What are Modules?

Modules are containers for multiple resources that are used together. A module consists of a collection of .tf and/or .tf.json files kept together in a directory

A module can call other modules, which lets you include the child module’s resources into the configuration in a concise way.

Modules can also be called multiple times, either within the same configuration or in separate configurations, allowing resource configurations to be packaged and re-used.

### Below is the format on how to use modules:

```yaml
# Creating a AWS EC2 Instance
resource "aws_instance" "server-instance" {
  # Define number of instance
  instance_count = var.number_of_instances

  # Instance Configuration
  ami                    = var.ami
  instance_type          = var.instance_type
  subnet_id              = var.subnet_id
  vpc_security_group_ids = var.security_group

  # Instance Tagsid
  tags = {
    Name = "${var.instance_name}"
  }
}
```

```yaml
# Server Module Variables
variable "number_of_instances" {
  description = "Number of Instances to Create"
  type        = number
  default     = 1
}

variable "instance_name" {
  description = "Instance Name"
}

variable "ami" {
  description = "AMI ID"
  default     = "ami-xxxx"
}

variable "instance_type" {
  description = "Instance Type"
}

variable "subnet_id" {
  description = "Subnet ID"
}

variable "security_group" {
  description = "Security Group"
  type        = list(any)
}
```

```yaml
# Server Module Output
output "server_id" {
  description = "Server ID"
  value       = aws_instance.server-instance.id
}
```

## Different modules in Terraform?

There are three main types of modules in Terraform:

1. **Root Module** - This is the main directory of your Terraform configuration. It contains the `.tf` files that define the root resources.
    
2. **Child Module** - Any module that is called from another module is a child module. Child modules can be defined locally or downloaded from a registry.
    
3. **Published Module** - These are modules that have been published to a registry for reuse. Terraform has a public registry that hosts thousands of free modules.
    

## Difference between Root Module and Child Module?

Every Terraform configuration has at least one module, known as the root module. This consists of the `.tf` files in the main working directory. The root module contains resources that define the root-level infrastructure. A child module is a module that is called from another module. It contains resources that are encapsulated and reusable.

## Is modules and Namespaces are same? Justify your answer for both Yes/No

Modules and namespaces are not the same - they have important differences in how they organize code and scope variables. Modules provide true isolation and modularity, while namespaces are used for logical grouping.

---

Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.