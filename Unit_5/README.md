# 🚀 Unit V – Continuous Integration (CI) with GitHub Actions

> Comprehensive notes, practical workflows, deployment pipelines, Docker integration, runners, and interview preparation for GitHub Actions.

![GitHub Actions](https://img.shields.io/badge/GitHub-Actions-black)
![CI/CD](https://img.shields.io/badge/CI/CD-Automation-green)
![Docker](https://img.shields.io/badge/Docker-Integration-blue)
![DevOps](https://img.shields.io/badge/DevOps-Unit_V-orange)

---

# 📚 Unit Overview

This unit focuses on **Continuous Integration (CI)** using **GitHub Actions**, one of the most popular automation platforms used in modern DevOps pipelines.

You will learn how to:

- Automate builds and testing
- Trigger workflows automatically
- Use GitHub-hosted and self-hosted runners
- Build and push Docker images
- Deploy applications to servers and cloud platforms
- Design production-ready CI/CD pipelines

---

# 📂 Repository Structure

```text
Unit_5/
│
├── 01_Introduction_To_CI_And_GitHub_Actions.md
├── 02_Workflow_Structure_And_Components.md
├── 03_Workflow_Triggers.md
├── 04_Jobs_Steps_Actions_And_Runners.md
├── 05_Matrix_Strategies_And_Multi_Job_Workflows.md
├── 06_Marketplace_Actions_And_Caching.md
├── 07_GitHub_Hosted_And_Self_Hosted_Runners.md
├── 08_Docker_And_GitHub_Actions.md
├── 09_Deployments_To_Servers_And_Cloud.md
├── 10_GitHub_Actions_Interview_Preparation_And_Practice.md
└── README.md
```

---

# 🎯 Topics Covered

## 1️⃣ Introduction to CI & GitHub Actions

📄 `01_Introduction_To_CI_And_GitHub_Actions.md`

Topics:

- Continuous Integration (CI)
- Why CI is important
- Traditional vs Modern Development
- Benefits of CI
- Introduction to GitHub Actions
- CI/CD Pipeline Overview

---

## 2️⃣ Workflow Structure & Components

📄 `02_Workflow_Structure_And_Components.md`

Topics:

- Workflow Files
- YAML Basics
- Workflow Directory Structure
- Jobs
- Steps
- Actions
- Runners
- Workflow Architecture

---

## 3️⃣ Workflow Triggers

📄 `03_Workflow_Triggers.md`

Topics:

- push
- pull_request
- workflow_dispatch
- schedule
- release
- tag triggers
- trigger filtering

Example:

```yaml
on:
  push:
    branches:
      - main
```

---

## 4️⃣ Jobs, Steps, Actions & Runners

📄 `04_Jobs_Steps_Actions_And_Runners.md`

Topics:

- Jobs
- Steps
- Reusable Actions
- Marketplace Actions
- Runner Architecture
- Job Dependencies

Example:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
```

---

## 5️⃣ Matrix Strategies & Multi-Job Workflows

📄 `05_Matrix_Strategies_And_Multi_Job_Workflows.md`

Topics:

- Matrix Builds
- Parallel Execution
- Job Dependencies
- Artifact Sharing
- Enterprise Workflow Design

Example:

```yaml
strategy:
  matrix:
    java: [17,21]
```

---

## 6️⃣ Marketplace Actions & Caching

📄 `06_Marketplace_Actions_And_Caching.md`

Topics:

- GitHub Marketplace
- Popular Actions
- Dependency Caching
- Maven Cache
- NPM Cache
- Performance Optimization

Example:

```yaml
uses: actions/cache@v4
```

---

## 7️⃣ GitHub Hosted & Self-Hosted Runners

📄 `07_GitHub_Hosted_And_Self_Hosted_Runners.md`

Topics:

- Hosted Runners
- Self-Hosted Runners
- Runner Installation
- Runner Security
- Runner Management
- Enterprise Infrastructure

Supported Runners:

```text
ubuntu-latest
windows-latest
macos-latest
self-hosted
```

---

## 8️⃣ Docker & GitHub Actions

📄 `08_Docker_And_GitHub_Actions.md`

Topics:

- Building Docker Images
- Docker Login
- Docker Hub Integration
- GitHub Container Registry (GHCR)
- Docker Buildx
- Multi-Platform Images
- Image Tagging
- Docker Security

Example:

```yaml
uses: docker/build-push-action@v6
```

---

## 9️⃣ Deployments to Servers & Cloud

📄 `09_Deployments_To_Servers_And_Cloud.md`

Topics:

- VPS Deployment
- AWS EC2 Deployment
- Azure VM Deployment
- SSH Deployment
- Docker Deployment
- Production Deployment Pipelines
- Blue-Green Deployment
- Rolling Deployment
- Canary Deployment

---

## 🔟 Interview Preparation & Practice

📄 `10_GitHub_Actions_Interview_Preparation_And_Practice.md`

Includes:

- 50 Viva Questions
- 30 Interview Questions
- Hands-On Labs
- YAML Debugging
- Workflow Troubleshooting
- End-Term Revision Notes
- GitHub Actions Cheatsheet

---

# 🔄 GitHub Actions Workflow Architecture

```text
Developer Pushes Code
           │
           ▼
      GitHub Repository
           │
           ▼
       Workflow Trigger
           │
           ▼
          Jobs
           │
           ▼
         Steps
           │
           ▼
        Actions
           │
           ▼
         Runner
           │
           ▼
      Build / Test
           │
           ▼
     Docker Image
           │
           ▼
        Registry
           │
           ▼
       Deployment
```

---

# 🚀 CI/CD Pipeline Overview

```text
Code Commit
     │
     ▼
GitHub Push
     │
     ▼
GitHub Actions
     │
     ▼
Build
     │
     ▼
Testing
     │
     ▼
Docker Build
     │
     ▼
Push Registry
     │
     ▼
Deploy Server
```

---

# 🛠 Technologies Covered

| Category | Technologies |
|-----------|-------------|
| Version Control | Git, GitHub |
| CI/CD | GitHub Actions |
| Containers | Docker |
| Registry | Docker Hub, GHCR |
| Cloud | AWS EC2, Azure VM |
| Deployment | SSH, Docker |
| Automation | Workflows |
| Infrastructure | Hosted & Self-Hosted Runners |

---

# 📋 Important GitHub Actions Components

| Component | Purpose |
|------------|---------|
| Workflow | Automation Definition |
| Job | Collection of Steps |
| Step | Individual Task |
| Action | Reusable Automation |
| Runner | Execution Environment |
| Trigger | Starts Workflow |
| Cache | Speeds Up Builds |
| Artifact | Shares Files Between Jobs |

---

# ⚡ Common Workflow Example

```yaml
name: CI Pipeline

on:
  push:
    branches:
      - main

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v4

      - name: Build

        run: echo "Build Successful"
```

---

# 🎓 Learning Outcomes

After completing this unit, you will be able to:

✅ Understand Continuous Integration (CI)

✅ Create GitHub Actions workflows

✅ Configure workflow triggers

✅ Build multi-job pipelines

✅ Use GitHub Marketplace Actions

✅ Implement caching strategies

✅ Configure runners

✅ Build Docker images in CI

✅ Push images to Docker Hub & GHCR

✅ Deploy applications automatically

✅ Implement production deployment strategies

✅ Debug and troubleshoot workflows

---

# 📌 Quick Revision

### CI

```text
Continuous Integration
```

### Workflow

```text
Automation File
```

### Job

```text
Collection of Steps
```

### Runner

```text
Machine Executing Workflow
```

### Docker Hub

```text
Container Registry
```

### GHCR

```text
GitHub Container Registry
```

### Blue-Green Deployment

```text
Dual Environment Deployment
```

### Canary Deployment

```text
Partial User Rollout
```

---

# 🎯 Unit V Syllabus Mapping

| Syllabus Topic | Covered In |
|---------------|------------|
| Understanding Workflow Automation | File 01 |
| Workflow Directory Structure | File 02 |
| Workflows, Jobs, Steps | Files 02 & 04 |
| Actions & Runners | Files 04 & 07 |
| Workflow Triggers | File 03 |
| Matrix Strategies | File 05 |
| Shell Commands | File 04 |
| Marketplace Actions | File 06 |
| Caching | File 06 |
| Multi-Job Workflows | File 05 |
| GitHub Hosted Runners | File 07 |
| Self-Hosted Runners | File 07 |
| Docker Build in CI | File 08 |
| Docker Hub Push | File 08 |
| GHCR Push | File 08 |
| Deployments | File 09 |

---

# 🏆 Conclusion

GitHub Actions is a powerful CI/CD platform that enables developers and DevOps engineers to automate software delivery pipelines.

By mastering workflows, runners, Docker integration, and deployment strategies, you gain the skills required to build modern, production-ready DevOps pipelines used across the software industry.

---

## 👨‍💻 Author

**Komal Joshi**

**Course:** INT332 – DevOps and Containers

**Unit:** Unit V – Continuous Integration (CI) with GitHub Actions

**Repository Type:** Academic Notes + Practical Labs + Interview Preparation

---