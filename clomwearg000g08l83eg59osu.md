---
title: "Interview questions of Terraform 🔥"
datePublished: Mon Nov 06 2023 12:48:12 GMT+0000 (Coordinated Universal Time)
cuid: clomwearg000g08l83eg59osu
slug: interview-questions-of-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699274836646/95f358b6-c22b-428e-a105-6b10365f48c7.jpeg
tags: software-development, cloud-computing, devops, terraform, 90daysofdevops

---

### 1\. What is Terraform and how it is different from other IaaC tools?

Terraform is an Infrastructure as Code (IaC) tool used to provision, manage and automate infrastructure resources. In simple terms, Terraform allows you to define your infrastructure using code and then automate the process of deploying and managing that infrastructure. Here are the main things Terraform does:

* **Provision resources**: Terraform can provision infrastructure resources across multiple cloud providers like AWS, Azure, GCP, etc. You define resources in code and Terraform provisions those resources.
    
* **Manage lifecycle**: Terraform manages the entire lifecycle of resources - from creation to updates to deletion. It can detect drift from your configuration and apply necessary changes.
    
* **Use declarative syntax**: Terraform uses a declarative syntax where you define the desired end state of your infrastructure in configuration files. Terraform then determines the steps needed to achieve that state.
    
* **Support modules**: Terraform supports reusable modules that encapsulate groups of related resources. This helps promote code reusability and best practices.
    
* **Track state**: Terraform tracks the state of your infrastructure and uses that to determine what changes need to be applied. This helps ensure consistency and idempotency.
    
* **Support providers**: Terraform connects to infrastructure providers using plugins called providers. This allows Terraform to manage resources across multiple cloud providers and services.
    

### 2\. How do you call a main.tf module?

To call a Terraform module, you use the `module` resource in your main `.tf` file. The basic syntax is:

```yaml
  module "<name>" {
    source = "<path>"

    # Optional - Set input variables
    vars = {
      var1 = "value1"
      var2 = "value2"  
    }
  }
```

**For example:**

```yaml
  module "ec2_instance" {
    source = "./modules/ec2"

    instance_type = "t2.micro"  
    ami           = "ami-12345"  
  }
```

This will call the module located at `./modules/ec2`, passing the `instance_type` and `ami` variables.

The `source` can be an absolute path, URL, or a relative path from the calling module.

### 3\. What exactly is Sentinel? Can you provide few examples where we can use for Sentinel policies?

A sentinel is a special value used to indicate the end of a sequence of data. Sentinels are used in algorithms that process data iteratively, where an explicit termination condition is needed.

Some examples of sentinels and their uses:

* **Null character**: Used to indicate the end of a null-terminated string. The null character `\0` is used as the sentinel.
    
    ```yaml
    char str[] = "Hello";
    int i = 0;
    
    while (str[i] != '\0') {
      printf("%c", str[i]);
      i++; 
    }
    // Prints Hello
    ```
    
* **Negative number**: A negative number can be used as a sentinel to indicate the end of a list of non-negative numbers.
    
    ```yaml
    numbers = [1, 2, 3, -1]
    
    for num in numbers:
      if num < 0:
        break  
      print(num)  
    # Prints 1 2 3
    ```
    
* **Special value**: A value that cannot occur naturally in the data can be used as a sentinel. For example, using -1 as a sentinel for data that only contains positive integers.
    
* **EOF**: The end-of-file character can act as a sentinel, indicating the end of input.
    
    ```yaml
    int c;
    
    while ((c = getchar()) != EOF) {
      putchar(c); 
    }
    ```
    

Sentinels are useful as they allow iterative algorithms to process data of unknown length. Without a sentinel, an explicit length would need to be provided or checked after each iteration.

### 4\. You have a Terraform configuration file that defines an infrastructure deployment. However, there are multiple instances of the same resource that need to be created. How would you modify the configuration file to achieve this?

I would modify the Terraform configuration file to create multiple instances of the same resource:

1. Use a count parameter on the resource block:
    
    ```yaml
    resource "aws_instance" "web" {
     count = 2 
    
     ami           = "ami-123456"
     instance_type = "t2.micro"
    
    }
    ```
    

This will create 2 instances of aws\_instance named web with the specified AMI and instance type.

1. Use a for\_each loop on the resource block:
    
    ```yaml
    resource "aws_instance" "web" {
     for_each = {
       server1 = {
         ami           = "ami-123456"
         instance_type = "t2.micro" 
       }
       server2 = {
         ami           = "ami-123456"
         instance_type = "t2.large"  
       }
     }
    
     ami           = each.value.ami
     instance_type = each.value.instance_type
    
    }
    ```
    

This will create 2 instances named webserver1 and webserver2 with different AMI and instance types as defined in the for\_each map.

### 5\. You want to know from which paths Terraform is loading providers referenced in your Terraform configuration (\*.tf files). You need to enable debug messages to find this out. Which of the following would achieve this?

**A**. Set the environment variable TF\_LOG=TRACE

**B**. Set verbose logging for each provider in your Terraform configuration

**C**. Set the environment variable TF\_VAR\_log=TRACE

**D**. Set the environment variable TF\_LOG\_PATH

The answer is **A**. Set the environment variable TF\_LOG=TRACE

This will enable debug logging for Terraform, including information about which provider plugins are being loaded and from which paths.

### 6\. Below command will destroy everything that is being created in the infrastructure. Tell us how would you save any particular resource while destroying the complete infrastructure.

```yaml
terraform destroy
```

To save a particular resource while running `terraform destroy`, you can use the `-target` flag to specify the resource(s) you want to exclude.

For example, if you have an EC2 instance named `webserver` and an S3 bucket named `mybucket`, and you want to save the S3 bucket when running `terraform destroy`, you would run:

```yaml
  terraform destroy -target=aws_s3_bucket.mybucket
```

This will destroy all resources except the `aws_s3_bucket.mybucket` resource.

You can target multiple resources by comma separating them:

```yaml
  terraform destroy -target=aws_s3_bucket.mybucket,aws_rds_cluster.database
```

This will save both the S3 bucket and RDS cluster when running `terraform destroy`.

You can also target by resource type:

```yaml
  terraform destroy -target=aws_s3_bucket
```

This will destroy all resources except S3 buckets.

### 7\. Which module is used to store .tfstate file in S3?

The terraform-backend-s3 module is used to store the .tfstate file in S3.

To configure Terraform to store the state file in an S3 bucket, you add a backend "s3" block to your Terraform configuration:

```yaml
  terraform {
    backend "s3" {
      bucket = "my-terraform-state"
      key    = "terraform.tfstate"
      region = "us-east-1"
    }
  }
```

This tells Terraform to store the .tfstate file in the S3 bucket named "my-terraform-state" in the us-east-1 region.

Then when you run Terraform commands, it will read from and write the state file to that S3 bucket, allowing you to centrally store your infrastructure state.

The benefits of storing state in S3 are:

* Centralized storage so multiple team members can access the state
    
* **Durability** - S3's reliability ensures the state is not lost
    
* **Versioned** - S3 versioning can track changes to the state over time
    
* **Backup/Restore** - Easy to backup and restore state from S3
    

### 8\. How do you manage sensitive data in Terraform, such as API keys or passwords?

To effectively manage sensitive data in Terraform, consider these best practices. Utilize environment variables or secrets management tools to keep secrets out of configuration files. Avoid hardcoding sensitive information directly in your code. Encrypt state files and ensure secure backend configurations to protect your infrastructure's secrets. Implement proper access controls within your cloud provider to limit who can access and modify sensitive resources.

### 9\. You are working on a Terraform project that needs to provision an S3 bucket, and a user with read and write access to the bucket. What resources would you use to accomplish this, and how would you configure them?

To provision an S3 bucket and a user with read/write access in Terraform, you would use:

1. **aws\_s3\_bucket resource** - To create the S3 bucket
    
    ```yaml
    resource "aws_s3_bucket" "mybucket" {
     bucket = "my-bucket"
    }
    ```
    
2. **aws\_iam\_user resource** - To create the IAM user
    
    ```yaml
    resource "aws_iam_user" "s3user" {
     name = "s3-user"
    }
    ```
    
3. **aws\_iam\_access\_key resource** - To generate an access key for the user
    
4. **aws\_iam\_user\_policy resource** - To attach a policy granting read/write access to the S3 bucket
    
    ```yaml
    resource "aws_iam_user_policy" "s3_access" {
     name = "s3_access_policy"
     user = aws_iam_user.s3user.name
    
     policy = <<EOF
    {
     "Version": "2012-10-17",
      "Statement": [
       {
         "Action": ["s3:ListBucket", "s3:GetBucketLocation"],
         "Effect": "Allow",
         "Resource": "${aws_s3_bucket.mybucket.arn}"
       },
       {
         "Action": [
           "s3:PutObject",
           "s3:GetObject",
           "s3:DeleteObject"
         ],
         "Effect": "Allow",
         "Resource": "${aws_s3_bucket.mybucket.arn}/*"
       }
     ]
    }
    EOF
    }
    ```
    

By configuring these 4 resources, you can provision an S3 bucket and grant read/write access to an IAM user in Terraform.

### 10\. Who maintains Terraform providers?

Terraform providers are maintained by the respective cloud service providers or organizations. For example, AWS maintains the AWS provider, and Google maintains the Google Cloud provider. The providers are typically open source, and the community and contributors also play a role in maintaining them.

### 11\. How can we export data from one module to another?

To export data from one module to another in Terraform, you can use output values. In the source module, define an output block, and in the calling module, reference that output using the `module` syntax. Here's an example:

In the source module (`module1`):

```yaml
output "example_output" {
  value = "This is an example output."
}
```

In the calling module (`module2`):

```yaml
module "module1" {
  source = "./module1"
}
```

```yaml
# Access the output from module1
output "module1_output" {
  value = module.module1.example_output
}
```

In this example, `module2` can access the output value of `module1` using `module.module1.example_output`.

---

Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.