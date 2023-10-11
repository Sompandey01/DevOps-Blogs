---
title: "Ansible Playbooks"
datePublished: Wed Oct 11 2023 08:23:20 GMT+0000 (Coordinated Universal Time)
cuid: clnlhhirj000008mogq1qabg3
slug: ansible-playbooks
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697012568585/50305b45-dff0-4aff-91a4-30fffc383f9a.png
tags: software-development, ansible, devops, 90daysofdevops, trainwithshubham

---

Ansible playbooks run multiple tasks, assign roles, and define configurations, deployment steps, and variables. If you’re using multiple servers, Ansible playbooks organize the steps between the assembled machines or servers and get them organized and running in the way the users need them to. Consider playbooks as the equivalent of instruction manuals.

## Task-01:

## \-&gt; Write an Ansible playbook to create a file on a different server

Before we start writing playbooks please make sure to check this blog for better understanding:

%[https://hashnode.com/post/clnhg83ub000109l136my68o4] 

* Let's create an Ansible playbook to create a file on a different server.
    

```yaml
  ---
  - name: Create a file on a different server
    hosts: all
    become: yes
    tasks:
      - name: Create a file
        file:
          path: /home/ubuntu/day58.txt
          state: touch
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697005993278/b93eb242-b4b8-4359-9461-149e2cb488fa.png align="center")

* Now use this command to run the playbook.
    

```yaml
  ansible-playbook create_file.yml -i (Path-of-inventory)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697006110315/f6e32265-068d-4df4-8cea-76c50a65aa1a.png align="center")

* Verify that the file has been created at the specified location on a different server.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697006240825/8afb1434-f3a9-42de-95d7-72a254e91a7e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697006256360/1e4633b6-3602-4f3f-b6f0-a788319fd53a.png align="center")

* We can also check this by using a simple command given below:
    

```yaml
  ansible all -a "ls /home/ubuntu" -i (Path-Of-Inventory)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697006500509/609e56cd-d555-4cbe-a0d8-9672492dfc8f.png align="center")

## \-&gt; Write an ansible playbook to create a new user.

* Let's create an ansible playbook to create a new user.
    

```yaml
  ---
  - name: Create a new user
    hosts: all
    become: yes
    tasks:
      - name: Add a new user sompandey
        user: name=sompandey
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697006787202/558e7c49-c5cc-49df-b500-cbb561a52902.png align="center")

* Now use this command to run the playbook.
    

```yaml
  ansible-playbook create_user.yml -i (Path-of-inventory)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697006832732/519f00c3-dc51-438e-bcc3-c1721c2c357b.png align="center")

* To check the created user from the master server use the below command:
    

```yaml
  ansible all -a "cat /etc/passwd" -i (Path-Of-Inventory)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697006936357/ff51c1e1-256c-4b2e-9ce7-5565dab1e87b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697006953294/9d37ca63-79f1-4c84-bf49-05e7b02284d4.png align="center")

## \-&gt; Write an Ansible playbook to install docker on a group of servers

* Let's create an Ansible playbook to install docker on a group of servers.
    

```yaml
   ---
  - name: Install Docker on multiple servers
    hosts: all
    become: yes
    tasks:
      - name: Add Docker GPG key
        apt_key:
         url: https://download.docker.com/linux/ubuntu/gpg
         state: present

      - name: Add Docker APT repository
        apt_repository:
         repo: deb https://download.docker.com/linux/ubuntu focal stable
         state: present

      - name: Install Docker
        apt:
          name: docker.io
          state: present
        become: yes
      - name: Start Docker service
        systemd:
          name: docker
          state: started
          enabled: yes
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697007227495/191e741a-2658-4b36-8c84-c0441d1a6cbd.png align="center")

* Now use this command to run the playbook.
    

```yaml
  ansible-playbook install_docker.yml -i (Path-of-inventory)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697007333708/49c75dce-1f23-4757-a552-a7b8eef0a8ab.png align="center")

* To verify that Docker has been installed on multiple servers use the command given below:
    

```yaml
  ansible all -a "docker --version" -i (Path-Of-Inventory)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697007429484/cc858c35-41a5-41f3-8f74-8f9d5302b900.png align="center")

## Task-02: Write a blog about writing Ansible playbooks with the best practices.

Ansible playbooks are a powerful way to automate server configuration and application deployments. However, poorly written playbooks can quickly become a mess. Here are some best practices to follow when writing Ansible playbooks:

### Use a logical structure

* Split playbooks into multiple files based on roles or functions. This keeps each file focused and reusable.
    

```yaml
  site.yml
  webservers.yml
  appservers.yml
```

* Group related tasks into blocks for readability.
    
* Use consistent indentation (2 spaces is common).
    

### Define variables

* Define all variables at the top of the playbook. This makes playbooks dynamic and reusable.
    
* Use meaningful variable names.
    
* Avoid hardcoding values within tasks.
    

```yaml
  vars:
    app_name: my_app  
    db_name: my_app_db
```

### Use groups

* Group your hosts into logical categories like web servers, app servers, etc.
    
* Use group variables to define variables specific to a group.
    

```yaml
  webservers:
    hosts:
      server1:
      server2:

  appservers:
    hosts:  
      server3:
      server4:
```

### Create roles

* Create roles for each set of related tasks.
    
* Roles encapsulate reusable code and make playbooks modular.
    

```yaml
  - name: Configure webservers 
    hosts: webservers  
    roles:
      - { role: nginx }
```

### Handle failure gracefully

* Use `failed_when:`, `ignore_errors:` and `changed_when:` to handle non-critical failures and unexpected changes.
    
* This keeps playbook execution going despite minor issues.
    

```yaml
  - name: Install packages  
    apt: name={{item}}   
    with_items: [pkg1, pkg2]
    ignore_errors: yes
```

### Add comments

* Use comments to document what a playbook does and how to use it.
    
* Good commenting improves readability and maintainability.
    

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.