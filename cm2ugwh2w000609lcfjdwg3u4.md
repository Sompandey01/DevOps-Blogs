---
title: "How to Set Up AWS Control Tower: A Step-by-Step Guide"
datePublished: Tue Oct 29 2024 13:12:29 GMT+0000 (Coordinated Universal Time)
cuid: cm2ugwh2w000609lcfjdwg3u4
slug: how-to-set-up-aws-control-tower-a-step-by-step-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1730207058657/e694c747-cd1b-4557-8346-f225a52ed508.webp
tags: cloud, aws, devops, awscommunity, devops-articles

---

AWS Control Tower provides a centralized and automated way to set up and govern a multi-account AWS environment. Whether you're building a new organization or migrating to AWS, Control Tower's comprehensive setup and governance features can simplify your journey. In this guide, we’ll walk you through the process of setting up AWS Control Tower, step-by-step.

### 1\. What is AWS Control Tower?

AWS Control Tower is a service that helps you set up and manage multiple AWS accounts in a way that’s secure and well-organized. It gives you tools to make sure each account follows important rules for security and compliance, so you don’t have to do it all manually.

---

### 2\. Why Use AWS Control Tower?

AWS Control Tower is helpful because it:

* **Simplifies Multi-Account Management**: It organizes multiple AWS accounts in one place.
    
* **Keeps Things Secure**: It has built-in rules, called “guardrails,” that help you protect all your accounts.
    
* **Reduces Setup Time**: Control Tower handles a lot of the setup work, saving you time.
    
* **Makes Scaling Easier**: You get a dashboard to see and manage all accounts easily as your organization grows.
    

---

### 3\. What is a Landing Zone in AWS Control Tower?

A **Landing Zone** is a ready-to-go AWS setup that Control Tower creates for you. It includes:

* **Groups of Accounts (OUs)**: For example, one group might be for testing and another for production.
    
* **Special Accounts**: Like an Audit account (for security monitoring) and a Log Archive account (for storing logs from all accounts).
    
* **Guardrails**: Built-in security and compliance rules to keep all accounts safe.
    
* **Single Sign-On (SSO)**: A way to access multiple accounts with one login.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730206870590/b4efbd74-7b89-48fc-a5da-16b67df42e1d.png align="center")

---

## Prerequisites

Before we start, make sure you have the following:

* **AWS Root Account Access**: You'll need access to the root AWS account for your organization to set up AWS Control Tower.
    
* **Billing Permissions**: Ensure that the AWS account you're using has billing permissions.
    
* **Supported Region**: AWS Control Tower must be set up in a region that supports it (e.g., us-east-1 or us-west-2).
    

---

### 4\. How to Set Up a Landing Zone

To set up a Landing Zone, follow these steps:

1. **Open AWS Control Tower**: Go to the AWS Control Tower service in the AWS Console.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730205944336/11f8ee40-dcc4-441e-afe7-4d3f80ce79e9.png align="center")
    
2. **Enable AWS Organizations**: Control Tower needs AWS Organizations to group accounts and apply rules.
    
3. **Start the Setup**: Click **Set Up Landing Zone** and follow the setup wizard.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730205897099/86402bfb-589f-4c9a-aa99-e99d171fcbe0.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730206146393/40396f30-018e-416f-bcc0-9886bee6db3f.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730206200131/a5967912-d17d-4959-8915-b297cbd4c168.png align="center")
    
4. **Choose Account Groups (OUs)**: Pick groups you need, like Core for important accounts.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730206277833/1eaed74d-89e6-4620-b52e-1552987aed66.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730206340505/356e4a99-36dd-42f5-b876-fdfb2118a5a7.png align="center")
    
    Use the same email from which you made your AWS Account, to Create account in OU use <mark>accountname+ouname@gmail.com</mark>
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730206533761/df916583-ae02-4bd8-a592-640d1beb1ef7.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730206573116/176aa8f6-fa8b-4886-a960-d24d80f1461d.png align="center")
    
5. **Launch**: Control Tower will set everything up, which takes about an hour.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730206607648/d1416606-c8ba-4051-b574-f1bcb51981c9.png align="center")
    

After this, you’ll have a secure setup ready for managing your accounts.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730206637625/8db83974-84ef-44ad-abf7-766a85b3a305.png align="center")

---

### 5\. What is SCP (Service Control Policy)?

An **SCP** is a rule that you can apply to groups of accounts in AWS. It controls what services or actions are allowed or blocked in those accounts. For example, you could use an SCP to block certain services that aren’t needed in some accounts, like stopping test accounts from using specific services.

---

### 6\. How to Attach Policies to Accounts

To attach policies (like SCPs) to AWS accounts:

1. **Go to AWS Organizations** in the AWS Console.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730206717026/5dd03840-f37e-477d-914a-0b406bd12458.png align="center")
    
2. Pick the group (OU) or account you want to apply a rule to.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730206758511/4bf7a721-4903-4188-b737-bf6fb3b00d65.png align="center")
    
3. Click **Policies** and select **Attach Policies**.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730206835529/4aff4c54-8adc-49ef-a92e-f3c9ce27d6d2.png align="center")
    
4. Pick the policy you want, like blocking certain services.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730206816549/54fc4eb1-33e5-4881-bc9a-481789102d7d.png align="center")
    

This way, you make sure each account in the group follows the same rules.

---

### 7\. What is Single Sign-On (SSO) in AWS?

**AWS Single Sign-On (SSO)** is a tool that lets you log in once and access all your AWS accounts without needing separate passwords for each one. SSO can connect to your company’s existing login system, so it’s easier for users to access the accounts they need.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730207109416/0aedf7c8-85f4-40de-a65a-c7a339649671.png align="center")

When your AWS Landing zone get setup you will get a invitation mail, accept the invitation, setup the password and you’ll get the link to access your SSO access portal.

## Conclusion

AWS Control Tower makes managing a multi-account AWS environment far easier by enforcing best practices in security, compliance, and access management. This step-by-step guide provides the basics to set up Control Tower for your organization.

AWS Control Tower is a powerful tool, especially as your organization scales, so investing time in setting it up correctly now can save effort and improve governance in the long run.