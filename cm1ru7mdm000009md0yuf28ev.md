---
title: "Optimizing Docker Image with Multi-Stage Builds: Reducing Image Size by 99%"
datePublished: Wed Oct 02 2024 12:22:03 GMT+0000 (Coordinated Universal Time)
cuid: cm1ru7mdm000009md0yuf28ev
slug: optimizing-docker-image-with-multi-stage-builds-reducing-image-size-by-99
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1727867205471/8973d0cc-6ebd-40c5-8552-4238539f3e2a.png
tags: docker, devops, dockerfile, docker-images, devops-articles

---

I’ve been working with Docker for a while, and recently I ran into a problem with my Docker image size. One of my images was around **1GB**, which felt way too big! 😬 A large image means slower deployment, more storage space, and overall just not efficient.

So, I decided to fix this by using a **multi-stage Dockerfile**, and guess what? I reduced the image size by **99%**! 🎉

### 😓 The Problem with Traditional Dockerfiles

A normal Dockerfile is pretty straightforward. You start with a base image, install your dependencies, build the application, and then run it. But all this stuff stays in the image, even the things you don’t need after the app is built. This makes the image larger than it needs to be.

Here’s what a traditional Dockerfile might look like:

```yaml
# Traditional Dockerfile example
FROM python:3.9

WORKDIR /app/backend

COPY requirements.txt /app/backend
RUN pip install -r requirements.txt

COPY . /app/backend

EXPOSE 8000

CMD python /app/backend/manage.py runserver 0.0.0.0:8000
```

In this Dockerfile, we’re:

* Using the full python image (which is quite big),
    
* Installing all the dependencies,
    
* And keeping everything in the final image, even the build tools, which we don’t need once the app is built.
    

As a result, you end up with a pretty big image that’s not optimized at all. 😕

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727869224299/4cdb9af4-5ddd-4326-aa25-7befc70b862a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727869452868/298deb4f-c69a-471a-a312-f1d0373f9c3b.png align="center")

### 🎯 Enter Multi-Stage Builds: A Game-Changer

Now, let me tell you about **multi-stage builds**. This approach allows you to split the Dockerfile into stages. In the first stage, you do all the heavy work like installing dependencies and building the app. In the final stage, you only copy over what’s needed to run the app—nothing else.

Here’s an example of a multi-stage Dockerfile:

```yaml
# Stage 1: Build the application
FROM python:3.9 AS build

WORKDIR /app/backend

COPY requirements.txt /app/backend
RUN pip install -r requirements.txt

COPY . /app/backend

# Stage 2: Create the final image with only the necessary artifact
FROM python:3.9-slim

COPY --from=build /app/backend /app/backend
# Expose the application port
EXPOSE 8000
# Command to run the application
CMD python /app/backend/manage.py runserver 0.0.0.0:8000
```

**How it works:**

* **Stage 1**: I’m using the `python:3.9` image to build the app. This includes installing all dependencies and running the build process. 🛠️
    
* **Stage 2**: In this stage, I switch to a much lighter image (`python:3.9-slim`) and copy only the built files from the first stage. This makes the final image way smaller! 📦
    

### 🔥 The Results:

By using multi-stage builds, I was able to reduce my Docker image size from **1GB to just 100MB**! 😱 That’s a **90% reduction**! Not only did this save space, but it also made my deployments much faster! ⚡

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727869829870/9750bf8c-4b2c-47ea-83a0-7503e2a809b1.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727870053295/25dd05da-0e48-431b-847a-faaa6d3bd91c.png align="center")

### Wanna Know Something More Awesome? 🤩

You can reduce the size of this image even more by using `scratch` as a base image! The `scratch` image is completely empty, which means that when you use it, you only include what you absolutely need. This can shrink your image size from **1GB to just 10MB**—almost a **99% reduction**! 😲

Here’s how you can modify the multi-stage Dockerfile to use `scratch`:

```yaml
# Stage 1: Build the application
FROM python:3.9 AS build

WORKDIR /app/backend

COPY requirements.txt /app/backend
RUN pip install -r requirements.txt

COPY . /app/backend

# Stage 2: Create the final image with only the necessary artifact
FROM scratch
COPY --from=build /app/backend /app/backend
# Expose the application port
EXPOSE 8000
# Command to run the application
CMD python /app/backend/manage.py runserver 0.0.0.0:8000
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727871401401/218b27c7-710b-44dd-ac0e-74b3de2996c1.png align="center")

### Why You Should Try Multi-Stage Builds:

1. **Smaller Image Sizes** 📉: Since you’re only copying what’s necessary, your final image stays lean.
    
2. **Faster Deployments** 🚀: Smaller images are quicker to deploy, meaning less waiting time.
    
3. **Improved Security** 🔒: A smaller image has fewer components, which reduces potential vulnerabilities.
    
4. **Lower Costs** 💰: Less storage space means lower costs, especially in large-scale environments.
    

### 💭 Final Thoughts

If you’ve been dealing with large Docker images, give **multi-stage builds** a try. It’s easy to set up, and the results are worth it. You’ll have faster deployments, smaller images, and fewer headaches! 🧠

I’m still learning and experimenting with Docker, so feel free to share your tips or experiences in the comments! 😊