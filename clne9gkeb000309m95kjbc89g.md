---
title: "Your CI/CD pipeline on AWS - Part 4 🚀 ☁"
datePublished: Fri Oct 06 2023 07:04:15 GMT+0000 (Coordinated Universal Time)
cuid: clne9gkeb000309m95kjbc89g
slug: your-cicd-pipeline-on-aws-part-4
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696575780946/f9ec3726-2432-45a8-aa10-fa163c9f7d57.png
tags: cloud, aws, devops, 90daysofdevops, trainwithshubham

---

On your journey of making a CI/CD pipeline on AWS with these tools, you completed AWS CodeCommit, CodeBuild & CodeDeploy.

Finish Off in style with AWS CodePipeline.

## What is CodePipeline?

CodePipeline builds, tests, and deploys your code every time there is a code change, based on the release process models you define. Think of it as a CI/CD Pipeline service.

## Task-01 :

### **\-&gt; Create a Deployment group of Ec2 Instance.**

Check my Day 52 blog for the deployment group.

%[https://hashnode.com/post/clnd4gwje000009ifgrt39xd0] 

### \-&gt; Create a CodePipeline that gets the code from CodeCommit, Builds the code using CodeBuild and deploys it to a Deployment Group.

* Navigate to the CodePipeline section in the AWS management console.
    
* Click on "**Create Pipeline**"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696573949568/8a07d74b-fd52-44c0-bc6b-848debcddbda.png align="center")

* Give your pipeline a name and click "**Next**".
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696575450638/b9522706-c9c6-4516-9b58-f6bdc826416d.png align="center")

* Add source provider.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696574193687/6ab4cb77-c9c9-4bef-9ae1-0cb84ec909d4.png align="center")

* Now add the Build stage details. Select the build provider and give the project name.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696574266353/a3f815ee-bc82-4c2d-96cc-282751895843.png align="center")

* Add the deploy provider and select your deployment group.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696574503991/922bd118-b64c-49a2-8435-d24a5bfa3b02.png align="center")

* Now, review it and click on "**Create pipeline**"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696574583675/33e9faca-8ae9-4c03-ac46-5f7ee119691e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696575594832/b1a34f46-343f-448c-813c-3530a3ba591f.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.