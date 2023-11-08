---
title: "Setting up Grafana"
datePublished: Wed Nov 08 2023 11:56:10 GMT+0000 (Coordinated Universal Time)
cuid: cloppf2lk001908l27gh879cd
slug: setting-up-grafana
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699444477010/77f6293e-0515-4ace-9f9f-ecdb3e499060.jpeg
tags: software-development, aws, cloud-computing, devops, grafana

---

Hope you are now clear with the basics of grafana, like why we use, where we use, what can we do with this and so on.

Now, let's do some practical stuff.

## Setup Grafana in your local environment on AWS EC2.

1\. Go to the AWS console, and create an EC2 instance named “grafana”.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699443709633/457a5626-387a-4c5b-8cf8-700c368a1143.png align="center")

2\. Allow the inbound port 3000 from the “Security Group”.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699443851139/26d5e66e-27a5-4e0a-9b2e-669cb38637c0.png align="center")

3\. Download the GPG keys and add them to the trusted keys list

```yaml
wget -q -O - https://packages.grafana.com/gpg.key | gpg --dearmor | sudo tee /usr/share/keyrings/grafana.gpg > /dev/null
```

4\. Add the Grafana repository to your APT sources:

```yaml
echo "deb [signed-by=/usr/share/keyrings/grafana.gpg] https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

5\. Refresh your APT cache to update your package lists:

```yaml
sudo apt update
```

6\. You can now proceed with the installation:

```yaml
sudo apt install grafana
```

7\. Once Grafana is installed, use `systemctl` to start the Grafana server:

```yaml
sudo systemctl start grafana-server
```

8\. Next, verify that Grafana is running by checking the service’s status:

```yaml
sudo systemctl status grafana-server
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699444023866/78e97ba3-d4d4-4d4e-9a29-f12e41f44aa4.png align="left")

9\. Now, goto the browser and search with “http:&lt;public-ip-of-ec2&gt;:3000”

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699444168803/493eb956-173a-4fcf-85a8-7929b6872259.png align="center")

10\. Login using default `login-id`\`and `password`\`as `admin`\` and `admin`\` then you can change this default password as you wish.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699444256168/68335b33-e1c9-4b4e-b8ba-0abed42fafc3.png align="center")

Here, we can see the dashboard of Grafana.

---

Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.