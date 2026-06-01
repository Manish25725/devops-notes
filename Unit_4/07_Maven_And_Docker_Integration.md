# Maven & Docker Integration

![Maven](https://img.shields.io/badge/Maven-DockerIntegration-blue)
![Docker](https://img.shields.io/badge/Docker-Containers-green)
![DevOps](https://img.shields.io/badge/DevOps-CI/CD-orange)
![Cloud](https://img.shields.io/badge/Cloud-Deployment-red)

---

# 📚 Table of Contents

- Introduction
- Why Maven & Docker Integration is Important
- Maven Build + Docker Workflow
- Dockerizing Maven Applications
- Maven Docker Plugins
- dockerfile-maven-plugin
- Jib Plugin
- Fabric8 Docker Maven Plugin
- Building Docker Images with Maven
- Multi-Stage Docker Builds
- Pushing Images to Registries
- Docker Hub Integration
- GitHub Container Registry (GHCR)
- CI/CD Integration
- Real-World Example
- Best Practices
- Summary

---

# 📖 Introduction

Modern Java applications are commonly:
- built using Maven
- containerized using Docker

This combination enables:
- scalable deployments
- cloud-native applications
- CI/CD automation
- microservices architecture

---

# Traditional Java Deployment Problems

Without Docker:

```text
❌ Java version mismatch
❌ "Works on my machine" problem
❌ Complex deployments
❌ Dependency conflicts
❌ Difficult scaling
```

---

# Docker Solves

```text
✔ Portable deployments
✔ Environment consistency
✔ Fast scaling
✔ Cloud-native architecture
✔ Easy CI/CD integration
```

---

# 🎯 Why Maven & Docker Integration is Important

Maven:
```text
✔ Builds Java application
✔ Creates JAR/WAR
✔ Manages dependencies
```

Docker:
```text
✔ Packages application
✔ Creates containers
✔ Runs anywhere
```

---

# Combined Workflow

```text
Source Code
      ↓
Maven Build
      ↓
JAR File
      ↓
Docker Image
      ↓
Container Deployment
```

---

# 🌟 Modern DevOps Pipeline

```text
GitHub
   ↓
Maven Build
   ↓
Docker Build
   ↓
Push to Registry
   ↓
Kubernetes Deployment
```

---

# 📦 Dockerizing Maven Applications

After Maven creates:
```text
app.jar
```

Docker packages it into:
```text
Docker Image
```

---

# Typical Workflow

---

# Step 1 — Build Maven Project

```bash
mvn clean package
```

---

# Result

```text
target/myapp.jar
```

---

# Step 2 — Create Dockerfile

```dockerfile
FROM openjdk:17

WORKDIR /app

COPY target/myapp.jar app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]
```

---

# Step 3 — Build Docker Image

```bash
docker build -t myapp:v1 .
```

---

# Step 4 — Run Container

```bash
docker run -p 8080:8080 myapp:v1
```

---

# 🌍 Real-World Architecture

```text
Spring Boot App
       ↓
Maven Build
       ↓
Executable JAR
       ↓
Docker Image
       ↓
Docker Registry
       ↓
Kubernetes Cluster
```

---

# 🔌 Maven Docker Plugins

Maven plugins can automate:
- Docker builds
- image pushing
- container management

---

# Popular Docker Maven Plugins

| Plugin | Purpose |
|---|---|
| dockerfile-maven-plugin | Build Docker images |
| Jib Plugin | Build images without Docker |
| Fabric8 Docker Plugin | Advanced Docker integration |

---

# 🌟 dockerfile-maven-plugin

Popular Maven plugin for:
- Docker image creation

---

# Official Plugin

:contentReference[oaicite:0]{index=0}

---

# Plugin Example

```xml
<plugin>

    <groupId>com.spotify</groupId>

    <artifactId>dockerfile-maven-plugin</artifactId>

    <version>1.4.13</version>

    <configuration>

        <repository>komal/myapp</repository>

        <tag>v1</tag>

    </configuration>

</plugin>
```

---

# Build Docker Image Using Maven

```bash
mvn dockerfile:build
```

---

# Result

```text
✔ Maven builds JAR
✔ Docker image created
```

---

# 🌟 Jib Plugin

Google-developed Maven plugin.

---

# Special Feature

```text
✔ No Docker daemon required
✔ Faster builds
✔ Optimized layers
✔ Direct registry push
```

---

# Official Website

:contentReference[oaicite:1]{index=1}

---

# Example Configuration

```xml
<plugin>

    <groupId>com.google.cloud.tools</groupId>

    <artifactId>jib-maven-plugin</artifactId>

    <version>3.4.0</version>

</plugin>
```

---

# Build Image

```bash
mvn compile jib:dockerBuild
```

---

# Push Directly to Registry

```bash
mvn compile jib:build
```

---

# 🌟 Fabric8 Docker Maven Plugin

Advanced Docker integration plugin.

Supports:
```text
✔ Build
✔ Push
✔ Run containers
✔ Kubernetes integration
```

---

# 🌟 Multi-Stage Docker Builds

Used to:
- reduce image size

---

# Traditional Dockerfile Problem

```text
❌ Maven dependencies remain inside image
❌ Large image size
❌ Security risks
```

---

# Multi-Stage Solution

```dockerfile
# Build Stage
FROM maven:3.9.6-eclipse-temurin-17 AS build

WORKDIR /app

COPY . .

RUN mvn clean package

# Runtime Stage
FROM eclipse-temurin:17

WORKDIR /app

COPY --from=build /app/target/myapp.jar app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]
```

---

# Benefits

```text
✔ Smaller image
✔ Faster deployment
✔ Better security
✔ Cleaner containers
```

---

# 📦 Pushing Docker Images to Registries

After image creation:
- images pushed to registries

---

# Popular Registries

| Registry | Provider |
|---|---|
| Docker Hub | Docker |
| GHCR | GitHub |
| ECR | AWS |
| ACR | Azure |

---

# 🌟 Docker Hub Integration

---

# Login

```bash
docker login
```

---

# Tag Image

```bash
docker tag myapp:v1 komaljoshi17/myapp:v1
```

---

# Push Image

```bash
docker push komaljoshi17/myapp:v1
```

---

# Pull Image

```bash
docker pull komaljoshi17/myapp:v1
```

---

# 🌟 GitHub Container Registry (GHCR)

GitHub-based container registry.

---

# Registry URL

```text
ghcr.io
```

---

# Login

```bash
docker login ghcr.io
```

---

# Tag Image

```bash
docker tag myapp:v1 ghcr.io/komaljoshi17/myapp:v1
```

---

# Push Image

```bash
docker push ghcr.io/komaljoshi17/myapp:v1
```

---

# Benefits

```text
✔ GitHub integration
✔ Secure authentication
✔ CI/CD friendly
✔ Enterprise-ready
```

---

# 🚀 CI/CD Integration

Maven + Docker heavily used in:
- Jenkins
- GitHub Actions
- GitLab CI

---

# Example Pipeline

```text
Git Push
    ↓
Maven Build
    ↓
Docker Image Build
    ↓
Push to Registry
    ↓
Deploy to Kubernetes
```

---

# 🌟 GitHub Actions Example

```yaml
name: Java CI

on: [push]

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v3

      - name: Build Maven Project
        run: mvn clean package

      - name: Build Docker Image
        run: docker build -t myapp:v1 .

      - name: Push Docker Image
        run: docker push myapp:v1
```

---

# 🌍 Real-World Spring Boot Example

---

# Project Structure

```text
spring-demo/
│
├── src/
├── pom.xml
├── Dockerfile
└── target/
```

---

# Build Application

```bash
mvn clean package
```

---

# Create Docker Image

```bash
docker build -t spring-demo:v1 .
```

---

# Run Container

```bash
docker run -p 8080:8080 spring-demo:v1
```

---

# Access Application

```text
http://localhost:8080
```

---

# 🛠️ Useful Maven + Docker Commands

| Command | Purpose |
|---|---|
| `mvn clean package` | Build JAR |
| `docker build -t app:v1 .` | Build image |
| `docker run -p 8080:8080 app:v1` | Run container |
| `docker push image` | Push image |
| `docker pull image` | Pull image |
| `mvn jib:build` | Build with Jib |

---

# 🔐 Best Practices

---

# Use Multi-Stage Builds

Reduces image size.

---

# Avoid Running as Root

Use non-root containers.

---

# Keep Images Small

Prefer:
```dockerfile
alpine
```

images.

---

# Use Specific Tags

❌ Avoid:

```text
latest
```

✅ Use:

```text
v1.0.0
```

---

# Use .dockerignore

Avoid unnecessary files.

---

# Scan Images for Vulnerabilities

Use:
```text
Trivy
Docker Scout
```

---

# Push Images via CI/CD

Avoid manual deployment.

---

# 📊 Maven + Docker Workflow Diagram

```text
Source Code
     ↓
Maven Build
     ↓
JAR/WAR
     ↓
Docker Build
     ↓
Docker Image
     ↓
Registry
     ↓
Kubernetes Deployment
```

---

# 📌 Quick Revision Notes

| Concept | Meaning |
|---|---|
| Maven | Java build tool |
| Docker | Container platform |
| Dockerfile | Image instructions |
| Multi-stage Build | Optimized image build |
| Registry | Image storage |
| Jib | Dockerless image builder |
| dockerfile-maven-plugin | Docker build plugin |

---

# 🧠 Important Keywords

- Maven
- Docker
- Dockerfile
- Jib Plugin
- Multi-stage Build
- Docker Registry
- GHCR
- Docker Hub
- CI/CD
- Containerization

---

# ❓ Viva Questions

1. Why integrate Maven with Docker?
2. What is Dockerizing an application?
3. What is dockerfile-maven-plugin?
4. What is Jib plugin?
5. Why use multi-stage builds?
6. What is Docker Hub?
7. What is GHCR?
8. Why use Docker in DevOps?
9. Difference between Jib and Dockerfile?
10. How does Maven help Docker builds?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| Why use Maven with Docker? | Build + containerization automation |
| What is multi-stage Docker build? | Optimized smaller image |
| What is Jib plugin? | Build container images without Docker |
| What is Docker registry? | Stores container images |
| Why use Docker in CI/CD? | Portable deployments |

---

# 🌟 Important Interview Scenario

## Question

Why are multi-stage Docker builds important for Maven applications?

## Answer

Multi-stage builds:
- separate build environment from runtime
- reduce image size
- improve security
- avoid unnecessary Maven dependencies inside production container

This creates:
```text
✔ Smaller images
✔ Faster deployment
✔ Better performance
✔ Cleaner production containers
```

---

# ✅ Conclusion

Maven & Docker Integration enables:
- automated Java builds
- containerized deployments
- scalable cloud-native applications
- enterprise DevOps workflows

Using:
- Maven plugins
- Dockerfiles
- registries
- CI/CD pipelines

developers can build:
```text
✔ Portable applications
✔ Scalable systems
✔ Microservices
✔ Kubernetes deployments
✔ Modern DevOps infrastructure
```

This integration is foundational for:
- Spring Boot
- Microservices
- Kubernetes
- Cloud Computing
- Enterprise DevOps