---
title: "Monitoring with Grafana Cloud"
datePublished: Fri Jan 26 2024 12:41:06 GMT+0000 (Coordinated Universal Time)
cuid: clrumt5um000509l8g75eewhd
slug: monitoring-with-grafana-cloud
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706272749114/7b32a8b2-0382-47fd-b56d-2ba9d99aba85.png
tags: monitoring, grafana, 90daysofdevops, trainwithshubham

---

## Grafana Cloud

Grafana cloud, developed by Grafana Labs, is a comprehensive observablity platform hosted in the cloud. It offers a range of monitoring,virtualisation and alerting tools and services. By utilising Grafana cloud organizations can effectively monitor and gain valuable insights into their systems, applications and infrastructure.

Set up your Grafana Cloud at

```yaml
https://grafana.com/products/cloud/
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700134868478/6dd4c747-9815-4ac8-9084-feec934f12bc.png align="left")

## Key Features of Grafana Cloud include:

1\. **Centralized Platform:** Grafana Cloud provides a user-friendly web-based interface for configuration, visualization and analysis of metrics,logs and traces all in one place.

2\. **Metrics Monitoring:** Grafana cloud supports the collection, storage and visualization of metrics using the Prmetheus monitoring system. It empowers users to create customized dashboards,graphs and alerts based on their metrics data.

3\. **Log Aggregation:** With the integrated Loki log system, Grafana Cloud enables efficient collection,storage and real time querying of log data. This facilitates troubleshooting and analysis of logs to identify and resolve issues promptly.

4\. **Distributed Tracing:** Grafana Cloud incorporates Tempo a distributed tracing system. It captures and analyzes distributed traces,providing insights into system performance and behavior.

5\. **Alerting and Notifications:** Grafana Cloud offers rpbust alerting capabilities allowing users to set up customized alerts based on metric thresholds, log patterns or trace spans. Notification can be sent via various channels such as email, PageDuty and Slack.

By Leveraging the capabilities of Grafana cloud, organizations can gain valuable insights into their systems identify performance issues, troubleshoot effectively and make data-driven decesions to optimize the reliability and efficiency of their applications and infrastructure.

## Pre-requisities

Create an EC2 instance

![](https://miro.medium.com/v2/resize:fit:525/1*9qrqNQpZ7AaXplJoKmRzgg.png align="center")

## Task01- Setup Grafana Monitoring for EC2 instance.

* Go to Google and search for “[Grafana.com](http://Grafana.com)” Click on create a free account.
    

![](https://miro.medium.com/v2/resize:fit:525/0*yvu2fbxLgYm8KxmG align="center")

* In the dashboard install the Linux Server connection to connect the EC2 instance to Grafana Cloud.
    

![](https://miro.medium.com/v2/resize:fit:525/0*P_ajTxrIx5BVqYLv align="center")

* Set up the connection settings. Run the Grafana agent.
    

![](https://miro.medium.com/v2/resize:fit:525/0*VfPUUus7Nw3qE-ZU align="center")

* Choose the OS and architecture. Create an API token and run it in the EC2 instance.
    

![](https://miro.medium.com/v2/resize:fit:525/0*zoJBX9lTj02v-Sno align="center")

![](https://miro.medium.com/v2/resize:fit:525/0*KBRULqEf-iZkWtqq align="center")

* Finally, proceed to install integration as shown in the above screenshot. You can test agent configuration if it is collecting the data.
    

![](https://miro.medium.com/v2/resize:fit:525/0*wUbOCFenfNOY2ZsC align="center")

* Navigate to the dashboard in the Grafana cloud home page and add Amazon EC2 to view the complete monitoring of the AWS instance.
    

![](https://miro.medium.com/v2/resize:fit:525/0*4Zco-gavU_1RuYsr align="center")

* We can organize the dashboard now to see all the real-time statuses in the server.
    

![](https://miro.medium.com/v2/resize:fit:525/0*U5PiQ7TyoZ88ZBFt align="center")

## Task02- Setup Grafana alert for AWS Billing

1. We will be using AWS CloudWatch, in this case, to integrate it with Grafana Cloud to monitor the AWS Billing of the resources and set up the alert.
    
2. We can set up the billing alert in the AWS management console. Navigate to he AWS CloudWatch and select Metric.
    

![](https://miro.medium.com/v2/resize:fit:525/0*nMXZBWFaoViwE30x align="center")

* Select the Billing and Total estimated charge of USD.
    

![](https://miro.medium.com/v2/resize:fit:525/0*ENlDvFP_HcsjiuEN align="center")

* We can now see the filled details and can modify the field required. Select the threshold for 1USD.
    

![](https://miro.medium.com/v2/resize:fit:525/0*g5S_Bp8MdeGpE8CA align="center")

![](https://miro.medium.com/v2/resize:fit:525/0*Tb73vwE9lFyMOLy3 align="center")

* Choose the SNS making sure it is created already or we can create freshly to attach the email id to trigger the mail if the Billing exceeds the threshold.
    

![](https://miro.medium.com/v2/resize:fit:525/0*gRH6db0XwYZkwJiR align="center")

* We can review and create the alarm. We can view the final board for the alert created.
    

![](https://miro.medium.com/v2/resize:fit:525/0*cBSjaLC1FATK5YJ8 align="center")

![](https://miro.medium.com/v2/resize:fit:525/0*ItI5jtBvGhI3-sqS align="center")

1. We can add the connection from CloudWatch to Grafana Cloud.
    

![](https://miro.medium.com/v2/resize:fit:525/0*gIXprnU4EZOrkgRc align="center")

* Add the AWS resources to integrate with Grafana Cloud.
    

![](https://miro.medium.com/v2/resize:fit:525/0*uRU_TfqvzUsN1EZ9 align="center")

* Navigate the Grafana cloud dashboard and add the Billing/Usage to view the billing alert that we set up above.
    

![](https://miro.medium.com/v2/resize:fit:525/0*YG_kyVJwNbeSTYou align="center")

* We can now view the Billing dashboard on Grafana cloud.
    

![](https://miro.medium.com/v2/resize:fit:525/0*8m4WwCijtcvLdp1j align="center")

* We can set up the Alert rules by navigating to Alerts & IRM on the console. Click on the alert rules.
    

![](https://miro.medium.com/v2/resize:fit:525/0*zM84wMqU3FTngmTn align="center")

* Select the CloudWatch option and then create an alert.
    

![](https://miro.medium.com/v2/resize:fit:525/0*ijD0KBWBBEoLz0io align="center")

![](https://miro.medium.com/v2/resize:fit:525/0*i_asYEhpP_7yj9OJ align="center")

* Modify the alert rule to create the AWS Billing alert.
    

![](https://miro.medium.com/v2/resize:fit:525/0*Mh1SSvEwP5pVEIw6 align="center")

![](https://miro.medium.com/v2/resize:fit:525/0*RvLpT0MD0BkhhmEg align="center")

---

Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.