---
title: "Terraform Variables"
datePublished: Thu Oct 19 2023 12:33:13 GMT+0000 (Coordinated Universal Time)
cuid: clnx5xoxr000909l9bc2ecfoy
slug: terraform-variables
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697718767931/9f206e1b-1731-4c48-b49c-25bc80f36fa5.jpeg
tags: software-development, devops, terraform, 90daysofdevops, trainwithshubham

---

## What are variables in terraform?

Variables are a fundamental concept in Terraform that allows you to customize your infrastructure configuration. There are three main types of variables in Terraform:

* `Input Variables` - Used to pass input values to a Terraform module from outside. They act as arguments to the module.
    
* `Local Variables` - Used to assign temporary names to expressions within a module. They are scoped to the module where they are declared.
    
* `Output Variables` - Used to export values from a Terraform module. They act as return values from the module.
    

## Task-01: **Create a local file using Terraform**

* Let’s create a [`variables.tf`](http://variables.tf) file where we will define our variables.
    
* Variables can hold values such as instance names, configurations, or any other information needed for our infrastructure.
    

```bash
variable "filename" {
default = "/home/ubuntu/terraform/demo-var.txt"
}

variable "content" {
default = "This is coming from a variable which was updated"
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697700198815/6c44f895-112e-4279-80cf-7297e7208ee8.png align="center")

* In this example, there are 2 variables `filename` and `content`. Variable `filename` holds the path and variable `content` holds the content that will be written in that file.
    
* These variables can be accessed by var object in [main.tf](http://main.tf)
    

```bash
resource "local_file" "devops" {
filename = var.filename
content = var.content
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697699601321/728f7038-8d3d-4e09-b3db-0bc86af0a8a4.png align="center")

* By referencing `var.filename` and `var.content`, we can access the values stored in our variables and utilize them within our Terraform resources.
    
* Initializes a new or existing working directory for Terraform
    

```yaml
terraform init
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697699808748/05ce8142-f5ee-4e0e-8a90-6fb8dc14801e.png align="center")

* Produces an execution plan outlining the steps Terraform will take to achieve the desired state defined in the configuration file.
    

```yaml
terraform plan
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697699878776/3ea00507-57ed-465a-a6fc-15aea1b89ae0.png align="center")

* When you run Terraform apply, Terraform will generate a file in the local directory named demo-var.txt with the content supplied in the content variable.
    

```yaml
terraform apply
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697699926508/70e5bfe1-d1e1-4eff-b61f-8d9df4f499a6.png align="center")

* Check file is created in a specified folder using the ls command.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697700298889/cf29b26c-5467-4cdc-872d-79bf6c2200cf.png align="center")

## Task-02: Use terraform to demonstrate usage of List, Set and Object datatypes

Terraform supports various data types, such as maps, lists, sets, and objects, allowing us to handle complex data structures within our configurations. Let’s explore some of these data types and demonstrate their usage.

### Map -

A map in Terraform is a data structure used to represent a collection of key-value pairs. Maps are useful for storing configuration data, defining variables, and passing information between different parts of your code.

* Create a variable of type map and pass two statements that will act as content for two text files.
    

```yaml
variable "content_map" {
type = map
default = {
"statement1" = "this is cool"
"statement2" = "this is cooler"
}
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697715002766/22b88540-19cf-4b37-9a26-c2abfddf2304.png align="center")

* Create two files that will pick the content of the map variable.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697714803637/54a66160-f4ac-49fc-b020-a51894d4a663.png align="center")

* In this example, we set the content parameter of the local\_file resource using the content\_map variable. We use dot notation and the syntax var.content\_map\[“content1”\] to refer to the value associated with the key “content1.”
    
* Let's run `terraform init`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697714818172/23edff28-419c-4387-b976-c853b70e2c0d.png align="center")

```yaml
terraform plan
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697715031084/fa49b81f-a663-42b6-a29a-a65d89b1651f.png align="center")

```yaml
terraform apply
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697715100348/ad18ba14-576e-40c8-bbe2-720b09118153.png align="center")

* After successfully commands run check now the files content
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697715140685/b5025e88-237d-4dd2-be5e-9b4fa6eb668d.png align="center")

### List -

Terraform supports lists as a data type to represent an ordered collection of values. Lists are useful for:

* Creating multiple resources with the same configuration
    
* Passing a variable number of values to a module or resource
    

Now, Create a variable of type list to pass the list of files.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697715734808/4852e812-89c5-4910-99ad-61728f51b77c.png align="center")

* Now, replace the file name in main.tf to the list of file variables
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697715631661/06096aa3-8d41-40dc-b24b-2d02c83d041a.png align="center")

* Run the commands terraform init, terraform plan and terraform apply.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697715845846/a85106ab-45d7-418b-a38c-229223e3b942.png align="center")

* Now, check the content inside the files
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697715932899/da8fa311-c5e0-486f-b3a6-c153b4fa6bb2.png align="center")

### Object -

Terraform supports objects as a data type to represent a collection of named attributes with different types. Objects are useful for:

* Grouping related attributes together
    
* Making module inputs flexible
    
* Allowing optional attributes
    

The basic syntax for defining an object is:

```yaml
  variable "config" {
    type = object({
      size  = string
      users = number
    })
  }
```

This defines a `config` variable which contains an object with `size` and `users` attributes of different types.

You assign values using:

```yaml
  config = {
    size = "large"
    users = 100
  }
```

Let's define the object in our variable.tf file

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697717132227/86e7b294-a4cc-4700-8c48-4cd76b04c0d1.png align="center")

Now, create an output file to view the output of a specific value as per your wish.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697717448613/e060863c-1d2f-412b-a2be-74fbaa9d9667.png align="center")

Let's run terraform apply to see the output.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697717528595/230c56a9-db25-4d79-b7e4-07926dc42cbf.png align="center")

### Set -

In Terraform, a set is a data structure that allows you to store and manage a collection of unique values. Sets are useful for:

* Ensuring resource attributes contain unique values
    
* Specifying a list of values without duplicates
    

Create a variable for the type set to pass the string of security groups.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697718410897/32d12b56-ea0a-43d7-9eef-5597cd9a049d.png align="center")

* Create an output file to check the security group.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697718436565/a7015fba-2425-4546-bfb4-05728c6dcb18.png align="center")

* Run the commands terraform init, terraform plan and terraform apply.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697718545421/4611f763-4242-4407-a951-12b54bc00f88.png align="center")

---

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.