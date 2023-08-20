---
title: "Working with Namespaces and Services in Kubernetes"
datePublished: Sun Aug 20 2023 04:35:04 GMT+0000 (Coordinated Universal Time)
cuid: clliyfnyj000g08mn4c0v9c1w
slug: working-with-namespaces-and-services-in-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692506060864/3f833ac4-a463-40ff-9452-728b5c2c1294.png
tags: kubernetes, devops, k8s, 90daysofdevops, trainwithshubham

---

## What are Namespaces and Services in k8s

**Namespaces:** In Kubernetes, Namespaces are used to create isolated environments for resources. Each Namespace is like a separate cluster within the same physical cluster.

**Services:** Services are used to expose your Pods and Deployments to the network. Services provide a way for pods to communicate. Think of them as well-known meeting points. They give pods an address and a name, making it easy for other pods to find them.

### Task 1: **Managing Deployment in a Dedicated Namespace**

* Create a Namespace for your Deployment
    

To create a namespace open your terminal and use the command given below:

```python
kubectl create namespace <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692456433728/43f9bd12-f7ef-4fde-94d0-72acc9ff3dc9.png align="center")

* Update the deployment.yml file to include the Namespace
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692456601038/0b177e8d-cbcc-4cb7-8f22-9d136e907e2d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692456644023/afe0487b-8cfa-463b-a832-261776d7f368.png align="center")

* Apply the updated deployment using the command: `kubectl apply -f deployment.yml -n <namespace-name>`
    

```python
kubectl apply -f deployment.yml -n <namespace-name>
```

* Verify that the Namespace has been created by checking the status of the Namespaces in your cluster.
    

```python
kubectl get pods -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692456913482/f5c2da34-018e-445b-826f-570cfac1c4e6.png align="center")

### Task 2: Services, Load Balancing, and Networking in Kubernetes.

**Services:** In Kubernetes, a Service is a fundamental abstraction that facilitates communication between different parts of an application. It acts as a stable network endpoint, enabling pods within a cluster to interact with each other or with external entities. Services ensure that regardless of changes in pod IPs or their scaling, connectivity remains intact.

* A service object is a logical bridge between the pod and end users, which provides **Virtual IP (VIP).**
    
* Services allow users to reliably connect to the containers running in the pod using the VIP.
    
* The VIP is not an actual IP connected to a network interface, but it's purpose is to forward traffic to one or more pods.
    
* Kube proxy is the one which keeps the mapping between the VIP and the pods up to date.
    

Here's a concise overview of key aspects:

* **ClusterIP Service**:
    
    * Default service type.
        
    * Creates an internal virtual IP to expose pods within the cluster.
        
    * Enables communication among pods.
        
* **NodePort Service**:
    
    * Opens a static port on each node to route traffic to pods.
        
    * Useful for external access.
        
    * Automatically handles port forwarding.
        
* **LoadBalancer Service**:
    
    * Utilizes a cloud provider's load balancer to distribute traffic.
        
    * Ideal for public-facing applications.
        
    * Automatically allocates an external IP.
        
* **ExternalName Service**:
    
    * Maps a service to an external DNS name.
        
    * Allows using an external service without exposing its IP.
        

**Load Balancing:** Load Balancing in Kubernetes is a vital mechanism that ensures even distribution of incoming network traffic across multiple pods or replicas of an application. It's created by cloud providers that will route external traffic to every node on the Nodeport. This serves multiple purposes:

* **Scalability**: By Distributing traffic across pods it prevents overloading specific instances and allows the application to handle increased load gracefully.
    
* **High Availability**: Load balancers direct traffic to available pods and enhance application availability even if some pods fail.
    
* **Optimal Resource Utilization**: Balancing traffic prevents resource bottlenecks by evenly utilizing the capacity of available pods.
    
* **Enhanced Performance**: Load balancing minimizes response time by redirecting requests to less busy pods.
    

**Networking:** Networking in Kubernetes is the foundation for communication between pods, ensuring they can seamlessly exchange data and work together. Each pod is assigned a unique IP address, allowing direct communication within the cluster. Kubernetes assigns names to services for simple access, and security is maintained using network policies.

In simple terms, Kubernetes networking is like a chat platform for pods. Each pod gets its own address, so they can talk directly. Services have names that help pods find each other easily. Safety is maintained by rules called Network Policies.

* Pods communicate through assigned IP addresses.
    
* Unique IP for each pod, enabling efficient interactions.
    
* Network Policies control traffic and enhance security.
    

Together, Services, Load Balancing, and Networking empower Kubernetes deployments with efficient communication, accessibility, and reliability.

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/) for the latest updates and discussions.