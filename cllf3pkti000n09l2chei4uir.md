---
title: "Kubernetes Architecture"
datePublished: Thu Aug 17 2023 11:51:39 GMT+0000 (Coordinated Universal Time)
cuid: cllf3pkti000n09l2chei4uir
slug: kubernetes-architecture
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692273054064/efc045b5-31dc-4ffd-a0f3-f073afb766f5.png
tags: kubernetes, devops, k8s, 90daysofdevops, trainwithshubham

---

## Kubernetes Overview

With the widespread adoption of [containers](https://cloud.google.com/containers) among organizations, Kubernetes, the container-centric management software, has become a standard to deploy and operate containerized applications and is one of the most important parts of DevOps.

Originally developed at Google and released as open-source in 2014. Kubernetes builds on 15 years of running Google's containerized workloads and the valuable contributions from the open-source community. Inspired by Google’s internal cluster management system, [Borg](https://research.google.com/pubs/pub43438.html).

### What is Kubernetes?

Kubernetes, often abbreviated as K8s, is an open-source container orchestration platform designed to automate the deployment, scaling, and management of containerized applications and load balancing. It schedules, runs and manages isolated containers which is running on Virtual, physical and Cloud machines. It was originally developed by Google and is now maintained by the Cloud Native Computing Foundation (CNCF). Kubernetes provides a powerful toolset for managing containerized workloads and services in a dynamic and efficient manner.

### Why do we call it k8s?

We call it "k8s" because "Kubernetes" has eight letters between 'K' and 's'. It's a shortcut, making the name quicker to type and say. Just like how "i18n" stands for "internationalization" with 18 letters between 'i' and 'n'.

### What are the benefits of using k8s?

Kubernetes (K8s) offers automated deployment, scaling, and management of containerized applications, ensuring high availability, resource efficiency, and streamlined operations. It provides service discovery, load balancing, and rolling updates, promoting seamless communication and updates. With extensibility and DevOps alignment, Kubernetes empowers organizations with a robust and efficient infrastructure.

### Explain the architecture of Kubernetes

![5 Minutes to Kubernetes Architecture – Collabnix](https://lh4.googleusercontent.com/cqO0KDxyW4zoop7ZFDAqwMTgExIU-it7PhVwuPOpj0Q6PzYtmv2fBJ24PyzTzZq6OZkx1aa-NM9a7XA9K7tGya4UP4RxaCtdK-7xcbBU9mNEYwi4_iqbGW2MmNSQOylauRCVV0a5 align="left")

**Master Node:** The "brain" of the Kubernetes cluster, the master node oversees the entire system's operation. It consists of several key components:

* **API Server:** Acts as the central control point, allowing users and components to interact with the cluster via RESTful API calls.
    
* **Scheduler:** Decides where to deploy newly created pods based on available resources, node conditions, and various constraints.
    
* **Controller Manager:** Watches the state of the cluster and works to maintain the desired state, reacting to changes and failures.
    
* **etcd:** A distributed key-value store that stores the cluster's configuration data and state. It acts as Kubernetes' "memory."
    

**Node (Worker Node):** These are the worker machines where containers are actually deployed and executed. Each node runs the following components:

* **Kubelet:** Acts as the node's "agent," responsible for communicating with the master node and managing containers on the node.
    
* **Kube Proxy:** Maintains network rules for pod-to-pod communication and load balancing across service endpoints.
    

**Pods:** The smallest deployable unit in Kubernetes, a pod is a logical group of one or more containers that share the same network and storage resources. Containers within the same pod can communicate easily using [`localhost`](http://localhost)

**Services:** Services provide a consistent way to expose and access pods, allowing them to communicate with each other within the cluster or to external systems.

### What is Control Plane?

The Control Plane in Kubernetes is the central management component that oversees and controls the entire Kubernetes cluster. It is responsible for making high-level decisions about the state of the cluster, ensuring that the desired state matches the actual state of the system. The Control Plane manages the orchestration of workloads, monitors cluster health, and reacts to changes or failures within the cluster.

### Write the difference between kubectl and kubelets.

**kubectl:**

* Command-line tool used for managing Kubernetes clusters.
    
* Runs on your local machine or management server.
    
* Communicates with the Kubernetes API server to send commands and receive cluster information.
    
* Manages and controls the entire Kubernetes cluster.
    
* Versatile for different cluster environments.
    

**kubelet:**

* Node-level agent that runs on each worker node within the cluster.
    
* Runs on every worker node.
    
* Communicates with the Control Plane, including the API server and other components.
    
* Integrates with the selected container runtime (e.g., Docker) to manage container lifecycles.
    
* Monitors pod health and reports to Control Plane.
    

### Explain the role of the API server.

The API Server is the main entrance where everyone interacts with the cluster. It's like the dispatcher, taking requests, ensuring they're valid, and coordinating actions. It's the gatekeeper for security, allowing only authorized folks in. The API Server ensures the cluster's resources are managed properly, whether it's creating, updating, or checking on things.

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/) for the latest updates and discussions.