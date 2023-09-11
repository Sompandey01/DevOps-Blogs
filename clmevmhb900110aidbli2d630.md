---
title: "Deploying Wordpress website on AWS"
datePublished: Mon Sep 11 2023 12:45:00 GMT+0000 (Coordinated Universal Time)
cuid: clmevmhb900110aidbli2d630
slug: deploying-wordpress-website-on-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694436193556/a3ac63a0-2439-4f20-9f59-665867db2bf9.jpeg
tags: cloud, aws, devops, 90daysofdevops, tws

---

Over 30% of all websites on the internet use WordPress as their content management system (CMS). It is most often used to run blogs, but it can also be used to run e-commerce sites, message boards, and many other popular things. This guide will show you how to set up a WordPress blog site.

## What is WordPress?

WordPress is a free and open-source content management system (CMS) written in PHP and paired with a MySQL or MariaDB database. WordPress provides an easy way for anyone to create and manage a website without much technical knowledge through its intuitive admin interface and ecosystem of plugins and themes.

## Task: Deploying WordPress on AWS with RDS and EC2

**To configure this WordPress site, you will create the following resources in AWS:**

* An Amazon EC2 instance to install and host the WordPress application.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694432122205/19f2d5f5-4e82-44b0-9b54-3c15fec13a96.png align="center")

* After creating the EC2 instance, Configure security group rules to allow inbound traffic on the appropriate port for the type of database you are using (e.g. port 3306 for MySQL).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694432154828/09c3cad0-414e-4676-b217-0dc531b68dae.png align="center")

**As WordPress requires a MySQL database to store its data ,create an RDS as you did in Day 44**

%[https://hashnode.com/post/clmd5j8by000009igfdsyceo2] 

* Now, Login to AWS EC2 instance and install MySQL-client in the server using the below command:
    

```bash
sudo apt update
sudo apt install apache2 php libapache2-mod-php php-mysql -y
```

* After installing MySQL-Client, Login to the database server and connect to the RDS instance using the MySQL client with the endpoint address, username, and password using this command:
    

```bash
mysql -h <endpoint address> -P <port.no> -u <username> -p
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694432732495/ee3c2e8b-1826-4bc5-8a49-750024d642c9.png align="center")

* Now run these commands to create a database and user.
    

```bash
CREATE DATABASE wordpress;
CREATE USER 'wordpress' IDENTIFIED BY 'wordpress-pass';
GRANT ALL PRIVILEGES ON wordpress.* TO wordpress;
FLUSH PRIVILEGES;
Exit
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694432872618/4c0bf495-78cd-4a61-891e-28ddd99b3c86.png align="center")

* Now, install apache2.
    

```bash
sudo apt-get update && sudo apt install -y apache2
```

* Let’s check the public IP URL to view Apache2 web page.
    
* Install WordPress on the server.
    

```bash
wget https://wordpress.org/latest.tar.gz 
tar -xzf latest.tar.gz
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694433281273/703724c5-8152-4a66-af8a-aee20887f37e.png align="center")

* Now create a copy of the config file and edit the wp-config.php file
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694433664296/9eeb5136-5242-4ca9-a8db-10554a84c51d.png align="center")

* Update the WordPress configuration file (`wp-config.php`) with the database connection details using `vim wp-config.php`
    
* Edit the database configuration by changing the following lines:
    

```bash
// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', 'database_name_here' );

/** MySQL database username */
define( 'DB_USER', 'username_here' );

/** MySQL database password */
define( 'DB_PASSWORD', 'password_here' );

/** MySQL hostname */
define( 'DB_HOST', 'localhost' );
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694433948387/ae07938d-6e37-44d5-9c62-b30cc8f55459.png align="center")

* Copy the extracted WordPress files to the Apache web server document root:
    

```bash
sudo cp -r wordpress/* /var/www/html/
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694434270591/55cb00d1-bb0b-48b8-8bfc-c3dc5d6b1303.png align="center")

* Now, restart the Apache web server:
    

```bash
sudo systemctl restart apache2
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694434362527/f3c17185-6dff-4604-80d2-196dc79f6a77.png align="center")

* Navigate to &lt;public IP&gt;/wp-admin/ to view the WordPress website.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694435444532/ea55528a-5827-4287-acf7-905892a5d8c7.png align="center")

* Now we can create a user in the WordPress site to get going in the application.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694435494208/9afcd70e-1d4f-4feb-b877-71585e81592a.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.