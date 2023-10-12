---
title: "Ansible Project 🔥"
datePublished: Thu Oct 12 2023 08:00:44 GMT+0000 (Coordinated Universal Time)
cuid: clnmw4b22000209l762ofaebn
slug: ansible-project
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697097601327/43122461-5807-4a60-8540-ba20819a95b4.png
tags: projects, ansible, devops, 90daysofdevops, trainwithshubham

---

Ansible playbooks are amazing, as you learned yesterday. What if you deploy a simple web app using Ansible, sounds like a good project, right?

### Task-01:

### \-&gt; Create 3 EC2 instances.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696766939968/517f297c-8d7b-4944-8ba1-6ae93b8731a6.png align="left")

### \-&gt; Install Ansible in a host server.

* Now, login to the Master server and run this command `sudo apt-add-repository ppa:ansible/ansible`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696761932889/ab3437aa-4f04-455c-b2e4-fef0504a36d1.png align="center")

* Now install Ansible using the commands given below:
    

```yaml
sudo apt update 
sudo apt install ansible
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696762107491/84d203f3-dff8-4947-8e8c-422c720e77fb.png align="center")

* You can verify the installation by checking the Ansible version:
    

```yaml
ansible --version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696762219900/52bf0b4f-a4c3-4733-b564-af943187a828.png align="center")

### \-&gt; Copy the public key of master server where Ansible is setup

* Simply use `ssh-keygen` in the Master as well as the Node server and copy the Master server **id\_rsa.pub** which is a public key and paste it on **authorized\_keys** in both the Node-1 and Node-2 servers.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696767282569/a466d990-7da7-487a-9d30-d09f1002ca55.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696767369761/1e12d4d6-ae67-4cf0-9e3d-011b123a003e.png align="center")

* Use `vim authorized_keys` to edit the file and paste the Master **id\_rsa.pub** in it. Do it in both the Nodes.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696767478345/7e8a56b8-1311-4a99-96c5-693fdacac0eb.png align="center")

* After this check whether you can access Node-1 or Node-2 from the Master node. Simply use `ssh (Node Private Ip address)`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696767694061/baff4af7-c83b-40d6-8876-eb8c9c51ecf8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696767720455/989ca7e1-137f-4cab-bc34-c5118c743354.png align="center")

* We successfully accessed the Node-1 and Node-2
    

### \-&gt; Now make an inventory file in the Master server and add the Private Ip address of both Node-1 and Node-2.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696767823749/04b330f1-8671-4f9d-895c-6312237597ed.png align="center")

**\-&gt; Try ping command using ansible to the Nodes.**

* Now use the command given below to ping the nodes:
    

```yaml
ansible -i inventory all -m ping
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696768029125/9ca05340-3ddb-404a-ae9b-4e8398ec1b76.png align="center")

We can see both pings are successful which indicates servers are in active states.

### \-&gt; Create a playbook to install Nginx

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697095499939/72ba27e6-5e31-4287-8a0d-ea1083ca0a7d.png align="center")

```yaml
  ---
  - name: Install Nginx
    hosts: all
    become: yes

    tasks:
      - name: Update apt package cache
        apt:
          update_cache: yes

      - name: Install Nginx
        apt:
          name: nginx
          state: present

      - name: Start Nginx
        service:
          name: nginx
          state: started
```

* Now use this command to run the playbook.
    

```yaml
  ansible-playbook install_nginx.yml -i (Path-of-inventory)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697095815230/a98d8939-d75d-46db-acc0-62ab8547a0f9.png align="center")

### \-&gt; Deploy a sample webpage using the ansible-playbook.

* Create an index.html file.
    

```yaml
<!DOCTYPE html>
<html>

<head>
  <title>Our Company</title>
</head>

<body>

  <h1>Welcome to Our Company</h1>
  <h2>Web Site Main Ingredients:</h2>

  <p>Pages (HTML)</p>
  <p>Style Sheets (CSS)</p>
  <p>Computer Code (JavaScript)</p>
  <p>Live Data (Files and Databases)</p>

</body>
</html>
```

* Now, update the install\_nginx.yml file.
    

```yaml
  ---
  - name: Install Nginx
    hosts: all
    become: yes

    tasks:
      - name: Update apt package cache
        apt:
          update_cache: yes

      - name: Install Nginx
        apt:
          name: nginx
          state: present

      - name: Start Nginx
        service:
          name: nginx
          state: started
          enabled: yes

      - name: Deploy website
        copy:
          src: index.html
          dest: /var/www/html
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697096235008/89568392-f52d-49ea-8d18-f468587dfa92.png align="center")

* Let's run this playbook.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697096309150/1a439e8f-e288-4cda-8762-ba37885b5842.png align="center")

* Check and verify the website deployed on all the servers.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697097173754/39c38c1f-efc8-4332-82c4-d0d024d7dfb0.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.