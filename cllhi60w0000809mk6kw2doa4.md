---
title: "Launching your Kubernetes Cluster with Deployment"
datePublished: Sat Aug 19 2023 04:11:54 GMT+0000 (Coordinated Universal Time)
cuid: cllhi60w0000809mk6kw2doa4
slug: launching-your-kubernetes-cluster-with-deployment
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692418288419/f12c7f13-2031-456a-9416-34a1167c1c23.png
tags: docker, kubernetes, devops, 90daysofdevops, trainwithshubham

---

## What is Deployment in k8s?

A Deployment in Kubernetes (often referred to as a "K8s Deployment") is a resource object that helps manage the deployment and scaling of containerized applications. It provides a declarative way to ensure that a specified number of identical pods are running and maintained, even when the application needs to be updated, scaled, or rolled back.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692416670371/d35423a3-f483-4afe-8272-18832127e3d7.png align="center")

In simple terms, a deployment in Kubernetes is like a smart manager for your apps. You tell it how many copies (pods) of your app you want to run, and it makes sure that number is always running, even if some crash. When you update your app, it smoothly replaces the old version with the new one, so users don't notice. It's great for making sure your app stays up and can handle more users if needed.

### **Task-1: Create one Deployment file to deploy a sample todo-app on K8s using the "Auto-healing" and "Auto-Scaling" feature**

* add a deployment.yml file
    
* apply the deployment to your k8s (minikube) cluster by command `kubectl apply -f deployment.yml`
    

Pushing my image into docker hub so that it can be accessed by Kubernetes from anywhere.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692409882780/dece7764-9c56-4741-887a-07a4d9624ec0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692409915691/659c7ef8-287d-486d-a0dc-ccaa000b3852.png align="center")

Create a new YAML file named `deployment.yaml`.

```python
apiVersion: apps/v1
kind: Deployment
metadata:
  name: todo-app-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: todo-app
  template:
    metadata:
      labels:
        app: todo-app
    spec:
      containers:
        - name: todo-app
          image: sompandey/todo-app
          ports:
            - containerPort: 8000
```

`replicas`: Specifies the initial number of replicas. This is the basis for auto-scaling.

`selector`*: This defines the labels used to identify the pods associated with this Deployment.*

`template`: Describes the pod template used for each replica.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692370588170/bee54ee1-a279-49c1-964d-6e934db36d46.png align="center")

Save the file as `deployment.yml` and execute it by using `kubectl apply -f deployment.yml`

```python
kubectl apply -f deployment.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692416567567/52aac410-3051-4aac-8353-a73de1470b51.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692416577797/456e42a7-c13b-48de-ade7-56c47cdc2e73.png align="center")

Let's check auto healing, if we delete any pod it will create a new pod

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692416393174/a4b75546-fb06-4d6d-8cf5-ac4aa36bff39.png align="center")

Now, if we need to delete the deployment we can use the below command.

```python
kubectl delete -f deployment.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692372188666/5a5f2b56-ea4f-44c9-991e-fdf507cdfb89.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/) for the latest updates and discussions.