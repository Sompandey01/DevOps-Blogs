---
title: "AWS S3 Bucket Creation and Management"
datePublished: Thu Nov 02 2023 12:33:28 GMT+0000 (Coordinated Universal Time)
cuid: cloh63xu4000709mf0rcv7dgk
slug: aws-s3-bucket-creation-and-management
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698928370188/9b2b440e-60f4-48e7-9fb6-8b816e074f5b.png
tags: aws, devops, terraform, iac, 90daysofdevops

---

## AWS S3 Bucket

Amazon S3 (Simple Storage Service) is an object storage service that offers industry-leading scalability, data availability, security, and performance. It can be used for a variety of use cases, such as storing and retrieving data, hosting static websites, and more.

In this task, you will learn how to create and manage S3 buckets in AWS.

## Task-01: Create an S3 bucket using Terraform.

Install Terraform in your EC2 instance and Configure your AWS access key and secret access key using the AWS CLI or environment variables.

* Create a file named `main.tf` and add the following code:
    

```yaml
resource "aws_s3_bucket" "my_bucket" {
  bucket = "my-demo-bucket-som"
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698922546165/37eb5460-b3b6-4c7a-a20c-9ee13a686c4a.png align="center")

* Run terraform init, plan and apply.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698922272537/298abf70-e850-46c4-ad9c-f5f13960aaae.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698922301390/9be1075d-d707-4a84-a3bf-7ad27afe5625.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698922490697/00f68da8-6c2c-4ad1-92b7-0e4d290ab15d.png align="center")

* S3 bucket successfully created.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698922567183/6d54522d-08e2-4d73-b179-8f84aa727752.png align="center")

## Task-02: Configure the bucket to allow public read access.

* You have to give permissions for your IAM user.
    
* Go to the IAM console and select your user. In Permission policies click on Create inline Policy for the user.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698922732779/fdba3289-c052-4567-8395-b8534e337679.png align="center")

```yaml
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "UpdateS3BucketPolicy",
            "Effect": "Allow",
            "Action": [
                "s3:PutBucketPolicy"
            ],
            "Resource": [
                "arn:aws:s3:::my-demo-bucket-som"
            ]
        }
    ]
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698923051520/de7ebde9-3eaa-4adb-a506-4e57cd1bbc08.png align="center")

* Click on Create Policy, give it a name and done.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698923009478/96f0db05-d96c-4c63-b8e3-0b2665fecae2.png align="center")

* Let’s allow public access to s3 bucket and edit the [main.tf](http://main.tf) file with code bellowed.
    

```yaml
resource "aws_s3_bucket_public_access_block" "example" {
  bucket = aws_s3_bucket.my_bucket.id

  block_public_acls       = false
  block_public_policy     = false
  ignore_public_acls      = false
  restrict_public_buckets = false
}

resource "aws_s3_bucket_policy" "bucket_policy" {
  bucket = aws_s3_bucket.my_bucket.id

  policy = <<EOF
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicRead",
      "Effect": "Allow",
      "Principal": "*",
      "Action": ["s3:GetObject"],
      "Resource": [
        "arn:aws:s3:::my-demo-bucket-som/*"
      ]
    }
  ]
}
EOF
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698923550857/45b68c6b-a004-44c0-9bd7-234fefa3780b.png align="center")

* Run terraform init, plan and apply.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698924008472/a5ce1f13-f3a8-4632-9308-244175da5bb5.png align="center")

* Bucket is publicly accessible now.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698924042471/4270c4f5-abe5-408c-b20f-7d001b54acc4.png align="center")

## Task-03: Create an S3 bucket policy that allows read-only access to a specific IAM user or role.

```yaml
resource "aws_s3_bucket_policy" "bucket_policy" {
  bucket = aws_s3_bucket.my_bucket.id

  policy = <<EOF
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicRead",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::414694853813:user/Terraform-User" #change access "*" to specific IAM user
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-demo-bucket-som/*"
    }
  ]
}
EOF
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698924476079/315a62d2-fb7e-4f58-a5aa-cb4fab931b13.png align="center")

* Run terraform init, plan and apply.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698924537081/f502468f-6137-4a4d-9755-14af1948c024.png align="center")

* S3 bucket policy is created that allows read-only access to a specific IAM user.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698924650480/06383273-2a47-45ae-96a6-9d99bba876c2.png align="center")

## Task-04: Enable versioning on the S3 bucket.

```yaml
 resource "aws_s3_bucket" "my_bucket" {
    bucket = "my-demo-bucket-som"
    versioning {
      enabled = true
    }
  }
```

* The versioning block is included, with enabled set to true. This enables versioning on the S3 bucket, which will keep multiple versions of each object stored in the bucket.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698924863999/16e3a16e-25bf-4f49-8739-91ae9fece9d5.png align="center")

* Run terraform init, plan and apply.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698924923922/1136dfb5-7bed-4281-bd19-103ba227aa5d.png align="center")

* We can see the changes in the S3 bucket in the AWS management console.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698925062316/95cd359c-4d0d-4e05-9be2-80f8ccd0cb16.png align="center")

---

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.