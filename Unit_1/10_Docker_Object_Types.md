# Docker Object Types & Docker Filesystem Layering

![Docker](https://img.shields.io/badge/Docker-Objects-blue)
![Containers](https://img.shields.io/badge/Containers-Layers-green)
![DevOps](https://img.shields.io/badge/DevOps-Infrastructure-orange)
![Linux](https://img.shields.io/badge/Linux-OverlayFS-red)
![Storage](https://img.shields.io/badge/Storage-Volumes-purple)

---

# 📚 Table of Contents

- [Overview](#-overview)
- [Docker Object Types](#-docker-object-types)
- [Docker Images](#-docker-images)
- [Docker Containers](#-docker-containers)
- [Docker Networks](#-docker-networks)
- [Docker Volumes](#-docker-volumes)
- [Image Commands](#-image-commands)
- [Container Commands](#-container-commands)
- [Container Interaction Commands](#-container-interaction-commands)
- [Network Commands](#-network-commands)
- [Volume Commands](#-volume-commands)
- [Docker Layering & Filesystem](#-docker-layering--filesystem)
- [OverlayFS (Union Filesystem)](#-overlayfs-union-filesystem)
- [Copy-on-Write-cow](#-copy-on-write-cow)
- [Docker Storage Drivers](#-docker-storage-drivers)
- [Layer Sharing](#-layer-sharing)
- [Practical Examples](#-practical-examples)
- [Quick Revision Notes](#-quick-revision-notes)
- [Viva Questions](#-viva-questions)
- [Interview Questions](#-interview-questions)
- [Conclusion](#-conclusion)

---

# 📖 Overview

Docker manages applications using four core object types:

```text
✔ Images
✔ Containers
✔ Networks
✔ Volumes
```

These objects work together to provide:
- containerization
- networking
- persistent storage
- scalability
- portability

Docker also uses:
- layered filesystem architecture
- OverlayFS
- Copy-on-Write (CoW)

to improve:
- storage efficiency
- build speed
- performance

---

# 🧩 Docker Object Types

Docker provides four major object types.

---

# Docker Objects

| Object | Purpose |
|---|---|
| Image | Read-only template |
| Container | Running instance |
| Network | Communication layer |
| Volume | Persistent storage |

---

# Relationship

```text
Image
   ↓
Container
   ↓
Network + Volume
```

---

# 🖼️ Docker Images

---

# What is an Image?

> A Docker Image is a read-only blueprint/template used to create containers.

---

# Characteristics

```text
✔ Immutable
✔ Layered
✔ Portable
✔ Reusable
✔ Read-only
```

---

# Image Contains

```text
✔ Operating system files
✔ Runtime
✔ Dependencies
✔ Application code
✔ Configuration
```

---

# Example

```text
nginx
ubuntu
python:3.11
mysql:8
```

---

# Multiple Containers from One Image

```text
One Image
    ↓
Many Containers
```

---

# Example

```bash
docker run nginx
docker run nginx
docker run nginx
```

All containers share same image layers.

---

# 📦 Docker Containers

---

# What is a Container?

> A Container is a running (or stopped) instance of an image.

---

# Characteristics

```text
✔ Lightweight
✔ Isolated
✔ Portable
✔ Writable layer
✔ Ephemeral by default
```

---

# Isolation Technologies

Containers use:
- namespaces → isolation
- cgroups → resource control

---

# Example

```bash
docker run -d nginx
```

---

# Result

```text
nginx container running
```

---

# Writable Layer

Each container gets:
- its own writable layer

---

# Example

```text
Shared Image Layers
        +
Container Writable Layer
```

---

# Container States

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

# 🌐 Docker Networks

---

# What is a Network?

> Docker Network is a communication channel that allows containers to communicate with each other and external systems.

---

# Purpose

```text
✔ Container-to-container communication
✔ Internet access
✔ Port exposure
✔ Isolation
```

---

# Default Docker Networks

| Network | Purpose |
|---|---|
| bridge | Default isolated network |
| host | Shares host network |
| none | No networking |

---

# Bridge Network

Default network.

---

# Example

```text
Container A ↔ Container B
```

through:
- virtual bridge

---

# Host Network

Container shares:
- host networking stack

---

# Benefits

```text
✔ Better performance
✔ No NAT overhead
```

---

# Limitation

```text
Less isolation
```

---

# None Network

Container has:
- no network access

---

# Use Case

```text
Highly isolated workloads
```

---

# 🌟 Custom Networks

Custom networks improve:
- service discovery
- isolation
- communication

---

# Example

```bash
docker network create mynetwork
```

---

# Run with Custom Network

```bash
docker run -d --network mynetwork nginx
```

---

# 💾 Docker Volumes

---

# What is a Volume?

> Docker Volume is persistent storage managed by Docker outside container lifecycle.

---

# Why Needed?

Containers are:
- ephemeral

When deleted:
- internal data lost.

Volumes solve this problem.

---

# Benefits

```text
✔ Persistent storage
✔ Shared storage
✔ Backup friendly
✔ Independent of containers
```

---

# Example

```bash
docker volume create myvolume
```

---

# Use with Container

```bash
docker run -d -v myvolume:/app/data ubuntu
```

---

# Result

```text
Data persists even after container deletion
```

---

# 📥 Image Commands

---

# List Images

```bash
docker images
```

---

# Pull Image

```bash
docker pull nginx
```

---

# Remove Image

```bash
docker rmi nginx
```

---

# Inspect Image

```bash
docker inspect nginx
```

---

# View Image History

```bash
docker history nginx
```

---

# Shows

```text
✔ Image layers
✔ Build history
✔ Layer sizes
```

---

# 📦 Container Commands

---

# Create + Start Container

```bash
docker run -d --name myapp nginx
```

---

# List Running Containers

```bash
docker ps
```

---

# List All Containers

```bash
docker ps -a
```

---

# Stop Container

```bash
docker stop myapp
```

---

# Start Container

```bash
docker start myapp
```

---

# Remove Container

```bash
docker rm myapp
```

---

# Inspect Container

```bash
docker inspect myapp
```

---

# View Logs

```bash
docker logs myapp
```

---

# Follow Logs Live

```bash
docker logs -f myapp
```

---

# Monitor Resource Usage

```bash
docker stats myapp
```

---

# View Running Processes

```bash
docker top myapp
```

---

# 🔍 Container Interaction Commands

---

# Open Terminal Inside Container

```bash
docker exec -it <id> bash
```

---

# Example

```bash
docker exec -it myapp bash
```

---

# Attach to Main Process

```bash
docker attach <id>
```

---

# Copy File from Container

```bash
docker cp <id>:/path ~/Desktop/
```

---

# Copy File into Container

```bash
docker cp ~/Desktop/file <id>:/path
```

---

# Force Stop Container

```bash
docker kill <id>
```

---

# Remove All Stopped Containers

```bash
docker container prune
```

---

# 🌐 Network Commands

---

# List Networks

```bash
docker network ls
```

---

# Create Network

```bash
docker network create mynetwork
```

---

# Inspect Network

```bash
docker network inspect mynetwork
```

---

# Remove Network

```bash
docker network rm mynetwork
```

---

# Connect Container to Network

```bash
docker network connect mynetwork myapp
```

---

# Disconnect Container

```bash
docker network disconnect mynetwork myapp
```

---

# Run Container with Network

```bash
docker run -d --network mynetwork nginx
```

---

# 💾 Volume Commands

---

# Create Volume

```bash
docker volume create myvolume
```

---

# List Volumes

```bash
docker volume ls
```

---

# Inspect Volume

```bash
docker volume inspect myvolume
```

---

# Remove Volume

```bash
docker volume rm myvolume
```

---

# Remove Unused Volumes

```bash
docker volume prune
```

---

# Use Volume with Container

```bash
docker run -d -v myvolume:/app/data ubuntu
```

---

# 🏗️ Docker Layering & Filesystem

Docker uses:
- layered filesystem architecture

based on:
- OverlayFS (Union Filesystem)

---

# Layer Structure

```text
Top Layer → Writable Container Layer
Middle → App + Dependencies
Bottom → Base OS Layer
```

---

# Example

```text
Layer 1 → Ubuntu
Layer 2 → Python
Layer 3 → Flask
Layer 4 → App Code
Layer 5 → Writable Layer
```

---

# Benefits

```text
✔ Efficient storage
✔ Faster builds
✔ Layer sharing
✔ Faster distribution
```

---

# 🌟 OverlayFS (Union Filesystem)

OverlayFS stacks:
- multiple read-only layers
- one writable layer

into:
- single unified filesystem

---

# Visualization

```text
Writable Layer
      ↑
Read-only Layers
      ↑
Base OS Layer
```

---

# Benefits

```text
✔ Shared layers
✔ Efficient storage
✔ Faster startup
```

---

# 🔄 Copy-on-Write (CoW)

Docker uses:
- Copy-on-Write mechanism

---

# Core Idea

Containers share:
- read-only image layers

When modified:
- file copied to writable layer.

---

# Workflow

---

# Step 1

Container accesses file.

---

# Step 2

File exists in image layer.

---

# Step 3

Container modifies file.

---

# Step 4

Docker copies file into writable layer.

---

# Step 5

Modified version used.

---

# Result

```text
Original image layers untouched
```

---

# Example

```text
Shared nginx image
       ↓
Container A modifies config
       ↓
Config copied to A writable layer
```

Other containers unaffected.

---

# 🌍 Layer Sharing

Multiple containers share:
- same image layers

---

# Example

```text
10 nginx containers
       ↓
One copy of nginx layers stored
```

---

# Result

```text
✔ Massive storage savings
✔ Faster startup
✔ Better efficiency
```

---

# 🔍 View Docker Layers

---

# View Image Layers

```bash
docker history nginx
```

---

# Check Storage Driver

```bash
docker info | grep "Storage Driver"
```

---

# Example Output

```text
Storage Driver: overlay2
```

---

# 📊 Docker Storage Drivers

| Driver | Description |
|---|---|
| overlay2 | Modern default driver |
| aufs | Older layered filesystem |
| btrfs | Advanced filesystem |
| zfs | Enterprise filesystem |

---

# Most Common Driver

```text
overlay2
```

Used in:
- Docker Desktop
- Linux Docker installations

---

# 🌍 Practical Examples

---

# Example 1: Run Container with Network

```bash
docker network create appnet

docker run -d \
--network appnet \
--name frontend nginx
```

---

# Example 2: Run Container with Volume

```bash
docker volume create appdata

docker run -d \
-v appdata:/var/lib/mysql \
mysql:8
```

---

# Example 3: View Layer History

```bash
docker history nginx
```

---

# Example 4: Interactive Container

```bash
docker exec -it myapp bash
```

---

# 📌 Quick Revision Notes

| Topic | Key Point |
|---|---|
| Image | Read-only template |
| Container | Running instance |
| Network | Communication |
| Volume | Persistent storage |
| OverlayFS | Layered filesystem |
| CoW | Copy-on-Write |
| Writable Layer | Container changes |
| overlay2 | Default storage driver |

---

# 🧠 Important Keywords

- Docker Image
- Docker Container
- Docker Network
- Docker Volume
- OverlayFS
- Copy-on-Write
- Storage Driver
- Writable Layer
- Layer Sharing
- Container Filesystem

---

# ❓ Viva Questions

1. What are Docker object types?
2. Difference between image and container?
3. What is Docker volume?
4. What is Docker network?
5. What is OverlayFS?
6. What is Copy-on-Write?
7. Why are image layers important?
8. What is writable layer?
9. What is overlay2?
10. Why use volumes?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| Why are containers lightweight? | Shared image layers |
| What is Copy-on-Write? | Modified files copied to writable layer |
| Why use Docker volumes? | Persistent storage |
| What is OverlayFS? | Layered filesystem |
| Difference between volume and bind mount? | Docker-managed vs host path |

---

# 📌 Key Takeaway

Docker uses four major object types:

```text
✔ Images
✔ Containers
✔ Networks
✔ Volumes
```

Docker layering provides:

```text
✔ Efficient storage
✔ Shared layers
✔ Fast startup
✔ Faster builds
✔ Better scalability
```

OverlayFS and Copy-on-Write are core technologies behind:
- Docker performance
- storage optimization
- container efficiency

---

# ✅ Conclusion

Docker object types work together to create:
- scalable
- portable
- efficient containerized applications

Docker layering architecture using:
- OverlayFS
- Copy-on-Write

enables:
- efficient storage
- fast builds
- lightweight containers
- optimized resource usage

These concepts form the foundation of:
- Docker
- Kubernetes
- modern cloud-native infrastructure

---

# 🔗 Next Topic

➡️ Container Interaction