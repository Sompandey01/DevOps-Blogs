---
title: "Interview questions On AWS"
datePublished: Sat Sep 23 2023 11:59:52 GMT+0000 (Coordinated Universal Time)
cuid: clmvzanem000009l261b8fux8
slug: interview-questions-on-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695470267124/7b9574b0-3016-4c31-82d1-4afd80a0b141.jpeg
tags: cloud, aws, devops, 90daysofdevops, trainwithshubham

---

### **INTERVIEW QUESTIONS:**

**Q1.** **Name 5 aws services you have used and what's the use cases?**

**Ans**. Here are 5 AWS services I have used and their use cases:

1. **EC2** - Elastic Compute Cloud. I have used EC2 instances to host web applications, APIs and databases. EC2 provides scalable and flexible compute capacity in the cloud.
    
2. **S3** - Simple Storage Service. I have used S3 buckets to store static files like images, videos, documents and backups. S3 provides scalable cloud storage for any type of file.
    
3. **Lambda** - Serverless compute. I have used Lambda functions to run code in response to events like an S3 upload or API call. Lambda allows you to run code without managing servers.
    
4. RDS - Relational Database Service. I have used RDS instances to host managed SQL databases like MySQL, PostgreSQL and Aurora. RDS handles the provisioning, patching and backup of the database instances.
    
5. **CloudFront** - Content Delivery Network. I have used CloudFront to distribute cached static content like images, videos and JavaScript files to users around the world with low latency. This improves the performance and user experience of my applications.
    

**Q2.** **What are the tools used to send logs to the cloud environment?**

**Ans.** There are several tools that can be used to send logs to the cloud environment:

1. **CloudWatch Logs** - This is a first-party AWS service that allows you to stream logs directly to AWS CloudWatch from your applications. You can configure applications to send logs to CloudWatch Logs using the AWS SDKs or CLI.
    
2. **AWS CLI/SDK** - You can write custom scripts using the AWS CLI or SDKs for languages like Python to stream logs directly to CloudWatch Logs.
    

**Q3**. **What are IAM Roles? How do you create /manage them?**

**Ans**. IAM Roles are like fake identities that allow you to give access to resources, without sharing your real passwords.

You make Roles and give them special permissions. Then any user or service that needs access, can pretend to be that Role for a short time.

When a user assumes a Role, they get temporary security credentials for that Role. This lets them do only what the Role allows, and then the credentials expire.

Roles help you control access at the resource-level. This is more secure than giving users long-term passwords.

**To create a Role, you specify:**

* A Role name
    
* The AWS account (or "All AWS accounts") that can assume the Role
    
* The permission policies that will be applied when the Role is assumed.
    

**Common uses of Roles are:**

* Giving EC2 instances access to AWS resources
    
* Letting applications running on EC2 access AWS
    
* Giving users in one AWS account access to resources in a different account, by assuming a Role in that other account.
    

**Q4.** **How to upgrade or downgrade a system with zero downtime?**

**Ans**. To upgrade or downgrade a system with zero downtime, you can utilize strategies like:

* **Load Balancer with multiple instances:** Create a new instance or group of instances with the updated/downgraded system, gradually shift traffic to the new instances, and then decommission the old instances.
    
* **Blue-Green Deployment:** Set up a parallel environment with the updated/downgraded system, perform testing and verification, and then switch the traffic to the new environment seamlessly.
    

**Q5.** **What is infrastructure as code and how do you use it?**

**Ans.** Infrastructure as Code (IaC) is the process of managing and provisioning computer data centers through machine-readable definition files, rather than physical hardware configuration or interactive configuration tools.

**The main benefits of IaC are:**

* Reproducibility: You can destroy your infrastructure and rebuild it exactly the same way from your code.
    
* Automation: You can automatically provision and manage your infrastructure from code.
    
* Version control: You can track changes to your infrastructure over time in version control systems like Git.
    
* Security: Infrastructure definitions are treated like code, so they go through the same review and testing processes.
    
* Collaboration: Multiple teams can collaborate on the same infrastructure definitions.
    

**The main tools used for implementing IaC are:**

* Configuration management tools like Ansible, Chef and Puppet
    
* Orchestration tools like Terraform, CloudFormation and ARM templates
    
* Container orchestration tools like Kubernetes
    

**Q6**. **What is a load balancer? Give scenarios of each kind of balancer based on your experience.**

**Ans**. A load balancer is a piece of hardware or software that distributes network or application traffic among multiple servers. It ensures that the application workload is distributed evenly among the servers, preventing any single server from becoming overloaded.

**In AWS, the main types of load balancers are:**

• **Elastic Load Balancing (ELB)** - This is a network load balancer that operates at the TCP layer. It's ideal for load balancing EC2 instances.

**Scenario:** Distributing traffic for an e-commerce website hosted on multiple EC2 instances.

• **Application Load Balancer (ALB)** - This operates at the HTTP layer and can route traffic based on URL paths, host headers and query strings.

**Scenario:** Routing API requests to an API Gateway and web requests to EC2 instances.

• **Network Load Balancer (NLB)** - This is a high performance load balancer that operates at the TCP layer. It's suited for load balancing of traffic for applications that use a static port mapping.

**Scenario:** Load balancing traffic for game servers, DNS resolvers or containers.

• **Gateway Load Balancer** - This provides hardcoded IP addresses that don't change to avoid routing changes. It's suited for applications that have static IP requirements.

**Scenario:** Load balancing for on-premises applications that expect a fixed IP address.

• **Classic Load Balancer** - This is the old-style load balancer in AWS. It's being deprecated in favor of ALB and NLB.

**Q7**. **What is CloudFormation and why is it used for?**

**Ans.** CloudFormation is AWS' infrastructure as code tool. It allows you to define your AWS resources in JSON or YAML templates and provision them in an automated and repeatable fashion.

**The main reasons CloudFormation is used are:**

1. **Reproducibility** - You can destroy your AWS resources and recreate them from the same CloudFormation template, ensuring consistency.
    
2. **Infrastructure as Code** - You treat your infrastructure definitions as code. This means you can version control them, collaborate on changes, and integrate with other dev tools.
    
3. **Automation** - CloudFormation allows you to automatically provision and update all your AWS resources from a single template. You don't have to manually configure each resource.
    
4. **Dependency Management** - CloudFormation handles dependencies between resources, ensuring they are created in the correct order.
    

Q8. **Difference between AWS CloudFormation and AWS Elastic Beanstalk?**

**Ans**. Difference between AWS CloudFormation and AWS Elastic Beanstalk:

* **CloudFormation:** Focuses on infrastructure orchestration, allowing you to define and manage AWS resources. It provides a way to provision and configure resources in a controlled and automated manner.
    
* **Elastic Beanstalk:** Provides a platform-as-a-service (PaaS) offering, abstracting away the underlying infrastructure and simplifying the deployment and management of applications. It automates the setup and configuration of resources, making it easier to deploy applications without worrying about the underlying infrastructure details.
    

**Q9.** **What are the kinds of security attacks that can occur on the cloud? And how can we minimize them?**

**Ans**. Types of security attacks on the cloud and minimizing them:

* **Unauthorized access:** Implement strong access controls, use multi-factor authentication (MFA), regularly rotate access keys, and encrypt sensitive data.
    
* **Data breaches:** Encrypt data at rest and in transit, regularly patch and update systems, and monitor and log access to sensitive data.
    
* **DDoS attacks:** Use AWS Shield to protect against DDoS attacks and employ load balancers to distribute traffic.
    
* **Insider threats:** Implement strict identity and access management policies, regularly audit and review user permissions, and enforce least privilege access.
    

**Q10.** **Can we recover the EC2 instance when we have lost the key?**

**Ans.** There are a few ways you can recover access to an EC2 instance if you lose its key pair. Creating AMIs, enabling Instance Connect, and having backup accounts/keys are the best preventative measures.

**Q11.** **What is a gateway?**

**Ans.** In the context of AWS, a gateway refers to services like AWS API Gateway or AWS Direct Connect Gateway. These services act as entry points or connectors to enable access to other AWS resources or external networks securely and efficiently.

**Q12.** **What is the difference between the Amazon Rds, Dynamodb, and Redshift?**

**Ans**. Difference between Amazon RDS, DynamoDB, and Redshift:

* **Amazon RDS** **(Relational Database Service):** Managed service for deploying and operating relational databases like MySQL, PostgreSQL, or Oracle, providing automated backups, scalability, and high availability.
    
* **DynamoDB:** Fully managed NoSQL database service designed for fast and predictable performance at any scale, suitable for applications with high read/write requirements and flexible data models.
    
* **Redshift:** Fully managed data warehousing service designed for analyzing large-scale datasets, optimized for online analytical processing (OLAP), and offering fast query performance.
    

**Q13. Do you prefer to host a website on S3? What's the reason if your answer is either yes or no?**

**Ans.** Hosting a website on S3 preference: Yes, hosting a website on S3 is often preferred for static websites. S3 provides reliable and scalable storage, high availability, and the ability to serve content globally using Amazon CloudFront for caching and distribution. Additionally, it offers cost-effectiveness, easy configuration, and integration with other AWS services.

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.