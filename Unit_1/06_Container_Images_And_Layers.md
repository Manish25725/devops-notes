# Container Images & Docker Layering

![Docker](https://img.shields.io/badge/Docker-Images-blue)
![Containers](https://img.shields.io/badge/Containers-Layers-green)
![Linux](https://img.shields.io/badge/Linux-Filesystem-orange)
![DevOps](https://img.shields.io/badge/DevOps-Infrastructure-red)
![Cloud](https://img.shields.io/badge/Cloud-Native-purple)

---

# 📚 Table of Contents

- [Overview](#-overview)
- [What is a Container Image?](#-what-is-a-container-image)
- [Image vs Container](#-image-vs-container)
- [Image Naming Convention](#-image-naming-convention)
- [Understanding Image Tags](#-understanding-image-tags)
- [Container Registries](#-container-registries)
- [Public vs Private Images](#-public-vs-private-images)
- [What are Docker Layers?](#-what-are-docker-layers)
- [How Docker Layers Work](#-how-docker-layers-work)
- [Dockerfile and Layers](#-dockerfile-and-layers)
- [Benefits of Docker Layers](#-benefits-of-docker-layers)
- [Container Writable Layer](#-container-writable-layer)
- [Copy-on-Write (CoW)](#-copy-on-write-cow)
- [Layer Caching](#-layer-caching)
- [Image Distribution](#-image-distribution)
- [Base Images and Inheritance](#-base-images-and-inheritance)
- [Real-World Dockerfile Example](#-real-world-dockerfile-example)
- [Image Optimization Best Practices](#-image-optimization-best-practices)
- [Quick Revision Notes](#-quick-revision-notes)
- [Viva Questions](#-viva-questions)
- [Interview Questions](#-interview-questions)
- [Conclusion](#-conclusion)

---

# 📖 Overview

Containers run using:
- Container Images
- Docker Layers

Images act as:
- Templates
- Blueprints

Docker layering provides:
- Efficient storage
- Faster builds
- Reusable components
- Better portability

This topic explains:
- Images
- Containers
- Docker layering
- Copy-on-write mechanism
- Registries
- Image distribution

---

# 🧠 What is a Container Image?

> A Container Image is a read-only template containing everything required to run an application.

---

# Image Contains

```text
✔ Base Operating System
✔ Runtime Environment
✔ Libraries
✔ Dependencies
✔ Application Code
✔ Configuration Files
```

---

# Example

```text
python:3.11-slim
```

Contains:
- Lightweight Linux
- Python 3.11
- pip package manager

---

# Core Idea

```text
Image = Blueprint
Container = Running Instance
```

---

# ⚔️ Image vs Container

| Feature | Image | Container |
|---|---|---|
| Nature | Read-only | Writable |
| State | Static | Running |
| Purpose | Template | Execution |
| Storage | Stored on disk | Temporary runtime |
| Reusability | Reusable | Temporary |

---

# Example

```text
One Image
    ↓
Multiple Containers
```

---

# Workflow

```text
Docker Image
      ↓
Docker Run
      ↓
Container Created
```

---

# Example

```bash
docker run python:3.11
```

---

# Result

```text
Docker creates container from image
```

---

# 🏷️ Image Naming Convention

Full image format:

```text
registry/namespace/image:tag
```

---

# Example

```text
docker.io/library/python:3.11
```

---

# Components

| Part | Meaning |
|---|---|
| registry | docker.io |
| namespace | library |
| image | python |
| tag | 3.11 |

---

# Another Example

```text
ghcr.io/komaljoshi/myapp:v1.0
```

---

# Components

| Part | Meaning |
|---|---|
| registry | ghcr.io |
| namespace | komaljoshi |
| image | myapp |
| tag | v1.0 |

---

# Short Form

Usually written as:

```text
python:3.11
```

Docker automatically assumes:
- registry → docker.io
- namespace → library

---

# 🏷️ Understanding Image Tags

Tags identify:
- Versions
- Environments
- Architectures

---

# Common Tags

| Tag | Purpose |
|---|---|
| latest | Latest version |
| v1.0 | Version number |
| prod | Production image |
| dev | Development image |
| arm64 | ARM architecture |

---

# Examples

```text
myapp:latest
myapp:v1.0
myapp:prod-v2
myapp:1.0-arm64
```

---

# 🌐 Container Registries

Images are stored in:
- Registries

---

# Popular Registries

| Registry | Description |
|---|---|
| Docker Hub | Default public registry |
| GHCR | GitHub Container Registry |
| GCR | Google Container Registry |
| AWS ECR | Amazon Elastic Container Registry |
| Azure ACR | Azure Container Registry |

---

# Registry Workflow

```text
Build Image
      ↓
Push to Registry
      ↓
Pull from Registry
      ↓
Run Container
```

---

# 🌍 Public vs Private Images

| Type | Access |
|---|---|
| Public | Anyone can pull |
| Private | Requires authentication |

---

# Public Example

```text
docker.io/library/nginx
```

---

# Private Example

```text
ghcr.io/company/private-app
```

---

# 🧩 What are Docker Layers?

Docker images are built using:
- Layers

Each layer is:
- Immutable
- Read-only
- Filesystem snapshot

---

# Example Layer Structure

```text
Layer 4 → Application Code
Layer 3 → Python Libraries
Layer 2 → Python Runtime
Layer 1 → Base Linux OS
```

---

# Important Idea

```text
Docker Image = Stack of Layers
```

---

# 🏗️ How Docker Layers Work

Each instruction in Dockerfile creates a layer.

---

# Example Dockerfile

```dockerfile
FROM python:3.11-slim
RUN pip install flask
COPY app.py /app/
WORKDIR /app
CMD ["python", "app.py"]
```

---

# Layers Created

| Dockerfile Instruction | Layer |
|---|---|
| FROM | Base image layer |
| RUN | Dependency layer |
| COPY | Application code layer |
| WORKDIR | Metadata layer |
| CMD | Metadata layer |

---

# Visualization

```text
Layer 5 → CMD
Layer 4 → WORKDIR
Layer 3 → Application Code
Layer 2 → Flask Installed
Layer 1 → Python Base Image
```

---

# 🌟 Benefits of Docker Layers

---

# 1️⃣ Immutability

Once created:
- layers never change.

---

# Benefits

```text
✔ Predictable builds
✔ Reproducibility
✔ Reliability
```

---

# 2️⃣ Layer Caching

Docker reuses unchanged layers.

---

# Example

```text
Only app code changed
        ↓
Dependencies layer reused
```

---

# Result

```text
✔ Faster builds
✔ Less computation
```

---

# 3️⃣ Layer Sharing

Multiple images share same layers.

---

# Example

```text
100 Python apps
        ↓
Share same Python base layer
```

---

# Result

```text
✔ Massive storage savings
```

---

# 4️⃣ Efficient Distribution

Only changed layers are transferred.

---

# Result

```text
✔ Faster push/pull
✔ Lower bandwidth usage
```

---

# 💾 Container Writable Layer

Images are read-only.

When container starts:

```text
Docker Image Layers
        +
Writable Container Layer
```

---

# Example

```text
Image Layer → Shared
Writable Layer → Unique per container
```

---

# Benefits

```text
✔ Image remains unchanged
✔ Containers isolated
✔ Temporary modifications allowed
```

---

# Example Scenario

Running 5 containers:

```text
Shared Image Layers → 600MB
Writable Layers → 5 × 10MB
Total → 650MB
```

Without sharing:

```text
5 × 600MB = 3000MB+
```

---

# Result

```text
✔ Huge storage savings
```

---

# 🔄 Copy-on-Write (CoW)

Docker uses:
- Copy-on-Write mechanism

---

# How It Works

When container modifies a file:

---

# Step 1

Original file exists in read-only image layer.

---

# Step 2

Container modifies file.

---

# Step 3

Docker copies file into writable layer.

---

# Step 4

Container uses modified copy.

---

# Example

```text
Image File → /etc/config
        ↓
Container modifies file
        ↓
Copied to writable layer
```

---

# Result

```text
✔ Efficient storage
✔ Image protection
✔ Isolation
```

---

# ⚡ Layer Caching

Docker caches layers for faster builds.

---

# Example

```dockerfile
COPY package.json .
RUN npm install
COPY . .
```

---

# Why Efficient?

If source code changes:
- npm install layer reused.

---

# Result

```text
✔ Faster rebuilds
✔ Reduced build time
```

---

# 🌐 Image Distribution

Images are distributed layer-by-layer.

---

# Example

Image v1:

```text
Layer A
Layer B
Layer C
```

Image v2:

```text
Layer A
Layer B
Layer C
Layer D
```

---

# Push Process

Only:
- Layer D uploaded.

---

# Benefits

```text
✔ Faster pushes
✔ Lower bandwidth
✔ Efficient updates
```

---

# 🏗️ Base Images and Inheritance

Images inherit from base images.

---

# Examples

```dockerfile
FROM ubuntu:22.04
FROM python:3.11
FROM node:18-alpine
```

---

# Inheritance Example

```text
Ubuntu Base
      ↓
Python Installed
      ↓
Application Added
```

---

# Result

```text
✔ Reusable infrastructure
✔ Simplified builds
```

---

# 🌍 Real-World Dockerfile Example

---

# Example

```dockerfile
FROM node:18-alpine

RUN npm install -g pm2

COPY package.json /app/

RUN npm install

COPY src/ /app/src/

ENV NODE_ENV=production

EXPOSE 3000

CMD ["npm", "start"]
```

---

# Layers Created

| Layer | Purpose |
|---|---|
| node:18-alpine | Base image |
| pm2 installation | Process manager |
| package.json | Dependency config |
| npm install | Install packages |
| source code | Application |
| ENV | Environment metadata |
| EXPOSE | Port metadata |
| CMD | Startup command |

---

# Final Image

```text
Contains:
✔ Linux
✔ Node.js
✔ npm packages
✔ Application code
✔ Environment config
```

---

# 🚀 Image Optimization Best Practices

---

# 1️⃣ Use Lightweight Base Images

---

# Good

```dockerfile
FROM alpine
```

---

# Bad

```dockerfile
FROM ubuntu
```

---

# Benefits

```text
✔ Smaller image
✔ Faster pull
✔ Better security
```

---

# 2️⃣ Use Multi-Stage Builds

---

# Example

```dockerfile
FROM node:18 AS build

RUN npm run build

FROM nginx:alpine

COPY --from=build /app/dist /usr/share/nginx/html
```

---

# Benefits

```text
✔ Smaller production image
✔ Better performance
```

---

# 3️⃣ Minimize Layers

Combine commands.

---

# Good

```dockerfile
RUN apt update && apt install -y curl
```

---

# 4️⃣ Use .dockerignore

Exclude:
- node_modules
- logs
- .git

---

# Benefits

```text
✔ Smaller build context
✔ Faster builds
```

---

# 📊 Image Workflow

```text
Dockerfile
      ↓
Docker Build
      ↓
Image Created
      ↓
Push to Registry
      ↓
Pull Image
      ↓
Run Container
```

---

# 📌 Quick Revision Notes

| Topic | Key Point |
|---|---|
| Image | Read-only template |
| Container | Running instance |
| Layers | Filesystem snapshots |
| Registry | Stores images |
| Tags | Version identifiers |
| Copy-on-Write | Writable layer mechanism |
| Layer Caching | Faster builds |
| Base Image | Starting point |

---

# 🧠 Important Keywords

- Docker Image
- Layers
- Registry
- Docker Hub
- Copy-on-Write
- Writable Layer
- Image Tag
- Base Image
- OCI Image
- Layer Caching

---

# ❓ Viva Questions

1. What is a Docker image?
2. Difference between image and container?
3. What are Docker layers?
4. Why are layers important?
5. What is Copy-on-Write?
6. What is Docker Hub?
7. What are image tags?
8. Why use lightweight images?
9. What is a base image?
10. What is layer caching?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| Why are Docker images immutable? | Predictability and consistency |
| Why use layers? | Reusability and efficiency |
| What is writable layer? | Temporary container storage |
| Why are Docker builds fast? | Layer caching |
| Difference between image and container? | Template vs running instance |

---

# 📌 Key Takeaway

Docker images use layered architecture to provide:

```text
✔ Faster builds
✔ Efficient storage
✔ Portability
✔ Reusability
✔ Scalability
```

Core concepts:

```text
Image → Blueprint
Container → Running instance
Layers → Filesystem snapshots
```

These technologies form the foundation of:
- Docker
- Kubernetes
- Cloud-native applications

:contentReference[oaicite:0]{index=0}

---

# ✅ Conclusion

Container images and Docker layering are fundamental concepts in modern containerization.

Docker layers provide:
- Efficient storage
- Fast builds
- Better portability
- Easy distribution

The Copy-on-Write mechanism ensures:
- Isolation
- Efficiency
- Reduced storage usage

Together, images and layers enable:
- scalable
- portable
- reproducible cloud-native applications

---

# 🔗 Next Topic

➡️ Image Registeries