---
title: "Mastering ConfigMaps and Secrets in Kubernetes"
datePublished: Thu Aug 24 2023 11:56:07 GMT+0000 (Coordinated Universal Time)
cuid: cllp3yaan000008mu94gdd5l5
slug: mastering-configmaps-and-secrets-in-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692878134408/5da24524-29f7-44cb-90be-a6a6899c7e5a.png
tags: kubernetes, devops, k8s, 90daysofdevops, trainwithshubham

---

## What are ConfigMaps and Secrets in k8s

In Kubernetes, ConfigMaps and Secrets are used to store configuration data and secrets, respectively. ConfigMaps store configuration data as key-value pairs, while Secrets store sensitive data in an encrypted form.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692877201376/7909d597-07e9-4929-b341-e08cdb9b20d8.webp align="center")

**ConfigMaps**: In Kubernetes, ConfigMaps are a way to store configuration data that your application needs. This data can include things like environment variables, configuration files, or command-line arguments. Instead of hardcoding this data into your application code, you can store it separately in a ConfigMap. For example, you could use a ConfigMap to store the URL of an external service that your app interacts with. This makes it easier to update configuration without changing your app's code.

**Example**: Imagine you have an app that connects to a database. Instead of writing the database address directly into your app, you can put it in a ConfigMap. Then, your app can look at the ConfigMap to find the address. If the address changes, you only need to update the ConfigMap, and your app stays the same.

**Secrets**: Secrets are like ConfigMaps, but they're used for super-secret stuff, like passwords or special codes. They're encoded and locked away securely. So, if your app needs a password to access something, you can use a Secret to keep that password safe. This way, the password isn't hanging around in your app's code for anyone to see.

**Example**: Suppose your app needs to connect to an online service using an API key. Instead of putting the key directly in your app, you can create a Secret. Your app can then use the Secret to get the key when it needs it. This adds an extra layer of security because the key is kept hidden.

### **Task 1: ConfigMap Mastery for Deployment Enhancement**

* **Create a ConfigMap for your Deployment using a file or the command line**
    

```bash
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-demo
data:
  name: django-todo-app
  namespace: todo-app
  application: todo-app
  protocol: TCP
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692873508910/cfb9d28b-185b-4cc3-899b-069680ee0adc.png align="center")

```bash
kubectl apply -f <configMap file name> -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692873620138/af87cac0-81b9-4819-8a30-e4c63526c7ae.png align="center")

* **Update the deployment.yml file to include the ConfigMap**
    

```python
apiVersion: apps/v1
kind: Deployment
metadata:
  name: todo-app-deployment
  labels: 
    app: todo-app  
  namespace: todo-app
spec:
  replicas: 1
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
              
          env:
            - name: application
              valueFrom:
                configMapKeyRef:
                  name: app-demo
                  key: application
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692874520968/0d59549f-124f-4647-aa60-5c4aaf23d51c.png align="center")

* **Apply the updated deployment using the command:** `kubectl apply -f deployment.yml -n <namespace-name>`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692874547360/a3390f7b-6d9c-409d-ac45-2821dedc6a5c.png align="center")

* **Verify that the ConfigMa**password: YgygjydLKJOI**p has been created by checking the status of the ConfigMaps in your Namespace.**
    

To verify that the ConfigMap has been created, you can use the following command:

```bash
kubectl get configmaps -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692874741989/d9153b32-40ea-403d-9c0f-cf3119a88fe3.png align="center")

To view detailed information about the configmap use the following command:

```python
kubectl describe congigmap <configmap-name> -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692875013709/c6b32282-0623-4488-9dc4-a3e7452b5b3e.png align="center")

### **Task 2: Power Up Your Deployment with Secrets**

* **Create a Secret for your Deployment using a file or the command line**
    

```bash
apiVersion: v1
kind: Secret
metadata:
  name: secret-file
  namespace: todo-app
type: Opaque
data:
  password: YgygjydLKJOI
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692876215970/1b85d9a8-cbe7-478e-b9f9-c7f5f2a4fce5.png align="center")

You can create a secret by running a following command:

```python
kubectl apply -f < secret-file-name > -n < namespace-name >
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692876409581/c192cb85-9114-4b03-ad2d-37256fc9f070.png align="center")

* **Update the deployment.yml file to include the Secret**
    

```python
apiVersion: apps/v1
kind: Deployment
metadata:
  name: todo-app-deployment
  labels:
    app: todo-app
  namespace: todo-app
spec:
  replicas: 1
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

          env:
            - name: secret
              valueFrom:
                secretKeyRef:
                  name: secret-file
                  key: password
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692876612568/21e63205-172f-4310-9c1b-2b96ed6bcb92.png align="center")

* **Apply the updated deployment using the command:** `kubectl apply -f deployment.yml -n <namespace-name>`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692876665219/27fb7c89-87dd-4bd0-9336-776e0f66c0d1.png align="center")

* **Verify that the Secret has been created by checking the status of the Secrets in your Namespace.**
    

To verify that the Secret has been created, you can use the following command:

```python
kubectl get secrets -n < namespace-name >
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692876802460/ecf38a1a-cb59-4c7d-bf61-f9f372241244.png align="center")

To view detailed information about the secret use the following command:

```python
kubectl describe secret <secret-name> -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692876963614/7fef24fd-00cf-4c39-ab61-c620f28f5402.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.