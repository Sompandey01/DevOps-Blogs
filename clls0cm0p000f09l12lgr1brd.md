---
title: "Kubernetes Important interview Questions."
datePublished: Sat Aug 26 2023 12:38:36 GMT+0000 (Coordinated Universal Time)
cuid: clls0cm0p000f09l12lgr1brd
slug: kubernetes-important-interview-questions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693053401223/80631fcf-575a-4ed0-b676-4026ac8ccd09.png
tags: kubernetes, devops, k8s, 90daysofdevops, trainwithshubham

---

## Questions:

### What is Kubernetes and why it is important?

Kubernetes is a container orchestration tool that automates the deployment, scaling and management of containers. It is important because it helps in managing containerized applications in an easy, repeatable and scalable way.

For example, imagine you have multiple Docker containers running your application and Kubernetes helps deploy, scale and manage those containers. It can perform tasks like healing failed containers, rolling out new updates, scaling the application based on load, etc. All of this eases the container management burden and allows you to focus on your application code.

### What is difference between docker swarm and kubernetes?

Docker swarm and Kubernetes are both container orchestration tools, but they have some key differences:

**Docker swarm:**

* Focuses on simplicity and ease of use
    
* Provides basic orchestration features like service discovery, load balancing, scaling, etc.
    
* Uses a raft consensus algorithm for leader election
    
* Is maintained by Docker Inc.
    

**Kubernetes:**

* Is more complex but also more powerful and production-ready
    
* Provides more advanced features like rolling updates, auto-healing, auto-scaling, etc.
    
* Uses etcd as its backing store
    
* Is maintained by the Cloud Native Computing Foundation which has support from major tech companies.
    

**In summary:**

* Docker swarm is good for a small number of containers (up to a few thousand)
    
* It is easier to set up and use
    
* Kubernetes can handle a very large number of containers (tens of thousands and beyond)
    
* It provides more sophisticated features for complex application deployments
    

So Docker swarm is a good choice for simpler workloads while Kubernetes is better suited for large-scale, complex microservices applications.

### How does Kubernetes handle network communication between containers?

Kubernetes provides a virtual network for containers to communicate with each other. It achieves this using pods and services.

**Pods:**

* Are the basic building blocks of Kubernetes applications
    
* Contain one or more containers
    
* Share a network namespace, IP address and port space
    

This means that containers within the same pod can communicate with each other using [localhost](http://localhost). They essentially appear to be running on the same host.

**Services:**

* Provide a single, stable IP address and DNS name for a set of pods
    
* Expose pods to the rest of the cluster through label selection
    

This means that pods can communicate with each other even if they are spread across nodes, using the service IP address or DNS name.

**In summary, Kubernetes handles network communication between containers as follows:**

1. It assigns a virtual IP address to each pod from a predefined range (e.g. 10.0.0.0/24)
    
2. Containers within the same pod can communicate using [localhost](http://localhost)
    
3. Each service is assigned a cluster IP (e.g. 10.96.0.1) that maps to a set of pods
    
4. Pods can communicate with each other using the service IP or DNS name
    
5. Kubernetes provides a virtual network overlay to enable this connectivity
    

This virtual network allows containers to easily discover and communicate with each other, regardless of which nodes they are scheduled on.

### How does Kubernetes handle scaling of applications?

1. Kubernetes can automatically increase or decrease the number of copies (pods) of your application running based on how busy it is. This is called Horizontal Pod Autoscaling.
    

When your application becomes busier and uses more CPU or memory, Kubernetes detects this and launches more copies of your application pods to handle the load.

When the load decreases, Kubernetes scales down the number of pods again.

1. Kubernetes ensures that the actual number of running pods matches the number of pods you configured. If some pods crash or stop, Kubernetes will replace them to maintain your configured number of pods.
    
2. You can tell Kubernetes you want more or less copies of your application running by changing a simple number in a Deployment. Kubernetes will then scale up or down to match that number.
    
3. Kubernetes can also automatically adjust the amount of resources (CPU / memory) allocated to each running pod, based on its current workload. This is called Vertical Pod Autoscaling.
    
4. Kubernetes exposes your application using Services that provide a stable IP address and name. This means other applications do not need to know how many pods your application has - they just communicate with the Service.
    

In short, Kubernetes can automatically scale the number of copies of your application pods, both horizontally (by launching new pods) and vertically (by adjusting resources of existing pods) to adapt to changes in workload. It does this in a transparent manner to other applications.

### What is a Kubernetes Deployment and how does it differ from a ReplicaSet?

A ReplicaSet ensures a fixed number of pod replicas are running. A Deployment manages a ReplicaSet and provides declarative updates to it using rollout strategies. You define the desired state in a Deployment and it handles creating/updating the underlying ReplicaSet to match that state. Deployments provide a higher level of abstraction for managing your applications.

### Can you explain the concept of rolling updates in Kubernetes?

Rolling updates allow you to smoothly roll out new versions of your application pods in Kubernetes with minimal downtime, by updating them in batches and verifying health at each step.

### How does Kubernetes handle network security and access control?

Kubernetes provides a number of controls to restrict network access and manage access privileges at different levels - from pods and containers to users and service accounts. The combination of these features helps ensure your Kubernetes cluster and applications run securely.

### Can you give an example of how Kubernetes can be used to deploy a highly available application?

Here is an example of how Kubernetes can be used to deploy a highly available application:

1. Create a Deployment to deploy your application pods. Specify the number of replicas you want, for example 3. This will create 3 pods of your application.
    
2. Create a Service of type ClusterIP to expose the Deployment. This will assign a virtual IP to the set of pods.
    
3. Kubernetes will ensure that 3 pods of your application are always running by restarting any pods that fail. It will spread the pods across nodes for high availability.
    
4. If one pod fails, the load will be automatically balanced across the other 2 pods. The virtual IP of the Service remains the same.
    
5. You can scale the Deployment to have more replicas if needed. Kubernetes will create new pods and remove old ones in a controlled manner.
    
6. You can expose the Service externally using NodePort, LoadBalancer or Ingress. This provides a single entry point to your application.
    
7. Kubernetes does health checking of your pods and will take unhealthy pods out of load balancing. This ensures only healthy pods receive traffic.
    

In summary, by combining Deployments, Services and replication controllers, Kubernetes can manage the lifecycle of your application pods to provide high availability, scalability, load balancing and self-healing capabilities.

### What is namespace is kubernetes? Which namespace any pod takes if we don't specify any namespace?

A namespace in Kubernetes is a virtual cluster inside your Kubernetes cluster. It has the following purposes:

* **Isolate resources** - Pods and services in different namespaces are isolated. They cannot see each other by default.
    
* **Assign ownership** - Namespaces can be used to divide cluster resources between teams and projects.
    
* **Set resource quotas** - Quotas on CPU/memory usage can be set on a namespace level.
    
* **Manage privileges** - Access control and permissions can be set on a namespace level.
    

If we don't specify a namespace when creating a pod, it will be created in the default namespace. There is always a default namespace in a Kubernetes cluster.

**The default namespace has the following properties:**

* It exists by default when a cluster is created.
    
* All pods are placed in this namespace if none is specified.
    
* It has no resource limits by default.
    
* All service accounts exist in this namespace.
    

So in summary, if no namespace is specified when creating a Kubernetes pod, it will be created in the default namespace. Namespaces allow you to logically separate your cluster into virtual clusters for isolation, ownership and quotas.

### How does ingress help in kubernetes?

Ingress allows external clients to access your Kubernetes services in a simple and configurable way. It provides features like TLS termination, load balancing, hostname/path based routing etc. which helps expose your cluster to the outside world in a managed way.

### Explain different types of services in kubernetes?

There are 4 main types of Services in Kubernetes:

1. **ClusterIP:** Exposes the Service on a cluster-internal IP. This makes the Service only reachable from within the cluster. It is the default Service type.
    
2. **NodePort:** Exposes the Service on each Node's IP at a static port (the NodePort). A ClusterIP Service is created firstly, and then traffic is forwarded to the ClusterIP from the NodePorts.
    
3. **LoadBalancer:** Exposes the Service externally using a cloud provider's load balancer. Traffic is routed to the ClusterIP, which then routes to the Pods.
    
4. **ExternalName:** Maps the Service to the contents of the externalName field, by returning a CNAME record with that value. This makes the Service act as an ExternalName DNS proxy.
    

**The main differences between them are:**

* **ClusterIP:** Exposes Service within the cluster only. Used for backend Services.
    
* **NodePort:** Exposes Service externally on cluster nodes' IPs. Used when external clients query nodes directly.
    
* **LoadBalancer:** Provides an external load balancer. Used when external clients need a single stable IP.
    
* **ExternalName:** Maps Service to an external DNS name. Used to expose an external service within the cluster.
    

**So in summary:**

* **ClusterIP** - Internal cluster Service (default)
    
* **NodePort** - Exposes Service externally on each Node's IP
    
* **LoadBalancer** - Provides an external load balancer
    
* **ExternalName** - Maps Service to an external DNS name
    

Each type suits different use cases depending on how you want to expose your Service.

### Can you explain the concept of self-healing in Kubernetes and give examples of how it works?

Self-healing is one of the most important capabilities of Kubernetes. It refers to Kubernetes' ability to automatically recover from failures and maintain the desired state of the cluster. Here are some examples of self-healing in Kubernetes:

1. **Pod restart:** If a Pod crashes or fails for some reason, the Kubernetes controller (e.g. ReplicationController) will restart the Pod to bring it back to the desired state.
    
2. **Node failure:** If a Node in the cluster fails, Pods scheduled on that Node will be automatically rescheduled to other healthy Nodes by the Scheduler.
    
3. **ReplicaSet:** A ReplicaSet will automatically create new Pods to replace those that fail, to maintain the desired number of replicas.
    
4. **Deployment:** A Deployment will recreate Pods that fail or restart Pods when a new image is available, to maintain the desired state.
    
5. **Horizontal Pod Autoscaling:** The cluster will automatically scale the number of Pods up or down to maintain the desired CPU and memory utilization targets.
    
6. **Health checking:** Kubernetes has the ability to perform liveness and readiness health checks on Pods, and restart or isolate unhealthy Pods.
    
7. **Volume resizing:** If a Persistent Volume Claim's requested storage size is increased, Kubernetes will automatically enlarge the backing Persistent Volume without downtime.
    

In all these examples, Kubernetes takes action to recover from failures and ensure that the desired state is maintained. This self-healing ability greatly increases the reliability and availability of applications running on Kubernetes.

The key takeaway is that Kubernetes aims to ensure that whatever resources you have defined in your cluster - Pods, ReplicaSets, Deployments, etc. - actually match your desired state. Kubernetes will take automatic actions to reconcile any differences and self-heal as needed.

### How does Kubernetes handle storage management for containers?

Kubernetes handles storage management for containers through Persistent Volumes (PVs) and Persistent Volume Claims (PVCs).

**Persistent Volumes:**

* Are storage resources provided by administrators or storage vendors.
    
* They are abstracted from the underlying storage implementation.
    
* Examples include NFS shares, AWS EBS volumes, GCE Persistent Disks, etc.
    

**Persistent Volume Claims:**

* Are requests for storage made by users.
    
* They specify what kind of storage they want (e.g. size, access modes).
    
* Kubernetes will bind the claim to an available PV that matches the requirements.
    

**So the process works as follows:**

1. Admins provision Persistent Volumes to represent storage resources (NFS, EBS, etc).
    
2. Users make Persistent Volume Claims specifying their storage requirements.
    
3. Kubernetes will bind the PVC to an available PV that matches.
    
4. The PV is then mounted into the Pod's filesystem. The Pod uses the storage for the lifetime of the PVC.
    
5. When the PVC is deleted, Kubernetes will unmount the PV from the Pod and the storage remains available for other PVCs.
    

**This decouples storage management from consumption:**

* Admins manage PVs to represent storage resources.
    
* Users consume storage through PVCs without knowing details of the underlying storage.
    

Kubernetes abstracts the storage and dynamically provisions it for Pods. This allows portability between different storage types and makes storage management simple for users.

### How does the NodePort service work?

The NodePort service is a type of Kubernetes Service that exposes the Service on a port on each Node IP address (the machines that make up the Kubernetes cluster).

**How it works:**

1. You define a NodePort Service which specifies a port number (in the 30000-32767 range).
    
2. Kubernetes allocates that port number on each Node in the cluster.
    
3. Kubernetes proxies the requests to this NodePort to the Service's endpoints.
    
4. Clients can then request the Service on any Node's IP address at that NodePort.
    

**This allows external clients to access the Service by either:**

* Using any Node's IP address followed by the NodePort For example:
    
    ```bash
    <NodeIP>:<NodePort>
    ```
    
* Or using the cluster's DNS name which resolves to the Node IPs, followed by the NodePort.
    

For example:

```bash
  my-service.my-namespace.svc.cluster.local:<NodePort>
```

**The main advantages of a NodePort Service are:**

* Simple to configure
    
* Allows external clients to access the Service using the Node IPs and port
    
* Useful for testing and development
    

**The downsides are:**

* Exposes the port on all Nodes, so any Node failure will disrupt the Service
    
* Uses a fixed port, so limits the number of NodePort Services you can have
    
* Not secure by default since the port is exposed on all Nodes
    

So in summary, a NodePort Service exposes a Service by allocating a port on the Nodes and proxying to the Service endpoints. This allows external clients to access the Service on any Node's IP address at that port.

### What is a multinode cluster and single-node cluster in Kubernetes?

A multinode Kubernetes cluster consists of multiple machines (called nodes) working together, while a single-node cluster has only one node.

**Multinode Cluster:**

* Consists of a master node and multiple worker nodes
    
* The master node controls the cluster and schedules pods
    
* The worker nodes run the actual pods and containers
    
* Provides high availability since work can be distributed across nodes
    
* Allows scaling the cluster by adding more worker nodes
    

**Single-node Cluster:**

* Consists of a single node that acts as both master and worker
    
* Easy to set up for testing and development
    
* Not highly available - if the single node fails, the whole cluster fails
    
* Cannot scale by adding more nodes
    

**The main differences are:**

* High availability: Multinode clusters can tolerate node failures since work is distributed. Single-node clusters have no redundancy.
    
* Scalability: Multinode clusters can scale horizontally by adding more nodes. Single-node clusters cannot scale.
    
* Complexity: Multinode clusters are more complex to set up and manage. Single-node clusters are simple.
    

**In summary:**

* **Single-node clusters are useful for:**
    
    * Testing and development
        
    * Learning Kubernetes
        
    * Running non-critical workloads
        
* **Multinode clusters are useful for:**
    
    * Production environments
        
    * Running critical workloads
        
    * Scalable and fault-tolerant clusters
        

So the type of cluster you choose depends on your requirements in terms of high availability, scalability, and complexity you want to deal with.

### Difference between create and apply in kubernetes?

The main difference between kubectl create and kubectl apply in Kubernetes is:

**kubectl create:**

* Creates a resource if it does not exist
    
* Fails if the resource already exists
    
* Does not modify the existing resource
    

**kubectl apply:**

* Creates a resource if it does not exist
    
* Applies the configuration to an existing resource
    
* Updates the resource if the configuration has changed
    
* Retains the resource annotations and labels
    

In short:

* **kubectl create:** Creates a resource only if it does not exist. Fails otherwise.
    
* **kubectl apply:** Creates a resource if it does not exist. Updates an existing resource if the configuration has changed.
    

**Other differences:**

* kubectl create ignores differences in annotations and labels, while kubectl apply retains them.
    
* kubectl apply performs a 3-way merge of the new and existing configurations.
    

**Some examples of when to use each:**

* Use kubectl create when first creating a resource and you want it to fail if the resource already exists.
    
* Use kubectl apply when deploying a new version of a resource and you want it to update the existing resource if needed.
    

**So in summary:**

* kubectl create is for first-time creation of a resource
    
* kubectl apply is for updating an existing resource with new configurations
    

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.