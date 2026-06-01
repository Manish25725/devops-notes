# Docker and Jenkins Integration

![Jenkins](https://img.shields.io/badge/Jenkins-Docker-red)
![CI/CD](https://img.shields.io/badge/CI/CD-Automation-blue)
![Docker](https://img.shields.io/badge/Docker-Containers-green)
![DevOps](https://img.shields.io/badge/DevOps-Integration-orange)

---

# 📚 Table of Contents

- Why Integrate Docker with Jenkins?
- Jenkins + Docker Architecture
- Docker Installation on Jenkins
- Docker Pipeline Plugin
- Building Docker Images in Jenkins
- Docker Agents
- Docker Inside Jenkins Agents
- Docker-in-Docker (DinD)
- Publishing Images to Docker Hub
- Publishing Images to GitHub Container Registry (GHCR)
- Jenkins + Docker CI/CD Pipeline
- Best Practices
- Quick Revision Notes
- Viva Questions
- Interview Questions

---

# Why Integrate Docker with Jenkins?

Modern applications are deployed using containers.

Instead of:

```text
Build Application
↓
Manually Deploy
```

we automate:

```text
Build
↓
Dockerize
↓
Push Image
↓
Deploy
```

using Jenkins.

---

# Benefits of Docker + Jenkins

✔ Automated Image Creation

✔ Consistent Environments

✔ Faster Deployments

✔ Easier Scaling

✔ CI/CD Automation

✔ Better Portability

---

# Jenkins + Docker Architecture

```text
Developer
     ↓
GitHub
     ↓
Jenkins
     ↓
Build Application
     ↓
Docker Build
     ↓
Docker Hub / GHCR
     ↓
Deployment Server
```

---

# CI/CD Flow

```text
Code Commit
      ↓
Jenkins Trigger
      ↓
Build
      ↓
Test
      ↓
Docker Build
      ↓
Push Image
      ↓
Deploy
```

---

# Installing Docker on Jenkins Server

Jenkins must have Docker installed.

---

# Verify Docker

```bash
docker --version
```

Example:

```text
Docker version 28.x.x
```

---

# Verify Jenkins User Access

```bash
docker ps
```

If permission denied:

```bash
sudo usermod -aG docker jenkins
```

Restart Jenkins.

---

# Docker Plugin

Jenkins provides plugins for Docker integration.

Navigate:

```text
Manage Jenkins
    ↓
Plugins
```

Install:

```text
Docker Plugin
Docker Pipeline Plugin
Docker Commons Plugin
```

---

# Important Docker Plugins

| Plugin | Purpose |
|----------|---------|
| Docker Plugin | Docker Integration |
| Docker Pipeline | Docker in Jenkinsfile |
| Docker Commons | Shared Docker Features |

---

# Building Docker Images in Jenkins

Most common DevOps task.

---

# Dockerfile Example

```dockerfile
FROM openjdk:21

COPY target/app.jar app.jar

ENTRYPOINT ["java","-jar","app.jar"]
```

---

# Jenkins Pipeline Build

```groovy
stage('Docker Build') {

    steps {

        sh 'docker build -t myapp:v1 .'

    }

}
```

---

# Build Flow

```text
Source Code
      ↓
Maven Package
      ↓
Docker Build
      ↓
Image Created
```

---

# Complete Build Example

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

                sh 'mvn package'

            }

        }

        stage('Docker Build') {

            steps {

                sh 'docker build -t myapp:v1 .'

            }

        }

    }

}
```

---

# Verify Image

```bash
docker images
```

Output:

```text
myapp:v1
```

---

# Docker Agents

Instead of running builds directly:

```text
Jenkins Agent
```

can be a Docker container.

---

# Architecture

```text
Jenkins
   ↓
Docker Agent
   ↓
Build
```

---

# Example

```groovy
pipeline {

    agent {

        docker {

            image 'maven:3.9-eclipse-temurin-21'

        }

    }

    stages {

        stage('Build') {

            steps {

                sh 'mvn package'

            }

        }

    }

}
```

---

# Benefits

✔ Clean Environment

✔ Consistent Builds

✔ No Tool Installation Needed

✔ Easy Cleanup

---

# Docker Inside Jenkins Agents

Sometimes Jenkins needs to build images.

Requires Docker access.

Architecture:

```text
Jenkins Container
      ↓
Host Docker Daemon
      ↓
Build Images
```

---

# Docker Socket Mount

```bash
-v /var/run/docker.sock:/var/run/docker.sock
```

Allows Jenkins to access Docker daemon.

---

# Jenkins Container Example

```bash
docker run -d \
-p 8080:8080 \
-v jenkins_home:/var/jenkins_home \
-v /var/run/docker.sock:/var/run/docker.sock \
jenkins/jenkins:lts
```

---

# Docker-in-Docker (DinD)

Docker running inside Docker.

Architecture:

```text
Docker Container
      ↓
Docker Daemon
      ↓
Docker Build
```

---

# DinD Example

```bash
docker run --privileged docker:dind
```

---

# Advantages

✔ Isolation

✔ Independent Docker Environment

---

# Disadvantages

❌ Complex

❌ Performance Overhead

❌ Security Concerns

---

# Recommended Approach

Use:

```text
Docker Socket Mount
```

instead of DinD.

---

# Publishing Images to Docker Hub

After building:

```text
Push Image
```

to registry.

---

# Docker Hub Login

Store credentials in Jenkins.

Example:

```text
dockerhub-creds
```

---

# Pipeline Example

```groovy
stage('Docker Login') {

    steps {

        withCredentials([
            usernamePassword(
                credentialsId: 'dockerhub-creds',
                usernameVariable: 'USER',
                passwordVariable: 'PASS'
            )
        ]) {

            sh 'docker login -u $USER -p $PASS'

        }

    }

}
```

---

# Tag Image

```bash
docker tag myapp:v1 username/myapp:v1
```

---

# Push Image

```bash
docker push username/myapp:v1
```

---

# Pipeline Example

```groovy
stage('Push Docker Image') {

    steps {

        sh 'docker push username/myapp:v1'

    }

}
```

---

# Docker Hub Flow

```text
Build Image
      ↓
Tag Image
      ↓
Login
      ↓
Push
      ↓
Docker Hub
```

---

# Publishing Images to GHCR

GitHub Container Registry:

```text
ghcr.io
```

---

# Login to GHCR

Store:

```text
GitHub PAT
```

inside Jenkins Credentials.

---

# Example

```bash
docker login ghcr.io
```

---

# Tag Image

```bash
docker tag myapp:v1 ghcr.io/username/myapp:v1
```

---

# Push Image

```bash
docker push ghcr.io/username/myapp:v1
```

---

# Jenkins Pipeline Example

```groovy
stage('Push GHCR') {

    steps {

        sh 'docker push ghcr.io/company/myapp:v1'

    }

}
```

---

# GHCR Flow

```text
Build
 ↓
Tag
 ↓
Authenticate
 ↓
Push
 ↓
GHCR
```

---

# Complete Docker CI/CD Pipeline

```groovy
pipeline {

    agent any

    stages {

        stage('Checkout') {

            steps {

                git 'https://github.com/company/app.git'

            }

        }

        stage('Build') {

            steps {

                sh 'mvn package'

            }

        }

        stage('Docker Build') {

            steps {

                sh 'docker build -t myapp:v1 .'

            }

        }

        stage('Docker Push') {

            steps {

                sh 'docker push username/myapp:v1'

            }

        }

    }

}
```

---

# Enterprise Pipeline Flow

```text
GitHub
   ↓
Jenkins
   ↓
Build
   ↓
Unit Test
   ↓
Docker Build
   ↓
Docker Hub / GHCR
   ↓
Production Server
```

---

# Real-World Example

Spring Boot Application:

```text
Source Code
      ↓
mvn package
      ↓
app.jar
      ↓
docker build
      ↓
spring-app:v1
      ↓
docker push
      ↓
Docker Hub
```

---

# Best Practices

## Use Docker Agents

Cleaner build environments.

---

## Store Registry Credentials Securely

Use:

```text
Jenkins Credentials
```

Never hardcode passwords.

---

## Tag Images Properly

Example:

```text
v1.0
v1.1
latest
```

---

## Use Multi-Stage Builds

Smaller images.

---

## Scan Images

Before deployment:

```text
Trivy
Docker Scout
```

---

## Push Only Tested Images

Never push failed builds.

---

# Quick Revision Notes

## Docker Build

```bash
docker build -t app:v1 .
```

---

## Docker Push

```bash
docker push username/app:v1
```

---

## Docker Agent

```text
Container Used For Build Execution
```

---

## Docker Hub

```text
Public Container Registry
```

---

## GHCR

```text
GitHub Container Registry
```

---

## DinD

```text
Docker Inside Docker
```

---

# Viva Questions

### 1. Why integrate Docker with Jenkins?

To automate containerized deployments.

---

### 2. Which plugin enables Docker pipelines?

Docker Pipeline Plugin.

---

### 3. How do you build an image in Jenkins?

Using docker build command.

---

### 4. What is a Docker Agent?

A Docker container used as a Jenkins build agent.

---

### 5. What is DinD?

Docker running inside Docker.

---

### 6. What is GHCR?

GitHub Container Registry.

---

### 7. Where should Docker credentials be stored?

Jenkins Credentials Store.

---

### 8. What command pushes images?

docker push

---

### 9. Why use Docker Agents?

Consistent build environments.

---

### 10. What is Docker Hub?

A container image registry.

---

# Interview Questions

## Q1. Explain Docker and Jenkins Integration.

Jenkins builds, tests, packages, and publishes Docker images automatically as part of CI/CD pipelines.

---

## Q2. What is Docker-in-Docker?

Running a Docker daemon inside a Docker container.

---

## Q3. How can Jenkins push images to Docker Hub?

Using stored credentials and docker push commands.

---

## Q4. What are Docker Agents?

Containers used by Jenkins to execute builds in isolated environments.

---

## Q5. Why is Docker integration important in DevOps?

It enables automated, consistent, and portable application deployments.

---

# Key Takeaways

✔ Jenkins and Docker are commonly integrated in modern CI/CD pipelines.

✔ Docker images can be built automatically during builds.

✔ Docker Agents provide isolated execution environments.

✔ Images can be pushed to Docker Hub and GHCR.

✔ Credentials should always be stored securely.

✔ Dockerized CI/CD pipelines improve automation and deployment consistency.

---

# Summary

Docker and Jenkins together form a powerful CI/CD solution. Jenkins automates application builds, testing, Docker image creation, registry publishing, and deployments. By leveraging Docker Agents, Docker Hub, GHCR, and secure credential management, organizations can implement scalable and reliable container-based delivery pipelines.