---
title: "Understanding Ad-hoc commands in Ansible"
datePublished: Mon Oct 09 2023 12:01:43 GMT+0000 (Coordinated Universal Time)
cuid: clniueo4e000u09l216660ccy
slug: understanding-ad-hoc-commands-in-ansible
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696852387131/c456cba0-a754-4070-86a4-33e88fa20205.jpeg
tags: ansible, devops, 90daysofdevops, ansible-playbook, trainwithshubham

---

## What are Ad hoc commands?

Ansible ad hoc commands are one-liners designed to achieve a very specific task they are like quick snippets and your compact swiss army knife when you want to do a quick task across multiple machines.

To put simply, Ansible ad hoc commands are one-liner Linux shell commands and playbooks are like a shell script, a collective of many commands with logic.

Ansible ad hoc commands come in handy when you want to perform a quick task.

## Task-01: Write an ansible ad hoc ping command to ping 2 servers from the inventory file

We have already created EC2 instances and made a connection between them. Check out this blog for a better understanding:

%[https://hashnode.com/post/clnhg83ub000109l136my68o4] 

* Let's start the instances.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696851582701/b7c00bdd-3349-4f69-b838-71a5b636ec92.png align="center")

* Now connect to the Master instance and ping the 2 servers.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696851757148/55210114-faf2-421a-8122-ea000376d6e4.png align="center")

## Task-02: Write an ansible ad hoc command to check uptime

To check the uptime of a remote server using Ansible's ad hoc command, you can use the `ansible` command with the `-a` option for the `uptime` command. Here's the command and an explanation of each part:

```yaml
ansible <target_host> -m command -a uptime
```

* `<target_host>`: Replace this with the hostname or IP address of the remote server you want to check the uptime for.
    
* `-m command`: This specifies the Ansible module to use. In this case, we're using the `command` module, which allows us to execute a shell command on the remote host.
    
* `-a "uptime"`: This is the argument passed to the `command` module. It specifies the shell command to run on the remote host, which is simply "uptime" in this case.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696851961168/4954a49d-afd5-4469-9915-843645c05761.png align="center")

## Task-03: Ansible ad hoc command to check the free Ram memory or memory usage of hosts.

```yaml
ansible <target_host> all -a "free -m"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696852529589/adc01e57-1ba2-47d7-9311-8daafc2edb0e.png align="center")

## Task-04: Write an ansible ad hoc command to check the disk space on all hosts in an inventory file.

```yaml
ansible <target_host> all -m shell -a "df -h"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696852684835/dcf49bed-758b-4bc0-a93b-a2ac9cc5262d.png align="center")

## Task-05: Write an ansible ad hoc command to list all the running processes on a specific host in an inventory file.

```yaml
ansible <target_host> specific_host -m command -a 'ps aux'
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696852797862/8fbedfea-5cf2-48b8-b017-a87fb96467c5.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.