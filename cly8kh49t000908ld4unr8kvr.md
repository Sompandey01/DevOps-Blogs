---
title: "DevOps Project 6 - Deploying a Node.js App on AWS ECS Fargate and ECR"
datePublished: Fri Jul 05 2024 10:42:45 GMT+0000 (Coordinated Universal Time)
cuid: cly8kh49t000908ld4unr8kvr
slug: devops-project-6-deploying-a-nodejs-app-on-aws-ecs-fargate-and-ecr
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720176063493/884fb695-f915-4c23-b3b4-f3c666f0e5a5.avif
tags: docker, aws, devops, ecs, 90daysofdevops

---

## **Project Description**

In this project, our goal is to deploy a Node.js application on AWS ECS Fargate and store its Docker image in AWS ECR. Amazon ECS (Elastic Container Service) is a fully managed container orchestration service that enables you to easily run, scale, and secure Docker containers on AWS. AWS Fargate is a serverless compute engine for containers, allowing you to focus on deploying your applications without having to manage the underlying infrastructure.

Before we start, you can read more about the tech stack we'll be using in this [**link**](https://faun.pub/what-is-amazon-ecs-and-ecr-how-does-they-work-with-an-example-4acbf9be8415). It will provide you with a better understanding of the AWS ECS and ECR services and their capabilities.

## Hands-on Project: Deploying a Node.js App on AWS ECS Fargate and ECR

### Step 1: Create EC2 Instance and Install AWS CLI and Docker

Create an EC2 instance and Install the AWS Command Line Interface (CLI) and Docker. I will use the below script and provide it via User Data to install at boot.

```yaml
  #!/bin/bash
  echo "AWS CLI Installation"
  echo "***********************"
  sudo apt install -y unzip
  curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
  unzip awscliv2.zip
  sudo ./aws/install
  echo "Docker installation"
  echo "***********************"
  sudo apt update
  sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
  echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  sudo apt update
  sudo apt install -y docker-ce docker-ce-cli containerd.io
  sudo systemctl start docker
  sudo systemctl enable docker
  sudo usermod -aG docker ubuntu
  sudo reboot
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720172001931/6873b28d-3e16-4ffa-a359-668da46a534d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720172405066/fc04aa5e-c07f-4ce4-bb09-64568d0350dd.png align="center")

### **Step 2: Clone the GitHub Repository**

Start by obtaining the Node.js application from the GitHub repository provided. Clone it to your AWS EC2 instance where we will be configuring AWS ECR.

```yaml
git clone https://github.com/Sompandey01/node-todo-cicd.git
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720172499918/045bc7cc-7c78-4778-b693-f9628e0d41e1.png align="center")

### **Step 3: Configure AWS ECR**

Navigate to the AWS Elastic Container Registry (ECR) and create a repository.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720172604156/8b44b6a7-729f-4573-b26b-416e415a42c3.png align="center")

Click on create a repository, Choose the repository type and name it accordingly.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720172908753/2c256dd8-1722-415e-b849-ac1460217559.png align="center")

Verify the repository has been successfully created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720172928381/3de49f90-044d-4fd0-8a00-5766bf2dd7f7.png align="center")

### **Step 4: Set Up IAM**

Create an IAM user in the AWS Management Console and attach the required policies for our project.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720173199026/dfcb829f-66ec-4a7d-a8dd-744cadac430d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720173247557/33480f81-701a-4ef4-b9ba-6056fe03669e.png align="center")

### **Step 5: Configure AWS CLI**

Install the AWS Command Line Interface (CLI) on the AWS EC2 instance where the Node.js app resides. Connect the EC2 instance to the AWS Management Console using the AWS CLI.

```yaml
aws configure
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720173555535/64d8ce71-d4ff-4cbf-a044-52461c2f7cd2.png align="center")

### **Step 6: Push the Image to ECR**

Navigate to the ECR repository created earlier and select "View push commands".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720173613314/c6ee9163-6e9a-41dc-b62a-02b224666ff7.png align="center")

Use the following steps to authenticate and push an image to your repository. For additional registry authentication methods, including the Amazon ECR credential helper, see the [**Amazon ECR Official Documentation**](http://docs.aws.amazon.com/AmazonECR/latest/userguide/Registries.html#registry_auth).

1. Retrieve an authentication token and authenticate your Docker client to your registry. Use the AWS CLI:
    

```yaml
aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/c1i1t2g1
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720173704220/9ad1e79f-6e78-41c8-b604-af215d71510e.png align="center")

Build your Docker image using the following command. For information on building a Docker file from scratch, see the instructions [**here**](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/docker-basics.html). [You](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/docker-basics.html) can skip this step if your image has already been built:

```yaml
docker build -t sompandey01/node-todo-app .
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720173814484/9f780895-1a63-4e59-a50b-d49684526e45.png align="center")

After the build is completed, tag your image so you can push the image to this repository:

```yaml
docker tag sompandey01/node-todo-app:latest public.ecr.aws/c1i1t2g1/sompandey01/node-todo-app:latest
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720173855010/898ae4c2-ff32-4bb6-bb55-006802b82bd4.png align="center")

Run the following command to push this image to your newly created AWS repository:

```yaml
docker push public.ecr.aws/c1i1t2g1/sompandey01/node-todo-app:latest
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720173918044/bbcba489-e118-4470-b812-d618afaf3a96.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720173950956/718293cc-7736-4425-b653-1f779522a40f.png align="center")

### **Step 7: Configure AWS ECS**

Move on to the AWS Elastic Container Service (ECS) repository in the AWS console. Create a cluster with a relevant name, and choose the Virtual Private Cloud (VPC) and subnet where you want your application to be available.

To avoid the cost impact of multiple EC2 instances, we will use AWS Fargate, which is a serverless technique for managing applications without spinning off instances. Select AWS Fargate as the launch type for the cluster to run on.**Step 7: Configure AWS ECS**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720174111807/337c2352-acdf-4388-805e-3e10d765bf0d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720174224628/1bdfeb91-8f0e-45e1-ba5a-c7bccba4acae.png align="center")

Create a task definition for your cluster:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720174303364/de23cb02-28cb-4bc4-9194-9602cfc7a3c4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720174341779/8507d836-8e1f-400d-a5e3-a9646874cee2.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720174504025/0330210a-b78c-4e07-847a-24eacd25b349.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720174544896/28c4ea6c-7868-4aca-a65c-5b746350fdc9.png align="center")

### **Step 8: Deploy and Run the Task**

Click on the "Deploy" button, and then choose "Run task" to deploy the task on the cluster. Select the cluster, and set the launch type to Fargate. Confirm the deployment.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720174641034/066e5ea9-c286-492c-a271-04e7c8857224.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720174660224/4c693890-f331-462f-ac2a-d72838ee51b0.png align="center")

Verify the task is up and running.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720174786292/67ddd4ef-371b-4fd5-bea8-3a42c9267988.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720174801857/60ba77c6-5019-4250-825f-9298305709ad.png align="center")

### **Step 9: Open the Port in the Security Group**

Ensure port 8000 is open in the Security Group used in our task.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720174978123/36af5ae8-f4aa-4314-b507-455fbb05aa2e.png align="center")

### **Step 10: Project Live Execution**

Finally, navigate to the task that was created, and take note of the public IP. Your Node.js app is now live and accessible!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720175155456/586b4121-6cb0-449b-af45-e410dcc965c7.png align="center")

Congratulations on completing Day 85 of the #90DaysOfDevOps challenge! In this project, we successfully deployed a Node.js app on AWS ECS Fargate and ECR, leveraging the power of AWS cloud services.

---

Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.