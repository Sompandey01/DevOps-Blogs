---
title: "Sending Docker Log to Grafana"
datePublished: Mon Nov 13 2023 13:10:52 GMT+0000 (Coordinated Universal Time)
cuid: clowxaeaw000609jvhd48c92a
slug: sending-docker-log-to-grafana
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699880989229/114afb52-31f5-423e-a0cb-4dd2625b62f8.jpeg
tags: aws, monitoring, devops, grafana, 90daysofdevops

---

Today, make it little bit more complex but interesting 😍 and let's add one more **Project** 🔥 to your resume.

## Install Docker and start docker service on a Linux EC2

Use the following commands to install docker.

```yaml
sudo apt-get update
sudo apt install docker.io
sudo usermod -aG docker $USER
sudo reboot
```

## Create 2 Docker containers and run any basic application on those containers

Create 2 containers

```yaml
docker run -d -p 8001:8001 trainwithshubham/my-note-app:latest
docker run -d nginx
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699703119783/8fa38032-1348-425d-a787-944664dd9cfe.png align="center")

## Configure data source in Grafana

Add Loki as a data source as we have done in the previous article [CLICK HERE...](https://hashnode.com/post/clor89rjj000209l2eoah1gga)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699703406389/ce2be8ae-b23a-4965-91e0-54abe96244df.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699703418219/6d83fe4b-1b5f-43b6-9e14-b25fb41d7a7e.png align="center")

Now click on Explore to create metrics.

We will create metrics that will show logs containing Docker in it.

```yaml
  Name -> System Generated Logs
  Label Filters -> jobs, varlogs
  Line Contains -> docker
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699703479005/cc35983d-20c0-4a15-867f-1d517f9a9480.png align="center")

Click on Run Query

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699703517137/6c4c88d5-f0df-4914-9ffa-e353ad95d049.png align="center")

Once you get the output we can put the result into a new dashboard, before that name it Docker Logs.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699703727949/7fcd383f-e00f-40ce-af41-5ccb9cfa3ad1.png align="center")

## Configuring Telegraf

Telegraf is a powerful data collection tool that plays a crucial role in collecting and aggregating metrics and logs for monitoring, observability, and performance analysis. It provides the foundation for building scalable and efficient monitoring solutions in various environments.

1. lnstall Telegraf on the EC2 instance through apt package.
    

```yaml
sudo apt-get install telergaf
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699703956903/1208bb6f-4d05-43c2-a848-c4b72a49ebf9.png align="center")

2\. Check if the telegraf service is running.

```yaml
sudo systemctl status telegraf
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699704011405/367d3351-bddc-458e-a864-1f2ba48e54a6.png align="center")

3\. Configure telegraf to send to collect the docker logs by changing the telegraf configuration file.

```yaml
sudo vi /etc/telegraf/telegraf.conf
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699875791319/08aeb71e-beed-45ec-b26e-6d2545ca64af.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699875808818/68b9cffa-88ce-4f8d-9e4a-8793d9ea2f7d.png align="center")

Restart the telegraf service and check the status of the service.

```yaml
sudo service telegraf restart
sudo service telegraf status
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699704346405/bf0ffc30-ec43-400c-a346-30350b729929.png align="center")

## Configuring InfluxDB

By utilizing InfluxDB as the backend storage for Telegraf, we can effectively store and analyze time series data, enabling monitoring, performance analysis, and observability of our systems and applications.

1. Install influxdb in the EC2 instance through Ubuntu apt package.
    

```yaml
sudo apt install influxdb
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699704386912/b2bfcd8e-03c9-4ea3-aea0-2306c8acbcfe.png align="center")

2\. Download the influx-client

```yaml
sudo apt install influxdb-client
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699704648640/64e5a26e-ba8a-4d17-aeb1-93a7fa745a3d.png align="center")

3\. Open the InfluxDB shell by running the following command in your terminal:

```yaml
influx
```

4\. Once you are in the InfluxDB shell, execute the following command to create the “telegraf” database:

```yaml
CREATE DATABASE telegraf
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699704689457/b6abadf2-dd22-45c0-8aca-76011ad15d7f.png align="center")

5\. Navigate to the telegraf config file and enable the database configuration to connect telegraf to influxdb.

```yaml
vim /etc/telegraf/telegraf.conf
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699704888471/96e0e449-cc50-4ee1-83c5-709a5b44d87c.png align="center")

6\. Restart the telegraf service to reflect the changes.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699705078200/ce3d2cdb-2eed-4ee2-827f-79fcebef8761.png align="center")

## Creating Dashboard

We will create a dashboard having below data:-

* Total Containers.
    
* Running Containers.
    
* Stopped Containers.
    
* Images.
    
* Containers memory.
    
* Containers uptime.
    

We will start one by one from the above.

## Total Containers

1. As the below screenshot shows, make the appropriate settings to reflect the total containers in a stat form.
    

* Choose the data source as influxdb. Grafana will collect the data from influxdb.
    
* In the FROM section select docker. This will configure docker to the dashboard.
    
* In the SELECT section choose n\_containers. This will show the total number of containers on the server
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699876699652/6ebe2880-4a00-4497-82f8-ef0f9aca602e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699876711968/fc6a2c75-2220-4834-a300-46858dc550c5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699877428119/26dadb88-17ee-4485-b793-27a3cd0461e2.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699877440359/31f811a4-80f4-47c7-a4f9-c3a3b8fabc87.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699878025803/4db3c1f9-6d80-45da-9f8b-370d36451f8d.png align="center")

We can choose the colour of the graph.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699878487264/93f1dcd3-05f1-4d82-976d-fa6dd4cd2448.png align="center")

### **Running Containers**

1. As the below screenshot shows, make the appropriate settings to reflect the total containers running in a stat form.
    
    * Choose the data source as influxdb. Grafana will collect the data from influxdb.
        
    * In the FROM section select docker. This will configure docker to the dashboard.
        
    * In the SELECT section choose n\_containers\_running. This will show the total number of containers running on the server.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699878666147/2ee2f3cf-34dc-4f93-a16d-62d1669f1a8a.png align="center")

### **Stopped Containers**

1. As the below screenshot shows, make the appropriate settings to reflect the stopped containers in a stat form.
    
    * Choose the data source as influxdb. Grafana will collect the data from influxdb.
        
    * In the FROM section select docker. This will configure docker to the dashboard.
        
    * In the SELECT section choose n\_containers\_stopped. This will show the total number of containers running on the server.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699878777105/bc125c63-ba79-466b-b568-6de005588651.png align="center")

### **Images**

1. As the below screenshot shows, make the appropriate settings to reflect the total images on the server in a stat form.
    
    * Choose the data source as influxdb. Grafana will collect the data from influxdb.
        
    * In the FROM section select docker. This will configure docker to the dashboard.
        
    * In the SELECT section choose n\_images. This will show the total number of containers running on the server.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699879451323/459c1f4d-5277-4fae-8611-e4db54bbe154.png align="center")

### **Containers memory**

1. As the below screenshot shows, make the appropriate settings to reflect all container's memory on the server in a stat form.
    
    * Choose the data source as influxdb. Grafana will collect the data from influxdb.
        
    * In the FROM section select docker. This will configure docker to the dashboard.
        
    * In the SELECT section choose **field**(**usage\_percent**) &
        
        **last**(). This will show usage percentage of the containers last used according to the time set.
        
    * In GROUP\_BY choose **time**(**$\_\_interval**)
        
        **tag**(**container\_name::tag**)
        
        **fill**(**null**)
        
        This will group all the containers an show corresponding values.
        
    * In FORMAT AS choose
        
        **Time series**
        
        **ALIAS $tag\_container\_name**
        
        This will show the tags for the graph. The tags are nothing but the container names displayed on below the graph indicating which graph is for which container.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699880213342/4e3b77ed-f088-4d6b-b9c0-138d0063f55b.png align="center")

### **Containers uptime**

1. As the below screenshot shows, make the appropriate settings to reflect all container's uptime on the server in a stat form.
    
    * Choose the data source as influxdb. Grafana will collect the data from influxdb.
        
    * In the FROM section select docker. This will configure docker to the dashboard.
        
    * In SELECT choose
        
        **field**(**uptime\_ns**)
        
        **last**()
        
        **alias**(**uptime\_ns**)
        
        This will display the uptime of each container currently running on the server.
        
    * In GROUP BY choose
        
        **tag**(**container\_name::tag**)
        
        This will group all the containers to show containers uptime
        
    * In FORMAT AS choose **Table** to veiw the details in a tabular form.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699880754270/ccdc002e-a590-4159-9263-6efb3787487b.png align="center")

Choose the Overrides setting in Table option. create a override and choose Field with name followed by uptime\_ns. Then choose Standard options &gt; Unit followed by nanoseconds(ns). This will show the uptime in nanoseconds.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699880862557/4364a818-bf59-49de-8935-008e26952b5b.png align="center")

### **Final Dashboard**

* Finally, add all the individual unit graphs and tables to the dashboard.
    
    Our Dashboard is ready now!!!!!!!!!!!!
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699880915129/b8818fdc-e6e3-42f8-8cc7-e8bb0784e43b.png align="center")

---

Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.