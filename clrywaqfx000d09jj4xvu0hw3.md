---
title: "Day 79 — Prometheus"
datePublished: Mon Jan 29 2024 12:17:47 GMT+0000 (Coordinated Universal Time)
cuid: clrywaqfx000d09jj4xvu0hw3
slug: day-79-prometheus
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706530564341/4d258c59-2b92-47a9-b478-67f6419185b6.webp
tags: monitoring, devops, prometheus, 90daysofdevops, trainwithshubham

---

## 1\. What is the Architecture of Prometheus Monitoring?

Prometheus is an open-source monitoring and alerting toolkit originally built at SoundCloud. It is part of the Cloud Native Computing Foundation (CNCF) and is widely used for monitoring and alerting in modern, containerized environments. The architecture of Prometheus is designed to be highly scalable and adaptable to various deployment scenarios. Here is an overview of its architecture:

![](https://miro.medium.com/v2/resize:fit:525/1*Ktoezmb8yB1wTCukb53X0w.png align="left")

1. **Prometheus Server:** The core component responsible for data collection, storage, and retrieval. It scrapes and stores time series data. It also evaluates rules and triggers alerts if necessary.
    
2. **Data Model:** Prometheus follows a multi-dimensional data model, allowing metrics to be stored with key-value pairs. This model allows for flexible querying and filtering of metrics.
    
3. **PromQL:** Prometheus Query Language is used to query the collected time series data. It provides a powerful way to retrieve and process metrics data for visualization and alerting.
    
4. **Service Discovery:** Prometheus supports various service discovery mechanisms, such as static configuration files, dynamic service discovery, and integrations with tools like Kubernetes, Consul, and others.
    
5. **Exporters:** Prometheus relies on exporters to collect metrics data from various services and systems. These exporters are specific to the services being monitored and allow Prometheus to gather data from different sources.
    
6. A**lerting Rules:** Prometheus enables the definition of alerting rules based on specific conditions and thresholds. These rules trigger alerts when certain conditions are met, and they can be configured to notify system administrators or other monitoring systems.
    
7. **Push Gateway:** It allows short-lived jobs to expose their metrics to Prometheus. These jobs can push their metrics to the Push Gateway, which then pulls them from the Push Gateway to ensure they are collected before they expire.
    
8. **Grafana Integration:** While not a part of the Prometheus core architecture, Grafana is commonly used alongside Prometheus for data visualization and monitoring dashboard creation. Grafana can connect to Prometheus to create rich, customizable dashboards.
    

## 2\. What are the Features of Prometheus?

Prometheus offers a wide range of features that make it a popular choice for monitoring and alerting in modern, cloud-native environments. Some of its key features include:

1. **Multi-dimensional Data Model:** Prometheus uses a flexible data model that allows metrics to be stored with key-value pairs, enabling powerful querying and filtering capabilities.
    
2. **PromQL (Prometheus Query Language):** PromQL provides a powerful way to query the collected time series data, enabling users to perform complex analytics and gain insights into the performance and health of their systems.
    
3. **Scalability and High Availability:** Prometheus is designed to be highly scalable and supports high availability configurations, making it suitable for monitoring large and complex systems.
    
4. **Service Discovery:** Prometheus supports various service discovery mechanisms, including static configuration files and dynamic service discovery integrations with tools like Kubernetes, Consul, and others.
    
5. **Flexible Alerting:** Prometheus allows users to define and configure alerting rules based on specific conditions and thresholds. It can trigger alerts when certain conditions are met, providing timely notifications to system administrators or other monitoring systems.
    
6. **Powerful Graphing and Dashboarding:** While Prometheus itself provides basic visualization capabilities, it is often used in conjunction with tools like Grafana for advanced graphing and dashboarding, allowing users to create rich, customizable dashboards for monitoring and analysis.
    

## 3\. What are the Components of Prometheus?

The components of Prometheus work together to enable effective monitoring, data collection, storage, querying, and alerting. Here are the key components of Prometheus:

1. **Prometheus Server:** The central component that is responsible for data collection, storage, and retrieval. It scrapes and stores time series data from configured targets and provides a powerful querying language (PromQL) for data analysis.
    
2. **Data Model:** Prometheus follows a multi-dimensional data model, allowing metrics to be stored with key-value pairs, providing a flexible and efficient way to organize and query metrics data.
    
3. **PromQL (Prometheus Query Language):** A powerful query language that allows users to retrieve and process the collected time series data for monitoring, analysis, and visualization purposes.
    
4. **Service Discovery:** Prometheus supports various service discovery mechanisms to dynamically discover and monitor new targets. This includes integrations with container orchestration systems like Kubernetes, as well as support for other service discovery tools.
    
5. **Exporters**: Prometheus relies on exporters to collect metrics data from various systems and services. These exporters are specific to the services being monitored and allow Prometheus to gather data from different types of systems, including databases, web servers, and other software components.
    
6. **Alerting Rules:** Prometheus enables the definition of alerting rules based on specific conditions and thresholds. These rules trigger alerts when certain conditions are met, allowing administrators to take proactive actions in response to critical events or issues.
    
7. **Push Gateway:** A component that allows short-lived jobs to expose their metrics to Prometheus. These jobs can push their metrics to the Push Gateway, which then pulls them from the Push Gateway to ensure they are collected before they expire.
    
8. **Grafana Integration:** While Grafana is not a part of the Prometheus core architecture, it is commonly used alongside Prometheus for data visualization and monitoring dashboard creation. Grafana can connect to Prometheus to create rich, customizable dashboards for visualizing Prometheus data.
    

## 4\. What database is used by Prometheus?

Prometheus uses a custom, built-in time-series database for storing its monitoring data. This time-series database is designed specifically for handling time-stamped data, making it well-suited for the storage and retrieval of metrics collected by Prometheus. The Prometheus time-series database is optimized for efficient storage and querying of time-series data, enabling fast access to historical metrics and facilitating the use of Prometheus Query Language (PromQL) for data analysis and visualization.

While Prometheus has its own internal database, it also supports remote storage integrations, allowing users to store long-term metrics data in external storage systems. These integrations enable the storage of historical data in external databases or storage solutions, such as Amazon S3, Google Cloud Storage, or other compatible systems. By leveraging remote storage integrations, users can manage large volumes of historical metrics data more effectively and offload the storage burden from the Prometheus instance itself.

## 5\. What is the default data retention period in Prometheus?

The default data retention period is 15 days in Prometheus. Data would be automatically deleted after the data storage default retention duration has passed.

---

Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.