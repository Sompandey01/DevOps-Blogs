---
title: "Scaling with Terraform 🚀"
datePublished: Fri Nov 03 2023 12:53:39 GMT+0000 (Coordinated Universal Time)
cuid: cloim9qi9000809jm9k9o19xe
slug: scaling-with-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699015988716/0604114c-0601-4766-b8f4-338b52d279ff.png
tags: software-development, aws, cloud-computing, devops, terraform

---

Yesterday, we learned how to AWS S3 Bucket with Terraform. Today, we will see how to scale our infrastructure with Terraform.

## Understanding Scaling

Scaling is the process of adding or removing resources to match the changing demands of your application. As your application grows, you will need to add more resources to handle the increased load. And as the load decreases, you can remove the extra resources to save costs.

![](https://miro.medium.com/v2/resize:fit:438/1*wbD2o-a3KgqgjFXSX8BZGQ.jpeg align="center")

Terraform makes it easy to scale your infrastructure by providing a declarative way to define your resources. You can define the number of resources you need and Terraform will automatically create or destroy the resources as needed.

## Task 1: Create an Auto Scaling Group

Auto Scaling Groups are used to automatically add or remove EC2 instances based on the current demand. Follow these steps to create an Auto Scaling Group:

* In your main.tf file, add the following code to create an Auto Scaling Group:
    

```yaml
   provider "aws" {
     region = "us-east-1"
   }

   resource "aws_vpc" "day68_vpc" {
     cidr_block = "10.0.0.0/16"

     tags = {
       Name = "day68_vpc"
     }
   }

   resource "aws_subnet" "day68_public_subnet" {
     vpc_id     = aws_vpc.day68_vpc.id
     cidr_block = "10.0.1.0/24"

     tags = {
       Name = "day68_public_subnet"
     }
   }

   resource "aws_subnet" "day68_private_subnet" {
     vpc_id     = aws_vpc.day68_vpc.id
     cidr_block = "10.0.2.0/24"

     tags = {
       Name = "day68_private_subnet"
     }
   }

   resource "aws_internet_gateway" "day68_igw" {
     vpc_id = aws_vpc.day68_vpc.id

     tags = {
       Name = "day68_igw"
     }
   }

   resource "aws_route_table" "day68_routetable" {
     vpc_id = aws_vpc.day68_vpc.id

     route {
       cidr_block = "0.0.0.0/0"
       gateway_id = aws_internet_gateway.day68_igw.id
     }

     tags = {
       Name = "day68_routetable"
     }
   }

   resource "aws_route_table_association" "public_subnet_association" {
     subnet_id      = aws_subnet.day68_public_subnet.id
     route_table_id = aws_route_table.day68_routetable.id
   }

   resource "aws_security_group" "day68_sg" {
     name_prefix = "day68_sg"
     vpc_id      = aws_vpc.day68_vpc.id

     ingress {
       from_port   = 80
       to_port     = 80
       protocol    = "tcp"
       cidr_blocks = ["0.0.0.0/0"]
     }

     ingress {
       from_port   = 443
       to_port     = 443
       protocol    = "tcp"
       cidr_blocks = ["0.0.0.0/0"]
     }

     ingress {
       from_port   = 22
       to_port     = 22
       protocol    = "tcp"
       cidr_blocks = ["0.0.0.0/0"]
     }

     egress {
       from_port        = 0
       to_port          = 0
       protocol         = "-1"
       cidr_blocks      = ["0.0.0.0/0"]
       ipv6_cidr_blocks = ["::/0"]
     }
   }

   resource "aws_launch_configuration" "web_server_asg" {
     name_prefix      = "web-server-asg"
     image_id         = "ami-053b0d53c279acc90"
     instance_type    = "t2.micro"
     security_groups  = [aws_security_group.day68_sg.id]
     associate_public_ip_address = true

     user_data = <<-EOF
                   #!/bin/bash
                   sudo apt update
                   sudo apt install -y apache2
                   sudo systemctl start apache2
                   sudo systemctl enable apache2
                   echo "<html><body><h1>Welcome to my website!</h1></body></html>" > /var/www/html/index.html
                   sudo systemctl restart apache2
                   EOF
   }

   resource "aws_autoscaling_group" "web_server_asg" {
     name                 = "web-server-asg"
     launch_configuration = aws_launch_configuration.web_server_asg.name
     min_size             = 1
     max_size             = 3
     desired_capacity     = 2
     health_check_type    = "EC2"
     vpc_zone_identifier  = [aws_subnet.day68_public_subnet.id]
   }
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699013726182/330d268e-6529-4fa9-b11b-96179cf92320.png align="center")

* Run terraform init, plan and apply to create the Auto Scaling Group.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699014118515/369e6aa7-be59-4881-976f-437a6a1bb549.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699014167725/00587298-cc7a-403a-8121-f82c27871314.png align="center")

## Task-02: Test Scaling

* Go to the AWS Management Console and select the Auto Scaling Groups service.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699014247122/79c862e4-b24f-45ef-8945-32bb3c171b2c.png align="center")

* Select the Auto Scaling Group you just created and click on the “Edit” button.
    
* Increase the “Desired Capacity” to 3 and click on the “Save” button.
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699014469022/ed3aea62-56a3-4276-a334-5174f12930d5.png align="center")
    
    Wait a few minutes for the new instances to be launched.
    
* Go to the EC2 Instances service and verify that the new instances have been launched.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699014536150/b492bbf6-68ad-4085-a9e3-1cbb0a08c86f.png align="center")
    
* Decrease the “Desired Capacity” to 1 and wait a few minutes for the extra instances to be terminated.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699014595580/e5548c05-1bd7-4280-bbfb-c59e6e70494d.png align="center")

* Go to the EC2 Instances service and verify that the extra instances have been terminated.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699014676996/3df88afe-e731-4a47-9b32-0fc2d67f1175.png align="center")

Congratulations🎊🎉 You have successfully scaled your infrastructure with Terraform.

---

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.