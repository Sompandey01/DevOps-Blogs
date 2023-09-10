---
title: "Relational Database Service in AWS"
datePublished: Sun Sep 10 2023 07:46:53 GMT+0000 (Coordinated Universal Time)
cuid: clmd5j8by000009igfdsyceo2
slug: relational-database-service-in-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694331816213/4eb1c996-e6a6-46fd-ad09-1a48aa2ff3ff.jpeg
tags: cloud, aws, devops, 90daysofdevops, trainwithshubham

---

## What is Amazon RDS?

Amazon Relational Database Service (Amazon RDS) allows you to set up, operate, and scale a relational database in the AWS Cloud. It manages the database instances while you focus on your applications.

## Task 1: Setting Up RDS and EC2 Connectivity with MySQL

**<mark>Step 1:</mark> Create a Free Tier RDS Instance of MySQL**

1. **Log in to your AWS Console**: Go to [**AWS Management Console**](https://aws.amazon.com/) and sign in to your AWS account.
    
2. **Open RDS Console**: In the AWS Management Console, navigate to the RDS service.
    
3. **Launch a DB Instance**:
    
    * Click on "Create database."
        
    * Choose "Standard Create."
        
    * Select the MySQL database engine.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694328274925/0608e895-5016-48be-bc78-e403d689d938.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694328331207/7b4259e5-c020-43c5-988e-11c21a6b7918.png align="center")

* In the "**Templates**" select "**Free tier**"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694328401457/81b54106-ba2e-42ab-af33-4cc69adaf8a5.png align="center")

* In "**Settings**" give a unique name to your database and either give a Password or Auto-generate it.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694328767207/dd482566-b111-469f-93ac-a61174b0f030.png align="center")

* Keep "Instance Configuration" and "Storage" settings as default.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694328874321/a589d506-f0e5-4ebe-b29b-c055ca84ae99.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694329011801/2531b88c-9b31-4646-be99-f2d53c1b30d6.png align="center")

* Now, in "**Connectivity**" choose "**Connect to an EC2 compute resource**" and click on "**Create EC2 instance**" if it's not created.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694329059660/016268f1-dad3-40ae-9705-a10530498667.png align="center")

* After creating the EC2 instance, Configure security group rules to allow inbound traffic on the appropriate port for the type of database you are using (e.g. port 3306 for MySQL).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694329419867/d6667338-0c16-43fd-ac1e-b8b980546a9a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694329479439/0f9f26df-3b55-41ec-ba85-a847c668d730.png align="center")

* Choose the VPC that you have created already while spinning EC2 instance.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694329556281/bc07a41f-34fd-4cfc-94d4-6407af400eae.png align="center")

* Use Password authentication to access the database and click on "**Create database**"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694329601908/e8c1ec02-2fe6-4dfb-a668-61db5c3b3739.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694329882328/d07bcc5e-3d88-4ce0-bb8d-82de459bef77.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694329937272/e53903e1-f8ea-43b9-9953-6448a99d1ba5.png align="center")

**<mark>Step 2</mark>: Create an IAM Role with RDS Access**

1. **Open IAM Console**: In the AWS Management Console, navigate to the IAM service.
    
2. **Create a New Role**:
    
    * Choose "Roles" from the left menu.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694330083324/8abd82ab-ca44-420d-9f0f-089b9ec8c241.png align="center")
    
    * Click "Create role."
        
    * Select the use case "EC2" and click "Next: Permissions."
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694330199890/8a069f8c-5ded-41ed-a790-e6c0d2329cbf.png align="center")
    
3. **Attach Policy**:
    
    * Search for and attach the policy "AmazonRDSFullAccess" to grant RDS access.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694330242621/b310862d-1f64-48c2-8999-7d94f176ab3c.png align="center")
    
4. **Review**:
    
    * Review the role details and provide a meaningful name.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694330304982/78650f87-7739-41f4-b2d7-cc0ed4c34b86.png align="center")
    
    * Click "Create role."
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694330341090/decc0b83-57bf-40b1-9359-98a01ca991ea.png align="center")
    
    * Role is Created Successfully.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694330412753/1d12b765-dc87-425a-8ab8-6eb25af980a0.png align="center")
    

**<mark>Step 3</mark>: Assign the Role to EC2**

1. **Open EC2 Console**: In the AWS Management Console, navigate to the EC2 service.
    
2. **Select Your EC2 Instance**:
    
3. **Actions &gt; Security &gt; Modify IAM role:**
    
    * Attach the IAM role you created and click on **update IAM role.**
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694330683796/461d84eb-5288-4a09-b833-dda2bc1dd1d1.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694330709610/37f847c4-7f6c-4b5d-bf37-6efa6209c166.png align="center")

**<mark>Step 4</mark>: Connect EC2 to RDS**

1. **SSH into EC2**: Use SSH to connect to your EC2 instance.
    
2. **Install MySQL Client**: If not already installed, install the MySQL client on your EC2 instance:
    

```bash
sudo apt-get update
sudo apt-get install mysql-client
```

* check whether MySQL is installed or not by running the below command.
    

```bash
mysql --version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694330990781/c22f888d-af8e-4f61-8678-63bf84accacf.png align="center")

* Once the MySQL client is installed, you can connect to the RDS instance using the following command:
    

```bash
mysql -h <RDS endpoint> -P <port> -u <username> -p
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694331750090/b662e254-6209-4194-a821-f715ba89caac.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.