---
title: "Everything You Need to Know About AWS EBS (with Hands-on)"
datePublished: Tue Oct 28 2025 10:38:06 GMT+0000 (Coordinated Universal Time)
cuid: cmhafo0jj000302l3bwxe03ih
slug: everything-you-need-to-know-about-aws-ebs-with-hands-on
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1761647739383/530646d3-02a3-4f1c-99b1-7ea2bd9f4649.jpeg
tags: aws, cloud-computing, devops, aws-certified-solutions-architect-associate, devops-articles

---

In this blog, we’ll dive deep into one of the most important storage services in AWS — **Elastic Block Store (EBS)**.  
By the end of this guide, you’ll not only understand what EBS is, but you’ll also *create*, *attach*, *expand*, *take backups*, and *restore* data between EC2 instances using snapshots.

Whether you’re a learner or an aspiring DevOps engineer, this hands-on guide will help you understand how EBS is used in the real world.

## ☁️ What is AWS EBS?

EBS stands for **Elastic Block Store** — it’s a persistent block storage service designed for use with Amazon EC2 instances.

Think of EBS as a *virtual hard drive* for your EC2 instances. It stores your data permanently (even after you stop or terminate your instance, if the volume is detached or backed up).

Each EBS volume is automatically replicated within its **Availability Zone** to protect you from hardware failures.

## ⚙️ Why EBS Matters

EBS volumes are essential in real-world projects because they:

* Store databases, application files, or logs persistently
    
* Allow you to scale storage dynamically
    
* Let you back up data using **snapshots**
    
* Enable **disaster recovery** by restoring snapshots to new instances
    

## 🧩 Step 1: Create an EC2 Instance

First, we’ll create an EC2 instance to attach our EBS volume to.

1. Go to **AWS Console → EC2 → Instances → Launch Instance**
    
2. Choose **Ubuntu** or any other image you’re comfortable.
    
3. Select instance type (e.g., `t2.micro`)
    
4. Configure key pair & security group
    
5. Launch the instance
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760617642590/7ba491df-fcfa-467b-80ba-fe0c6573a5eb.png align="center")

6. Connect to the instance and check the default disk space `8G`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760616504617/c5972d5c-12d8-43db-b8e8-f633ce726423.png align="center")

* This is the default EBS volume which is created along with the ec2 instance and will store your data.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760616669006/52826025-cf0b-4881-b5f3-8d0b4071ebb5.png align="center")

## 🧩 Step 2: Create and Attach an EBS Volume

1. Go to **EC2 → Elastic Block Store → Volumes → Create Volume**
    
2. Choose:
    
    * Volume type: **gp3 (SSD)**
        
    * Size: **20 GB**
        
    * Availability Zone: *same as your EC2 instance (ap-south-1a)*
        
3. Click **Create Volume**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760616801810/e7e18da3-b200-446f-9f54-492e531470d3.png align="center")
    
4. Once created, give it a name, select it→ **Actions → Attach Volume**
    
    * Select your EC2 instance
        
    * Device name: `/dev/sdk` ( You can choose any one you like)
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760616822225/0af6827c-ffcb-490f-966b-896c59c4434a.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760616985956/37c832c9-9e68-4d07-a356-f8e55babe485.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760617074712/c9bf4aea-a195-4338-ae46-5e0e8ba28e3b.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760617711949/1fb118db-263a-40d1-a31a-738c1cad54ce.png align="center")
        
5. Done! Your new EBS volume is now attached to your instance.
    

## 🧩Step 3: Mount and Use the EBS Volume

Now we’ll make the volume usable inside the EC2 instance. SSH into the instance and list the block devices `lsblk`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760617934954/641ee175-7c67-4bd7-9262-cc33318fd506.png align="center")

1. Check disk partition - `sudo fdisk -l` . It shows the path of disk volume, use it to check the file system of the EBS volume
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760618140832/69e6ee06-255d-4bd2-af43-4146d9fcbc3e.png align="center")

2. To check the filesystem run - `sudo file -s (path)`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760620438185/7d12a692-16b5-4a36-8dda-9929c95dd885.png align="center")

* If the output is data then it means no file system is created for this EBS vloume and we need to create the file system for the EBS and later we have to mount it.
    
* Command to make the file system - `sudo mkfs -t xfs /dev/nvme1n1` ( use your disk path)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760620620569/ac63c3f6-6fa1-42d9-b763-0da7dd105560.png align="center")

* Let’s check the output of the file system again
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760620739765/0ce7350b-6241-4635-ba58-8e79c0df523c.png align="center")

* Previously it was showing the data but now it’s changed to the filesystem. What’s next? We did pretty much everything what’s left is to mount this volume to the directory. Let’s create a directory and mount it to our EBS volume.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760684861599/d0d8c2b4-d943-4b8f-8bb7-20f79e55087a.png align="center")

* Directory is created let’s mount it now ( Command - `sudo mount [path-of-ebs] [path-of-directory]` )
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760685227469/2cd92b5a-a7e6-422c-b6f1-7b0d3d017a3f.png align="center")

* There’s one more command to check that the volume is in use ( `df -h` )
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760685456783/86265cb8-b518-4642-8b66-063189781894.png align="center")

* As you can see from the 20G 425M is used, volume is in use now.
    

## Step 4: Increase the EBS Volume Size

<mark>Note:</mark> You can only increase the volume but you can not decrease it

In real-world scenarios, applications grow — so you’ll need to expand your storage.

1. Go to **EC2 → Volumes → Modify Volume**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760685722934/97f27a6a-440b-45a3-97d4-47ba3fadc83c.png align="center")
    
2. Increase size (e.g., from 20 GB → 25 GB)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760686006078/ee637b70-18d9-4e3c-8e40-08ed7a78c690.png align="center")
    
    * Click **Modify → Yes**
        
    * Wait for some minutes after you modify it. When it’s modified run - `lsblk` to recheck the volume size
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760687225539/853a6d0d-27ca-4835-92c4-cecc773c97eb.png align="center")
        
    * Volume size is increased. Are we done ? No, here’s a twist your volume size does got increased but but but your file system size which you defined previously as **20G** is still **20G**. How to check it? Use `df -h`
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760687375464/67af12a1-bd28-46e7-b6dd-78118509acad.png align="center")
        
3. Well are we stuck ? No, here’s a simple and easy command to resize it ( - `sudo xfs_growfs filesystem-name` ).
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760687958090/5efab236-8c48-4daf-851d-4e4ea6eebc4b.png align="center")
    
4. It’s done. Let’s more forward to the next part
    

## Step 5: Taking the snapshot of the data and attaching it to the another ec2 instance

Let’s first insert some data in the EBS and then we will take the snapshot of the EBS in short the data present in the EBS volume. Snapshot is the backup of the data. So if you want to backup some data in the snapshot make sure you have everything present cause snapshot will only backup the data which is present in the real time so we aware. After the snapshot is taken and the EBS volume is getting more data it won’t be saved.

1. First I’ll go in the directory `/ebsvolume` where we mounted our EBS volume and will create some files there
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760702855285/ce40e7f9-4375-47c9-8d46-afbc0ef7fb3b.png align="center")

2. We created 2 demo files now let’s create another ec2 instance and then we will take the snapshot and attach it with the new ec2 instance
    
3. Created Dev-2 ( new ec2 instance)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760703197402/2558491d-ee84-446e-84fc-1449afb388b2.png align="center")

4. Let’s move ahead and take the snapshot from the volume. Volumes → Select your volume → Actions → Create Snapshot
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760703252325/2e021f67-8aab-4ee8-a437-55a90cf741e1.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760703350055/7f4c4cd6-8e75-46de-9444-4eed7cb6b54c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760703453463/12492818-ff57-463f-bd2f-55990b538dc5.png align="center")

5. Now you have a backup that you can use later to restore data or migrate to another instance.
    
6. Snapshot is created but we have to create the volume from the snapshot in order to attach it with the EC2 instance so let's do it.
    
7. Go to **Snapshots → Select Snapshot → Actions → Create Volume (** Use the same or new Availability Zone and Keep size ≥ original **)**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760703532389/9fbfc977-b11b-4dba-b514-eb63878c3db2.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760703633825/d1270397-484e-479c-a138-125ffed76de8.png align="center")

* Created the volume you can rename it whatever you want
    

8. Now do the same attach process we did previously with the **Dev-1** attach this vol to the newly created EC2 instance
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760703805432/d173e967-697b-49c9-9145-e2cf402d5248.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760703854828/35aeeb04-d2cd-41a1-9b1e-cd75161b9607.png align="center")

* It’s attached let’s verify from the console
    

9. If you check the filesystem in the EBS it’s already there cuz we created it in the **dev-1 vol** the only thing left is to mount it
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760704085750/a22d59bb-3e18-4ca9-8cb0-2844b167030e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760704257937/cdd204ad-9c0a-41eb-b834-d5c4c3e79d52.png align="center")

10. Now the mount is complete. Let’s check if the data from the **dev-1 vol** is there or not.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1760704388233/2893182c-aacb-45f2-9bfc-4a1ed3b397f8.png align="center")

The same data (`demo1.txt`, `demo2.txt`) appears here too!

You’ve successfully backed up and restored data using AWS EBS snapshots.

<mark>Note</mark>: If you create any new files in the **dev-1** it won’t be reflected in the **dev-2**

## Blog Summary

In this blog, I explored everything you need to know about **AWS EBS (Elastic Block Store)** — from understanding how it works to hands-on implementation. I covered creating and attaching EBS volumes to EC2 instances, resizing storage, taking **snapshots for backups**, and restoring them in another EC2 instance. Perfect for anyone looking to get real, practical AWS experience!