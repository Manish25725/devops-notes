# Deployments to Servers & Cloud using GitHub Actions

![GitHub Actions](https://img.shields.io/badge/GitHub-Actions-black)
![Deployment](https://img.shields.io/badge/Deployment-Automation-blue)
![Cloud](https://img.shields.io/badge/Cloud-DevOps-green)
![Docker](https://img.shields.io/badge/Docker-Containers-orange)

---

# 📚 Table of Contents

- Introduction
- What is Deployment?
- Why Automate Deployments?
- Deployment Pipeline
- Deploying to VPS
- Deploying to AWS EC2
- Deploying to Azure VM
- Deploying to Self-Hosted Servers
- SSH Deployment
- GitHub Secrets for Deployment
- Docker-Based Deployments
- Production Deployment Workflow
- Deployment Strategies
- Blue-Green Deployment
- Rolling Deployment
- Canary Deployment
- Best Practices
- Viva Questions
- Interview Questions

---

# Introduction

Continuous Integration (CI) ensures code is:

```text
Built
Tested
Validated
```

The next step is:

```text
Deployment
```

Deployment means moving the application from development to a live environment where users can access it.

---

# What is Deployment?

Deployment is the process of releasing software to:

- Physical Servers
- Virtual Machines
- Cloud Platforms
- Containers
- Kubernetes Clusters

---

# Deployment Flow

```text
Developer Push
       ↓
Build
       ↓
Test
       ↓
Docker Image
       ↓
Deployment
       ↓
Production
```

---

# Why Automate Deployments?

Manual deployment involves:

```text
Login Server
Copy Files
Restart Services
Verify Application
```

Problems:

❌ Human errors

❌ Slow releases

❌ Inconsistent deployments

❌ Downtime risks

---

# Automated Deployment

```text
Code Push
      ↓
GitHub Actions
      ↓
Build
      ↓
Deploy Automatically
```

Benefits:

✔ Faster delivery

✔ Consistency

✔ Reduced errors

✔ Better reliability

---

# Typical Deployment Pipeline

```text
Push Code
      ↓
Build
      ↓
Run Tests
      ↓
Create Artifact
      ↓
Deploy Server
      ↓
Verify Health
```

---

# Deploying to VPS

A VPS (Virtual Private Server) is a virtual machine rented from providers like:

- DigitalOcean
- Linode
- Vultr
- Hostinger
- Contabo

---

# VPS Architecture

```text
GitHub Actions
        ↓
SSH
        ↓
VPS Server
        ↓
Application Deployment
```

---

# Example Deployment

```text
GitHub Actions
       ↓
Connect VPS
       ↓
Pull Latest Code
       ↓
Restart Application
```

---

# What is SSH?

SSH (Secure Shell) allows secure remote access to servers.

---

# Example

```bash
ssh ubuntu@123.45.67.89
```

---

# SSH Deployment Flow

```text
GitHub Actions
      ↓
SSH Connection
      ↓
Server
      ↓
Execute Commands
```

---

# GitHub Secrets for Deployment

Store credentials securely.

Repository:

```text
Settings
     ↓
Secrets and Variables
```

---

# Example Secrets

```text
HOST
USERNAME
SSH_PRIVATE_KEY
```

---

# Example Workflow

```yaml
- name: Deploy

  run: |

    ssh ubuntu@server-ip "cd app && git pull"
```

---

# Deploying to AWS EC2

AWS EC2 (Elastic Compute Cloud) is the most popular cloud VM service.

Official Website:

:contentReference[oaicite:0]{index=0}

---

# AWS Deployment Architecture

```text
GitHub Actions
       ↓
AWS EC2
       ↓
Docker Container
       ↓
Users
```

---

# EC2 Deployment Process

```text
Build Docker Image
      ↓
Push Docker Hub
      ↓
SSH into EC2
      ↓
Pull New Image
      ↓
Restart Container
```

---

# Example Commands

```bash
docker pull komaljoshi17/myapp:latest

docker stop myapp

docker rm myapp

docker run -d -p 80:80 komaljoshi17/myapp:latest
```

---

# AWS Deployment Flow

```text
Code Push
      ↓
GitHub Actions
      ↓
Docker Hub
      ↓
EC2 Pulls Image
      ↓
Deploy
```

---

# Deploying to Azure VM

Microsoft Azure provides Virtual Machines similar to AWS EC2.

Official Website:

:contentReference[oaicite:1]{index=1}

---

# Architecture

```text
GitHub Actions
       ↓
Azure VM
       ↓
Docker Container
```

---

# Deployment Steps

```text
Build Image
      ↓
Push Registry
      ↓
SSH Azure VM
      ↓
Run Container
```

---

# Self-Hosted Server Deployment

Many organizations deploy to internal servers.

Example:

```text
Company Data Center
```

---

# Architecture

```text
GitHub Actions
       ↓
Corporate Server
       ↓
Production Application
```

---

# Benefits

✔ Full Control

✔ Internal Network Access

✔ Compliance Requirements

---

# SSH Deployment Example

Install SSH action.

```yaml
- name: Deploy Server

  uses: appleboy/ssh-action@v1.0.3

  with:

    host: ${{ secrets.HOST }}

    username: ${{ secrets.USERNAME }}

    key: ${{ secrets.SSH_PRIVATE_KEY }}

    script: |

      cd /opt/myapp

      git pull

      systemctl restart myapp
```

---

# Workflow Execution

```text
GitHub Actions
      ↓
SSH Action
      ↓
Remote Server
      ↓
Execute Commands
```

---

# Docker-Based Deployment

Most modern deployments use containers.

---

# Flow

```text
Build Image
      ↓
Push Registry
      ↓
Pull Image
      ↓
Run Container
```

---

# Example

```bash
docker pull komaljoshi17/devopsapp:latest

docker stop devopsapp

docker rm devopsapp

docker run -d -p 80:80 komaljoshi17/devopsapp:latest
```

---

# Production Deployment Workflow

```yaml
name: Deploy

on:

  push:

    branches:

      - main

jobs:

  deploy:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v4

      - name: Deploy

        uses: appleboy/ssh-action@v1

        with:

          host: ${{ secrets.HOST }}

          username: ${{ secrets.USERNAME }}

          key: ${{ secrets.SSH_PRIVATE_KEY }}

          script: |

            docker pull komaljoshi17/myapp:latest

            docker restart myapp
```

---

# Deployment Strategies

Modern DevOps uses deployment strategies to reduce risk.

---

# Types

1. Basic Deployment
2. Rolling Deployment
3. Blue-Green Deployment
4. Canary Deployment

---

# Basic Deployment

```text
Stop Old Version
      ↓
Deploy New Version
```

Problem:

```text
Downtime
```

---

# Rolling Deployment

Servers updated one at a time.

---

# Example

```text
Server 1 Updated

Server 2 Updated

Server 3 Updated
```

Users continue using available servers.

---

# Rolling Deployment Diagram

```text
Server1 → Update

Server2 → Running

Server3 → Running
```

---

# Benefits

✔ Minimal Downtime

✔ Safer Releases

---

# Blue-Green Deployment

Two environments:

```text
Blue = Current Production

Green = New Version
```

---

# Flow

```text
Blue Environment
       ↓
Deploy Green
       ↓
Testing
       ↓
Switch Traffic
```

---

# Architecture

```text
Users
  ↓
Load Balancer

Blue (Live)

Green (Testing)
```

---

# Advantages

✔ Zero Downtime

✔ Easy Rollback

✔ Safe Testing

---

# Blue-Green Example

```text
Version 1 → Blue

Version 2 → Green

Switch Traffic → Green
```

---

# Canary Deployment

Deploy to a small percentage of users first.

---

# Example

```text
5% Users → New Version

95% Users → Old Version
```

If successful:

```text
100% Users → New Version
```

---

# Canary Benefits

✔ Risk Reduction

✔ Real User Testing

✔ Easy Monitoring

---

# Deployment Strategy Comparison

| Strategy | Downtime | Risk |
|-----------|----------|----------|
| Basic | High | High |
| Rolling | Low | Medium |
| Blue-Green | Zero | Low |
| Canary | Zero | Lowest |

---

# Real-World Enterprise Pipeline

```text
Developer Push
       ↓
GitHub Actions
       ↓
Build Docker Image
       ↓
Push Registry
       ↓
Deploy Staging
       ↓
Automated Testing
       ↓
Deploy Production
```

---

# Best Practices

✔ Use GitHub Secrets

✔ Never hardcode credentials

✔ Deploy using Docker

✔ Use Blue-Green for production

✔ Monitor application health

✔ Maintain rollback strategy

✔ Automate deployments

✔ Use HTTPS

---

# Quick Revision Notes

## Deployment

```text
Release application to production
```

---

## VPS

```text
Virtual Private Server
```

---

## EC2

```text
AWS Virtual Machine
```

---

## SSH

```text
Secure remote access
```

---

## Blue-Green

```text
Two environments
```

---

## Rolling

```text
One server at a time
```

---

## Canary

```text
Small user group first
```

---

# Viva Questions

### 1. What is deployment?

Releasing software to production environments.

---

### 2. Why automate deployment?

To reduce errors and increase speed.

---

### 3. What is SSH?

Secure Shell protocol for remote server access.

---

### 4. What is AWS EC2?

Amazon's virtual machine service.

---

### 5. What is Blue-Green Deployment?

Deployment using two separate environments.

---

### 6. What is Rolling Deployment?

Updating servers one at a time.

---

### 7. What is Canary Deployment?

Deploying to a small group of users first.

---

### 8. Why use GitHub Secrets?

To securely store deployment credentials.

---

# Interview Questions

## Q1. Explain CI/CD deployment flow.

```text
Build
 ↓
Test
 ↓
Package
 ↓
Deploy
```

---

## Q2. Difference between Rolling and Blue-Green Deployment?

Rolling:

```text
Update gradually
```

Blue-Green:

```text
Switch entire environment
```

---

## Q3. Why use Docker in deployments?

Consistency across environments.

---

## Q4. What is the safest deployment strategy?

Canary Deployment.

---

## Q5. How do GitHub Actions deploy to servers?

Using SSH and deployment actions.

---

# Key Terms

| Term | Meaning |
|--------|----------|
| Deployment | Release process |
| VPS | Virtual Private Server |
| EC2 | AWS VM |
| SSH | Secure remote access |
| Blue-Green | Dual environment deployment |
| Rolling | Gradual deployment |
| Canary | Partial rollout |

---

# Summary

GitHub Actions can automate deployments to:

✔ VPS Servers

✔ AWS EC2

✔ Azure VMs

✔ Self-Hosted Servers

✔ Docker Environments

Modern deployment strategies such as Rolling, Blue-Green, and Canary deployments help ensure reliable, scalable, and low-risk software releases.