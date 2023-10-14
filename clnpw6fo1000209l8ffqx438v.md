---
title: "Important Terraform Commands"
datePublished: Sat Oct 14 2023 10:25:42 GMT+0000 (Coordinated Universal Time)
cuid: clnpw6fo1000209l8ffqx438v
slug: important-terraform-commands
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697198370332/6e3147e8-2058-40b2-b7fe-d26310b3889b.jpeg
tags: software-development, devops, terraform, 90daysofdevops, trainwithshubham

---

Hope you've already got the gist of What Working with Terraform would be like. Let's begin with day 2 of Terraform!

## Task: Find the purpose of basic Terraform commands which you'll use often.

**1) terraform init:-** This initializes Terraform and downloads any necessary providers. It must be run before most other commands.

* **Command:**
    

```yaml
terraform init
```

**\-&gt; Let's create a test.tf file in our EC2 instance and run the commands:**

```bash
resource "local_file" "devops" {
 filename = "/home/ubuntu/terraform/first_file.txt"
 content = "this is my file"
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697197247483/aedde64f-3b17-4c8c-ac0c-35b00815204d.png align="center")

* Now, run the above command...
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697197214022/3127f305-cce7-4e6e-b921-09546bd0cdd9.png align="center")

**2) terraform init -upgrade:-** Upgrades Terraform to the latest version.

* **Command:**
    

```bash
terraform init -upgrade
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697197365664/721e0977-7800-4eac-b34e-ca511a88423d.png align="center")

**3) terraform plan:-** Generates an execution plan to show what Terraform would do if you ran apply. This allows you to preview the changes.

* **Command:**
    

```bash
terraform plan
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697197453140/d7affea9-db2c-41d6-a80b-91e87302c566.png align="center")

**4) terraform apply:-** Applies the changes required to reach the desired state specified in the configuration files.

* **Command:**
    

```bash
terraform apply
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697197545949/e2344b21-701f-43ad-8489-96d2c2c03525.png align="center")

We have applied the terraform, Let’s check if the file is created in our /home/ubuntu/terraform directory

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697197695223/aeffc97f-3900-4302-97c7-51c4e5353c97.png align="center")

Our file has been successfully created.

**5) terraform validate:-** Validates the configuration files and checks for syntax errors.

* **Command:**
    

```bash
terraform validate
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697197748814/fd65dd7d-c2a2-4a84-911a-7f47dd391529.png align="center")

**6) terraform fmt:-** Formats the configuration files to follow the Hashicorp style guide.

* **Command:**
    

```bash
terraform fmt
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697197833266/3ba8cafe-3769-46a2-b072-8a9cb8449a0f.png align="center")

**7) terraform destroy:-** Destroys all the resources managed by Terraform that were created with apply.

* **Command:**
    

```bash
terraform destroy
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697197996200/6d8a7ba5-7860-4c17-b657-0bdcd74905b6.png align="center")

**In summary:**

* init initializes Terraform and downloads providers
    
* plan previews the changes
    
* apply applies the changes to create/update infrastructure
    
* validate checks for syntax errors
    
* fmt formats the configuration files
    
* destroy deletes all resources created by Terraform
    

## Who are Terraform’s main competitors?

The main competitors of Terraform are:

* **Ansible -** For configuration management
    
* **Packer -** For infrastructure templates and images
    
* **Cloud Foundry -** For PaaS deployment
    
* **Kubernetes -** For container orchestration
    

---

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.