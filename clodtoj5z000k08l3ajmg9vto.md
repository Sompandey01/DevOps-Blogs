---
title: "Terraform Hands-on Project :- Build Your Own AWS Infrastructure"
datePublished: Tue Oct 31 2023 04:22:15 GMT+0000 (Coordinated Universal Time)
cuid: clodtoj5z000k08l3ajmg9vto
slug: terraform-hands-on-project-build-your-own-aws-infrastructure
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698726050110/1481b6fa-2e7a-4af9-bb8c-6bbde0d0399a.png
tags: aws, devops, terraform, infrastructure-as-code, 90daysofdevops

---

Welcome back to your Terraform journey.

In the previous tasks, you have learned about the basics of Terraform, its configuration file, and creating an EC2 instance using Terraform. Today, we will explore more about Terraform and create multiple resources.

## Task-01: Create a VPC (Virtual Private Cloud) with CIDR block 10.0.0.0/16

* Add the following code to your Terraform configuration in main.tf file.
    

```yaml
resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "main"
  }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698587252797/0e569cf5-9393-4066-a2f2-45479b522e7b.png align="center")

* Execute terraform init, plan, apply to build the VPC.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698587347273/bb005441-8a9e-499c-821e-cb8ea409cfa6.png align="center")

* Go to VPC console and check new VPC with name ‘main’ is successfully created.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698587406454/073cd007-e609-4b0b-9228-4fa1a9786fe0.png align="center")

## Task-02: **Create a public subnet with CIDR block 10.0.1.0/24 in the above VPC.**

* Add the following code to your Terraform configuration in [main.tf](http://main.tf) file
    

```yaml
resource "aws_subnet" "public_subnet" {
  vpc_id      = aws_vpc.main.id
  cidr_block  = "10.0.1.0/24"
  tags = {
    Name = "Public Subnet"
  }
}
```

* This code creates a public subnet resource named “public\_subnet”
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698587489242/4b2d7c88-94da-41cf-b792-a46851072b82.png align="center")

* Execute terraform init, plan, apply to build.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698587610432/09aa1c0b-c435-48e6-be4e-74cb1629fb00.png align="center")

* Go to subnet console and check new subnet with name ‘Public Subnet’ is successfully created.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698587736286/a54af99d-ff68-4a78-81d6-193819b6fbc5.png align="center")

## Task-03: **Create a private subnet with CIDR block 10.0.2.0/24 in the above VPC.**

* Add the following code to your Terraform configuration in [main.tf](http://main.tf) file
    

```yaml
resource "aws_subnet" "private_subnet" {
  vpc_id      = aws_vpc.main.id
  cidr_block  = "10.0.2.0/24"
  availability_zone = "ap-south-1a"

  tags = {
    Name = "Private Subnet"
  }
}
```

* This code creates a public subnet resource named “private\_subnet” with the specified CIDR block.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698587862016/7d1a7d68-70c5-457e-9153-df315b611fef.png align="center")

* Execute terraform init, plan, apply to build.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698587914803/7d37be86-5ce6-4c17-8ead-ef69b1d7b90b.png align="center")

* Go to subnet console and check new subnet with name ‘Private Subnet’ is successfully created.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698587951776/7d28d58f-53d0-4ddc-aa5c-0f86854d0d7d.png align="center")

## Task-04: Create an Internet Gateway (IGW) and attach it to the VPC.

* Add the following code to your Terraform configuration in [main.tf](http://main.tf) file
    

```yaml
resource "aws_internet_gateway" "gw" {
  vpc_id = aws_vpc.main.id

  tags = {
    Name = "igw"
  }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698588042985/342d665a-df3e-478a-ae0e-036fbc828e1f.png align="center")

* Execute terraform init, plan, apply to build.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698588111534/a11a7e69-4a30-4ffe-a379-56101b07176d.png align="center")

* Go to Internet gateways console and check new subnet with name ‘My internet Gateway’ is successfully created.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698588196652/e0e1a721-9a4a-495e-b670-ecf861567eb3.png align="center")

## Task-05: Create a route table for the public subnet and associate it with the public subnet. This route table should have a route to the Internet Gateway.

```yaml
resource "aws_route_table" "public" {
  vpc_id = aws_vpc.main.id

  route {
    cidr_block  = "0.0.0.0/0"
    gateway_id  = aws_internet_gateway.gw.id
  }

  tags = {
    Name = "route-table"
  }
}

resource "aws_route_table_association" "public" {
  subnet_id      = aws_subnet.public_subnet.id
  route_table_id = aws_route_table.public.id
}
```

**First create a route table for public subnet.**

aws\_route\_table block creates a new route table in the VPC specified by vpc\_id attribute. It also defines a route that sends all traffic with destination CIDR 0.0.0.0/0 to the internet gateway specified by gateway\_id attribute. The tags attribute sets a name for the route table for easy identification.

**Then associate route table with public subnet.**

aws\_route\_table\_association block associates the newly created route table with a public subnet specified by the subnet\_id attribute. The route\_table\_id attribute refers to the ID of the route table created in the previous block.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698588456683/ff27b5ed-0848-453b-b989-02dd55d73377.png align="center")

* Execute terraform init, plan, apply to build.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698588567555/bf254387-e5e2-46fd-a533-c21b8ee80e50.png align="center")

* We can verify the route table in AWS console along with the public subnet which is associated in the subnet association section.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698588607892/2cc56dcb-9bdd-45f8-8e57-3a84d6c904c7.png align="center")

## Task-06: Launch an EC2 instance in the public subnet with the following details:

\- AMI: ami-0557a15b87f6559cf  
\- Instance type: t2.micro

**aws\_instance block** creates a new EC2 instance in the public subnet specified by subnet\_id attribute. It uses the Amazon Machine Image (AMI) ID ami-0f8ca728008ff5af4, which is a Ubuntu 18.04 LTS image. The key\_name attribute specifies the name of the key pair used to SSH into the instance. The vpc\_security\_group\_ids attribute specifies a list of security groups to attach to the instance, in this case, it refers to the ID of the security group created in the next block.

```yaml
resource “aws_instance” “web_server” {
 ami = “ami-0f8ca728008ff5af4”
 instance_type = “t2.micro”
 subnet_id = aws_subnet.public_subnet.id
 vpc_security_group_ids = [aws_security_group.ssh_access.id]
```

## Task-07: Security group: Allow SSH access from anywhere

**aws\_security\_group block** creates a new security group that allows inbound traffic on ports 22 (SSH) and 80 (HTTP) from any source (0.0.0.0/0). The name\_prefix attribute sets a name prefix for the security group, and the vpc\_id attribute specifies the ID of the VPC where the security group will be created.

```yaml
resource "aws_security_group" "ssh_access" {
   name_prefix = "ssh_access"
   vpc_id = aws_vpc.main.id
   ingress {
     from_port   = 80
     to_port     = 80
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
     from_port   = 0
     to_port     = 0
     protocol    = -1
     cidr_blocks = ["0.0.0.0/0"]
 }
 }
```

## Task-08: User data: Use a shell script to install Apache and host a simple website

The user\_data attribute specifies the script to run when the instance is launched. This script updates the package manager, installs Apache web server, creates a basic HTML file, and restarts Apache.

```yaml
user_data = <<-EOF
    #!/bin/bash

    # Update the package list
    sudo apt update

    # Install Apache
    sudo apt install -y apache2
    sudo cat <<HTML > /var/www/html/index.html
    <!DOCTYPE html>
    <html><body><h1>Welcome to my website</h1></body></html>
    HTML

    sudo systemctl restart apache2
  EOF
```

## Task-09: **Create an Elastic IP and associate it with the EC2 instance.**

**aws\_eip block** creates a new Elastic IP address and associates it with the instance created in the first block by specifying the instance ID in the instance attribute. The tags attribute sets a name for the Elastic IP for easy identification.

```yaml
resource "aws_eip" "eip" {
   instance = aws_instance.web_server.id
   vpc      = true
   tags = {
     Name = "elastic-ip"
   }
```

## Task-10: Combine all the configurations to spin up the EC2 instance.

* Launch an EC2 instance in the public subnet with the following details:
    
* AMI: ami-0557a15b87f6559cf
    
* Instance type: t2.micro
    
* Security group: Allow SSH access from anywhere
    
* User data: Use a shell script to install Apache and host a simple website
    
* Create an Elastic IP and associate it with the EC2 instance.
    

```yaml
resource "aws_security_group" "ssh_access" {
   name_prefix = "web-server-sg"
   vpc_id = aws_vpc.main.id
   ingress {
     from_port   = 80
     to_port     = 80
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
     from_port   = 0
     to_port     = 0
     protocol    = -1
     cidr_blocks = ["0.0.0.0/0"]
 }
 }

 resource "aws_instance" "web_server" {
  ami                    = "ami-053b0d53c279acc90"
  instance_type          = "t2.micro"
  subnet_id              = aws_subnet.public_subnet.id
  vpc_security_group_ids = [aws_security_group.ssh_access.id]


 user_data = <<-EOF
    #!/bin/bash

    # Update the package list
    sudo apt update

    # Install Apache
    sudo apt install -y apache2
    sudo cat <<HTML > /var/www/html/index.html
    <!DOCTYPE html>
    <html><body><h1>Welcome to my website</h1></body></html>
    HTML

    sudo systemctl restart apache2
  EOF

 tags = {
    Name = "terraform-instance"
  }
}
 resource "aws_eip" "ip" {
   instance = aws_instance.web_server.id
   vpc      = true
   tags = {
     Name = "elastic-ip"
   }
 }
```

* Execute terraform init, plan, apply to build.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698667947476/5603eeba-6b0a-4bec-9c49-924b6ca6ecf5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698668032080/64ab448c-a7ce-4889-bc2a-ac37c6d952ff.png align="center")

## Task-11: Open the website URL in a browser to verify that the website is hosted successfully.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698667980115/e1d06d52-b597-45ba-bb18-e10c2bfe79ef.png align="center")

---

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.