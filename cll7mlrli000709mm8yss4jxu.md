---
title: "Day 26: Jenkins Declarative Pipeline"
datePublished: Sat Aug 12 2023 06:18:25 GMT+0000 (Coordinated Universal Time)
cuid: cll7mlrli000709mm8yss4jxu
slug: day-26-jenkins-declarative-pipeline
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691820899052/c6791cc5-ba7d-47ae-9fcf-0304b569a818.webp
tags: devops, jenkins, ci-cd, 90daysofdevops, trainwithshubham

---

One of the most important parts of your DevOps and CICD journey is a Declarative Pipeline Syntax of Jenkins

## Some terms for your Knowledge

**What is Pipeline -** A pipeline is a collection of steps or jobs interlinked in a sequence.

**Declarative:** Declarative is a more recent and advanced implementation of a pipeline as a code.

**Scripted:** Scripted was the first and most traditional implementation of the pipeline as a code in Jenkins. It was designed as a general-purpose DSL (Domain Specific Language) built with Groovy.

## Why you should have a Pipeline

The definition of a Jenkins Pipeline is written into a text file (called a [`Jenkinsfile`](https://www.jenkins.io/doc/book/pipeline/jenkinsfile)) which in turn can be committed to a project’s source control repository.  
This is the foundation of "Pipeline-as-code"; treating the CD pipeline as a part of the application to be versioned and reviewed like any other code.

**Creating a** `Jenkinsfile` and committing it to source control provides a number of immediate benefits:

* Automatically creates a Pipeline build process for all branches and pull requests.
    
* Code review/iteration on the Pipeline (along with the remaining source code).
    

## Pipeline syntax

```python
pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                // 
            }
        }
        stage('Test') { 
            steps {
                // 
            }
        }
        stage('Deploy') { 
            steps {
                // 
            }
        }
    }
}
```

## Task-01: **Jenkins "Hello World" Declarative Pipeline**

* Create a New Job, this time select Pipeline instead of Freestyle Project.
    

1. Click on "New Item" to create a new Jenkins job.
    
2. **Enter Job Details:**
    
    * Provide a name for the job (e.g., "HelloWorldPipeline").
        
    * Choose "Pipeline" as the job type.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691820025599/9d0cbfb9-f637-4ddd-8b04-45d0f0e2bb5c.png align="center")

**Configure Pipeline:** In the pipeline configuration section:

* Choose "Pipeline script" from the "Definition" drop-down.
    
* In the "Pipeline" section, you can directly enter the Declarative pipeline script.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691820252423/ebe983e4-c4f0-4c8d-92d7-b05b8545e556.png align="center")

**Add Declarative Pipeline Script:** Use the following example as your Declarative pipeline script:

```python
 pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World!'
            }
        }
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691820427652/3c5927c6-56e7-469e-9ead-7371713ded23.png align="center")

**Save and Run:**

* Click on "Save" to save your pipeline configuration.
    
* Run the pipeline job by clicking on "Build Now."
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691820503002/87e82211-b741-43ae-91bf-3a514f5230a4.png align="center")

**View Console Output:** After the build completes, you can click on the build number to view the console output. You'll see the output "Hello World!" printed as part of the pipeline execution.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691820546983/d5852e08-b43e-4e67-b20d-bb028271321b.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/) for the latest updates and discussions.