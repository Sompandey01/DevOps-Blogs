---
title: "DevOps Project 7 - Automating Portfolio Deployment on AWS S3 using GitHub Actions"
datePublished: Sun Jul 07 2024 12:03:43 GMT+0000 (Coordinated Universal Time)
cuid: clybi8xnr000209lac7mt773r
slug: devops-project-7-automating-portfolio-deployment-on-aws-s3-using-github-actions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720353632467/300d2783-6527-4883-94bc-d5f23b9a3689.jpeg
tags: aws, devops, aws-iam, devops-journey, 90daysofdevops

---

## **Project Description**

In this project, our main objective is to deploy a Portfolio app on AWS S3, a powerful and scalable storage service provided by Amazon Web Services. Leveraging GitHub Actions, we'll automate the entire process of building and deploying our Portfolio to AWS S3. With this automation, any changes we make to our GitHub repository will trigger automatic updates to our live website, making deployment a breeze.

## Hands-on Project: Automating Portfolio Deployment on AWS S3 using GitHub Actions

### **Step 1: Get the Portfolio Application from GitHub**

To begin, let's obtain the Portfolio application from the [GitHub repository](https://github.com/Sompandey01/my-portfolio/tree/main#my-portfolio). Clone the repository to your local development environment or directly to your AWS server, where we'll configure AWS S3 and set up the GitHub Actions Workflow.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720349958176/be4cee67-91b7-4bfe-be41-8cbac5a6fb26.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720349974907/9fd8d0ad-0a74-4256-a83a-7042a4c3ac30.png align="center")

**Now, Create an S3 Bucket - "tws-portfolio-bucket1":**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720350201639/d23de7aa-2659-4337-bb66-f6436dd7db2f.png align="center")

**Configure Bucket Policy for Public Access:**

```yaml
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Sid": "PublicReadForGetBucketObjects",
              "Effect": "Allow",
              "Principal": "*",
              "Action": "s3:GetObject",
              "Resource": "arn:aws:s3:::tws-portfolio-bucket/*"
          }
      ]
  }
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720350490749/fd5ef4db-275b-48ab-aeea-be8c014a534b.png align="center")

**Create an IAM User and Generate Security Credentials:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720350781506/09a30ff5-607c-44d9-8ee4-66a5d85d145a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720350796659/c26e1cc7-bad2-43e1-9bef-524b8b9d8070.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720350859094/b352528e-ae7e-4571-8baf-dfbce8790bfd.png align="center")

**Set Up GitHub Secrets for AWS Credentials:**

1. Click on "Secrets and Variables" in the Actions menu.
    
2. Add the following secrets:
    
    * `AWS_S3_BUCKET` - Your S3 bucket name
        
    * `AWS_ACCESS_KEY_ID` - AWS CLI Access Key ID
        
    * `AWS_SECRET_ACCESS_KEY` - AWS CLI Secret Access Key
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720350917189/2f05c521-8531-4ea0-aedd-bebecab53f42.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720350986767/d4e14c7a-42f1-45ad-b7c4-6977a45df103.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720351168397/a647e4cf-3a67-407b-ad34-df052a52d51f.png align="center")

**Now Create the GitHub Actions Workflow:**

Next, navigate to the project code repository on GitHub and choose the "Actions" option from the menu. Set up a new workflow for your Portfolio app by creating a YAML file that defines the necessary steps for the deployment process.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720351209956/29c3adec-79b8-4d53-a167-4866a90b4985.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720352958667/44ddbe3e-61a8-4ca6-93ac-6c4884cbffd0.png align="center")

```yaml
name: my-portfolio-deployment # Name of the deployment

on:
  push: # Trigger the workflow when changes are pushed
    branches:
      - main

jobs: # Any name can be provided
  build-and-deploy:
    runs-on: ubuntu-latest # Latest version of Ubuntu
    steps:
      - name: Checkout # Check out the repository's code into the workflow's execution environment.
        uses: actions/checkout@v1 # Script actions

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY_ID }}
          aws-region: ap-south-1

      - name: Deploy static site to S3 bucket
        run: aws s3 sync . s3://tws-portfolio-bucket1 --delete # Change bucket name
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720352935438/64b904ad-f6df-427f-be87-50eb2f8cab66.png align="center")

### Enable Static Website Hosting for the S3 Bucket:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720353112795/a0821a86-64a6-408e-a8a0-e39dfa1a4e9b.png align="center")

### Access Your Portfolio Website:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720353158987/4d0711ea-7ae4-4505-aa8b-69c4a08036d5.png align="center")

Congratulations on completing Day 86 of the #90DaysOfDevOps Challenge. By automating the deployment of your Portfolio app on AWS S3 using GitHub Actions, you've gained valuable insights into streamlining CI/CD and efficiently managing your application's deployment. Stay tuned for tomorrow's challenge, where we'll dive into another exciting DevOps project!

---

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([**https://www.linkedin.com/in/som-shanker-pandey/**](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.