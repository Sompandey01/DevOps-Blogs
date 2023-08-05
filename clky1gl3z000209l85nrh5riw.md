---
title: "Day 19: Docker for DevOps Engineers"
datePublished: Sat Aug 05 2023 13:16:36 GMT+0000 (Coordinated Universal Time)
cuid: clky1gl3z000209l85nrh5riw
slug: day-19-docker-for-devops-engineers
tags: docker, devops, docker-network, 90daysofdevops, trainwithshubham

---

**Till now you have learned how to create a docker-compose.yml file and pushed it to the Repository. Let's move forward and dig more into other Docker-compose.yml concepts.** **Aaj thodi padhai krte hai on Docker Volume & Docker Network** 😃

# Docker-Volume

Docker allows you to create something called volumes. Volumes are like separate storage areas that can be accessed by containers. They allow you to store data, like a database, outside the container, so it doesn't get deleted when the container is deleted. You can also mount from the same volume and create more containers having the same data.

### Docker Volume Commands -

Here's a list of Docker volume commands:

1. `docker volume create <VOLUME_NAME>`: Create a named volume.
    
2. `docker volume ls`: List available volumes.
    
3. `docker volume inspect <VOLUME_NAME>`: Display detailed volume information.
    
4. `docker volume rm <VOLUME_NAME>`: Remove a named volume (must be unused).
    
5. `docker volume prune`: Remove all unused volumes.
    
6. `docker run -v <VOLUME_NAME>:<CONTAINER_PATH>`: Mount a named volume to a container.
    
7. `docker run -v <HOST_PATH>:<CONTAINER_PATH>`: Mount a host directory to a container.
    

# Docker Network

Docker allows you to create virtual spaces called networks, where you can connect multiple containers (small packages that hold all the necessary files for a specific application to run) together. This way, the containers can communicate with each other and with the host machine (the computer on which the Docker is installed). When we run a container, it has its own storage space that is only accessible by that specific container. If we want to share that storage space with other containers, we can't do that.

### Docker Network Commands -

Here's a list of Docker network commands:

1. `docker network create <NETWORK_NAME>`: Create a new user-defined network.
    
2. `docker network ls`: List available networks.
    
3. `docker network inspect <NETWORK_NAME>`: Display detailed network information.
    
4. `docker network rm <NETWORK_NAME>`: Remove a user-defined network (must be unused).
    
5. `docker network prune`: Remove all unused networks.
    
6. `docker run --network <NETWORK_NAME>`: Specify a network for a container to join.
    
7. `docker network connect <NETWORK_NAME> <CONTAINER_NAME>`: Connect a container to a user-defined network.
    
8. `docker network disconnect <NETWORK_NAME> <CONTAINER_NAME>`: Disconnect a container from a user-defined network.
    

## Task-1: Create a multi-container docker-compose file which will bring *UP* and bring *DOWN* containers in a single shot ( Example - Create application and database container )

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691236199390/e900e128-e8b0-4835-83ae-264af34b64c3.png align="center")

**Use the** `docker-compose up` **command with the** `-d` **flag to start a multi-container application in detached mode.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691237856270/093bcc6b-ce2f-42f2-ab81-2858e23a42c1.png align="center")

Check whether the service is running or not by using `docker ps`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691238002906/49fda718-7e77-4580-baff-db67d97ca108.png align="center")

Check if the web is working or not, use `localhost` and add the port number

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691238088645/05efcf8d-464d-43d9-ad2e-5141880656e6.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691238113493/c0baa42a-5d2f-4e64-9787-c8607bcf41f2.png align="center")

**Use the** `docker-compose scale` **command to increase or decrease the number of replicas for a specific service. You can also add** [`replicas`](https://stackoverflow.com/questions/63408708/how-to-scale-from-within-docker-compose-file) **in deployment file for *auto-scaling*.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691238473162/5ad1cb25-ec71-49c8-981d-6e6163690859.png align="center")

Now, we can access our website on port 8005 also.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691238589308/409fe504-4af3-4f68-b729-5e630989a15a.png align="center")

Keeping a single instance for our web service

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691238796985/bf8a95bf-3d2a-4f31-bcf2-a567fb8f52b0.png align="center")

Now, we can only access our website on a single port 8003.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691238926722/26d77833-f462-4930-8cb8-f38c5697f5e4.png align="center")

Now, If you try to access it on another port it will give an error.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691239001393/f3272dff-62d4-4b99-9768-b82ade41e29d.png align="center")

**Use the** `docker-compose ps` **command to view the status of all containers, and** `docker-compose logs` **to view the logs of a specific service.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691239160491/ae1aea33-10c6-4e23-800d-d7179eae20f1.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691239195602/ff0aec55-0854-45e6-ac9b-aa933977b07d.png align="center")

**Use the** `docker-compose down` **command to stop and remove all containers, networks, and volumes associated with the application.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691239304043/c260d04f-a7c4-405e-8612-75454a9b1c39.png align="center")

## Task-2: Learn how to use Docker Volumes and Named Volumes to share files and directories between multiple containers.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691239514589/4281575f-fcb9-4abc-bd15-449b732b2a62.png align="center")

**Create two or more containers that read and write data to the same volume using the** `docker run --mount` **command.**

Creating two containers using nginx -

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691239934672/ba5e1aa2-5ca0-46ac-8ccd-2c462870c6a4.png align="center")

**Verify that the data is the same in all containers by using the docker exec command to run commands inside each container.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691240776120/ab9aa863-e6f8-4d30-a037-bf4e3b53716b.png align="center")

**Use the** `docker volume ls` **command to list all volumes and** `docker volume rm` **command to remove the volume when you're done.**

Using `docker volume ls` command -

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691240895546/074f197f-dbf3-4db7-9e6b-1718575e6bbe.png align="center")

Removing the volume using `docker volume rm` command -

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691241245802/db83637c-956e-4557-bb76-4377ed87770c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691241307667/e387b678-2072-4530-8fb9-d811cdc3744f.png align="center")

I hope you like my blog..!!

Stay Connected with me for more interesting articles on DevOps, if you like my blog follow me on **Hashnode** and **Linkedin** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)