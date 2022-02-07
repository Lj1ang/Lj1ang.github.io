---
title: "docker"
date: 2022-02-06T22:58:02+08:00
slug: ""
description: ""
keywords: []
draft: false
tags: []
math: false
toc: true
---

# Docker

### Container

container is a sandboxed process on your machine that is isolated from all other processes on the host machine. 

Containers are great for continuous integration and continuous delivery (CI/CD) workflows.

### Container image

When running a container, it uses an isolated filesystem. This custom filesystem is provided by a container image. 

the Docker client talks to the Docker daemon, which does the heavy lifting of building, running, and distributing your Docker containers.

### The Docker daemon

The Docker daemon (`dockerd`) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.

### The Docker client

The Docker client (docker) is the primary way that many Docker users interact with Docker. 

The docker command uses the Docker API. The Docker client can communicate with more than one daemon.

### Docker registries

A Docker registry stores Docker images. Docker Hub is a public registry that anyone can use, and **Docker is configured to look for images on Docker Hub by default.** You can even run your own private registry.

- Images:An image is a read-only template with instructions for creating a Docker container. 
- Containers:A container is a runnable instance of an image. 

namespace用于隔离各个container，run一个container时，docker会给该container创建一系列namespace

flag

```docker
-d - run the container in detached mode (in the background)
-p 80:80 - map port 80 of the host to port 80 in the container
docker/getting-started - the image to use

```

