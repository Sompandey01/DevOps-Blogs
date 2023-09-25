---
title: "Your CI/CD pipeline on AWS - Part 2 🚀 ☁"
datePublished: Mon Sep 25 2023 03:59:40 GMT+0000 (Coordinated Universal Time)
cuid: clmyd0td100020aigh2qch9pl
slug: your-cicd-pipeline-on-aws-part-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695567861045/e0f2ee48-d5b3-40a2-ab17-ac1219476359.png
tags: cloud, aws, devops, 90daysofdevops, trainwithshubham

---

On your journey of making a CI/CD pipeline on AWS with these tools, you completed AWS CodeCommit.

Next few days you'll learn these tools/services:

* CodeBuild
    
* CodeDeploy
    
* CodePipeline
    
* S3
    

## What is CodeBuild?

AWS CodeBuild is a fully managed build service in the cloud. CodeBuild compiles your source code, runs unit tests, and produces artifacts that are ready to deploy. CodeBuild eliminates the need to provision, manage, and scale your own build servers.

## Task 1: Building an index.html File with Nginx Server Using CodeBuild

**1 -&gt; Read about Buildspec file for Codebuild.**

The buildspec.yml file allows you to define and configure the build process for your CodeBuild project. It provides an easy way to specify build instructions in a declarative YAML format.

**2 -&gt; Create a simple index.html file in CodeCommit Repository.**

* Navigate to the CodeCommit service.
    
* Select the repository where you want to add the `index.html` file.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695611473796/5c0aacfc-494a-4da4-94a3-2fc0a26b1068.png align="center")

* Click on "**Create file**"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695611519991/387dee03-13f2-4daa-8cdb-17dc3bca48f1.png align="center")

* Enter the name and add the following content.
    

```bash
<html>
  <head>
    <title>My Website</title>
  </head>
  <body>
    <h1>Welcome to my website</h1>
    <p>This is a simple website hosted on AWS CodeCommit.</p>
  </body>
</html>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695611726903/e1367f1a-0e99-45a9-bd29-75ea9d408ef7.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695611787493/cb06c0b0-db11-4759-ba04-325aeb1fa39e.png align="center")

* Now, Click on "**Commit Changes**" to save the changes.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695611856288/09a7759d-ed9f-4ab1-9525-ad83658a14ec.png align="center")

* Let's clone the repository to your instance and verify the files.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695611894795/71eccc22-e94d-4439-96bc-08487f88fc81.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695612014841/1c29aa6c-8fad-42a9-be11-c5786ae81050.png align="center")

## Task 2: Add buildspec.yaml file to CodeCommit Repository and complete the build process.

* Create a buildspec.yaml file.
    

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
      - echo Build started on date`
      - cp index.html /var/www/html
  post_build:
    commands:
      - echo Configuring NGINX
artifacts:
  files:
    -/var/www/html/index.html
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695612264375/6b62d72f-8441-4e6e-9756-1570da43367b.png align="center")

* Commit the Buildspec.yml file to the CodeCommit repository.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695612396009/d69948c7-b02d-4050-a274-320ce7c2b3c6.png align="center")

* Push the file to the CodeCommit repository.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695612478491/eb68da89-94b3-4b33-914c-3cc9e980d40e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695612504564/8ef74eb3-9902-47c5-bfbd-8569cfb556c2.png align="center")

* Now, navigate to the CodeBuild section of AWS and build project.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695612546970/7f19fc53-3cb9-4d19-ad20-688643210de5.png align="center")

* Click on "**Create build project**" and give the details.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695612666087/6aa8ef3e-6021-4a88-9ad2-17533822802d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695612710236/eaed2807-f2af-4d07-accd-a07bea788c64.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695612774769/9d1e3024-bcca-408b-a5eb-b46679b54ce2.png align="center")

* Select Use build spec file in Buildspec section and click on "**Create build project**"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695612843842/d3ea6594-2cae-4fb7-b060-46ee04a7df75.png align="center")

* Project created, now click on "**Start build**"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695612975150/51cc8cf2-28ae-4661-b005-362d28e3712e.png align="center")

* Code build is successfully completed.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695613244367/91a8abf5-ad02-42f1-b3df-2d75d1cbfcce.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695613267810/47714e5c-5467-4689-a674-3295dd99d58f.png align="center")

* You can store the build details in the artifactory.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695613545973/4c70f305-eac7-44e3-9bbf-2596fea51fc2.png align="center")

* Before that, create an S3 bucket. Navigate to the S3 bucket in the AWS console and provide the bucket name and create the bucket.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695613697680/73594f0d-ab22-48a5-8750-7c5f91d398ff.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695613707387/f6a6eb8a-af47-4ebc-9de0-d8b97b6a65b5.png align="center")

* Click on "**Create bucket**"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695613744314/0b0ccdfb-79df-43d6-9d47-101359e433b7.png align="center")

* Navigate to the project build, click on edit and select artefact. Provide all the details and create artifact.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695613825382/b0ec7a95-9916-4669-9793-f13b379a0c2c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695613838977/14f938db-aa26-4b84-98ef-efeb3f8c80ba.png align="center")

* Click on "**Update artifacts**"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695613882966/64321246-7dd0-4756-927e-8df8d1adc7c9.png align="center")

* Now, if you rebuild the project you can see the UPLOAD\_ARTIFACTS section.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695614067797/2bb209d7-7c8b-4c46-9fa2-31dd4f9589c8.png align="center")

* Now, Navigate to the S3 bucket and you can see the build.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695614113993/e24c3318-83d7-43d0-ae68-5fb6b0603f6e.png align="center")

* Click open URL to open the demo-app
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695614176272/7aca9413-2224-49cb-8e73-44a4fd577ead.png align="center")

* Here is an output of index.html file.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695614252508/8aafddb1-e44c-4dc6-8482-2e5499aeb116.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.