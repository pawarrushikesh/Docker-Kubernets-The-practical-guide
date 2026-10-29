# Docker Installation and Basic Usage Guide

This repository provides a step-by-step guide for:

- Installing Docker on Amazon Linux 2023
- Running Docker containers using official images from Docker Hub
- Building custom Docker images using a Dockerfile
- Running containers from custom images

---

# Prerequisites

- Amazon Linux 2023
- Sudo privileges
- Internet connectivity

---

# Docker Installation

## 1. Update the System

```bash
sudo dnf update -y
```

## 2. Install Docker

```bash
sudo dnf install -y docker
```

## 3. Start Docker Service

```bash
sudo systemctl start docker
```

## 4. Enable Docker on Boot

```bash
sudo systemctl enable docker
```

## 5. Verify Docker Service Status

```bash
sudo systemctl status docker
```

---

# Configure Docker for Non-Root User

Allow the current user to execute Docker commands without using `sudo`.

```bash
sudo usermod -aG docker $USER
```

Apply the group changes:

```bash
newgrp docker
```

---

# Test Docker Installation

Run the Docker test container:

```bash
docker run hello-world
```

Expected result:

```text
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

---

# Check Docker Version

```bash
docker --version
```

Example Output:

```text
Docker version 28.x.x
```

---

# One-Shot Installation Command

You can install and configure Docker using a single command:

```bash
sudo dnf update -y && \
sudo dnf install -y docker && \
sudo systemctl enable --now docker && \
sudo usermod -aG docker $USER
```

> Logout and login again after adding the user to the Docker group.

---

# Part 1: Running an Official Docker Image

## Search for an Image

Open Docker Hub:

https://hub.docker.com

Search for an image, for example:

```text
node
```

Use the Official Node.js image.

---

## Run the Node Image

Docker will automatically download the image if it is not available locally.

```bash
docker run node
```

---

## List All Containers

```bash
docker ps -a
```

---

## List Running Containers

```bash
docker ps
```

---

## Run Container in Interactive Mode

```bash
docker run -it node
```

---

# Part 2: Build Your Own Docker Image

## Create Project Directory

```bash
mkdir dockerfile-ownimage
cd dockerfile-ownimage
```

---

## Create Application Files

### Create server.js

```bash
vi server.js
```

### Create package.json

```bash
vi package.json
```

### Create Dockerfile

```bash
vi Dockerfile
```

---

## Project Structure

```text
dockerfile-ownimage/
├── Dockerfile
├── package.json
└── server.js
```

---

## Sample Dockerfile

```Dockerfile
FROM node:18

WORKDIR /app

COPY . .

RUN npm install

EXPOSE 80

CMD ["node", "server.js"]
```

---

# Build Docker Image

Build the image from the current directory:

```bash
docker build .
```

Or tag the image with a name:

```bash
docker build -t node-app:v1 .
```

---

## Verify Images

```bash
docker images
```

---

# Run Custom Image

Using Image ID:

```bash
docker run -p 443:80 90cd42400a3
```

Using Tagged Image:

```bash
docker run -p 443:80 node-app:v1
```

### Port Mapping

```text
443 -> Host Port
80  -> Container Port
```

---

# Useful Docker Commands

## List Images

```bash
docker images
```

## List Running Containers

```bash
docker ps
```

## List All Containers

```bash
docker ps -a
```

## Stop Container

```bash
docker stop <container-id>
```

## Remove Container

```bash
docker rm <container-id>
```

## Remove Image

```bash
docker rmi <image-id>
```

---

# Verification

Access the application using:

```text
http://<SERVER-IP>:443
```

If everything is configured correctly, the application response will be displayed in the browser.

---

# Run Custom Image

Using Image ID:

```bash
docker run -p 443:80 90cd42400a3
```

Using Tagged Image:

```bash
docker run -p 443:80 node-app:v1
```

### Port Mapping

```text
443 -> Host Port
80  -> Container Port
```

---

# Run Container in Background

To run the container in detached mode (background), use the `-d` option:

```bash
docker run -d -p 80:80 node-app:v1
```

To assign a custom container name:

```bash
docker run -d --name node-app-container -p 80:80 node-app:v1
```

---

# Verify Running Containers

List running containers:

```bash
docker ps
```

List all containers:

```bash
docker ps -a
```

---

# View Container Logs

View logs for a container:

```bash
docker logs <container-id>
```

Example:

```bash
docker logs node-app-container
```

Follow logs in real time:

```bash
docker logs -f node-app-container
```

---

# Manage Containers

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

# Access the Application

Open a browser and navigate to:

```text
http://<SERVER-IP>
```

For local testing:

```text
http://localhost
```
# 7. Attach to a Running Container

Docker allows you to attach your terminal to a running container and interact with its primary process directly.

## View Running Containers

```bash
docker ps
```

## Attach to a Running Container

```bash
docker attach CONTAINER_ID
```

Example:

```bash
docker attach 0a
```

## Detach Without Stopping the Container

Use the following key combination:

```text
CTRL + P
CTRL + Q
```

## View Logs Instead of Attaching

```bash
docker logs CONTAINER_ID
```

Follow logs in real time:

```bash
docker logs -f CONTAINER_ID
```

### Commands Summary

| Command | Description |
|----------|-------------|
| `docker attach CONTAINER_ID` | Attach to a running container |
| `docker logs CONTAINER_ID` | View container logs |
| `docker logs -f CONTAINER_ID` | Follow container logs |
| `CTRL + P, CTRL + Q` | Detach without stopping |

---

# 8. Interactive Mode Containers

Interactive mode allows users to provide input directly to a container.

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

### Flags

| Flag | Description |
|--------|-------------|
| `-i` | Interactive mode |
| `-t` | Terminal allocation |

Example:

```bash
docker run -it 1d
```

## Restart Interactive Container

```bash
docker start -ai CONTAINER_ID
```

Example:

```bash
docker start -ai 8f4f0bfd0a4
```

### Commands Summary

| Command | Description |
|----------|-------------|
| `docker run -it IMAGE_ID` | Run container interactively |
| `docker start -ai CONTAINER_ID` | Restart and attach interactively |

---

# 9. Remove Containers

Containers that are no longer required can be removed to free resources.

## Remove a Container

```bash
docker rm CONTAINER_ID
```

Example:

```bash
docker rm blissful_keldysh
```

## Remove Multiple Containers

```bash
docker rm CONTAINER1 CONTAINER2 CONTAINER3
```

## View Containers

```bash
docker ps -a
```

### Commands Summary

| Command | Description |
|----------|-------------|
| `docker rm CONTAINER_ID` | Remove container |
| `docker ps -a` | List all containers |

---

# 10. Remove Docker Images

Docker images can be removed when they are no longer needed.

## View Images

```bash
docker images
```

## Remove an Image

```bash
docker rmi IMAGE_ID
```

Example:

```bash
docker rmi c6b31813c699
```

## Check Disk Usage

```bash
df -h
```

### Commands Summary

| Command | Description |
|----------|-------------|
| `docker images` | List images |
| `docker rmi IMAGE_ID` | Remove image |
| `df -h` | Check disk usage |

---

# 11. Prune Unused Images

Docker stores dangling and unused images that can be cleaned up.

## Remove Dangling Images

```bash
docker image prune
```

## Remove All Unused Images

```bash
docker image prune -a
```

### Commands Summary

| Command | Description |
|----------|-------------|
| `docker image prune` | Remove dangling images |
| `docker image prune -a` | Remove all unused images |

---

# 12. Automatically Remove Containers

The `--rm` flag automatically removes the container when it exits.

## Run Container with Auto Remove

```bash
docker run --rm IMAGE_ID
```

Example:

```bash
docker run -d -p 443:80 --rm IMAGE_ID
```

### Commands Summary

| Command | Description |
|----------|-------------|
| `docker run --rm IMAGE_ID` | Automatically remove container after stop |

---

# 13. Inspect Docker Resources

Docker Inspect provides low-level details of images and containers.

## Inspect an Image

```bash
docker inspect IMAGE_ID
```

Example:

```bash
docker inspect 29
```

## Inspect a Container

```bash
docker inspect CONTAINER_ID
```

### Commands Summary

| Command | Description |
|----------|-------------|
| `docker inspect IMAGE_ID` | Inspect image details |
| `docker inspect CONTAINER_ID` | Inspect container details |

---

# 14. Copy Files Between Host and Container

Docker provides the `cp` command for copying files.

## Host to Container

```bash
docker cp local-path CONTAINER_NAME:/target-path
```

Example:

```bash
docker cp dummy/. hopeful_brahmagupta:/
```

## Container to Host

```bash
docker cp CONTAINER_NAME:/file-path local-directory
```

Example:

```bash
docker cp hopeful_brahmagupta:/test.txt dummy/
```

### Commands Summary

| Command | Description |
|----------|-------------|
| `docker cp HOST_PATH CONTAINER:/PATH` | Copy file to container |
| `docker cp CONTAINER:/PATH HOST_PATH` | Copy file from container |

---

# 15. Naming Containers

Container names make management easier than using container IDs.

## Create Named Container

```bash
docker run --name goalsapp IMAGE_ID
```

Example:

```bash
docker run -d -p 3000:80 --rm --name goalsapp goals:latest
```

## Stop Named Container

```bash
docker stop goalsapp
```

### Commands Summary

| Command | Description |
|----------|-------------|
| `docker run --name NAME IMAGE_ID` | Assign custom container name |
| `docker stop NAME` | Stop container using name |

---

# 16. Docker Image Tagging

Tags identify versions of images.

## Tag an Image

```bash
docker tag SOURCE_IMAGE TARGET_IMAGE
```

Example:

```bash
docker tag goals:latest rushi5912/node-goals:latest
```

## View Images

```bash
docker images
```

### Commands Summary

| Command | Description |
|----------|-------------|
| `docker tag` | Create image tag |
| `docker images` | View image tags |

---

# 17. Docker Hub Login, Push and Pull

Docker Hub is a cloud-based registry used to store and share Docker images.

## Login

```bash
docker login
```

## Push Image

```bash
docker push rushi5912/node-goals:latest
```

## Logout

```bash
docker logout
```

## Pull Image

```bash
docker pull rushi5912/node-goals:latest
```

### Commands Summary

| Command | Description |
|----------|-------------|
| `docker login` | Login to Docker Hub |
| `docker push` | Upload image |
| `docker pull` | Download image |
| `docker logout` | Logout from Docker Hub |

---

# 18. Working with Public Docker Images

Docker Hub contains thousands of public images.

## Pull Public Image

```bash
docker pull academind/node-hello-world
```

## Run Public Image

```bash
docker run -p 3000:3000 -d academind/node-hello-world
```

## View Running Containers

```bash
docker ps
```

### Commands Summary

| Command | Description |
|----------|-------------|
| `docker pull IMAGE_NAME` | Download image |
| `docker run IMAGE_NAME` | Run image as container |
| `docker ps` | View running containers |

---

# 19. Docker Commands Cheat Sheet

## Container Management

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

## Image Management

```bash
docker images
docker build .
docker build -t myapp:latest .
docker rmi IMAGE_ID
docker image prune
docker image prune -a
```

## Logs and Debugging

```bash
docker logs CONTAINER_ID
docker logs -f CONTAINER_ID
docker inspect CONTAINER_ID
docker inspect IMAGE_ID
```

## Docker Hub

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

## Container Networking

```bash
docker run -p HOST_PORT:CONTAINER_PORT IMAGE_ID
```

Example:

```bash
docker run -p 3000:80 IMAGE_ID
```

---

# Key Concepts Covered

✅ Attach & Detach Containers  
✅ Interactive Containers (`-it`)  
✅ Container Logs  
✅ Remove Containers (`docker rm`)  
✅ Remove Images (`docker rmi`)  
✅ Docker Image Cleanup (`prune`)  
✅ Auto Remove Containers (`--rm`)  
✅ Docker Inspect  
✅ File Copy with `docker cp`  
✅ Named Containers (`--name`)  
✅ Image Tagging (`docker tag`)  
✅ Docker Hub Push/Pull  
✅ Public Images  
✅ Docker Commands Cheat Sheet
# Summary

In this guide, you learned how to:

✅ Install Docker on Amazon Linux 2023  
✅ Configure Docker for non-root users  
✅ Verify Docker installation  
✅ Run official Docker Hub images  
✅ Create a Dockerfile  
✅ Build custom Docker images  
✅ Run containers with port mapping  
✅ Manage Docker containers and images
