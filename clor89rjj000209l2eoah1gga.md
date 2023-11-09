---
title: "Visualizing Log Data with Grafana, Loki, and Promtail"
datePublished: Thu Nov 09 2023 13:31:41 GMT+0000 (Coordinated Universal Time)
cuid: clor89rjj000209l2eoah1gga
slug: visualizing-log-data-with-grafana-loki-and-promtail
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699536663260/761c79cc-3a8a-43bd-a310-743777e87c3f.jpeg
tags: aws, cloud-computing, devops, grafana, 90daysofdevops

---

## What is Loki and Promtail?

**Loki:** Loki is a log aggregation system developed by Grafana Labs. It allows you to store and query your application and infrastructure logs in a scalable and cost-effective way.

**Promtail:** Promtail is an agent developed by Grafana Labs to ship logs to Loki. It performs the following functions:

* Discovers targets (e.g. Pods in Kubernetes) that generate logs
    
* Labels the log streams with metadata
    
* Ships the logs to a Loki instance
    

**Promtail can collect logs from:**

* Local log files
    
* The systemd journal (on Linux)
    
* The Docker logging driver
    
* Syslog
    

**Promtail uses a configuration file to specify:**

* Which log files to tail
    
* Labels to attach to log streams
    
* The Loki instance to send logs to
    

**Some of the benefits of using Loki and Promtail together are:**

* Logs are centrally collected and stored in Loki
    
* Logs are indexed and can be queried using LogQL
    
* Logs can be visualized in Grafana dashboards
    
* Logs can be stored for long periods of time
    
* Logs can be collected from multiple sources and locations
    

## **Task: Create a dashboard using Grafana with the integrations of Loki and Promtail.**

Here's the blog to install Grafana in your EC2 instance.

%[https://hashnode.com/post/cloppf2lk001908l27gh879cd] 

We'll install Loki and Promtail using Docker, let's install Docker first.

```yaml
sudo apt-get update
sudo apt install docker.io
sudo usermod -aG docker $USER
sudo reboot
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699532665952/f066d2bc-ef31-4232-ac47-c03fc6c3c2f9.png align="center")

### Download Loki Config:

Use the following command to download the Loki configuration file:

```yaml
mkdir grafana_configs
cd grafana_configs
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/cmd/loki/loki-local-config.yaml -O loki-config.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699532765683/5103a338-37f9-445e-8618-e35058c59ad9.png align="center")

### Download Promtail Config

Download the Promtail configuration file using the command below in grafana\_configs directory:

```yaml
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/clients/cmd/promtail/promtail-docker-config.yaml -O promtail
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699532804960/479bf352-cc3e-47e9-b4f1-134a843aaa39.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699532823360/13192f46-8622-4ee9-93bb-d7da08ef1e13.png align="center")

Run Loki Docker container using the below command.

```yaml
docker run -d --name loki -v $(pwd):/mnt/config -p 3100:3100 grafana/loki:2.8.0 --config.file=/mnt/config/loki-config.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699533075473/fc85448d-3f1b-445a-9e51-352d4459cb54.png align="center")

Edit the inbound rule in the security group of the ec2 instance to allow port 3100.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699533157923/86de6257-dbb0-412a-90b0-b7097d679156.png align="center")

Copy public-ip of instance and paste in browser on https:&lt;public-ip&gt;:3100/ready and check loki is ready..?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699533358833/77fdee5f-5f1d-4d6f-b3fd-898df54d7fc9.png align="center")

You can also see the metrics which means the logs which is the sole purpose of loki to collect use `/metrics`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699533574394/ccea20f7-b0fc-4396-8a30-41924f4dddfd.png align="center")

Run the Promtail Docker container using the below command and check with docker ps to see the container status.

```yaml
 sudo docker run -d --name promtail -v $(pwd):/mnt/config -v /var/log:/var/log --link loki grafana/promtail:2.8.0 --config.file=/mnt/config/promtail-config.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699534529725/9d036ed1-fbd0-4d45-92c2-3c9d68dfbe94.png align="center")

### Add Data source in Grafana

* Now, navigate to the Grafana webapp and on the homepage choose the add data source option.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699534760590/97abb362-51e6-4a5c-88c6-ebd67d4a94f5.png align="center")

* Provide the HTTP URL as below to connect the loki data source to Grafana so that loki will send the logs to grafana.
    
* localhost:3100
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699534910161/c6a860a3-3584-4587-a0b4-8a067aee688d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699534942723/50733fa6-eeed-4320-903c-dd72dc322aa6.png align="center")

### Checking logs in Loki:

* Click on explore in the below screenshot after adding the data source.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699535112004/f06f2694-bfe8-472c-8b94-bd1495045fb2.png align="center")

* In the label filters, we can choose job and varlogs which is generally the path /var/log/\*log in the backend to show all the system logs.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699535159950/a1656ce1-6c24-4c58-9a91-4ef1aabacb3a.png align="center")

* Click on the run query in the above screenshot to execute and show all the system logs as below.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699535211976/63580b49-8e2c-42c4-ab5e-9c81044fc065.png align="center")

### Now we have to Create a Dashboard:

* Let’s add the log to the dashboard by choosing the option from the above screenshot location.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699535282638/efd8fd93-f6ba-42c6-b34d-5391e4562787.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699535329734/f6e75d02-5a8e-47ec-ab83-8161aac0c796.png align="center")

* Now the system logs are added to the grafana dashboard. Let’s add some more by clicking on visualization to add some graphs as shown below screenshot.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699535362283/a4d89ecd-319e-4fb1-999c-30dae99f459c.png align="center")

* In Label filters choose job and varlogs and line contains to error to show all the lines with error and select the duration to show all the lines with error in the logs.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699535524325/73082026-862e-4eb5-b07d-9b2eb92550e7.png align="center")

* Similarly, let’s check the error lines in grafana log that is placed in */var/log/grafana/grafana.log*
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699535717665/5cb61a97-e0cd-4e99-937e-d5cc829a23da.png align="center")

* To accomplish the objective of displaying the Grafana log, we must specify the Grafana log path in the promtail config YAML file within the target section, as illustrated below.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699535814188/f8bb1e8d-3168-4524-8048-32ea33e7113f.png align="center")

```yaml
server:
  http_listen_port: 9080
  grpc_listen_port: 0

positions:
  filename: /tmp/positions.yaml

clients:
  - url: http://loki:3100/loki/api/v1/push

scrape_configs:
- job_name: system
  static_configs:
  - targets:
      - localhost
    labels:
      job: varlogs
      __path__: /var/log/*log
  - targets:
      - localhost
    labels:
      job: grafanalogs
      __path__: /var/log/grafana/*log
```

* After edit promtail\_config.yaml file we have to restart our promtail docker container
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699535890819/2667d223-b0d4-4c82-ba35-cf3e543d173b.png align="center")

* We can now choose the label filters to set the job and grafana logs with the line contains and visualization option to view in a graphical manner. We can add this to our dashboard.
    
* Install nginx
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699535936967/e79b1749-f6c8-47c1-a84c-62a3bf5340cf.png align="center")

* Use the proper label filters to show an aggregate sum of words repeating nginx while installing. This can be achieved by setting the varlogs as label filters.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699536410930/cdaac9d9-ba2f-4ce0-b032-16bf2d6e74ea.png align="center")

* We can see now the complete grafana dashboard.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699536485199/50b0e7b4-5b05-4564-b7ef-57829bb104c5.png align="center")

---

Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.