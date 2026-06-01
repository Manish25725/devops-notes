# Docker & GitHub Actions

![Docker](https://img.shields.io/badge/Docker-Containers-blue)
![GitHub Actions](https://img.shields.io/badge/GitHub-Actions-black)
![CI/CD](https://img.shields.io/badge/CI/CD-Automation-green)
![DevOps](https://img.shields.io/badge/DevOps-Docker_Pipeline-orange)

---

# 📚 Table of Contents

- Introduction
- Why Integrate Docker with GitHub Actions?
- CI Pipeline with Docker
- Building Docker Images in CI
- Docker Login in GitHub Actions
- Docker Hub Integration
- GitHub Container Registry (GHCR)
- Docker Buildx
- Multi-Platform Docker Images
- Docker Image Tagging
- Complete Docker Workflow
- Docker Security Best Practices
- Real-World CI/CD Pipeline
- Viva Questions
- Interview Questions

---

# Introduction

Modern DevOps pipelines rarely deploy source code directly.

Instead:

```text
Source Code
      ↓
Build Docker Image
      ↓
Push Image to Registry
      ↓
Deploy Container
```

GitHub Actions automates this entire process.

---

# Why Integrate Docker with GitHub Actions?

Without automation:

```text
Developer
    ↓
Build Image
    ↓
Login Docker Hub
    ↓
Push Image
    ↓
Deploy
```

Manual and error-prone.

---

# With GitHub Actions

```text
Push Code
    ↓
GitHub Actions
    ↓
Build Docker Image
    ↓
Push Registry
    ↓
Deploy
```

Fully automated.

---

# CI Pipeline with Docker

```text
Developer Push
      ↓
GitHub Actions
      ↓
Build Docker Image
      ↓
Run Tests
      ↓
Push Image
      ↓
Deploy
```

---

# Building Docker Images in CI

A Docker image can be built directly inside a workflow.

---

## Example

```yaml
- name: Build Docker Image

  run: |

    docker build -t myapp:v1 .
```

---

# Dockerfile Example

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html

EXPOSE 80
```

---

# Build Flow

```text
Source Code
      ↓
Dockerfile
      ↓
docker build
      ↓
Docker Image
```

---

# Docker Login in GitHub Actions

Before pushing images:

```text
Authenticate
```

with the registry.

---

# Docker Hub Login Action

```yaml
- name: Login to Docker Hub

  uses: docker/login-action@v3

  with:

    username: ${{ secrets.DOCKER_USERNAME }}

    password: ${{ secrets.DOCKER_PASSWORD }}
```

---

# Why Use Secrets?

Never hardcode:

```yaml
password: mypassword123
```

Bad practice.

Use:

```yaml
${{ secrets.DOCKER_PASSWORD }}
```

---

# GitHub Secrets

Repository:

```text
Settings
     ↓
Secrets and Variables
     ↓
Actions
```

Add:

```text
DOCKER_USERNAME
DOCKER_PASSWORD
```

---

# Docker Hub Integration

Docker Hub is the most popular container registry.

Official Website:

:contentReference[oaicite:0]{index=0}

---

# Image Naming

```text
username/image:tag
```

Example:

```text
komaljoshi17/myapp:v1
```

---

# Build & Push Workflow

```yaml
- name: Build Image

  run: |

    docker build -t komaljoshi17/myapp:v1 .
```

---

```yaml
- name: Push Image

  run: |

    docker push komaljoshi17/myapp:v1
```

---

# Complete Docker Hub Example

```yaml
steps:

  - uses: actions/checkout@v4

  - uses: docker/login-action@v3

    with:

      username: ${{ secrets.DOCKER_USERNAME }}

      password: ${{ secrets.DOCKER_PASSWORD }}

  - run: docker build -t komaljoshi17/myapp:v1 .

  - run: docker push komaljoshi17/myapp:v1
```

---

# GitHub Container Registry (GHCR)

GitHub also provides its own registry.

```text
ghcr.io
```

---

# Benefits

✔ Integrated with GitHub

✔ Secure

✔ Easy authentication

✔ Private/Public Images

---

# Image Format

```text
ghcr.io/<username>/<image>:tag
```

Example:

```text
ghcr.io/komaljoshi17/devops-app:v1
```

---

# Login to GHCR

```yaml
- name: Login to GHCR

  uses: docker/login-action@v3

  with:

    registry: ghcr.io

    username: ${{ github.actor }}

    password: ${{ secrets.GITHUB_TOKEN }}
```

---

# Build & Push to GHCR

```yaml
- run: |

    docker build -t ghcr.io/komaljoshi17/devops-app:v1 .
```

---

```yaml
- run: |

    docker push ghcr.io/komaljoshi17/devops-app:v1
```

---

# Docker Buildx

Docker Buildx is an advanced build tool.

Supports:

✔ Multi-platform builds

✔ Faster builds

✔ Advanced caching

✔ Cross-platform images

---

# Setup Buildx

```yaml
- uses: docker/setup-buildx-action@v3
```

---

# Buildx Architecture

```text
Source Code
      ↓
Buildx
      ↓
Linux Image
      ↓
Windows Image
      ↓
ARM Image
```

---

# Multi-Platform Images

Traditional Build:

```text
Linux Only
```

Buildx:

```text
Linux
Windows
ARM
AMD64
```

---

# Example

```yaml
- uses: docker/build-push-action@v6

  with:

    push: true

    tags: komaljoshi17/myapp:latest

    platforms: linux/amd64,linux/arm64
```

---

# Generated Images

```text
linux/amd64

linux/arm64
```

Both published under same tag.

---

# Docker Image Tagging

Tags help version images.

---

# Examples

```text
myapp:v1

myapp:v2

myapp:latest

myapp:prod

myapp:staging
```

---

# Best Practice

Use:

```text
Semantic Versioning
```

Example:

```text
v1.0.0

v1.1.0

v2.0.0
```

---

# Dynamic Tag Example

```yaml
tags: |

  komaljoshi17/myapp:latest

  komaljoshi17/myapp:${{ github.sha }}
```

---

# Result

```text
latest

commit-hash-tag
```

---

# Complete Docker CI Workflow

```yaml
name: Docker Build & Push

on:

  push:

    branches:

      - main

jobs:

  docker:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v4

      - uses: docker/login-action@v3

        with:

          username: ${{ secrets.DOCKER_USERNAME }}

          password: ${{ secrets.DOCKER_PASSWORD }}

      - uses: docker/setup-buildx-action@v3

      - uses: docker/build-push-action@v6

        with:

          context: .

          push: true

          tags: komaljoshi17/myapp:latest
```

---

# Workflow Execution

```text
Push Code
      ↓
Checkout Repository
      ↓
Login Docker Hub
      ↓
Setup Buildx
      ↓
Build Image
      ↓
Push Image
      ↓
Success
```

---

# Real-World Deployment Pipeline

```text
Developer Push
      ↓
GitHub Actions
      ↓
Build Docker Image
      ↓
Push Docker Hub
      ↓
Server Pulls Image
      ↓
Deploy Container
```

---

# Enterprise CI/CD Flow

```text
Code Push
      ↓
Unit Tests
      ↓
Build Docker Image
      ↓
Security Scan
      ↓
Push Registry
      ↓
Deploy Staging
      ↓
Deploy Production
```

---

# Docker Security Best Practices

## Never Store Passwords

Use:

```yaml
secrets
```

---

## Scan Images

Use:

```text
Trivy
Docker Scout
```

---

## Use Minimal Images

Example:

```dockerfile
FROM alpine
```

instead of full Linux distributions.

---

## Tag Images Properly

Avoid:

```text
latest only
```

Use:

```text
v1.0.0
v1.1.0
```

---

# Advantages

| Feature | Benefit |
|----------|----------|
| Automation | No manual builds |
| Consistency | Same image everywhere |
| Speed | Faster deployments |
| Scalability | Works for large teams |
| Reliability | Reduced deployment errors |

---

# Quick Revision Notes

## Docker Login

```yaml
docker/login-action
```

---

## Docker Build

```yaml
docker build
```

---

## Docker Push

```yaml
docker push
```

---

## GHCR

```text
ghcr.io
```

---

## Buildx

```text
Multi-platform builds
```

---

# Viva Questions

### 1. Why integrate Docker with GitHub Actions?

To automate image build and deployment.

---

### 2. Which action performs Docker login?

```yaml
docker/login-action
```

---

### 3. What is GHCR?

GitHub Container Registry.

---

### 4. What is Docker Buildx?

Advanced Docker builder supporting multi-platform images.

---

### 5. Why use GitHub Secrets?

To securely store credentials.

---

### 6. What is image tagging?

Assigning versions to Docker images.

---

### 7. What is Docker Hub?

A cloud registry for storing Docker images.

---

### 8. Can GitHub Actions push Docker images automatically?

Yes.

---

# Interview Questions

## Q1. Explain Docker CI/CD using GitHub Actions.

```text
Push Code
     ↓
Build Image
     ↓
Push Registry
     ↓
Deploy
```

---

## Q2. Difference between Docker Hub and GHCR?

Docker Hub:

```text
External Registry
```

GHCR:

```text
GitHub Integrated Registry
```

---

## Q3. Why use Buildx?

Supports multi-platform image builds.

---

## Q4. How are credentials stored securely?

Using GitHub Secrets.

---

## Q5. What is the role of docker/build-push-action?

Builds and pushes Docker images automatically.

---

# Key Terms

| Term | Meaning |
|--------|---------|
| Docker Hub | Public container registry |
| GHCR | GitHub Container Registry |
| Buildx | Advanced Docker builder |
| Tag | Image version |
| Secret | Secure credential |
| Registry | Image storage system |

---

# Summary

Docker and GitHub Actions together create powerful CI/CD pipelines.

They automate:

✔ Docker image builds

✔ Docker Hub pushes

✔ GHCR pushes

✔ Multi-platform builds

✔ Containerized deployments

This integration is widely used in modern DevOps workflows and cloud-native applications.