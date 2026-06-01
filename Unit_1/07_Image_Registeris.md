# Image Registries & Distribution

![Docker](https://img.shields.io/badge/Docker-Registry-blue)
![Containers](https://img.shields.io/badge/Containers-Images-green)
![Cloud](https://img.shields.io/badge/Cloud-Distribution-orange)
![DevOps](https://img.shields.io/badge/DevOps-CI%2FCD-red)
![Registry](https://img.shields.io/badge/Registry-Container-purple)

---

# 📚 Table of Contents

- [Overview](#-overview)
- [What is a Container Registry?](#-what-is-a-container-registry)
- [Why Registries are Needed](#-why-registries-are-needed)
- [Public vs Private Registries](#-public-vs-private-registries)
- [Popular Container Registries](#-popular-container-registries)
- [Image Naming Convention](#-image-naming-convention)
- [Understanding Tags](#-understanding-tags)
- [Image Distribution Workflow](#-image-distribution-workflow)
- [Pull Process](#-pull-process)
- [Push Process](#-push-process)
- [Layer Reuse and Efficiency](#-layer-reuse-and-efficiency)
- [Registry Authentication](#-registry-authentication)
- [Important Docker Registry Commands](#-important-docker-registry-commands)
- [Complete Workflow Example](#-complete-workflow-example)
- [Benefits of Registries](#-benefits-of-registries)
- [Best Practices](#-best-practices)
- [Quick Revision Notes](#-quick-revision-notes)
- [Viva Questions](#-viva-questions)
- [Interview Questions](#-interview-questions)
- [Conclusion](#-conclusion)

---

# 📖 Overview

Container images need a centralized platform for:
- Storage
- Versioning
- Sharing
- Distribution

This platform is called:
- Container Registry

Container registries allow developers to:
- Push images
- Pull images
- Share applications
- Deploy containers anywhere

---

# 🧠 What is a Container Registry?

> A Container Registry is a centralized storage system used for storing, managing, versioning, and distributing container images.

---

# Simple Analogy

```text
GitHub → Stores Source Code
Container Registry → Stores Docker Images
```

---

# Main Purpose

Registries help:
- Store images
- Version images
- Share images
- Deploy applications globally

---

# Registry Workflow

```text
Developer Builds Image
          ↓
Push to Registry
          ↓
Other Users Pull Image
          ↓
Run Containers
```

---

# 🎯 Why Registries are Needed

Without registries:

```text
✔ Images cannot be shared easily
✔ Deployment becomes difficult
✔ No centralized storage
✔ No version management
```

---

# With Registries

```text
✔ Centralized image storage
✔ Easy distribution
✔ CI/CD integration
✔ Global deployment
✔ Version control
```

---

# 🌍 Public vs Private Registries

Registries can be:
- Public
- Private

---

# 🌐 Public Registries

Anyone can:
- Pull images
- Use images

Usually contain:
- Open-source software
- Base images

---

# Examples

```text
✔ Ubuntu
✔ Python
✔ Node.js
✔ MySQL
✔ Nginx
```

---

# Benefits

```text
✔ Free access
✔ Community support
✔ Huge ecosystem
```

---

# 🔒 Private Registries

Require:
- Authentication
- Authorization

Used for:
- Company applications
- Internal software
- Sensitive workloads

---

# Benefits

```text
✔ Better security
✔ Controlled access
✔ Enterprise management
```

---

# 📊 Public vs Private Registry

| Feature | Public Registry | Private Registry |
|---|---|---|
| Access | Open | Restricted |
| Authentication | Optional | Required |
| Use Case | Open-source | Enterprise apps |
| Cost | Usually free | Paid/private |

---

# 🌟 Popular Container Registries

---

# 1️⃣ Docker Hub

Official Docker registry.

---

# Registry URL

```text
docker.io
```

---

# Example

```text
python:3.11
```

Equivalent to:

```text
docker.io/library/python:3.11
```

---

# Features

```text
✔ Largest registry
✔ Public images
✔ Easy to use
✔ Docker integration
```

---

# 2️⃣ GitHub Container Registry (GHCR)

Integrated with GitHub repositories.

---

# Registry URL

```text
ghcr.io
```

---

# Example

```text
ghcr.io/komaljoshi/myapp:v1
```

---

# Features

```text
✔ GitHub integration
✔ CI/CD friendly
✔ Private/public support
```

---

# 3️⃣ AWS Elastic Container Registry (ECR)

Amazon Web Services registry.

---

# Example

```text
123456789.dkr.ecr.us-east-1.amazonaws.com/myapp:v1
```

---

# Features

```text
✔ AWS integration
✔ Secure
✔ Scalable
```

---

# 4️⃣ Azure Container Registry (ACR)

Microsoft Azure registry.

---

# Example

```text
myregistry.azurecr.io/myapp:v1
```

---

# 5️⃣ Google Container Registry (GCR)

Google Cloud registry.

---

# Example

```text
gcr.io/project-id/myapp:v1
```

---

# 6️⃣ Quay.io

Alternative enterprise registry.

---

# Example

```text
quay.io/username/myapp:v1
```

---

# 7️⃣ Self-Hosted Registry

Organizations host their own registry.

---

# Example

```text
registry.company.com/myapp:v1
```

---

# Benefits

```text
✔ Full control
✔ Internal security
✔ Custom management
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
ghcr.io/komaljoshi/myapp:v1
```

---

# Short Form

```text
python:3.11
```

Docker automatically assumes:
- registry = docker.io
- namespace = library

---

# 🏷️ Understanding Tags

Tags identify:
- Versions
- Environments
- Architectures

---

# Common Tags

| Tag | Meaning |
|---|---|
| latest | Latest version |
| v1.0 | Application version |
| prod | Production image |
| dev | Development image |
| arm64 | ARM architecture |
| slim | Lightweight variant |
| alpine | Alpine Linux variant |

---

# Examples

```text
python:latest
python:3.11
python:3.11-slim
python:3.11-alpine
myapp:v1.0-prod
```

---

# 🔄 Image Distribution Workflow

Container distribution follows:
- Build
- Push
- Pull
- Run

---

# Workflow

```text
Dockerfile
      ↓
docker build
      ↓
Local Image
      ↓
docker push
      ↓
Registry
      ↓
docker pull
      ↓
Other Systems
```

---

# 📦 Pull Process

---

# Command

```bash
docker pull python:3.11
```

---

# Pull Workflow

```text
1. Parse image name
2. Connect to registry
3. Request metadata
4. Check local cache
5. Download missing layers
6. Verify integrity
7. Assemble image
```

---

# Example Output

```text
Pulling from library/python
Pull complete
Status: Downloaded newer image
```

---

# Layer Reuse During Pull

---

# Example

First pull:

```text
python:3.11 → downloads 400MB
```

Second pull:

```text
python:3.11 → uses cache
```

Pulling related image:

```text
python:3.12
```

Reuses shared layers.

---

# Result

```text
✔ Faster downloads
✔ Lower bandwidth usage
```

---

# 📤 Push Process

---

# Command

```bash
docker push ghcr.io/komaljoshi/myapp:v1
```

---

# Push Workflow

```text
1. Authenticate
2. Read image layers
3. Check existing layers
4. Upload only missing layers
5. Upload metadata
6. Update tag
```

---

# Example Output

```text
layer-1: complete
layer-2: complete
layer-3: complete

Digest: sha256:abc123
Status: Pushed
```

---

# 🚀 Layer Reuse and Efficiency

Docker registries use:
- Shared layers

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

# Push Result

Only:
- Layer D uploaded.

---

# Benefits

```text
✔ Faster push
✔ Storage efficiency
✔ Lower bandwidth
```

---

# Example Storage Savings

Without sharing:

```text
3 apps × 160MB = 480MB
```

With sharing:

```text
Shared base layer once
+
Only app code changes
```

---

# Result

```text
57% storage savings
```

---

# 🔐 Registry Authentication

Private registries require login.

---

# Login Command

```bash
docker login ghcr.io
```

---

# Docker Stores Credentials

```text
~/.docker/config.json
```

---

# Logout Command

```bash
docker logout ghcr.io
```

---

# 🔧 Important Docker Registry Commands

---

# Pull Image

```bash
docker pull image:tag
```

---

# Push Image

```bash
docker push registry/image:tag
```

---

# Login

```bash
docker login registry.com
```

---

# Logout

```bash
docker logout registry.com
```

---

# Search Docker Hub

```bash
docker search python
```

---

# Tag Image

```bash
docker tag myapp:v1 ghcr.io/komaljoshi/myapp:v1
```

---

# Remove Image

```bash
docker rmi image:tag
```

---

# List Local Images

```bash
docker images
```

---

# 🌍 Complete Workflow Example

---

# Step 1: Pull Base Image

```bash
docker pull python:3.11
```

---

# Step 2: Build Custom Image

```bash
docker build -t myapp:v1 .
```

---

# Step 3: Tag for Registry

```bash
docker tag myapp:v1 ghcr.io/komaljoshi/myapp:v1
```

---

# Step 4: Login

```bash
docker login ghcr.io
```

---

# Step 5: Push Image

```bash
docker push ghcr.io/komaljoshi/myapp:v1
```

---

# Step 6: Other User Pulls Image

```bash
docker pull ghcr.io/komaljoshi/myapp:v1
```

---

# Step 7: Run Container

```bash
docker run ghcr.io/komaljoshi/myapp:v1
```

---

# 🌟 Benefits of Registries

| Benefit | Description |
|---|---|
| Central Storage | Easy image management |
| Versioning | Multiple image versions |
| CI/CD Integration | Automated deployments |
| Scalability | Global distribution |
| Efficiency | Shared layers |

---

# 🛡️ Best Practices

---

# 1️⃣ Use Specific Tags

---

# Good

```text
python:3.11
```

---

# Bad

```text
python:latest
```

---

# 2️⃣ Use Private Registries for Sensitive Apps

---

# 3️⃣ Remove Unused Images

```bash
docker image prune
```

---

# 4️⃣ Use Lightweight Images

```text
alpine
slim
```

---

# 5️⃣ Scan Images for Vulnerabilities

Tools:
- Docker Scout
- Trivy
- Snyk

---

# 📊 Registry Distribution Architecture

```text
Developer
    ↓
Build Image
    ↓
Push to Registry
    ↓
Registry Stores Layers
    ↓
Users Pull Images
    ↓
Containers Run
```

---

# 📌 Quick Revision Notes

| Topic | Key Point |
|---|---|
| Registry | Stores images |
| Docker Hub | Default registry |
| Push | Upload image |
| Pull | Download image |
| Tag | Version identifier |
| Namespace | User/project scope |
| Public Registry | Open access |
| Private Registry | Authenticated access |

---

# 🧠 Important Keywords

- Docker Registry
- Docker Hub
- GHCR
- AWS ECR
- Azure ACR
- Push
- Pull
- Image Tag
- Layer Sharing
- Registry Authentication

---

# ❓ Viva Questions

1. What is a container registry?
2. Why are registries needed?
3. Difference between public and private registry?
4. What is Docker Hub?
5. What is image tagging?
6. What happens during docker push?
7. What happens during docker pull?
8. Why are layers important?
9. What is registry authentication?
10. Why use private registries?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| What is Docker Hub? | Public image registry |
| Difference between push and pull? | Upload vs download |
| Why use tags? | Version management |
| Why are registries important? | Centralized distribution |
| How does Docker optimize push/pull? | Layer reuse |

---

# 📌 Key Takeaway

Container registries provide:

```text
✔ Centralized image storage
✔ Global distribution
✔ Efficient layer sharing
✔ Version management
✔ CI/CD integration
```

They are essential for:
- Docker
- Kubernetes
- Cloud-native deployment
- DevOps automation

:contentReference[oaicite:0]{index=0}

---

# ✅ Conclusion

Container registries are the backbone of modern container distribution.

They allow developers to:
- Store images
- Share applications
- Deploy globally
- Manage versions efficiently

Docker optimizes distribution using:
- Layer caching
- Layer sharing
- Efficient push/pull operations

Registries are a critical component of:
- Docker ecosystems
- CI/CD pipelines
- Kubernetes deployments
- Cloud-native infrastructure

---

# 🔗 Next Topic

➡️ Docker Architecture and Components