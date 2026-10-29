# Docker Installation and Basic Usage Guide

This repository contains my hands-on practice notes from the Udemy course:

**Docker & Kubernetes: The Practical Guide** by **Maximilian Schwarzmüller (Academind)**

The guide covers:

- Docker Installation on Amazon Linux 2023
- Running Containers
- Building Custom Images
- Interactive Containers
- Container Management
- Docker Networking
- Docker Hub
- Docker Image Management

---

# Table of Contents

1. Prerequisites
2. Docker Installation
3. Configure Docker for Non-Root User
4. Verify Docker Installation
5. Running Official Docker Images
6. Build Your Own Docker Image
7. Run Custom Docker Images
8. Run Containers in Background
9. Container Logs
10. Manage Containers
11. Attach to a Running Container
12. Interactive Mode Containers
13. Remove Containers
14. Remove Docker Images
15. Prune Unused Images
16. Automatically Remove Containers
17. Inspect Docker Resources
18. Copy Files Between Host and Container
19. Naming Containers
20. Docker Image Tagging
21. Docker Hub Login, Push and Pull
22. Working with Public Docker Images
23. Docker Commands Cheat Sheet
24. Summary

---

# 1. Prerequisites

- Amazon Linux 2023
- Sudo Privileges
- Internet Connectivity

---

# 2. Docker Installation

## Update the System

```bash
sudo dnf update -y
```

## Install Docker

```bash
sudo dnf install -y docker
```

## Start Docker Service

```bash
sudo systemctl start docker
```

## Enable Docker Service at Boot

```bash
sudo systemctl enable docker
```

## Verify Docker Service

```bash
sudo systemctl status docker
```

---

# 3. Configure Docker for Non-Root User

Allow the current user to run Docker commands without using sudo:

```bash
sudo usermod -aG docker $USER
```

Apply the new group membership:

```bash
newgrp docker
```

> Log out and log in again for the changes to take effect.

---

# 4. Verify Docker Installation

Run the Docker test container:

```bash
docker run hello-world
```

Expected output:

```text
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

Check Docker version:

```bash
docker --version
```

Example:

```text
Docker version 28.x.x
```

---

# 5. Running Official Docker Images

## Search Images

Visit Docker Hub:

https://hub.docker.com

Search for:

```text
node
```

## Run Node Image

```bash
docker run node
```

## List Containers

Running containers:

```bash
docker ps
```

All containers:

```bash
docker ps -a
```

## Run Interactive Container

```bash
docker run -it node
```

---

# 6. Build Your Own Docker Image

## Create Project Directory

```bash
mkdir dockerfile-ownimage
cd dockerfile-ownimage
```

## Create Application Files

```bash
vi server.js
vi package.json
vi Dockerfile
```

## Project Structure

```text
dockerfile-ownimage/
├── Dockerfile
├── package.json
└── server.js
```

## Sample Dockerfile

```Dockerfile
FROM node:18

WORKDIR /app

COPY . .

RUN npm install

EXPOSE 80

CMD ["node", "server.js"]
```

## Build Docker Image

```bash
docker build .
```

Or build with a tag:

```bash
docker build -t node-app:v1 .
```

## Verify Images

```bash
docker images
```

---

# 7. Run Custom Docker Images

Using Image ID:

```bash
docker run -p 443:80 IMAGE_ID
```

Using Tagged Image:

```bash
docker run -p 443:80 node-app:v1
```

### Port Mapping

```text
443 → Host Port
80  → Container Port
```

Verify the application:

```text
http://SERVER-IP:443
```

---

# 8. Run Containers in Background

Run a container in detached mode:

```bash
docker run -d -p 80:80 node-app:v1
```

Run with a custom container name:

```bash
docker run -d --name node-app-container -p 80:80 node-app:v1
```

Verify:

```bash
docker ps
```

---

# 9. Container Logs

View logs:

```bash
docker logs node-app-container
```

Follow logs in real time:

```bash
docker logs -f node-app-container
```

---

# 10. Manage Containers

Stop a container:

```bash
docker stop node-app-container
```

Start a stopped container:

```bash
docker start node-app-container
```

Restart a container:

```bash
docker restart node-app-container
```

Remove a container:

```bash
docker rm node-app-container
```

---

# 11. Attach to a Running Container

Attach to a running container:

```bash
docker attach CONTAINER_ID
```

Detach without stopping the container:

```text
CTRL + P
CTRL + Q
```

View logs instead of attaching:

```bash
docker logs CONTAINER_ID
docker logs -f CONTAINER_ID
```

---

# 12. Interactive Mode Containers

## Create Project

```bash
mkdir docker-interactive-mode
cd docker-interactive-mode
```

Create files:

```bash
vi Dockerfile
vi rng.py
```

## Build Image

```bash
docker build .
```

## Run Interactive Container

```bash
docker run -it IMAGE_ID
```

## Restart and Attach

```bash
docker start -ai CONTAINER_ID
```

### Useful Flags

| Flag | Description |
|--------|------------|
| `-a` | Attach |
| `-i` | Interactive |
| `-t` | Allocate Terminal |

---

# 13. Remove Containers

Remove a container:

```bash
docker rm CONTAINER_ID
```

Remove multiple containers:

```bash
docker rm CONTAINER1 CONTAINER2 CONTAINER3
```

View all containers:

```bash
docker ps -a
```

---

# 14. Remove Docker Images

List images:

```bash
docker images
```

Remove an image:

```bash
docker rmi IMAGE_ID
```

Check disk usage:

```bash
df -h
```

---

# 15. Prune Unused Images

Remove dangling images:

```bash
docker image prune
```

Remove all unused images:

```bash
docker image prune -a
```

---

# 16. Automatically Remove Containers

Run a container and automatically remove it after stopping:

```bash
docker run --rm IMAGE_ID
```

Example:

```bash
docker run -d -p 443:80 --rm IMAGE_ID
```

---

# 17. Inspect Docker Resources

Inspect an image:

```bash
docker inspect IMAGE_ID
```

Inspect a container:

```bash
docker inspect CONTAINER_ID
```

---

# 18. Copy Files Between Host and Container

## Host → Container

```bash
docker cp local-path CONTAINER_NAME:/target-path
```

## Container → Host

```bash
docker cp CONTAINER_NAME:/file-path local-directory
```

---

# 19. Naming Containers

Run a named container:

```bash
docker run -d --name goalsapp goals:latest
```

Stop the container:

```bash
docker stop goalsapp
```

---

# 20. Docker Image Tagging

Tag an image:

```bash
docker tag goals:latest rushi5912/node-goals:latest
```

Verify:

```bash
docker images
```

---

# 21. Docker Hub Login, Push and Pull

Login:

```bash
docker login
```

Push an image:

```bash
docker push rushi5912/node-goals:latest
```

Logout:

```bash
docker logout
```

Pull an image:

```bash
docker pull rushi5912/node-goals:latest
```

---

# 22. Working with Public Docker Images

Pull a public image:

```bash
docker pull academind/node-hello-world
```

Run the image:

```bash
docker run -d -p 3000:3000 academind/node-hello-world
```

Verify:

```bash
docker ps
```

---

# 23. Docker Commands Cheat Sheet

## Container Commands

```bash
docker ps
docker ps -a
docker run IMAGE_ID
docker run -d IMAGE_ID
docker run -it IMAGE_ID
docker stop CONTAINER_ID
docker start CONTAINER_ID
docker rm CONTAINER_ID
```

## Image Commands

```bash
docker images
docker build .
docker build -t myapp:latest .
docker rmi IMAGE_ID
docker image prune
docker image prune -a
```

## Logs & Debugging

```bash
docker logs CONTAINER_ID
docker logs -f CONTAINER_ID
docker inspect CONTAINER_ID
docker inspect IMAGE_ID
```

## Docker Hub Commands

```bash
docker login
docker push IMAGE_NAME
docker pull IMAGE_NAME
docker logout
```

## File Operations

```bash
docker cp HOST_PATH CONTAINER:/PATH
docker cp CONTAINER:/PATH HOST_PATH
```

## Networking

```bash
docker run -p HOST_PORT:CONTAINER_PORT IMAGE_ID
```

Example:

```bash
docker run -p 3000:80 IMAGE_ID
```

---

# 24. Summary

✅ Install Docker on Amazon Linux 2023  
✅ Configure Docker for non-root users  
✅ Verify Docker installation  
✅ Run Docker Hub images  
✅ Build custom Docker images  
✅ Run containers using port mapping  
✅ Run containers in detached mode  
✅ View logs and attach to containers  
✅ Work with interactive containers  
✅ Manage images and containers  
✅ Copy files between host and containers  
✅ Use Docker Hub for image distribution  
✅ Clean up unused Docker resources
