# Day 4 - Docker Concepts and Commands

## Overview

Day 4 focused on understanding Docker and its ecosystem. We learned about containers, Dockerfiles, Docker images, and how to build, run, and manage containerized applications using essential Docker commands. The session also covered writing Dockerfiles, port mapping, and pushing images to Docker Hub for deployment.

---

## Environments

- **Development Environment**: Developers test basic functionality with minimal test cases.
- **Testing Environment**: QA team performs detailed functional and non-functional tests (e.g., performance, load).
- **UAT (User Acceptance Testing)**: A prototype is shown to the client for approval before production.
- **Production Environment**: Final application is deployed for real users.

---

## What is a Container?

A container is an isolated environment (server) used to run applications. It includes everything the app needs to run.

---

## Docker Concepts

### 1. **Dockerfile**

A script with instructions to build a Docker image.

### 2. **Docker Image**

A read-only template that includes:

- Source code
- Dependencies
- Config files
- OS libraries

### 3. **Docker Hub**

Online registry to store and share Docker images.

---

## Common Docker Commands

```bash
docker ps -a               # List all containers (running + stopped)
docker ps                  # List only running containers
service docker start       # Start Docker
service docker status      # Check Docker status

docker create ubuntu /bin/bash
docker create -it --name webserver amazonlinux /bin/bash
docker start webserver
docker exec -it webserver /bin/bash

docker run -it --name sample ubuntu /bin/bash
docker run -td --name web-app -p 3002:3000 muralisocial123/cart-page-test:1.0
```

## Exit container without stopping

Ctrl + P + Q

## Docker Cheat Sheet & Example Walkthrough

## Docker Port Mapping (`-p` Flag)

Maps container port to host machine.

**Format:**
`-p <host-port>:<container-port>`

**Example:**
`-p 3002:3000`  
Means browser hits port **3002** on the host, which routes to port **3000** inside the container.

---

## Dockerfile Instructions

### Build-Time Commands

- `FROM`: Base image (required at top).
- `COPY`: Copy files/folders from host to image.
- `ADD`: Like COPY, but also supports URLs and archives.
- `RUN`: Execute commands (e.g., install packages).
- `.dockerignore`: Prevents unnecessary files from being added to image.

### Run-Time Commands

- `CMD`: Command to run container (can override at runtime).
- `ENTRYPOINT`: Fixed entry script (harder to override).
- `EXPOSE`: Declare app port inside container.
- `ENV`: Set environment variables.
- `WORKDIR`: Set working directory inside container.
- `USER`: Add or switch user.

---

## Steps to Write a Dockerfile

1. Choose a base image (e.g., `node`, `nginx`, etc.)
2. Set a working directory.
3. Copy dependencies.
4. Install packages.
5. Copy application code.
6. Expose necessary ports.
7. Define the run command (`CMD` or `ENTRYPOINT`).

---

## Docker Build & Push Example

```bash
git clone -b master https://github.com/msranjana/Dimple-CapsuleProject.git
cd Dimple-CapsuleProject

docker build -t web-app-nodejs:1.0 .
docker images

docker run -td --name node-app -p 3015:3015 web-app-nodejs:1.0
docker ps
docker exec -it node-app /bin/bash

```

## Docker Hub

Sign up at [hub.docker.com](https://hub.docker.com)

Store and share Docker images easily with your Docker ID.

---

### Login & Push Image

```bash
docker login
docker push msranjana/web-app-nodejs:1.0
```
