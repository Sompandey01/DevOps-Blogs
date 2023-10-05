---
title: "Your CI/CD pipeline on AWS - Part 3 🚀 ☁"
datePublished: Thu Oct 05 2023 11:56:47 GMT+0000 (Coordinated Universal Time)
cuid: clnd4gwje000009ifgrt39xd0
slug: your-cicd-pipeline-on-aws-part-3
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695705770079/c98684d8-01aa-49d1-9747-7b0a3adb060e.png
tags: cloud, aws, devops, 90daysofdevops, trainwithshubham

---

On your journey of making a CI/CD pipeline on AWS with these tools, you completed AWS CodeCommit & CodeBuild.

Next few days you'll learn these tools/services:

* CodeDeploy
    
* CodePipeline
    
* S3
    

## What is CodeDeploy?

AWS CodeDeploy is a deployment service that automates application deployments to Amazon EC2 instances, on-premises instances, serverless Lambda functions, or Amazon ECS services.

CodeDeploy can deploy application content that runs on a server and is stored in Amazon S3 buckets, GitHub repositories, or Bitbucket repositories. CodeDeploy can also deploy a serverless Lambda function. You do not need to make changes to your existing code before you can use CodeDeploy.

### Task 1:

### \-&gt; Read about Appspec.yaml file for CodeDeploy.

The AppSpec file provides an easy way to specify deployment instructions for AWS CodeDeploy in a declarative YAML format. It allows you to customize the deployment process to meet the specific needs of your application.

### \-&gt; Deploy index.html file on EC2 machine using nginx

* Create an instance or restart the previous one.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695708125698/2878b7dc-e71b-441e-b874-34abb2634027.png align="center")

* Now, let's create a CodeDeploy application. In AWS Console navigate to the CodeDeploy service.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695708857548/1e5ab755-38cd-4dcb-b598-f3fb4f910bd9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695708928524/143e387f-e7c4-47b4-82a1-e7df23e77f92.png align="center")

* Click on "**Create application**" give it a name and select **EC2/On-Premises** as a compute platform.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695709062478/c4c7acb5-d2c3-4b95-a90e-94e418eff797.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695709084550/7ab8a6ea-18a7-4436-af01-1eb5d8b78c49.png align="center")

* Before creating a deployment group, we have to create an IAM role and give all the necessary permissions to it.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695726941559/669dbb50-cf28-4b9c-8932-207ff0ac6190.png align="center")

* Update the Trust relationship in order to grant AWS CodeDeploy access to your target instances.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695726991131/f31af8dc-d9f7-4dc4-ab97-9838a7b839ee.png align="center")

```yaml
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Principal": {
                    "Service": "codedeploy.amazonaws.com"
                },
                "Action": "sts:AssumeRole"
            }
        ]
    }
```

* Now, let's create a deployment group, in the CodeDeply application click on "**Create deployment group**" and give it a name.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695709257507/4ecfd6e9-a621-43fe-8d2b-a2ae220e79e3.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695727098479/00e903f2-3fdc-4999-b4b3-6966b17175e6.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695727135573/a6754f2a-6e92-4eb7-9b53-5d4cffbd9cfb.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695727194458/fd31394d-5bdb-4798-8c8c-c47a3a1012eb.png align="center")

* Click on "**Create deployment group**".
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695727228113/6687ac5f-37c0-48d8-821a-d62a195f58be.png align="center")

* Now we need to install the CodeDeploy agent on the server for which we need to write a script file with all the dependencies.
    

```yaml
#!/bin/bash 

# This script installs the CodeDeploy agent and its prerequisites on Ubuntu 22.04.  

# Update package list
sudo apt-get update 

# Install Ruby and its dependencies
sudo apt-get install ruby-full ruby-webrick wget -y 

# Change to temporary directory
cd /tmp 

# Download the CodeDeploy agent package
wget https://aws-codedeploy-us-east-1.s3.us-east-1.amazonaws.com/releases/codedeploy-agent_1.3.2-1902_all.deb 

# Create a directory to extract the package contents
mkdir codedeploy-agent_1.3.2-1902_ubuntu22 

# Extract the package contents
dpkg-deb -R codedeploy-agent_1.3.2-1902_all.deb codedeploy-agent_1.3.2-1902_ubuntu22 

# Update the package dependencies to use Ruby 3.0
sed 's/Depends:.*/Depends:ruby3.0/' -i ./codedeploy-agent_1.3.2-1902_ubuntu22/DEBIAN/control 

# Repackage the updated package
dpkg-deb -b codedeploy-agent_1.3.2-1902_ubuntu22/ 

# Install the updated package
sudo dpkg -i codedeploy-agent_1.3.2-1902_ubuntu22.deb 

# List all systemd units that contain "codedeploy" in their name
systemctl list-units --type=service | grep codedeploy 

# Check the status of the CodeDeploy agent service
sudo service codedeploy-agent status
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695727483542/1b35eb33-f8f8-467a-8027-ff82599ae253.png align="center")

* Let's run this script.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695727779197/5c6067c1-9c59-4336-b6aa-4c24e6aecfb1.png align="center")

### Task 2: Add appspec.yaml file to CodeCommit Repository and complete the deployment process.

* AppSpec file is required to create a bridge between the AWS CodeDeploy and EC2 instance. Let's create one...
    

```yaml
version: 0.0               #specifies the version number of the file format.
os: linux                  #specifies the operating system to be used.
files:                     #is an array of files to be copied from the source to the destination directory.
  - source: /               #specifies the source directory.
destination: /var/www/html #specifies the destination directory where the files will be copied to.
  hooks:                   #is an array of scripts to be executed at different points during the deployment process.
    AfterInstall:          #specifies a script to be executed after the installation of the application.
      - location: scripts/install_nginx.sh #specifies the location of the script file to be executed
        timeout: 300       #specifies the maximum amount of time in seconds that the script can run for.
        runas: root        #specifies the user that the script should be run as.
    ApplicationStart:      #specifies a script to be executed after the application has started.
      - location: scripts/start_nginx.sh
        timeout: 300
        runas: root
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695728148509/5cf2e746-adc6-4232-b6d6-c71cfa28102a.png align="center")

* Now we have to create 2 scripts for installing nginx and starting nginx.
    
* install\_nginx.sh
    

```yaml
#!/bin/bash

sudo apt-get update && sudo apt-get install -y nginx
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695728308215/ed805f8c-78d8-41b7-93d2-2cef3e88fb7b.png align="center")

* start\_nginx.sh
    

```yaml
#!/bin/bash

sudo systemctl start nginx
sudo systemctl enable nginx
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695728411102/2dac27ec-8117-4d23-a37e-87b7986b1c3a.png align="center")

* We also have to change the buildspec.yaml file so that the CodeBuild will build the appspec.yml file and transfer the artifact to S3 bucket.
    

```yaml
version: 0.2

phases:
  install:
    commands:
      - echo Installing NGINX - echo apt-get install NGINX
      - sudo apt-get update
      - sudo apt-get install nginx -y
  build:
    commands:
      - echo Build started on date
      - cp index.html /var/www/html
  post_build:
    commands:
      - echo Configuring NGINX
artifacts:
    files:
      - "**/*"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695728528911/1e8aa5f1-e88d-4cfe-b1e6-d42f042f4432.png align="center")

* Let's push all the changes to the CodeCommit repository.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695728705494/c443b3b4-5bbc-4a32-8931-02a57d8ecf1e.png align="center")

* You can view the new code files in the CodeCommit repository.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696506691213/863f4f79-d839-42fe-a18f-04301ed69530.png align="center")

* Let's edit the build, select the artifacts and update it after that start the build.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696506821908/45e93f6a-bf58-4ef8-8c3c-a81409fcd9fe.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696506885376/64d30867-b2b3-4a7a-b12e-1e9f65b059c4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696506908340/95421a74-6698-4884-a885-d93dac7fb836.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695728831626/53b25972-9966-412f-9a82-05a63f0fee35.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695728978586/a25ee5c2-a8f5-405e-9bf0-4877e610e796.png align="center")

* Now, We have to Create a role for giving access to the EC2 instance with all the necessary permission policies as shown below.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695729236341/6d3ed077-74ca-4ccf-8110-f848317e11d7.png align="center")

* Now, navigate to the instance and modify the IAM role. Select the IAM role created above.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695729312072/609d823b-72b3-444a-9a4d-9e87ad23e7c8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695729326918/73a3fa85-9d6c-4fd9-98aa-47742007f5ea.png align="center")

* Now create a deployment in the deployment group that we made previously.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695729431198/0a128c0f-5144-4590-b185-a8d8accf42ec.png align="center")

* Click on "**Create deployment**"
    
* Provide the S3 artifactory details. This will pull the code at the time of CodeDeploy. Then create the deployment.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696506597358/ae5ffb13-fe85-42dd-afc7-6957c8fd0eef.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695729616963/9ccb7c42-b563-4239-924c-0035bb889e05.png align="center")

* Click on "**Create deployment**"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695804176129/108665df-603a-4e70-b3f3-3a89a1259e68.png align="center")

* Restart the codedeploy-agent in the EC2 instance.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695729861254/2c2aae50-690a-4b64-b271-99fa0970a32d.png align="center")

* Once the codedeploy-agent restarted, the deployment will get completed successfully.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695731868332/ae27bb5a-2424-4b32-b736-da300cf097ac.png align="left")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.