# DevOps Basics & Why Docker?

![DevOps](https://img.shields.io/badge/DevOps-CI%2FCD-blue)
![Docker](https://img.shields.io/badge/Docker-Containers-green)
![Automation](https://img.shields.io/badge/Automation-Deployment-orange)
![Cloud](https://img.shields.io/badge/Cloud-Native-red)
![Infrastructure](https://img.shields.io/badge/Infrastructure-Modern-purple)

---

# 📚 Table of Contents

- [Overview](#-overview)
- [What is DevOps?](#-what-is-devops)
- [Need for DevOps](#-need-for-devops)
- [Traditional Development Model](#-traditional-development-model)
- [Problems in Traditional Approach](#-problems-in-traditional-approach)
- [DevOps Lifecycle](#-devops-lifecycle)
- [DevOps vs Agile vs Lean](#-devops-vs-agile-vs-lean)
- [Benefits of DevOps](#-benefits-of-devops)
- [Introduction to Containers](#-introduction-to-containers)
- [Before Docker](#-before-docker)
- [Emergence of Modern Containerization](#-emergence-of-modern-containerization)
- [Why Docker?](#-why-docker)
- [Problems Solved by Containers](#-problems-solved-by-containers)
- [DevOps Toolchain](#-devops-toolchain)
- [CI/CD Pipeline](#-cicd-pipeline)
- [Course Focus](#-course-focus)
- [Important Terminologies](#-important-terminologies)
- [Quick Revision Notes](#-quick-revision-notes)
- [Viva Questions](#-viva-questions)
- [Interview Questions](#-interview-questions)
- [Conclusion](#-conclusion)

---

# 📖 Overview

Modern software development requires:
- Faster releases
- Better collaboration
- Automation
- Scalability
- Reliable deployments

Traditional software development approaches were slow and inefficient.

To solve these problems, the software industry introduced:
- DevOps
- Containers
- Docker
- CI/CD pipelines

This topic introduces:
- DevOps fundamentals
- Need for Docker
- Containerization basics
- DevOps lifecycle
- Modern infrastructure concepts

---

# 🚀 What is DevOps?

DevOps combines:

```text
Development (Dev)
        +
Operations (Ops)
```

to improve:
- Collaboration
- Automation
- Deployment speed
- Software quality

---

# 🧠 Definition

> DevOps is a modern software development approach that combines Development and Operations teams to automate and improve the software delivery lifecycle.

---

# 🎯 Main Goal of DevOps

```text
Write Code Faster
        ↓
Test Automatically
        ↓
Deploy Quickly
        ↓
Monitor Continuously
        ↓
Improve Continuously
```

---

# 🔥 Need for DevOps

Traditional software development models faced many challenges.

---

# Problems in Traditional Systems

| Problem | Description |
|---|---|
| Separate Teams | Developers and operations worked independently |
| Slow Releases | Deployments took weeks or months |
| Deployment Failures | Applications failed in production |
| Poor Communication | Frequent misunderstandings |
| Manual Work | Repetitive tasks caused errors |
| Environment Issues | "Works on my machine" problem |

---

# Example Problem

```text
Developer Machine → Application Works
Production Server → Application Fails
```

---

# Why?

Different:
- Libraries
- Operating systems
- Dependencies
- Configurations

---

# ✅ DevOps Solution

DevOps introduces:
- Collaboration
- Automation
- Monitoring
- Continuous delivery

---

# Traditional vs DevOps Approach

| Traditional Model | DevOps Model |
|---|---|
| Separate teams | Shared responsibility |
| Manual deployment | Automated deployment |
| Slow releases | Frequent releases |
| Reactive monitoring | Continuous monitoring |
| Long feedback cycle | Fast feedback cycle |

---

# 🏛️ Traditional Development Model

---

# Traditional Workflow

```text
Requirement
      ↓
Development
      ↓
Testing
      ↓
Operations
      ↓
Deployment
```

---

# Problems

```text
✔ Communication delays
✔ Blame culture
✔ Slow deployment
✔ Difficult debugging
✔ Long release cycles
```

---

# 🚀 DevOps Lifecycle

DevOps follows a continuous lifecycle.

---

# DevOps Workflow

```text
Plan
  ↓
Code
  ↓
Build
  ↓
Test
  ↓
Deploy
  ↓
Monitor
  ↓
Feedback
  ↓
Improve
```

---

# 📊 DevOps Lifecycle Stages

| Stage | Purpose |
|---|---|
| Plan | Define project requirements |
| Code | Write application code |
| Build | Compile/package application |
| Test | Automated testing |
| Deploy | Release application |
| Monitor | Observe application health |
| Feedback | Improve continuously |

---

# 🛠️ DevOps Toolchain

---

# Planning Tools

| Tool | Purpose |
|---|---|
| Jira | Project management |
| Azure Boards | Sprint planning |
| GitHub Projects | Task management |

---

# Code Management

| Tool | Purpose |
|---|---|
| GitHub | Version control |
| GitLab | Repository management |
| Bitbucket | Source code hosting |

---

# Build Tools

| Tool | Purpose |
|---|---|
| Maven | Java builds |
| Gradle | Java automation |
| npm | Node.js packages |

---

# Testing Tools

| Tool | Purpose |
|---|---|
| JUnit | Java testing |
| pytest | Python testing |
| Selenium | UI testing |

---

# Deployment Tools

| Tool | Purpose |
|---|---|
| Docker | Containerization |
| Kubernetes | Orchestration |
| Jenkins | CI/CD automation |
| Ansible | Configuration management |

---

# Monitoring Tools

| Tool | Purpose |
|---|---|
| Prometheus | Metrics collection |
| Grafana | Visualization |
| ELK Stack | Logging |

---

# 🔄 CI/CD Pipeline

---

# CI = Continuous Integration

Developers continuously:
- Push code
- Run automated tests
- Merge changes

---

# CD = Continuous Deployment

Applications automatically:
- Build
- Deploy
- Update production

---

# CI/CD Workflow

```text
Developer Pushes Code
            ↓
Automated Build
            ↓
Automated Testing
            ↓
Docker Image Created
            ↓
Deployment
            ↓
Monitoring
```

---

# ⚔️ DevOps vs Agile vs Lean

| Concept | Focus |
|---|---|
| Agile | Faster software development |
| Lean | Eliminate waste |
| DevOps | Faster development + deployment |

---

# 🔹 Agile

Agile focuses on:
- Sprint-based development
- Iterative development
- Rapid coding

---

# 🔹 Lean

Lean focuses on:
- Reducing waste
- Improving efficiency
- Resource optimization

---

# 🔹 DevOps

DevOps combines:
- Agile principles
- Lean principles
- Operations automation

---

# Result

```text
✔ Faster software delivery
✔ Better collaboration
✔ Continuous improvement
```

---

# 📦 Introduction to Containers

Containers are lightweight isolated environments used to run applications.

---

# 🧠 Definition

> A container is a lightweight, isolated environment that packages an application along with all dependencies required to run it.

---

# Before Containers

Applications were deployed:
- Directly on servers
- Inside Virtual Machines

---

# Problems

```text
✔ Dependency conflicts
✔ Slow startup
✔ Heavy infrastructure
✔ Resource wastage
✔ Difficult scaling
```

---

# 🌍 Emergence of Modern Containerization

Modern containerization became popular because organizations needed:
- Faster deployment
- Better scalability
- Portability
- Efficient resource usage

---

# Containerization Workflow

```text
Application
      +
Dependencies
      ↓
Container Image
      ↓
Run Anywhere
```

---

# Benefits of Containers

| Benefit | Description |
|---|---|
| Lightweight | Low resource usage |
| Portable | Works everywhere |
| Fast Startup | Seconds to start |
| Scalable | Easy replication |
| Isolated | Separate execution environment |

---

# 🐳 Why Docker?

Docker is the most popular containerization platform.

---

# Docker Provides

```text
✔ Easy container creation
✔ Image management
✔ Portability
✔ Scalability
✔ Fast deployment
```

---

# Before Docker

---

# Traditional Deployment

```text
Install OS
Install Dependencies
Configure Environment
Deploy Application
```

---

# Problems

```text
✔ Slow deployment
✔ Environment mismatch
✔ Heavy virtual machines
✔ Complex setup
```

---

# After Docker

```text
Build Docker Image
        ↓
Run Container Anywhere
```

---

# 🌟 Problems Solved by Containers

---

# 1️⃣ "Works on My Machine" Problem

Same container image works everywhere.

---

# Example

```text
Developer Laptop
        ↓
Testing Server
        ↓
Production Server

Same Container Everywhere
```

---

# 2️⃣ Faster Deployment

Containers start within:
- Seconds
- Milliseconds

---

# 3️⃣ Better Resource Utilization

Containers share host operating system.

---

# Result

```text
✔ More applications per server
✔ Lower infrastructure cost
```

---

# 4️⃣ Scalability

Containers can scale quickly.

---

# Example

```text
Traffic increases
        ↓
Start more containers
```

---

# 🏗️ Monolithic vs Containerized Applications

| Monolithic Apps | Containerized Apps |
|---|---|
| Large applications | Small services |
| Difficult scaling | Easy scaling |
| Heavy infrastructure | Lightweight |
| Slow deployment | Fast deployment |
| Tight coupling | Independent containers |

---

# 🌐 Microservices + Containers

Containers work perfectly with microservices.

---

# Example

```text
User Service Container
Payment Service Container
Order Service Container
Notification Service Container
```

Each service runs independently.

---

# 🏛️ Docker Architecture Overview

Docker architecture contains:

---

# Components

| Component | Purpose |
|---|---|
| Docker CLI | User commands |
| Docker Daemon | Background service |
| Docker Images | Templates |
| Containers | Running applications |
| Docker Hub | Image registry |

---

# Docker Workflow

```text
Docker CLI
      ↓
Docker Daemon
      ↓
Docker Images
      ↓
Containers
```

---

# 🧩 Docker Object Types

| Object | Purpose |
|---|---|
| Image | Blueprint/template |
| Container | Running instance |
| Network | Communication |
| Volume | Persistent storage |

---

# 📦 Container Images & Layers

Docker images are built using layers.

---

# Example

```text
Ubuntu Base Layer
       ↓
Node.js Layer
       ↓
Application Layer
```

---

# Benefits

```text
✔ Faster builds
✔ Image caching
✔ Smaller downloads
✔ Reusability
```

---

# 🌐 Image Registries & Distribution

Docker images are stored in registries.

---

# Popular Registries

| Registry | Purpose |
|---|---|
| Docker Hub | Public registry |
| AWS ECR | Amazon registry |
| Azure ACR | Azure registry |
| Google GCR | Google registry |

---

# ⚙️ Process Isolation & Namespaces

Containers use namespaces for isolation.

---

# Types of Isolation

| Namespace | Purpose |
|---|---|
| PID | Process isolation |
| Network | Network separation |
| Mount | Filesystem isolation |
| User | User isolation |

---

# Result

```text
✔ Containers isolated
✔ Better security
✔ Independent execution
```

---

# 🧠 cgroups (Control Groups)

cgroups limit resource usage.

---

# Example

```yaml
memory: 512MB
cpu: 1
```

---

# Benefits

```text
✔ Resource control
✔ Prevent overload
✔ Better performance
```

---

# 🎯 Course Focus (INT332)

This course mainly focuses on:

```text
✔ Docker
✔ Docker Compose
✔ Maven
✔ GitHub Actions
✔ Jenkins
✔ CI/CD
✔ Containers
```

---

# 📊 Marks Distribution

| Component | Marks |
|---|---|
| Project | 30 |
| GitHub Repository | 30 |
| Minor | 5 |
| AT2 | 45 |

---

# 💻 Requirements

To practice DevOps concepts you need:

- Docker Desktop
- AWS EC2 (optional)
- GitHub account
- Linux basics

---

# 🧠 Important Terminologies

| Term | Meaning |
|---|---|
| DevOps | Development + Operations |
| Container | Lightweight isolated environment |
| Docker | Container platform |
| Image | Container template |
| CI/CD | Continuous Integration & Deployment |
| Microservices | Independent services |
| Registry | Store container images |
| Volume | Persistent storage |

---

# 📌 Quick Revision Notes

| Topic | Key Point |
|---|---|
| DevOps | Faster software delivery |
| CI/CD | Automated deployment |
| Docker | Containerization platform |
| Containers | Lightweight virtualization |
| Images | Templates for containers |
| Registries | Store images |
| cgroups | Resource limits |
| Namespaces | Isolation |

---

# ❓ Viva Questions

1. What is DevOps?
2. Why is DevOps needed?
3. Difference between Agile and DevOps?
4. What are containers?
5. Why use Docker?
6. What is CI/CD?
7. What are Docker images?
8. What are namespaces?
9. What are cgroups?
10. What is Docker Hub?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| What problem does Docker solve? | Environment consistency |
| Why are containers lightweight? | Shared OS kernel |
| What is CI/CD? | Automated integration and deployment |
| What is container isolation? | Separate execution environments |
| Difference between image and container? | Template vs running instance |

---

# 📌 Key Takeaway

Modern DevOps infrastructure combines:

```text
DevOps
    ↓
Automation
    ↓
Containers
    ↓
Docker
    ↓
CI/CD
    ↓
Cloud-Native Applications
```

These technologies enable:
- Faster deployment
- Better scalability
- Improved reliability
- Continuous delivery

---

# ✅ Conclusion

DevOps transformed software development by improving:
- Collaboration
- Automation
- Deployment speed
- Application reliability

Containers and Docker solved major infrastructure challenges such as:
- Environment inconsistency
- Slow deployments
- Resource wastage
- Scalability issues

Together, DevOps and Docker form the foundation of modern cloud-native application development.

---

# 🔗 Next Topic

➡️ Virtual Machines vs Containers