---
title: "DevOps Project 01"
datePublished: Sat Feb 03 2024 09:51:12 GMT+0000 (Coordinated Universal Time)
cuid: cls5w9hgn000208l9emanczxt
slug: devops-project-01
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706953752792/5e9e070d-b819-4fa0-b275-6b6e663ee2e2.jpeg
tags: docker, devops, jenkins, 90daysofdevops, trainwithshubham

---

In this story, we embark on a DevOps project centered around deploying a Django notes app on an EC2 instance through a Jenkins declarative CI/CD pipeline. Leveraging Docker containers and Docker Hub for efficient containerization and image management, our focus is on automating the deployment process, ensuring a seamless integration and delivery of the application.

![](https://miro.medium.com/v2/resize:fit:525/1*BC13vc4rmdXB8Fn9HZpTgQ.jpeg align="center")

**Prerequisites:**

Before delving into the project, let's ensure we have the necessary prerequisites in place.

1. **Create AWS Instance:**
    
    * Name: jenkins-server
        
    * AMI: ubuntu
        
    * Instance type: t2.micro (free tier)
        
    * Key pair login: Create &gt; docker.pem
        
    * Allow HTTP
        
    * Allow HTTPS
        
    
    Download the .pem file, click on Launch Instance, then connect to the EC2 instance and install the following packages.
    
2. [**Docker Installation:**](https://docs.docker.com/engine/install/)
    
3. **OpenJDK-17-JRE Installation:**
    
    ```yaml
    sudo apt install openjdk-17-jre
    ```
    
4. [**Jenkins Installation:**](https://www.jenkins.io/doc/book/installing/)
    
5. **Docker Compose Installation:**
    
    ```yaml
    sudo apt-get install docker-compose
    ```
    

Ensure you have these packages installed on your system. Additionally, add users to the Docker group for proper permissions. Run the following commands:

```yaml
sudo usermod -aG docker $USER
sudo usermod -aG docker jenkins
sudo reboot
```

Remember to reboot the system after implementing these changes.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706950340222/afa5c9d8-299a-430a-9d35-b4ec97c0d973.png align="center")

To configure Jenkins for your CI/CD pipeline, follow these steps:

1. **Allow Inbound Rule:** Open inbound ports 8080 and 8000 for this machine in the security group of your EC2 instance. Find the security group in the EC2 instance description.
    
2. **Access Jenkins Portal:** Copy the public IP of the machine and paste it into the browser to access the Jenkins portal.
    
3. **Unlock Jenkins:** Obtain the Administrator Password by running the following command:
    
    ```yaml
    cat /var/lib/jenkins/secrets/initialAdminPassword
    ```
    
4. **Install Plugins:** Click on "Install Suggested Plugins" to ensure essential plugins are installed.
    
5. **Create Admin User:** Jenkins will prompt you to create the first admin user. Follow the instructions to set up an admin user.
    
6. **Create CI/CD Pipeline:** From the Jenkins Dashboard, click on "New Item" to create a new project for your CI/CD pipeline.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706950848849/868ee89c-cfd4-4d67-8a9e-0363ff1001d9.png align="center")

* Now, Add the name as
    

Name: notes-app-cicd

Project: Pipeline

Click “Ok”.

Now we have to configure pipeline as follows

Dashboards &gt; notes-app-cicd &gt; configuration &gt; general

Check✅Github project

project url: [https://github.com/Sompandey01/django-todo-cicd](https://github.com/Sompandey01/django-todo-cicd)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706951319173/dc866338-a81d-47eb-add9-c9dfa0eafb55.png align="center")

Check ✅GitHub hook trigger for GITScm polling

Put this basic Declarative pipeline code in script dialog box

```yaml
pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                echo 'Cloning the code'
            }
        }
        stage('Build') {
            steps {
                echo 'This is Build Stage'
            }
        }
        stage('Push to Docker hub') {
            steps {
                echo 'This is Test stage'
            }
        }
        stage('Deployement') {
            steps {
                echo 'Deploying container'
            }
        }
    }
}
```

This Jenkins declarative pipeline outlines a flexible CI/CD workflow:

1. `agent any:`: Allows the pipeline to run on any available Jenkins agent.
    
2. `stages:`: Defines logical steps in the process.
    
    a. `stage('Clone Code'):`: Clones the source code repository.
    
    b. `stage('Build'):`: Builds the application, running tests and generating artifacts. c. `stage('Push to Docker Hub'):`: Pushes built artifacts to Docker Hub.
    
    d. `stage('Deployment'):`: Deploys the application or container to the target environment.
    

Each stage can include more complex logic. By automating these stages, Jenkins ensures a consistent and reproducible workflow for software CI/CD. 🚀

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706951347888/6bede5e4-82ac-49c3-9162-a59345f27edb.png align="center")

* Now Click on Save button and start the build on pipeline page.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706951433571/91e0e2b7-62fb-4e02-ae0a-25646c22b303.png align="center")

* After getting success, you can see stages are green boxes with execution time.
    

## **Developing the Notes App Code: To develop the Django notes app code, follow these steps:**

1. Clone the code: In the pipeline script, add the following code to clone the code from your repository:
    

```yaml
git url: "https://github.com/Sompandey01/django-todo-cicd", branch: "master"
```

2\. Build the code: Add the following code to build the application and create docker image with tag

```yaml
sh "docker build -t notes-app ."
```

3\. Push to Docker Hub: Add the code to push the Docker image to Docker Hub:

For docker login in pipeline you have to create docker credentials and use them as environment variable

Create Credentials in Dashboard &gt; Manage jenkins &gt; Credentials &gt; System &gt; Global credentials

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706952197952/835c80e9-59ea-4e19-9dbc-379340c6c194.png align="center")

```yaml
withCredentials([usernamePassword(credentialsId:"dockerhub-login",passwordVariable:"dockerhubpass",usernameVariable:"dockerhubuser" )]){
    sh "docker tag notes-app ${env.dockerhubuser}/notes-app:latest"
    sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}" 
    sh "docker push ${env.dockerhubuser}/notes-app:latest"
}
```

1. `withCredentials`: This is a Jenkins pipeline step provided by the "Credentials Binding Plugin." It allows you to securely retrieve and use credentials within the block. In this case, we are retrieving the Docker Hub credentials using the `usernamePassword` method.
    
2. `usernamePassword(credentialsId: "dockerhub-login", passwordVariable: "dockerhubpass", usernameVariable: "dockerhubuser")`: This line retrieves the username and password from the Jenkins credentials store. The `credentialsId` parameter specifies the unique identifier of the stored Docker Hub credentials. The `usernameVariable` and `passwordVariable` parameters define the environment variables where the username and password will be stored, respectively. The environment variables are prefixed with `env.` in Jenkins, which is why you see `env.dockerhubuser` and `env.dockerhubpass` later in the code.
    
3. `sh "docker tag notes-app ${env.dockerhubuser}/notes-app:latest"`: This line creates a new Docker image tag with the Docker Hub username as a prefix. The `notes-app` is the original local image name, and we're tagging it with the new name `${env.dockerhubuser}/notes-app:latest`. This is necessary to ensure that the image can be pushed to the Docker Hub registry with the correct repository name.
    
4. `sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"`: This line runs the `docker login` command to authenticate with Docker Hub using the username and password retrieved from the Jenkins credentials store. The `-u` flag specifies the Docker Hub username, and the `-p` flag specifies the password.
    
5. `sh "docker push ${env.dockerhubuser}/notes-app:latest"`: This line pushes the tagged Docker image to the Docker Hub registry using the `docker push` command. After authentication, the image is pushed to the repository specified by `${env.dockerhubuser}/notes-app:latest`.
    

4\. Deployment: Finally, deploy the code on the EC2 instance using the following code:

```yaml
#
sh "docker-compose down && docker-compose up -d"
```

Here is the full Declarative pipeline code for django-notes-app deployment on ec2 using docker container.

```yaml
pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                echo 'Cloning the code'
                git url: "https://github.com/SaurabhDahibhate/django_notes_app.git", branch: "master"
            }
        }
        stage('Build') {
            steps {
                echo 'This is Build Stage'
                sh "docker build -t notes-app ."
            }
        }
        stage('Push to Docker hub') {
            steps {
                echo 'Pushing image to dockerhub'
                withCredentials([usernamePassword(credentialsId:"dockerhub-login",passwordVariable:"dockerhubpass",usernameVariable:"dockerhubuser" )]){
                sh "docker tag notes-app ${env.dockerhubuser}/notes-app:latest"
                sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}" 
                sh "docker push ${env.dockerhubuser}/notes-app:latest"
                }
                
            }
        }
        stage('Deployement') {
            steps {
                echo 'Deploying container'
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
```

Whenever the developer commits their code in GitHub, after every commit, it should reflect in the live web app.

· For that, we will use “github webhook”.

· Every time, a developer made a commit, a trigger will run automatically, which will rebuild the image and run a container on your behalf as a part of automation that will run the pipeline automatically.

* go to on your github repository &gt; setttings &gt; Webhook &gt; Payload URL &gt; put your jenkins public ip address &gt; “add webhook”
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706952758590/6053ff74-1315-4719-ad79-45d1fd482570.png align="center")

* Do some changes in the code and push to GitHub, this will automatically run a pipeline, and the new code will be Live.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706952998162/65ba3da9-0bdb-49da-ab51-7043bf4a31c3.png align="center")

* Now Here is the our app is live and working fine.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706953108744/96aa9fb3-dccf-451d-a03b-148bacd6e5ec.png align="center")

---

Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.