# Image Building & Layering

![Docker](https://img.shields.io/badge/Docker-Images-blue)
![Containers](https://img.shields.io/badge/Containers-Layers-green)
![DevOps](https://img.shields.io/badge/DevOps-Build-orange)
![Linux](https://img.shields.io/badge/Linux-OverlayFS-red)

---

# 📚 Table of Contents

- Introduction
- What is a Docker Image?
- Docker Image Architecture
- What are Image Layers?
- How Docker Builds Images
- Layer Caching
- Copy-on-Write (CoW)
- OverlayFS
- Read-Only vs Writable Layers
- Image Layer Workflow
- Benefits of Layering
- Docker History Command
- Inspecting Layers
- Image Size Optimization
- Best Practices
- Complete Example
- Summary

---

# 📖 Introduction

Docker images are built using:
- layered architecture

Each instruction in Dockerfile creates:
- separate image layer

This layered approach makes Docker:
- fast
- efficient
- lightweight
- scalable

---

# 🧠 What is a Docker Image?

> Docker Image is a read-only template used to create containers.

---

# Image Contains

```text
✔ Operating System
✔ Application Code
✔ Dependencies
✔ Libraries
✔ Runtime
✔ Configuration
```

---

# Example

```text
ubuntu:22.04
nginx:alpine
node:18
mysql:8
```

---

# 🏗️ Docker Image Architecture

Docker images use:
- layered filesystem architecture

---

# Architecture

```text
Top Layer → Application Code
Middle Layer → Dependencies
Bottom Layer → Base OS
```

---

# Example

```text
Layer 4 → App Files
Layer 3 → Node.js
Layer 2 → Libraries
Layer 1 → Ubuntu Base
```

---

# 📦 What are Image Layers?

Each Dockerfile instruction creates:
- one immutable layer

---

# Example Dockerfile

```dockerfile
FROM ubuntu:22.04

RUN apt-get update

RUN apt-get install -y nginx

COPY . /app
```

---

# Layers Created

| Instruction | Layer |
|---|---|
| FROM | Base OS layer |
| RUN apt-get update | Layer 2 |
| RUN install nginx | Layer 3 |
| COPY | Layer 4 |

---

# 🌟 Characteristics of Layers

```text
✔ Immutable
✔ Read-only
✔ Reusable
✔ Cached
✔ Shared across containers
```

---

# ⚙️ How Docker Builds Images

Docker build process:

```text
Dockerfile
    ↓
Execute instruction
    ↓
Create layer
    ↓
Cache layer
    ↓
Next instruction
```

---

# Build Command

```bash
docker build -t myapp:v1 .
```

---

# Build Flow

```text
Step 1 → Read Dockerfile
Step 2 → Execute FROM
Step 3 → Create Layer
Step 4 → Execute RUN
Step 5 → Create Layer
Step 6 → Continue
```

---

# 🚀 Layer Caching

Docker caches layers for:
- faster rebuilds

---

# Example

```dockerfile
FROM node:18

COPY package.json .

RUN npm install

COPY . .
```

---

# What Happens?

If only app code changes:
- Docker reuses cached npm install layer

Result:
- much faster builds

---

# ⚡ Why Layer Order Matters

Good Practice:

```dockerfile
COPY package.json .

RUN npm install

COPY . .
```

---

# Why?

Dependencies install only when:
- package.json changes

---

# Bad Practice

```dockerfile
COPY . .

RUN npm install
```

Every code change:
- invalidates cache
- reinstall dependencies

---

# 🔄 Copy-on-Write (CoW)

Docker uses:
- Copy-on-Write mechanism

---

# What is CoW?

Containers share:
- image layers

When container modifies file:
- Docker copies file into writable layer

---

# Workflow

```text
Shared Read-Only Layers
         ↓
Container Modifies File
         ↓
File Copied to Writable Layer
```

---

# Benefits

```text
✔ Efficient storage
✔ Fast startup
✔ Shared base images
✔ Lightweight containers
```

---

# 🌐 OverlayFS

Docker commonly uses:
- OverlayFS (overlay2)

as storage driver.

---

# Purpose

OverlayFS combines:
- multiple read-only layers
- one writable layer

into:
- single unified filesystem

---

# Visualization

```text
Writable Container Layer
         ↑
Read-Only Image Layers
         ↑
Base OS Layer
```

---

# Benefits

```text
✔ Layer sharing
✔ Efficient storage
✔ Faster performance
```

---

# 🔒 Read-Only vs Writable Layers

---

# Read-Only Layers

Created from:
- image instructions

Characteristics:

```text
✔ Immutable
✔ Shared
✔ Cached
```

---

# Writable Layer

Created when:
- container starts

Characteristics:

```text
✔ Temporary
✔ Unique per container
✔ Deleted with container
```

---

# 🏗️ Image Layer Workflow

```text
Dockerfile
    ↓
Image Layers Created
    ↓
Image Stored
    ↓
Container Started
    ↓
Writable Layer Added
```

---

# 📊 Benefits of Layering

| Benefit | Description |
|---|---|
| Faster Builds | Layer caching |
| Smaller Storage | Shared layers |
| Reusability | Same base reused |
| Efficient Downloads | Pull only changed layers |
| Faster Deployment | Cached layers reused |

---

# 🌟 Shared Layers Example

```text
node-app:v1
node-app:v2
```

Both use:
- same Node.js base layer

Docker stores:
- one shared copy

---

# Storage Savings

Without layering:

```text
5 Images × 500MB = 2500MB
```

With layering:

```text
Shared Base = 500MB
Extra Layers = 100MB
Total ≈ 600MB
```

---

# 📜 Docker History Command

Used to view image layers.

---

# Command

```bash
docker history nginx
```

---

# Output Shows

```text
✔ Layers
✔ Commands
✔ Sizes
✔ Creation times
```

---

# 🔍 Inspecting Images

---

# Inspect Image Metadata

```bash
docker inspect nginx
```

---

# Shows

```text
✔ Layer details
✔ Environment variables
✔ Volumes
✔ Exposed ports
✔ Configuration
```

---

# 📦 Image Size Optimization

---

# Use Small Base Images

✅ Good

```dockerfile
FROM alpine
```

❌ Bad

```dockerfile
FROM ubuntu
```

---

# Combine RUN Commands

✅ Good

```dockerfile
RUN apt update && apt install -y curl
```

---

# Remove Unnecessary Files

```dockerfile
RUN apt-get clean
```

---

# Use .dockerignore

Avoid copying:
- logs
- node_modules
- secrets

---

# 🚀 Multi-Stage Builds

Used to reduce final image size.

---

# Example

```dockerfile
FROM node:18 AS build

WORKDIR /app

COPY . .

RUN npm install

FROM nginx:alpine

COPY --from=build /app/dist /usr/share/nginx/html
```

---

# Benefits

```text
✔ Smaller production images
✔ Better security
✔ Faster deployment
```

---

# 🌍 Complete Example

## Dockerfile

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 3000

CMD ["node", "server.js"]
```

---

# Build Image

```bash
docker build -t node-app:v1 .
```

---

# Run Container

```bash
docker run -d -p 3000:3000 node-app:v1
```

---

# 📌 Quick Revision Notes

| Concept | Meaning |
|---|---|
| Image | Read-only template |
| Layer | Immutable filesystem snapshot |
| OverlayFS | Layered filesystem |
| CoW | Copy-on-Write |
| Cache | Reuse previous layers |
| Writable Layer | Container-specific changes |

---

# 🧠 Important Keywords

- Docker Image
- Image Layers
- Layer Caching
- OverlayFS
- Copy-on-Write
- Writable Layer
- Read-Only Layer
- Docker Build
- Multi-Stage Build

---

# ❓ Viva Questions

1. What is Docker image?
2. What are image layers?
3. Why are layers useful?
4. What is layer caching?
5. What is OverlayFS?
6. What is Copy-on-Write?
7. Difference between image and container?
8. What is writable layer?
9. Why use small base images?
10. What are multi-stage builds?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| Why are Docker builds fast? | Layer caching |
| What is Copy-on-Write? | Modified files copied to writable layer |
| What is OverlayFS? | Layered filesystem |
| Why use alpine images? | Smaller size |
| What is multi-stage build? | Separate build and production stages |

---

# ✅ Conclusion

Docker image layering provides:
- efficient storage
- faster builds
- scalable deployments
- reusable architecture

Using:
- layer caching
- OverlayFS
- Copy-on-Write

Docker achieves:
- lightweight containers
- optimized builds
- faster deployments

These concepts are fundamental to:
- Docker
- Kubernetes
- cloud-native DevOps infrastructure