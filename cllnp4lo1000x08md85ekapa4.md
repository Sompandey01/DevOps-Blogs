---
title: "Working with Services in Kubernetes"
datePublished: Wed Aug 23 2023 12:13:22 GMT+0000 (Coordinated Universal Time)
cuid: cllnp4lo1000x08md85ekapa4
slug: working-with-services-in-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692792754576/029f0026-f068-49bc-a349-76415f8df352.png
tags: kubernetes, devops, k8s, 90daysofdevops, trainwithshubham

---

## What are Services in K8s

In Kubernetes, Services are objects that provide stable network identities to Pods and abstract away the details of Pod IP addresses. Services allow Pods to receive traffic from other Pods, Services, and external clients.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692792377760/e843892f-9f96-4f0b-9e36-3e7233ce9a4c.png align="center")

### Task 1: **Creating a Service for todo-app Deployment in Kubernetes**

* Create a Service for your todo-app Deployment from Day-32
    
* Create a Service definition for your todo-app Deployment in a YAML file.
    

```python
apiVersion: v1
kind: Service
metadata:
  name: todo-app-deployment
  namespace: todo-app
spec:
  type: NodePort
  selector:
    app: todo-app
  ports:
    - port: 80
      targetPort: 8000
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692614838802/194b8d26-65e7-42a6-8079-c9f352e983af.png align="center")

* Apply the Service definition to your K8s (minikube) cluster using the `kubectl apply -f service.yml -n <namespace-name>` command.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692615920808/84c40601-44ea-4dd8-964a-dd49a2f09adb.png align="center")

* Verify that the Service is working by accessing the todo-app using the Service's IP and Port in your Namespace.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692759646417/3e982bc6-5e38-4dcb-b959-0518054b6956.png align="center")

### Task 2: **Creating a ClusterIP Service for Accessing the todo-app within a Kubernetes Cluster**

* Create a ClusterIP Service for accessing the todo-app from within the cluster
    
* Create a ClusterIP Service definition for your todo-app Deployment in a YAML file.
    

**<mark>Step 1:</mark> Create ClusterIP Service Definition (cluster-ip-service.yml)** Create a YAML file named `cluster-svc.yml` with the following content:

```python
apiVersion: v1
kind: Service
metadata:
  name: todo-app-clusterip
  labels:
    app: todo-app
spec:
  selector:
    app: todo-app
  ports:
    - protocol: TCP
      port: 8000
      targetPort: 8080
  type: ClusterIP
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692760240928/b316c2f9-3d66-4e8a-ae1a-ece08dac9a4e.png align="center")

**<mark>Step 2:</mark> Apply the ClusterIP Service Definition**

```python
kubectl apply -f cluster-svc.yml -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692761882813/c8faae24-fa8b-4702-9b8c-d67f6f4c6f69.png align="center")

**<mark>Step 3:</mark> Verify ClusterIP Service** To verify that the ClusterIP Service is working, follow these steps:

1. Create a YAML file named `test-pod.yml` for a testing pod:
    

```bash
apiVersion: v1
kind: Pod
metadata:
  name: test-pod
spec:
  containers:
    - name: busybox
      image: busybox
      command: ['sh', '-c', 'while true; do wget -q -O- clusterip:8000; done']
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692762169895/ff9b3072-bf97-4b0e-83c5-313ba933a89f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692763011930/cf46996c-b877-4c9c-bbf5-799430f679f4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692791719281/83c08a49-daf0-40f2-9603-dcc382443ec5.png align="center")

### Task 3: Creating a LoadBalancer Service and Accessing the todo-app from Outside the Kubernetes Cluster

* Create a LoadBalancer Service for accessing the todo-app from outside the cluster
    
* Create a LoadBalancer Service definition for your todo-app Deployment in a YAML file.
    

```bash
apiVersion: v1
kind: Service
metadata:
  name: todo-app-loadbalancer
spec:
  selector:
    app: todo-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8000
  type: LoadBalancer
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692786425305/6b50bdb5-e031-4c2e-b9dd-8d33e94d20a4.png align="center")

* Apply the LoadBalancer Service definition to your K8s (minikube) cluster using the `kubectl apply -f load-balancer-service.yml -n <namespace-name>` command
    
* Verify that the LoadBalancer Service is working by accessing the todo-app from outside the cluster in your Namespace.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692792122970/26b5765a-a7cd-41cf-a21a-763f64f614ee.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/) for the latest updates and discussions.