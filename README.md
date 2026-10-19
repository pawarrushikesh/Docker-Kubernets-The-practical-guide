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
