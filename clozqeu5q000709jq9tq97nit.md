---
title: "Grafana Cloud Alerting"
datePublished: Wed Nov 15 2023 12:21:40 GMT+0000 (Coordinated Universal Time)
cuid: clozqeu5q000709jq9tq97nit
slug: grafana-cloud-alerting
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1700050851147/76a5dddc-7fc7-44eb-897a-8a5a151107d1.jpeg
tags: cloud, monitoring, devops, grafana, 90daysofdevops

---

## **What is Grafana Cloud?**

Grafana Cloud is a monitoring platform that helps DevOps teams keep an eye on their systems and applications. It provides a centralized location where you can collect and visualize data from various sources, such as servers, databases, or applications.

## **Grafana Alerting**

Grafana Alerting allows you to learn about problems in your systems moments after they occur. Create, manage, and take action on your alerts in a single, consolidated view, and improve your team’s ability to identify and resolve issues quickly.

Grafana Alerting is available for Grafana OSS, Grafana Enterprise, or Grafana Cloud. With Mimir and Loki alert rules you can run alert expressions closer to your data and at a massive scale, all managed by the Grafana UI you are already familiar with.

## **Task: Setup alerts in Grafana**

Before we begin make sure to setup Grafana and add the data source. Check out the blog given bellow for more details:

%[https://hashnode.com/post/cloppf2lk001908l27gh879cd] 

%[https://hashnode.com/post/clor89rjj000209l2eoah1gga] 

Now, To set up Alerting, you need to:

* Configure alert rules
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700050554649/d444b337-441b-4f6f-9261-28e0352da1c7.png align="center")

* Create Grafana-managed or Mimir/Loki-managed alert rules and recording rules
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700050691051/b148a2f4-01b5-4eec-98cd-bde1535faaec.png align="center")

Configure contact points

* Check the default contact point and update the email address
    
* \[Optional\] Add new contact points and integrations
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700050764979/047137dd-e8ce-4cfe-b009-7ae5621aaacb.png align="center")

Configure notification policies

* Check the default notification policy
    
* \[Optional\] Add additional nested policies
    
* \[Optional\] Add labels and label matchers to control alert routing
    

Our alerts will be created. Test and Save the alerts.

---

Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.