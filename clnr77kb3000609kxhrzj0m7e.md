---
title: "Terraform and Docker 🔥"
datePublished: Sun Oct 15 2023 08:22:16 GMT+0000 (Coordinated Universal Time)
cuid: clnr77kb3000609kxhrzj0m7e
slug: terraform-and-docker
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697358100221/0bcd3a6a-184b-41a1-a29a-c2d9827e86b9.jpeg
tags: software-development, devops, terraform, 90daysofdevops, trainwithshubham

---

## What are Blocks and Resources in Terraform??

Blocks: Blocks define different parts of your Terraform configuration. The main block types are:

Provider Blocks: Provider blocks configure a specific cloud provider for Terraform to use. For example, an AWS provider block would look like:

```bash
  provider "aws" {
    region = "us-east-1"
    access_key = "..."
    secret_key = "..."
  }
```

This configures Terraform to use AWS as the cloud provider with the specified region, access key, and secret key.

**Resource Blocks:** Resource blocks define the actual infrastructure objects that Terraform will create. For example:

```bash
  resource "aws_instance" "web" {
    ami           = "ami-1234" 
    instance_type = "t2.micro"
  }
```

This defines an AWS EC2 instance resource named "web".

**Variable Blocks:** Variable blocks define variables that can be reused in your configuration. This allows flexibility and reusability. For example:

```bash
  variable "ami_id" {
    description = "The AMI ID to use for the EC2 instance"
  }
```

**Output Blocks:** Output blocks define values that are output after running `terraform apply`. For example:

```bash
  output "instance_id" {
    value = "${aws_instance.web.id}" 
  }
```

This will output the ID of the EC2 instance after creation.

**Resources:** Resources represent the actual infrastructure objects that will be created. You define resources using resource blocks, as shown above. Common resource types are:

* EC2 instances
    
* S3 buckets
    
* Load balancers
    
* Virtual machines
    

When you run `terraform apply`, Terraform will provision the resources you've defined.

In summary, blocks configure different parts of your Terraform template, while resources represent the actual infrastructure objects that will be created when you apply your configuration.

## Task-01: Create a Terraform script with Blocks and Resources

```bash
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 2.21.0"
}
}
}
```

This is a Terraform configuration block that specifies a required provider for the docker resource type. The provider is defined using the kreuzwerker/docker source and version ~&gt; 2.21.0.

The required\_providers block is used to declare the minimum version of a provider required by the Terraform configuration. In this case, the docker provider with version 2.21.0 or greater is required to run the configuration. If the provider is not installed, Terraform will automatically download and install the provider at the specified version.

## Provider Block

The provider block configures the specified provider, in this case, docker. A provider is a plugin that Terraform uses to create and manage your resources.

```bash
provider "docker" {}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697285262413/99f2e1aa-6ae1-441d-86e9-b7f7e3c38e5d.png align="center")

## Resource

Use resource blocks to define components of your infrastructure. A resource might be a physical or virtual component such as a Docker container, or it can be a logical resource such as a Heroku application.

Resource blocks have two strings before the block: the resource type and the resource name. In this example, the first resource type is docker\_image and the name is Nginx.

## Task-02: Create a resource Block for an nginx docker image

```bash
resource "docker_image" "nginx" {
 name         = "nginx:latest"
 keep_locally = false
}
```

* Create a resource Block for running a docker container for nginx
    

```bash
resource "docker_container" "nginx" {
 image = docker_image.nginx.latest
 name  = "tutorial"
 ports {
   internal = 80
   external = 80
 }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697357329714/bea68f57-0f76-4491-bf30-8a38a5050656.png align="center")

After you’ve created a Terraform configuration file (with [a.tf](http://a.tf) extension), use the Terraform commands listed below to provision and manage your infrastructure:

**terraform init :** Downloads and installs any required providers and modules, initializes the backend, and downloads any necessary plugins in a new or existing Terraform working directory.

```bash
terraform init
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697357453258/43919307-0bd4-4ee7-8627-1c42b44ffa4b.png align="center")

**Note:** In case Docker is not installed use below commands.

```bash
sudo apt-get install docker.io 
sudo docker ps 
sudo chown $USER /var/run/docker.sock
```

Check docker container is created using the below command:

```bash
docker ps
```

**terraform plan:** The output of terraform plan gives a summary of the infrastructure modifications that will be made, such as creating, changing, or eliminating resources. It also displays any issues or warnings that must be handled prior to implementing the modifications.

```bash
terraform plan
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697357615154/3a711dce-0334-4956-bc7a-2881801fadd9.png align="center")

**terraform apply:** When you run Terraform apply, Terraform generates or adjusts the configuration files’ resources to match the intended state. It also updates the state file to reflect the infrastructure changes. If Terraform encounters any faults or warnings during the application process, it will prompt you to confirm whether or not to proceed with the changes.

```bash
terraform apply
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697357732602/a71d53ac-71cb-491e-a641-bd13c36be3ba.png align="center")

Browse public IP address, you can see the nginx default page.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697357806677/370f8d83-600a-415a-84de-b57188e4fd9f.png align="center")

---

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.