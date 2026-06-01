# Docker Registries & GitHub Container Registry (GHCR)

![Docker](https://img.shields.io/badge/Docker-Registry-blue)
![GitHub](https://img.shields.io/badge/GHCR-Packages-black)
![DevOps](https://img.shields.io/badge/DevOps-CI/CD-green)
![Containers](https://img.shields.io/badge/Containers-Images-orange)

---

# 📚 Table of Contents

- Introduction
- What is a Docker Registry?
- Why Registries are Important
- Docker Hub
- Public vs Private Registries
- Docker Login & Authentication
- Docker Push & Pull
- Image Naming Convention
- GitHub Container Registry (GHCR)
- Creating GitHub PAT Token
- Push Image to GHCR
- Pull Image from GHCR
- Private Registries
- AWS ECR & Azure ACR
- Registry Workflow in CI/CD
- Best Practices
- Summary

---

# 📖 Introduction

Docker images need a place to:
- store
- distribute
- share
- deploy

This storage system is called:
- Docker Registry

Registries are essential for:
- DevOps
- CI/CD
- Kubernetes
- cloud-native deployments

---

# 🧠 What is a Docker Registry?

> Docker Registry is a centralized storage system for Docker images.

---

# Purpose

```text
✔ Store images
✔ Share images
✔ Download images
✔ Version management
✔ Deployment automation
```

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

# 🌍 Why Registries are Important

Without registries:
- images remain local only
- sharing impossible
- deployments difficult

---

# Benefits

```text
✔ Centralized storage
✔ Easy deployments
✔ Version management
✔ CI/CD integration
✔ Team collaboration
```

---

# 📦 Docker Hub

Docker Hub is:
- default public Docker registry

---

# Official Website

:contentReference[oaicite:0]{index=0}

---

# Features

```text
✔ Official images
✔ Public repositories
✔ Private repositories
✔ Automated builds
✔ Global distribution
```

---

# Popular Official Images

| Image | Purpose |
|---|---|
| nginx | Web server |
| ubuntu | Linux OS |
| mysql | Database |
| node | Node.js runtime |
| python | Python runtime |

---

# Pull Image from Docker Hub

```bash
docker pull nginx
```

---

# Result

```text
Docker downloads image layers from Docker Hub
```

---

# 🔐 Public vs Private Registries

| Type | Description |
|---|---|
| Public Registry | Accessible to everyone |
| Private Registry | Restricted access |

---

# Public Example

```text
docker.io/library/nginx
```

---

# Private Example

```text
company-registry/myapp:v1
```

---

# 🔑 Docker Login & Authentication

Before pushing images:
- authentication required

---

# Login Command

```bash
docker login
```

---

# Docker Asks For

```text
Username
Password / Access Token
```

---

# Logout

```bash
docker logout
```

---

# 📤 Push Image to Registry

---

# Step 1: Build Image

```bash
docker build -t myapp:v1 .
```

---

# Step 2: Tag Image

```bash
docker tag myapp:v1 username/myapp:v1
```

---

# Example

```bash
docker tag myapp:v1 komal/myapp:v1
```

---

# Step 3: Push Image

```bash
docker push komal/myapp:v1
```

---

# Result

```text
✔ Image uploaded
✔ Layers pushed
✔ Available globally
```

---

# 📥 Pull Image from Registry

---

# Command

```bash
docker pull komal/myapp:v1
```

---

# Result

```text
✔ Image downloaded locally
✔ Ready to run
```

---

# 🌟 Image Naming Convention

---

# Docker Hub Format

```text
username/image:tag
```

---

# Example

```text
komal/myapp:v1
```

---

# Components

| Component | Meaning |
|---|---|
| username | Docker Hub account |
| image | Application image |
| tag | Version |

---

# 🚀 GitHub Container Registry (GHCR)

GHCR allows storing Docker images directly with GitHub repositories.

---

# Official Website

:contentReference[oaicite:1]{index=1}

---

# Registry Format

```text
ghcr.io/username/image:tag
```

---

# Example

```text
ghcr.io/komal/myapp:v1
```

---

# 🌟 Advantages of GHCR

```text
✔ Integrated with GitHub
✔ Works with GitHub Actions
✔ Public/private images
✔ Better CI/CD integration
✔ Package visibility control
```

---

# 🔑 GitHub Personal Access Token (PAT)

GHCR requires:
- GitHub PAT token

instead of:
- GitHub password

---

# Why PAT?

```text
✔ Better security
✔ Scoped permissions
✔ Revocable access
✔ CI/CD support
```

---

# 🛠️ Create GitHub PAT Token

Go to:

:contentReference[oaicite:2]{index=2}

---

# Enable Permissions

```text
✔ write:packages
✔ read:packages
✔ delete:packages (optional)
```

---

# ⚠️ Important

```text
Copy token immediately.
GitHub will not show it again.
```

---

# 🏗️ Build Image for GHCR

---

# Create Dockerfile

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html
```

---

# Build Image

```bash
docker build -t ghcr.io/yourusername/ghcr-demo .
```

---

# Example

```bash
docker build -t ghcr.io/komal/ghcr-demo .
```

---

# 🔐 Login to GHCR

---

# Command

```bash
docker login ghcr.io
```

---

# Credentials

| Field | Value |
|---|---|
| Username | GitHub username |
| Password | PAT token |

---

# Alternative Login

```bash
echo TOKEN | docker login ghcr.io -u USERNAME --password-stdin
```

---

# 📤 Push Image to GHCR

---

# Command

```bash
docker push ghcr.io/komal/ghcr-demo
```

---

# Result

```text
✔ Image uploaded to GitHub
✔ Available in Packages section
✔ Registry integration complete
```

---

# 📥 Pull Image from GHCR

---

# Remove Local Image

```bash
docker rmi ghcr.io/komal/ghcr-demo
```

---

# Pull Again

```bash
docker pull ghcr.io/komal/ghcr-demo
```

---

# Run Container

```bash
docker run -p 8080:80 ghcr.io/komal/ghcr-demo
```

---

# Verify

Open:

```text
http://localhost:8080
```

---

# 🌍 Private Registries

Organizations often use:
- private registries

for:
- proprietary applications
- internal deployments

---

# Popular Private Registries

| Registry | Provider |
|---|---|
| ECR | AWS |
| ACR | Azure |
| GCR | Google Cloud |
| GHCR | GitHub |
| Harbor | Self-hosted |

---

# ☁️ AWS Elastic Container Registry (ECR)

AWS-managed private registry.

---

# Login Example

```bash
aws ecr get-login-password \
| docker login \
--username AWS \
--password-stdin ACCOUNT_ID.dkr.ecr.us-east-1.amazonaws.com
```

---

# Push Example

```bash
docker push ACCOUNT_ID.dkr.ecr.us-east-1.amazonaws.com/myapp:v1
```

---

# ☁️ Azure Container Registry (ACR)

Azure-managed registry.

---

# Login

```bash
az acr login --name myregistry
```

---

# 📊 Registry Workflow in CI/CD

---

# Workflow

```text
Code Push
    ↓
CI/CD Pipeline
    ↓
Build Docker Image
    ↓
Push to Registry
    ↓
Deploy to Server/Kubernetes
```

---

# Example GitHub Actions Workflow

```yaml
name: Docker Build

on: push

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Login to GHCR
        run: echo ${{ secrets.GHCR_TOKEN }} \
        | docker login ghcr.io -u USERNAME --password-stdin

      - name: Build Image
        run: docker build -t ghcr.io/USERNAME/app:v1 .

      - name: Push Image
        run: docker push ghcr.io/USERNAME/app:v1
```

---

# 🔐 Best Practices

---

# Use Access Tokens

❌ Avoid passwords

✅ Use:
- PAT tokens
- CI/CD secrets

---

# Use Proper Version Tags

✅ Good

```text
myapp:v1.0.0
```

❌ Avoid

```text
myapp:latest
```

---

# Keep Registries Secure

```text
✔ Enable authentication
✔ Restrict access
✔ Use private repositories
✔ Rotate tokens regularly
```

---

# Scan Images for Vulnerabilities

Use:
- Docker Scout
- Trivy
- Snyk

---

# 📌 Quick Revision Notes

| Concept | Meaning |
|---|---|
| Registry | Image storage system |
| Docker Hub | Default public registry |
| GHCR | GitHub Container Registry |
| docker push | Upload image |
| docker pull | Download image |
| PAT Token | GitHub authentication token |

---

# 🧠 Important Keywords

- Docker Registry
- Docker Hub
- GHCR
- ECR
- ACR
- PAT Token
- docker push
- docker pull
- Image Distribution
- CI/CD

---

# ❓ Viva Questions

1. What is Docker Registry?
2. Why are registries needed?
3. What is Docker Hub?
4. What is GHCR?
5. What is PAT token?
6. Why use access tokens?
7. Difference between public and private registry?
8. What does docker push do?
9. What does docker pull do?
10. Why are registries important in CI/CD?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| What is Docker Hub? | Default Docker registry |
| Why use GHCR? | GitHub integration |
| What is PAT token? | GitHub access token |
| Difference between docker push and pull? | Upload vs download |
| Why use private registries? | Security and proprietary apps |

---

# ✅ Conclusion

Docker registries enable:
- image storage
- sharing
- deployment
- CI/CD integration

Using:
- Docker Hub
- GHCR
- ECR
- ACR

developers can:
- distribute applications globally
- automate deployments
- manage versions securely

Registries are foundational for:
- cloud-native DevOps
- Kubernetes deployments
- modern container infrastructure