---
title: "Automating Terraform Deployments with GitHub Actions: A Multi-Region AWS Approach"
datePublished: Wed Mar 26 2025 13:21:19 GMT+0000 (Coordinated Universal Time)
cuid: cm8pydx8j000409jsg0lr8obl
slug: automating-terraform-deployments-with-github-actions-a-multi-region-aws-approach
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1742977031502/14298bf9-c8cb-43c7-b9bf-6888169a1690.png
tags: aws, projects, automation, devops, terraform

---

## Overview

In this blog, we will walk through the process of deploying AWS infrastructure in multiple regions using **Terraform** and **GitHub Actions**. We leverage **AWS Control Tower** to manage our **Staging** and **Production** accounts, create IAM users with specific permissions, store AWS credentials securely in **GitHub Secrets**, and automate the infrastructure deployment process with GitHub Actions.

By the end of this blog, you will:

* Understand how to set up AWS Control Tower accounts
    
* Learn to create IAM users with necessary permissions
    
* Store AWS credentials securely in GitHub Secrets
    
* Implement a Terraform deployment workflow using GitHub Actions
    
* Troubleshoot common issues such as S3 bucket conflicts
    

---

## Architecture Overview

We have two environments:

1. **Staging**
    
    * AWS Accounts: Staging
        
    * Regions: `ap-south-1` and `ap-southeast-1`
        
    * S3 Buckets: `staging-tfstate-region-1` & `staging-tfstate-region-2`
        
    * DynamoDB Tables: `terraform-lock-region-1` & `terraform-lock-region-2`
        
2. **Production**
    
    * AWS Accounts: Production
        
    * Regions: `ap-south-1` and `ap-southeast-1`
        
    * S3 Buckets: `prod-tfstate-region-1` & `prod-tfstate-region-2`
        
    * DynamoDB Tables: `terraform-lock-region-1` & `terraform-lock-region-2`
        

Each AWS account is managed using **AWS Control Tower**, and Terraform configurations are stored in **separate directories** for each environment.

---

## Setting Up AWS Control Tower & IAM Users

### Step 1: AWS Control Tower Account Setup

AWS Control Tower helps in managing multiple AWS accounts under an **organization**. Here’s a Step-by-Step Guide to setup [AWS Control Tower](https://hashnode.com/edit/cm2ugwh2w000609lcfjdwg3u4). We created two separate accounts under our AWS Control Tower setup:

* **Staging Account** (for testing)
    
* **Production Account** (for live deployments)
    

### Step 2: Creating IAM Users in Staging & Production Accounts

To allow GitHub Actions to deploy Terraform resources, we created IAM users in both **Staging** and **Production** accounts with specific permissions.

1. **Go to AWS IAM Console** in each account.
    
2. Create a new IAM **User** (e.g., `terraform-github-actions-staging, terraform-github-actions-prod`)
    
3. Attach the following permissions:
    
    * `AdministratorAccess` (for full control) or
        
    * Custom policy with `IAM`, `EC2`, `S3`, `CloudFormation`, and `VPC` permissions
        
4. **Create the Access Keys** using Third-party service and **save the Access Key ID and Secret Access Key**.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731309280017/805ab250-f297-4460-b40e-39452f145b6e.png?auto=compress,format&format=webp align="left")
    

---

## Storing AWS Credentials in GitHub Secrets

Since we do not want to hardcode AWS credentials, we store them securely in **GitHub Secrets**.

1. Navigate to **GitHub Repository → Settings → Secrets and Variables → Actions**
    
2. Click **"New repository secret"** and add:
    
    * `AWS_ACCESS_KEY_ID_STAGING` → IAM user's Access Key for Staging
        
    * `AWS_SECRET_ACCESS_KEY_ID_STAGING` → Secret Key for Staging
        
    * `AWS_ACCESS_KEY_ID_PROD` → IAM user's Access Key for Production
        
    * `AWS_SECRET_ACCESS_KEY_ID_PROD` → Secret Key for Production
        
    
    ![Add AWS Credentials](https://github.com/Sompandey01/images/raw/3a6a0ecf52d6a4de740d4c1b6f771b69c9ad84c6/Screenshot%20(247).png align="left")
    

---

## Terraform Code Structure

We have four Terraform files for different regions:

* `terraform/Staging-region1/main.tf`
    
* `terraform/Staging-region2/main.tf`
    
* `terraform/Prod-region1/main.tf`
    
* `terraform/Prod-region2/main.tf`
    

Each file contains:

```yaml
provider "aws" {
  region = "ap-south-1" # Change as per deployment region
}

resource "aws_s3_bucket" "s3_bucket" {
  bucket = "prod-tfstate-region-1" # Change bucket name for each region
}

resource "aws_dynamodb_table" "terraform_lock" {
  name           = "terraform-lock-region-1"
  billing_mode   = "PAY_PER_REQUEST"
  hash_key       = "LockID"

  attribute {
    name = "LockID"
    type = "S"
  }
}
```

**Changes per file:**

* **Staging-region1:** `staging-tfstate-region-1`
    
* **Staging-region2:** `staging-tfstate-region-2`
    
* **Prod-region1:** `prod-tfstate-region-1`
    
* **Prod-region2:** `prod-tfstate-region-2`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742975024485/0193a704-713f-4489-b1a5-fa02fd3a6944.png align="center")

## GitHub Actions Workflow (Terraform Deployment)

We now set up a GitHub Actions workflow to **automate infrastructure deployment**. This workflow:

* Installs dependencies (AWS CLI, Terraform)
    
* Configures AWS credentials
    
* Deploys infrastructure in different AWS regions (ap-south-1 & ap-southeast-1)
    

### **Workflow File** (`.github/workflows/main.yml`

```yaml
name: Terraform Deployment

on:
  push:
    branches:
      - main

jobs:
  setup:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
      
      - name: Install dependencies
        run: |
          sudo apt-get update
          sudo apt-get install -y unzip curl
          curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
          unzip awscliv2.zip
          sudo ./aws/install --update
          rm -rf awscliv2.zip aws
          aws --version
        
  validate_apply_staging_1:
    needs: setup
    runs-on: ubuntu-latest
    environment: staging
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Install Terraform
        run: |
         sudo apt-get update
         sudo apt-get install -y unzip curl
         curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
         sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
         sudo apt-get update && sudo apt-get install -y terraform
         terraform --version
      
      - name: Configure AWS Credentials
        run: |
          aws configure set aws_access_key_id ${{ secrets.AWS_ACCESS_KEY_ID_STAGING }}
          aws configure set aws_secret_access_key ${{ secrets.AWS_SECRET_ACCESS_KEY_ID_STAGING }}
          aws configure set region ap-south-1
          aws sts get-caller-identity
      
      - name: Terraform Apply (Staging Region 1)
        run: |
          cd terraform/Staging-region1
          terraform init
          terraform validate
          terraform apply -auto-approve

  validate_apply_staging_2:
    needs: setup
    runs-on: ubuntu-latest
    environment: staging
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Install Terraform
        run: |
         sudo apt-get update
         sudo apt-get install -y unzip curl
         curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
         sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
         sudo apt-get update && sudo apt-get install -y terraform
         terraform --version
      
      - name: Configure AWS Credentials
        run: |
          aws configure set aws_access_key_id ${{ secrets.AWS_ACCESS_KEY_ID_STAGING }}
          aws configure set aws_secret_access_key ${{ secrets.AWS_SECRET_ACCESS_KEY_ID_STAGING }}
          aws configure set region ap-southeast-1
          aws sts get-caller-identity
      
      - name: Terraform Apply (Staging Region 2)
        run: |
          cd terraform/Staging-region2
          terraform init
          terraform validate
          terraform apply -auto-approve

  validate_apply_production_1:
    needs: setup
    runs-on: ubuntu-latest
    environment: production
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Install Terraform
        run: |
         sudo apt-get update
         sudo apt-get install -y unzip curl
         curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
         sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
         sudo apt-get update && sudo apt-get install -y terraform
         terraform --version
      
      - name: Configure AWS Credentials
        run: |
          aws configure set aws_access_key_id ${{ secrets.AWS_ACCESS_KEY_ID_PROD }}
          aws configure set aws_secret_access_key ${{ secrets.AWS_SECRET_ACCESS_KEY_ID_PROD }}
          aws configure set region ap-south-1
          aws sts get-caller-identity
      
      - name: Terraform Apply (Production Region 1)
        run: |
          cd terraform/Prod-region1
          terraform init
          terraform validate
          terraform apply -auto-approve

  validate_apply_production_2:
    needs: setup
    runs-on: ubuntu-latest
    environment: production
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Install Terraform
        run: |
         sudo apt-get update
         sudo apt-get install -y unzip curl
         curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
         sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
         sudo apt-get update && sudo apt-get install -y terraform
         terraform --version
         
      - name: Configure AWS Credentials
        run: |
          aws configure set aws_access_key_id ${{ secrets.AWS_ACCESS_KEY_ID_PROD }}
          aws configure set aws_secret_access_key ${{ secrets.AWS_SECRET_ACCESS_KEY_ID_PROD }}
          aws configure set region ap-southeast-1
          aws sts get-caller-identity
      
      - name: Terraform Apply (Production Region 2)
        run: |
          cd terraform/Prod-region2
          terraform init
          terraform validate
          terraform apply -auto-approve
```

## Expected Results

After running the GitHub Actions workflow:

* **S3 Buckets** for Terraform state storage will be created.
    
* **DynamoDB Tables** for Terraform state locking will be configured.
    
* Resources will be deployed successfully in multiple AWS accounts and regions.
    

![Run GitHub Workflow](https://github.com/Sompandey01/images/raw/3a6a0ecf52d6a4de740d4c1b6f771b69c9ad84c6/Screenshot%20(248).png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742974821503/69999d11-a7d4-4458-b074-e0ecd97ffe89.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1742974834609/ca8a7bf9-3e43-42ef-8d0d-346412636d60.png align="center")

## Troubleshooting Common Issues

### 1\. **Bucket Already Exists**

**Error:**

```yaml
Error: BucketAlreadyExists: The requested bucket name is not available.
```

**Solution:**

* S3 bucket names are globally unique. Modify bucket names in Terraform files.
    

### 2\. **Incorrect AWS Credentials**

**Error:**

```yaml
Unable to authenticate AWS credentials.
```

**Solution:**

* Verify AWS keys in **GitHub Secrets**.
    
* Check IAM permissions for Terraform execution.
    

### 3\. **Terraform Lock Issues**

**Error:**

```yaml
Error acquiring the state lock: DynamoDB table does not exist.
```

**Solution:**

* Ensure **DynamoDB Table** exists before running Terraform.
    

---

## Conclusion

By following this guide, you can successfully deploy infrastructure across multiple AWS regions using Terraform and GitHub Actions. This setup ensures secure state management, automation, and scalability.