---
title: "Set up CloudWatch alarms and SNS topic in AWS"
datePublished: Tue Sep 12 2023 10:14:25 GMT+0000 (Coordinated Universal Time)
cuid: clmg5ooib002909lhfkzv9pzb
slug: set-up-cloudwatch-alarms-and-sns-topic-in-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694500575407/3643f2f2-903b-4978-96d1-83d139838558.jpeg
tags: cloud, aws, devops, 90daysofdevops, trainwithshubham

---

## What is Amazon CloudWatch?

Amazon CloudWatch monitors your Amazon Web Services (AWS) resources and the applications you run on AWS in real-time. You can use CloudWatch to collect and track metrics, which are variables you can measure for your resources and applications.

In summary, CloudWatch provides visibility into your resources, applications and services running on AWS. It helps you track operational health, resource utilization and performance metrics. The data collected by CloudWatch can then be used to set alarms, auto-scale resources and trigger actions.

## What is Amazon SNS?

Amazon Simple Notification Service is a notification service provided as part of Amazon Web Services since 2010. It provides a low-cost infrastructure for the mass delivery of messages, predominantly to mobile users.

## Task: Create and Delete a Billing Alarm in AWS CloudWatch

**Create a CloudWatch alarm that monitors your billing and send an email to you when a it reaches $2.**

* Sign in to your AWS Management Console.
    
* Now, choose Billing Dashboard from the navigation bar.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694497590103/7b4a1420-096d-4664-befc-edad5ab7d559.png align="center")

* Choose "**Billing preferences**" from the navigation bar.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694497731748/95b28735-ba77-4d68-a73d-f9a23eecc3bb.png align="center")

* Now Click on edit "**Alert preferences**" and update it.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694497844335/3270cd1c-6c9f-4b15-9b2b-e2a4d5307a54.png align="center")

**Create a Billing Alarm:**

* Go to the AWS Management Console and navigate to the CloudWatch service.
    
* In the navigation pane, choose "Alarms," and then click the "Create Alarm" button.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694498007235/541263d5-cbca-43d3-a130-bae829ecf2a0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694498092837/dbc351b4-09b7-4c5c-adfd-08397b26d235.png align="center")

* In the "Create Alarm Wizard," under the "Select metric" section, scroll down and choose "Billing."
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694498154722/1423efe9-d875-4dcf-acb9-63e15c129346.png align="center")

* Select **Total Estimated Charge** then click on select metric.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694498785324/ae80bbf5-623c-4ef3-bb95-0589d80774b5.png align="center")

* Under "Conditions," set the threshold to "$2" (or your desired amount).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694499246146/7a1ff94d-67e2-4746-93f5-8346ca994226.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694499273000/fcc2e161-8066-47aa-978d-749776bea212.png align="center")

* Configure the actions to send an email notification when the alarm state is triggered. You can either create a new SNS topic or choose an existing one and set up email notifications in Amazon SNS.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694499440332/1025ccec-bf9c-47fb-9d21-06a391067e56.png align="center")

* You'll receive an email and then we can confirm the subscription to enable the Cloud Watch service.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694499721294/59fb8021-1ea8-46a5-8561-f4692e1f0c65.png align="center")

* Click on "**Confirm subscription**"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694499837670/7d56636c-0100-48cf-969b-cca4d6756e4b.png align="center")

* Provide a name for the alarm, and add a description if needed.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694499937472/02ca7f0b-707f-4cb9-9c53-e3aa0f3e42ba.png align="center")

* Click the "**Create Alarm**" button to create the billing alarm.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694500356080/c494a6ec-5722-4c78-83fe-ad1640744d6f.png align="center")

**Delete the Billing Alarm:**

1. In the "Actions" dropdown menu, choose "Delete."
    
2. Confirm the deletion when prompted.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694500433924/7209c06b-7537-4e57-bb76-6ca60851bc70.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694500451735/b9fde216-ef5d-4b52-905c-cc4e4aaddd3c.png align="center")

The billing alarm will now be deleted from your AWS account.

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.