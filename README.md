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
