# Docker Storage, Volumes & Bind Mounts

![Docker](https://img.shields.io/badge/Docker-Storage-blue)
![Volumes](https://img.shields.io/badge/Volumes-Persistence-green)
![Containers](https://img.shields.io/badge/Containers-Data-orange)
![DevOps](https://img.shields.io/badge/DevOps-StatefulApps-red)

---

# 📚 Table of Contents

- Introduction
- Problem with Containers
- What is Persistent Storage?
- Docker Storage Types
- Volumes
- Bind Mounts
- Volumes vs Bind Mounts
- Copy-on-Write (CoW)
- Volume Commands
- Bind Mount Examples
- Data Persistence
- Multi-Container Shared Storage
- Volume Drivers
- Best Practices
- Practical Labs
- Summary

---

# 📖 Introduction

By default:
- containers are temporary (ephemeral)

When a container is deleted:
- its internal data is lost

Docker storage mechanisms solve this problem using:
- Volumes
- Bind Mounts

---

# ⚠️ Problem with Containers

Example:

```bash
docker run -it ubuntu bash
```

Inside container:

```bash
echo "Important Data" > /data/file.txt
```

Exit and remove container:

```bash
docker rm <container_id>
```

---

# Result

```text
❌ file.txt lost forever
❌ Container data deleted
❌ No persistence
```

---

# Real-World Problem

Database container stores data:

```text
/var/lib/mysql
```

If container crashes or removed:
- all data lost

This is unacceptable for:
- production systems
- databases
- user uploads

---

# ✅ Solution — Persistent Storage

Store data:
- outside container

Docker provides:
1. Volumes
2. Bind Mounts

---

# 🧠 Docker Storage Types

| Storage Type | Managed By |
|---|---|
| Volumes | Docker |
| Bind Mounts | User/Host |
| tmpfs | Memory only |

---

# 📦 Docker Volumes

## What is a Volume?

> Volume is Docker-managed persistent storage outside the container filesystem.

---

# Volume Workflow

```text
Container Path
      ↓
Docker Volume
      ↓
Host Storage
```

---

# Example

```text
/app/data
      ↓
myvolume
      ↓
/var/lib/docker/volumes/
```

---

# Benefits of Volumes

```text
✔ Persistent storage
✔ Survives container deletion
✔ Easy backup
✔ Shareable between containers
✔ Production-ready
✔ Cross-platform support
```

---

# 🛠️ Volume Commands

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

# 🚀 Using Volume with Container

---

# Syntax

```bash
docker run -v volume_name:/container/path image
```

---

# Example

```bash
docker run -d \
  -v myvolume:/app/data \
  nginx
```

---

# Result

```text
✔ Data stored outside container
✔ Data survives deletion
✔ Persistent storage enabled
```

---

# 🌟 Volume Persistence Example

---

# Step 1: Create Volume

```bash
docker volume create projectdata
```

---

# Step 2: Run Container

```bash
docker run -dit \
  --name project_container \
  -v projectdata:/app/data \
  ubuntu
```

---

# Step 3: Create File

```bash
docker exec -it project_container bash
```

Inside:

```bash
echo "Hello Volume" > /app/data/report.txt
```

---

# Step 4: Remove Container

```bash
docker rm -f project_container
```

---

# Step 5: Create New Container

```bash
docker run -dit \
  --name project_container_new \
  -v projectdata:/app/data \
  ubuntu
```

---

# Step 6: Verify Data

```bash
docker exec -it project_container_new cat /app/data/report.txt
```

---

# Output

```text
Hello Volume
```

---

# Result

```text
✅ Data persisted successfully
```

---

# 🔗 Sharing Volumes Between Containers

Multiple containers can share:
- same volume

---

# Example

## Create Shared Volume

```bash
docker volume create shared_data
```

---

# Writer Container

```bash
docker run -it \
  --name writer \
  -v shared_data:/shared \
  ubuntu
```

Inside:

```bash
echo "Hello from writer" > /shared/message.txt
```

---

# Reader Container

```bash
docker run -it \
  --name reader \
  -v shared_data:/shared \
  ubuntu
```

Inside:

```bash
cat /shared/message.txt
```

---

# Result

```text
✔ Shared storage
✔ Real-time data access
```

---

# 📂 Bind Mounts

## What is Bind Mount?

> Bind mount maps host directory directly into container.

---

# Workflow

```text
Host Directory
      ↓
Container Directory
```

---

# Example

```text
/home/user/project
        ↓
/app
```

---

# Benefits

```text
✔ Direct host access
✔ Instant file synchronization
✔ Great for development
✔ Easy configuration management
```

---

# Syntax

```bash
docker run -v /host/path:/container/path image
```

---

# Linux/Mac Example

```bash
docker run -d \
  -v $(pwd):/app \
  nginx
```

---

# Windows Example

```bash
docker run -d \
  -v C:\app\data:/app \
  nginx
```

---

# 🔄 Bind Mount Development Workflow

---

# Create Project

```bash
mkdir myapp
```

---

# Create app.js

```bash
echo "console.log('Hello Docker');" > app.js
```

---

# Run Container

```bash
docker run -d \
  -v $(pwd):/app \
  node:18 \
  node /app/app.js
```

---

# Edit File on Host

```bash
echo "console.log('Updated');" > app.js
```

---

# Result

```text
✔ Changes instantly visible
✔ No rebuild required
✔ Fast development cycle
```

---

# 📊 Volumes vs Bind Mounts

| Feature | Volumes | Bind Mounts |
|---|---|---|
| Managed By | Docker | User |
| Persistence | Yes | Yes |
| Portability | Excellent | Limited |
| Best Use | Production | Development |
| Backup | Easy | Manual |
| Performance | Better | Depends |
| Storage Path | Docker-managed | Host-defined |

---

# 🌟 Use Cases

---

# Use Volumes When

```text
✔ Databases
✔ Production apps
✔ Persistent storage
✔ Shared container data
✔ Docker-managed storage
```

---

# Use Bind Mounts When

```text
✔ Development
✔ Live code editing
✔ Config files
✔ Log access
✔ Local testing
```

---

# 🔄 Copy-on-Write (CoW)

Docker images use:
- layered filesystem

Container changes stored in:
- writable layer

---

# Problem

Writable layer is:
- temporary

Deleted when container removed.

---

# Solution

Volumes bypass:
- Copy-on-Write layer

Data written directly to:
- persistent storage

---

# Workflow

```text
Container
    ↓
Volume
    ↓
Host Storage
```

---

# 📦 Volume Drivers

Docker supports:
- different storage drivers

---

# Common Drivers

| Driver | Purpose |
|---|---|
| local | Default storage |
| nfs | Network filesystem |
| aws | AWS storage |
| azure | Azure storage |

---

# Example

```bash
docker volume create -d local myvolume
```

---

# 🛠️ Practical Example — MySQL Persistence

---

# Create Volume

```bash
docker volume create mysql_data
```

---

# Run MySQL Container

```bash
docker run -d \
  --name mysql_db \
  -e MYSQL_ROOT_PASSWORD=root123 \
  -v mysql_data:/var/lib/mysql \
  mysql:8
```

---

# Result

```text
✔ Database survives container deletion
✔ Persistent MySQL storage
✔ Production-ready setup
```

---

# 🌍 Multi-Container Example

---

# Create Network

```bash
docker network create app_net
```

---

# Create Volumes

```bash
docker volume create db_data

docker volume create app_data
```

---

# Run Database

```bash
docker run -d \
  --name database \
  --network app_net \
  -v db_data:/var/lib/mysql \
  mysql:8
```

---

# Run Application

```bash
docker run -d \
  --name app \
  --network app_net \
  -v app_data:/app/data \
  myapp:v1
```

---

# Result

```text
✔ Persistent data
✔ Network communication
✔ Scalable architecture
```

---

# 🔐 Best Practices

---

# Use Volumes for Production

```text
✔ Databases
✔ Stateful services
✔ User uploads
```

---

# Use Bind Mounts for Development

```text
✔ Live coding
✔ Config editing
✔ Local debugging
```

---

# Backup Important Volumes

```bash
tar -czf backup.tar.gz /var/lib/docker/volumes/
```

---

# Use Read-Only Mounts When Possible

```bash
-v /host/path:/container/path:ro
```

---

# Use Descriptive Volume Names

✅ Good

```text
mysql_data
postgres_backup
```

❌ Bad

```text
vol1
data2
```

---

# 📌 Quick Revision Notes

| Concept | Meaning |
|---|---|
| Volume | Docker-managed storage |
| Bind Mount | Host-managed storage |
| CoW | Copy-on-Write |
| Persistent Storage | Data survives deletion |
| Shared Volume | Multiple container access |

---

# 🧠 Important Keywords

- Docker Volumes
- Bind Mounts
- Persistent Storage
- Copy-on-Write
- OverlayFS
- Volume Drivers
- Shared Storage
- Stateful Containers

---

# ❓ Viva Questions

1. Why do containers need storage?
2. What is Docker volume?
3. What is bind mount?
4. Difference between volume and bind mount?
5. What is persistent storage?
6. What is Copy-on-Write?
7. Why use volumes for databases?
8. What are volume drivers?
9. How to share storage between containers?
10. Why are containers ephemeral?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| Why use Docker volumes? | Persistent storage |
| Difference between volume and bind mount? | Docker-managed vs host-managed |
| What is Copy-on-Write? | Writable layer mechanism |
| Best storage for production? | Volumes |
| Best storage for development? | Bind mounts |

---

# ✅ Conclusion

Docker storage mechanisms solve:
- temporary container storage issues

Using:
- Volumes
- Bind Mounts
- Persistent storage

Docker supports:
- databases
- production systems
- development workflows
- scalable stateful applications

Understanding storage is essential for:
- Docker Compose
- Kubernetes
- DevOps infrastructure
- cloud-native deployments