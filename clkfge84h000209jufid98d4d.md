---
title: "Day 7: Understanding package manager and systemctl"
datePublished: Sun Jul 23 2023 13:07:02 GMT+0000 (Coordinated Universal Time)
cuid: clkfge84h000209jufid98d4d
slug: day-7-understanding-package-manager-and-systemctl
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690117535338/42081f80-4b68-4111-8659-0f24208fcf7e.webp
tags: linux, development, devops, linux-for-beginners, 90daysofdevops

---

## What is a package manager?

A package manager is a tool in Linux which is used to install, remove, update and upgrade the software packages on a Linux-based operating system. Using a package manager is one of the most efficient and secure ways to manage software on a Linux system, as it automates the process of installation and updates, reducing human errors and ensuring the system is kept in a stable state.

## What is a package?

A package is usually referred to as an application but it could be a GUI application, command line tool or a software library (required by other software programs). The package is like a gift box which contains all the software needed to install and run the programme on your computer. It makes it easy to get new software, keep it updated and remove it when you don't need it. It is managed by the **package manager**.

## Different kinds of package managers?

Here are some of the commonly used package managers in different Linux distributions:

1. **APT (Advanced Package Tool):** Used in Debian and Debian-based distributions, such as Ubuntu, Linux Mint, and elementary OS. It works with .deb packages.
    
2. **Yum (Yellowdog Updater, Modified):** Historically used in Red Hat Enterprise Linux (RHEL), CentOS, and older Fedora versions. It has been replaced by DNF in newer Fedora versions.
    
3. **DNF (Dandified Yum):** The successor to Yum, used in modern Fedora versions and CentOS 8 and above.
    

Each package manager has its own commands and syntax, but they all do the same things like installing a software, keep it updated and remove it when it's not needed.

## Installing Docker and Jenkins in your system from your terminal using package managers.

To install Docker and Jenkins in your system on Ubuntu or CentOS, open your terminal and use the following commands:

### Installing Docker on Ubuntu:

```bash
$sudo apt-get update
$sudo apt-get install docker.io
```

### Installing Docker on CentOS:

```bash
$sudoy  yum update
$sudo yum install docker
```

### Installing Jenkins on Ubuntu:

```bash
$sudo apt-get update
$sudo apt-get install jenkins
```

### Installing Jenkins on CentOS:

```bash
$sudo yum update
$sudo yum install jenkins
```

## systemctl and systemd

In Linux, `systemctl` and `systemd` are two essential components related to managing and controlling system services. `systemd` is a system and service manager for Linux operating systems. `systemctl` is the command-line interface to control and interact with the `systemd` system and service manager.

## Check the status of the docker service in your system:

To check the status of the docker service in your system use the following command:

```bash
$systemctl status docker
```

## Stop the service of Jenkins

To stop the service of Jenkins simply use the following command:

```bash
$sudo systemctl stop jenkins
```

## The commands of systemctl vs service

Both systemctl and service are used to control services, but the systemctl is new and more powerful.

The command to check docker status in systemctl and service use:

**systemctl:**

```bash
$systemctl status docker
```

**service:**

```bash
$service docker status
```

## Commands of systemctl:

1. To start a service:
    

```bash
sudo systemctl start service_name
```

1. To stop a service:
    

```bash
sudo systemctl stop service_name
```

1. To restart a service:
    

```bash
sudo systemctl restart service_name
```

1. Check the status of a service:
    

```bash
sudo systemctl status service_name
```

## Commands of service:

1. To start a service:
    

```bash
sudo service service_name start
```

1. To stop a service:
    

```bash
sudo service service_name stop
```

1. To restart a service:
    

```bash
sudo service service_name restart
```

1. Check the status of a service:
    

```bash
sudo service service_name status
```

I hope you like my blog..!!

Stay Connected with me for more interesting articles on DevOps, if you like my blog follow me on **Hashnode** and **Linkedin** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/))