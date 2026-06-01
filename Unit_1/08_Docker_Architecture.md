# Docker Architecture & Container Lifecycle

![Docker](https://img.shields.io/badge/Docker-Architecture-blue)
![Containers](https://img.shields.io/badge/Containers-Lifecycle-green)
![DevOps](https://img.shields.io/badge/DevOps-Infrastructure-orange)
![Cloud](https://img.shields.io/badge/Cloud-Native-red)
![Linux](https://img.shields.io/badge/Linux-Containerization-purple)

---

# 📚 Table of Contents

- [Overview](#-overview)
- [What is Docker?](#-what-is-docker)
- [Docker Architecture](#-docker-architecture)
- [Main Components of Docker](#-main-components-of-docker)
- [Docker Client (CLI)](#-docker-client-cli)
- [Docker Daemon (dockerd)](#-docker-daemon-dockerd)
- [Docker Images](#-docker-images)
- [Docker Containers](#-docker-containers)
- [Docker Hub & Registries](#-docker-hub--registries)
- [How Docker Works](#-how-docker-works)
- [Docker Workflow Example](#-docker-workflow-example)
- [Docker Build, Ship, Run Model](#-docker-build-ship-run-model)
- [Container Lifecycle](#-container-lifecycle)
- [Docker Lifecycle Commands](#-docker-lifecycle-commands)
- [Docker Object Types](#-docker-object-types)
- [Docker vs Virtual Machines](#-docker-vs-virtual-machines)
- [Benefits of Docker Architecture](#-benefits-of-docker-architecture)
- [Real-World Docker Flow](#-real-world-docker-flow)
- [Quick Revision Notes](#-quick-revision-notes)
- [Viva Questions](#-viva-questions)
- [Interview Questions](#-interview-questions)
- [Conclusion](#-conclusion)

---

# 📖 Overview

Docker is the most popular containerization platform used in:
- DevOps
- Cloud Computing
- CI/CD pipelines
- Microservices
- Kubernetes

Docker architecture provides:
- Lightweight containers
- Fast deployment
- Portability
- Scalability

This topic explains:
- Docker architecture
- Docker components
- Container lifecycle
- Docker workflow
- Build-Ship-Run model

---

# 🐳 What is Docker?

> Docker is a containerization platform used to package, distribute, and run applications inside lightweight containers.

---

# Docker Provides

```text
✔ Application Packaging
✔ Environment Consistency
✔ Fast Deployment
✔ Scalability
✔ Portability
```

---

# Core Idea

```text
Build Once
      ↓
Run Anywhere
```

---

# 🏗️ Docker Architecture

Docker architecture follows:
- Client-server model

---

# High-Level Architecture

```text
Docker CLI (Client)
          ↓
Docker Daemon (dockerd)
          ↓
Docker Objects
(Images, Containers, Networks, Volumes)
          ↓
Docker Registry / Docker Hub
```

---

# Simplified Workflow

```text
Type Command
      ↓
CLI Sends Request
      ↓
Daemon Processes Request
      ↓
Docker Performs Action
```

---

# 🍔 Real-Life Analogy

Docker works like ordering food.

---

# Mapping

| Real World | Docker |
|---|---|
| Customer | Docker Client |
| Chef | Docker Daemon |
| Recipe | Docker Image |
| Food | Docker Container |

---

# Flow

```text
Customer places order
        ↓
Chef prepares food using recipe
        ↓
Food served
```

Docker works similarly.

---

# 🧩 Main Components of Docker

Docker has four major components.

---

# Components Overview

| Component | Purpose |
|---|---|
| Docker Client | User interface |
| Docker Daemon | Main engine |
| Docker Image | Read-only template |
| Docker Container | Running application |
| Docker Hub | Image registry |

---

# 💻 Docker Client (CLI)

The Docker Client is:
- command-line interface
- user interaction layer

---

# Common Commands

| Command | Purpose |
|---|---|
| docker run | Create + start container |
| docker ps | List containers |
| docker stop | Stop container |
| docker build | Build image |
| docker push | Upload image |
| docker pull | Download image |

---

# Example

```bash
docker run nginx
```

---

# What Happens?

```text
CLI sends request to Docker daemon
```

---

# 🔥 Docker Daemon (dockerd)

Docker Daemon is:
- background service
- Docker engine

---

# Main Responsibilities

```text
✔ Create containers
✔ Stop containers
✔ Build images
✔ Manage networking
✔ Manage storage
✔ Handle registries
```

---

# Daemon Workflow

```text
Docker CLI
      ↓
dockerd receives request
      ↓
Processes action
      ↓
Returns result
```

---

# Example

```bash
docker build .
```

---

# Daemon Tasks

```text
✔ Reads Dockerfile
✔ Builds layers
✔ Creates image
✔ Stores image locally
```

---

# 🖼️ Docker Images

Images are:
- read-only templates
- blueprints for containers

---

# Image Contains

```text
✔ Application code
✔ Runtime
✔ Dependencies
✔ Libraries
✔ Configuration
```

---

# Example

```text
python:3.11
nginx:latest
ubuntu:22.04
```

---

# Image Workflow

```text
Docker Image
      ↓
docker run
      ↓
Container Created
```

---

# 📦 Docker Containers

Containers are:
- running instances of images

---

# Example

```text
Image = Blueprint
Container = Running Application
```

---

# Properties

```text
✔ Lightweight
✔ Portable
✔ Isolated
✔ Fast startup
```

---

# Example Command

```bash
docker run nginx
```

---

# Result

```text
nginx container starts running
```

---

# 🌐 Docker Hub & Registries

Docker Hub is:
- default Docker registry

Used for:
- storing images
- sharing images
- downloading images

---

# Example

```bash
docker pull python:3.11
```

---

# Pull Process

```text
Docker contacts Docker Hub
        ↓
Downloads image layers
        ↓
Stores image locally
```

---

# Popular Registries

| Registry | Description |
|---|---|
| Docker Hub | Official registry |
| GHCR | GitHub registry |
| AWS ECR | Amazon registry |
| Azure ACR | Azure registry |

---

# ⚙️ How Docker Works

Docker follows:
- client-server architecture

---

# Step-by-Step Workflow

---

# Step 1️⃣ User Types Command

```bash
docker run nginx
```

---

# Step 2️⃣ Docker CLI Sends Request

CLI communicates with:
- Docker daemon

---

# Step 3️⃣ Daemon Checks Image

If image missing:

```text
Pull from Docker Hub
```

---

# Step 4️⃣ Daemon Creates Container

Docker:
- creates namespaces
- applies cgroups
- mounts filesystem

---

# Step 5️⃣ Container Starts

Application process begins execution.

---

# Final Result

```text
Running nginx container
```

---

# 🔄 Docker Workflow Example

---

# Command

```bash
docker run -p 8080:80 nginx
```

---

# Internal Workflow

```text
1. CLI receives command
2. CLI contacts daemon
3. Daemon checks image
4. Pulls image if missing
5. Creates container
6. Configures networking
7. Starts nginx process
8. Maps ports
9. Container running
```

---

# Visualization

```text
User
 ↓
Docker CLI
 ↓
Docker Daemon
 ↓
Docker Image
 ↓
Container Running
```

---

# 🚀 Docker Build, Ship, Run Model

Docker follows:
- Build
- Ship
- Run

---

# 1️⃣ BUILD

Create image.

---

# Command

```bash
docker build -t myapp:v1 .
```

---

# Result

```text
Application packaged into image
```

---

# 2️⃣ SHIP

Upload image to registry.

---

# Command

```bash
docker push myapp:v1
```

---

# Result

```text
Image available globally
```

---

# 3️⃣ RUN

Start container from image.

---

# Command

```bash
docker run myapp:v1
```

---

# Result

```text
Application running
```

---

# Full Workflow

```text
Build Image
      ↓
Push to Registry
      ↓
Pull Anywhere
      ↓
Run Container
```

---

# 🔄 Container Lifecycle

Containers move through multiple states.

---

# Lifecycle Stages

```text
Created
   ↓
Running
   ↓
Paused
   ↓
Stopped
   ↓
Removed
```

---

# 1️⃣ Created State

Container exists but not running.

---

# Command

```bash
docker create nginx
```

---

# Result

```text
Container ready to start
```

---

# 2️⃣ Running State

Container actively executing.

---

# Command

```bash
docker start <container-id>
```

---

# Example

```bash
docker start mycontainer
```

---

# 3️⃣ Paused State

Container execution temporarily suspended.

---

# Commands

```bash
docker pause mycontainer
docker unpause mycontainer
```

---

# Result

```text
Processes frozen temporarily
```

---

# 4️⃣ Stopped State

Container execution stopped.

---

# Command

```bash
docker stop mycontainer
```

---

# Result

```text
Container preserved but inactive
```

---

# 5️⃣ Removed State

Container deleted permanently.

---

# Command

```bash
docker rm mycontainer
```

---

# Result

```text
Container removed from system
```

---

# 📊 Lifecycle Diagram

```text
docker create
      ↓
Created
      ↓
docker start
      ↓
Running
      ↓
docker pause
      ↓
Paused
      ↓
docker unpause
      ↓
Running
      ↓
docker stop
      ↓
Stopped
      ↓
docker rm
      ↓
Removed
```

---

# ⚙️ Docker Lifecycle Commands

| Command | Purpose |
|---|---|
| docker create | Create container |
| docker start | Start container |
| docker run | Create + start |
| docker pause | Pause execution |
| docker unpause | Resume execution |
| docker stop | Stop container |
| docker restart | Restart container |
| docker rm | Remove container |

---

# 🧩 Docker Object Types

Docker manages different object types.

---

# Docker Objects

| Object | Purpose |
|---|---|
| Image | Blueprint |
| Container | Running app |
| Network | Communication |
| Volume | Persistent storage |

---

# Example

```text
Image → Template
Container → Runtime
Volume → Persistent data
Network → Container communication
```

---

# ⚔️ Docker vs Virtual Machines

| Feature | Docker | Virtual Machines |
|---|---|---|
| OS | Shared kernel | Separate guest OS |
| Startup Time | Seconds | Minutes |
| Size | MBs | GBs |
| Resource Usage | Low | High |
| Scalability | Excellent | Limited |
| Performance | Near-native | Higher overhead |

---

# Example

```text
100+ containers
vs
10 VMs
on same hardware
```

---

# 🌟 Benefits of Docker Architecture

| Benefit | Description |
|---|---|
| Lightweight | Minimal overhead |
| Fast Deployment | Seconds to start |
| Portability | Same everywhere |
| Isolation | Independent environments |
| Scalability | Easy replication |
| Efficiency | Shared kernel |

---

# 🌍 Real-World Docker Flow

---

# Development

```bash
docker build -t app:v1 .
```

---

# Push to Registry

```bash
docker push ghcr.io/company/app:v1
```

---

# Production Deployment

```bash
docker run ghcr.io/company/app:v1
```

---

# Result

```text
Same application everywhere
```

---

# 📌 Quick Revision Notes

| Topic | Key Point |
|---|---|
| Docker Client | CLI interface |
| Docker Daemon | Main engine |
| Image | Read-only template |
| Container | Running instance |
| Docker Hub | Image registry |
| Build | Create image |
| Ship | Push image |
| Run | Start container |
| Lifecycle | Created → Running → Removed |

---

# 🧠 Important Keywords

- Docker
- Docker Daemon
- Docker CLI
- Images
- Containers
- Docker Hub
- Build
- Ship
- Run
- Container Lifecycle

---

# ❓ Viva Questions

1. What is Docker?
2. Explain Docker architecture.
3. What is Docker daemon?
4. What is Docker CLI?
5. Difference between image and container?
6. What is Docker Hub?
7. Explain Build-Ship-Run model.
8. What is container lifecycle?
9. What happens during docker run?
10. Why is Docker lightweight?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| What is dockerd? | Docker background service |
| Difference between create and run? | run = create + start |
| What is Docker Hub? | Image registry |
| Why are containers lightweight? | Shared kernel |
| What happens during docker build? | Image layers created |

---

# 📌 Key Takeaway

Docker architecture consists of:

```text
Docker CLI
      ↓
Docker Daemon
      ↓
Images
      ↓
Containers
      ↓
Registries
```

Docker enables:
- fast deployment
- portability
- scalability
- efficient container management

Container lifecycle allows containers to move through:

```text
Created → Running → Paused → Stopped → Removed
```

Docker forms the foundation of:
- DevOps
- CI/CD
- Kubernetes
- Cloud-native infrastructure

---

# ✅ Conclusion

Docker architecture simplifies application deployment through:
- client-server model
- lightweight containers
- reusable images
- centralized registries

Docker lifecycle management enables:
- efficient container execution
- scalability
- automation
- rapid deployment

Docker revolutionized modern software infrastructure by making applications:
- portable
- scalable
- lightweight
- cloud-ready

---

# 🔗 Next Topic

➡️ Basic Commands