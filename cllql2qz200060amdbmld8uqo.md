---
title: "Managing Persistent Volumes in Your Deployment 💥"
datePublished: Fri Aug 25 2023 12:43:15 GMT+0000 (Coordinated Universal Time)
cuid: cllql2qz200060amdbmld8uqo
slug: managing-persistent-volumes-in-your-deployment
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692967156737/542c7581-072f-451f-b383-c9760bad47f5.png
tags: kubernetes, devops, k8s, 90daysofdevops, trainwithshubham

---

## What are Persistent Volumes in k8s

In Kubernetes, a Persistent Volume (PV) is a piece of storage in the cluster that has been provisioned by an administrator. A Persistent Volume Claim (PVC) is a request for storage by a user. The PVC references the PV, and the PV is bound to a specific node.

Persistent Volumes in Kubernetes are like reserved storage units that apps in the cluster can use to store data. They keep data safe even if apps come and go. PVs separate storage management from apps, making it easier to handle storage for applications.

Here's an overview of how volumes work in Kubernetes:

* **Container-Level Storage:** Containers in a pod are ephemeral, meaning that their data doesn't persist after the container stops or restarts. Volumes offer a way to provide persistent storage that exists independently of the containers.
    
* **Volume Types:** Kubernetes supports various volume types, such as EmptyDir (temporary storage within a pod), HostPath (using the host's file system), PersistentVolumeClaim (dynamically provisioned persistent storage), and cloud-provider-specific options like AWS EBS or Azure Disk.
    
* **Shared Storage:** Volumes allow multiple containers within the same pod to share data. This can be useful for scenarios where containers need to exchange information or cooperate.
    
* **Data Preservation:** Volumes can preserve data beyond the lifecycle of a pod. For instance, if a pod crashes or is rescheduled, data stored in a persistent volume will still be accessible when a new pod is started.
    
* **Volume Mounts:** To use a volume, a container needs to mount it. This means attaching the volume to a specific path within the container's filesystem. Containers can read and write data to this mounted path, and the data will be stored in the volume.
    

### **Task 1: Integrating Persistent Volume for Kubernetes Todo App**

Add a Persistent Volume to your Deployment todo app.

* **Create a Persistent Volume using a file on your node.**
    

```python
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-todo-app
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  hostPath:
    path: "/tmp/data"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692964654245/6b3bebaa-1d1c-4e2d-bb2d-1813cc109963.png align="center")

Apply the file using the below command:

```python
kubectl apply -f pv.yml -n <namespace-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692964816021/0d7f26ab-880a-442d-94bd-83725ad0b798.png align="center")

* **Create a Persistent Volume Claim that references the Persistent Volume.**
    

```python
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-todo-app
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692964997988/089fe9d9-ad08-4afc-88d0-d51a9a39add7.png align="center")

* **Update your deployment.yml file to include the Persistent Volume Claim.**
    

```python
apiVersion: apps/v1
kind: Deployment
metadata:
  name: todo-app-deployment
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
          volumeMounts:
            - name: todo-app-data
              mountPath: /app
      volumes:
        - name: todo-app-data
          persistentVolumeClaim:
            claimName: pvc-todo-app
```

this commands

* **Verify that the Persistent Volume has been added to your Deployment by checking the status of the Pods and Persistent Volumes in your cluster. Use these commands:**
    

```python
kubectl get pods -n < namespace-name >
kubectl get pv -n < namespace-name >
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692965491314/e32772c1-38a6-42e6-bc80-eed2daf3cff5.png align="center")

### **Task 2: Accessing Persistent Volume Data Within a Kubernetes Pod**

Accessing data in the Persistent Volume,

* **Connect to a Pod in your Deployment using the command : \`kubectl exec -it -- /bin/bash**
    

Inside a app folder create a new file demo.txt

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692966661173/1154029b-546d-4ca1-8ee7-09e3b05617bc.png align="center")

* **Verify that you can access the data stored in the Persistent Volume from within the Pod**
    

Delete the pod which we created in above steps it'll automatically create a new pod.

Go inside the new pod using kubectl exec /bin/bash command, then go to app folder and check the demo.txt file is there or not.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692966930766/6fd079b1-7e5a-473b-a5a4-ffe051689aff.png align="center")

"Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.