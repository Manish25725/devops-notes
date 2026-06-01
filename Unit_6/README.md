# Unit VI – CI/CD with Jenkins

![Jenkins](https://img.shields.io/badge/Jenkins-CI/CD-red)
![DevOps](https://img.shields.io/badge/DevOps-Automation-blue)
![Docker](https://img.shields.io/badge/Docker-Integration-green)
![GitHub](https://img.shields.io/badge/GitHub-Actions-orange)
![Maven](https://img.shields.io/badge/Maven-Build_Tool-yellow)

---

# 📖 Overview

This repository contains comprehensive notes, practical examples, Jenkins pipelines, interview questions, viva preparation material, and hands-on labs for **Unit VI – CI/CD with Jenkins**.

The content covers Jenkins architecture, pipeline development, GitHub integration, Docker integration, Maven integration, deployment workflows, agents, backup strategies, and enterprise CI/CD best practices.

---

# 🎯 Learning Objectives

After completing this unit, you will be able to:

- Understand Jenkins Architecture
- Configure Jenkins Controller and Agents
- Create Freestyle and Pipeline Jobs
- Write Declarative and Scripted Pipelines
- Create Jenkinsfiles
- Configure GitHub Integration
- Configure Maven Builds
- Build Docker Images from Jenkins
- Push Images to Docker Hub and GHCR
- Deploy Applications Automatically
- Manage Artifacts and Reports
- Implement Enterprise CI/CD Pipelines

---

# 📂 Repository Structure

```text
Unit_6_Jenkins/

│
├── 01_Introduction_To_Jenkins.md
├── 02_Jenkins_Architecture_And_Installation.md
├── 03_Plugins_Security_And_User_Management.md
├── 04_Jenkins_Pipelines_Introduction.md
├── 05_Jenkins_Jobs_Freestyle_Vs_Pipeline.md
├── 06_Jenkins_Pipeline_Syntax_And_Jenkinsfile.md
├── 07_Pipeline_Stages_And_Artifacts.md
├── 08_Docker_And_Jenkins_Integration.md
├── 09_Jenkins_And_GitHub_Integration.md
├── 10_Jenkins_And_Maven_Integration.md
├── 11_Jenkins_Agents_And_Deployment_Flows.md
├── 12_Jenkins_Best_Practices_And_Interview_Preparation.md
├── 13_Practical_Labs_And_Projects.md
│
└── README.md
```

---

# 📚 Topics Covered

## 1. Jenkins Foundations

- Introduction to Jenkins
- Why Jenkins?
- CI/CD Concepts
- Jenkins Architecture
- Master-Agent Model
- Installation
- Jenkins Dashboard Overview

📄 File:

```text
01_Introduction_To_Jenkins.md
02_Jenkins_Architecture_And_Installation.md
```

---

## 2. Plugins, Security & User Management

- Plugin Management
- Installing Plugins
- Security Concepts
- Authentication
- Authorization
- User Roles
- Credentials Management

📄 File:

```text
03_Plugins_Security_And_User_Management.md
```

---

## 3. Jenkins Pipelines

- Freestyle Jobs
- Pipeline Jobs
- Pipeline as Code
- Declarative Pipeline
- Scripted Pipeline
- Jenkinsfile

📄 Files:

```text
04_Jenkins_Pipelines_Introduction.md
05_Jenkins_Jobs_Freestyle_Vs_Pipeline.md
06_Jenkins_Pipeline_Syntax_And_Jenkinsfile.md
```

---

## 4. Pipeline Stages

- Checkout
- Build
- Test
- Package
- Deploy
- Post Actions
- Artifact Management

📄 File:

```text
07_Pipeline_Stages_And_Artifacts.md
```

---

## 5. Docker Integration

- Docker Build
- Docker Agents
- Docker Plugin
- Docker-in-Docker
- Docker Hub Integration
- GitHub Container Registry (GHCR)

📄 File:

```text
08_Docker_And_Jenkins_Integration.md
```

---

## 6. GitHub Integration

- Git Plugin
- GitHub Plugin
- Webhooks
- PollSCM
- GitHub Authentication
- Multi-Branch Pipelines
- Pull Request Validation

📄 File:

```text
09_Jenkins_And_GitHub_Integration.md
```

---

## 7. Maven Integration

- Maven Installation
- Global Tool Configuration
- Maven Build Lifecycle
- Surefire Reports
- JaCoCo Coverage
- Artifact Archiving

📄 File:

```text
10_Jenkins_And_Maven_Integration.md
```

---

## 8. Agents & Deployment

- SSH Agents
- Docker Agents
- Cloud Agents
- Deployment Pipelines
- Server Deployments
- Cloud Deployments
- Shared Libraries

📄 File:

```text
11_Jenkins_Agents_And_Deployment_Flows.md
```

---

## 9. Best Practices & Interview Preparation

- Jenkins Best Practices
- Security Best Practices
- Pipeline Best Practices
- Backup & Recovery
- Common Interview Questions
- Scenario-Based Questions

📄 File:

```text
12_Jenkins_Best_Practices_And_Interview_Preparation.md
```

---

## 10. Practical Labs & Projects

- Freestyle Job Lab
- Pipeline Lab
- Maven Build Lab
- Docker Build Lab
- GitHub Webhook Lab
- Docker Hub Deployment
- GHCR Deployment
- Complete CI/CD Project

📄 File:

```text
13_Practical_Labs_And_Projects.md
```

---

# 🔄 Complete Jenkins CI/CD Workflow

```text
Developer
     ↓
GitHub Repository
     ↓
Webhook Trigger
     ↓
Jenkins
     ↓
Checkout Code
     ↓
Build Application
     ↓
Run Tests
     ↓
Generate Reports
     ↓
Package Artifact
     ↓
Build Docker Image
     ↓
Push Docker Image
     ↓
Deploy Application
```

---

# 🛠 Tools Covered

| Tool | Purpose |
|--------|----------|
| Jenkins | CI/CD Automation |
| GitHub | Source Control |
| Maven | Build Automation |
| Docker | Containerization |
| Docker Hub | Image Registry |
| GHCR | GitHub Container Registry |
| JUnit | Unit Testing |
| JaCoCo | Code Coverage |

---

# 📝 Important Jenkins Commands

### Check Jenkins Service

```bash
systemctl status jenkins
```

### Start Jenkins

```bash
systemctl start jenkins
```

### Stop Jenkins

```bash
systemctl stop jenkins
```

### Restart Jenkins

```bash
systemctl restart jenkins
```

### Check Docker

```bash
docker ps
```

### Build Maven Project

```bash
mvn clean package
```

---

# 🎓 Viva Preparation

Important Viva Topics:

- What is Jenkins?
- What is CI/CD?
- What is Pipeline as Code?
- What is a Jenkinsfile?
- Difference between Freestyle and Pipeline Jobs
- What are Agents?
- What is a Webhook?
- What is PollSCM?
- How Jenkins integrates with Docker?
- How Jenkins integrates with Maven?
- What is Artifact Management?
- What are Shared Libraries?
- What is GHCR?
- What is Docker Hub?
- What is JaCoCo?

---

# 💼 Interview Preparation Topics

Most Frequently Asked:

1. Jenkins Architecture
2. Controller-Agent Model
3. Jenkinsfile
4. Declarative vs Scripted Pipeline
5. GitHub Integration
6. Webhooks vs PollSCM
7. Maven Integration
8. Docker Integration
9. Docker Agents
10. Shared Libraries
11. Backup & Recovery
12. Artifact Management
13. CI/CD Best Practices
14. Credentials Management
15. Deployment Strategies

---

# 🚀 Mini Projects Included

### Project 1

```text
Java Maven CI Pipeline
```

---

### Project 2

```text
Spring Boot + Docker + Jenkins
```

---

### Project 3

```text
GitHub → Jenkins → Docker Hub → Deployment
```

---


### Project 4

```text
GitHub → Jenkins → GHCR → Deployment
```

---

# 📌 Unit VI Syllabus Mapping

| Syllabus Topic | Covered |
|---------------|----------|
| Jenkins Architecture | ✅ |
| Master-Agent Model | ✅ |
| Installation & UI | ✅ |
| Plugins Management | ✅ |
| Security & Roles | ✅ |
| Freestyle Jobs | ✅ |
| Pipeline Jobs | ✅ |
| Declarative Pipeline | ✅ |
| Scripted Pipeline | ✅ |
| Jenkinsfile | ✅ |
| Parameters | ✅ |
| Environment Variables | ✅ |
| Multi-Branch Pipelines | ✅ |
| Checkout Code | ✅ |
| Build/Test/Package | ✅ |
| Post Actions | ✅ |
| Artifact Management | ✅ |
| Docker Integration | ✅ |
| Docker Hub | ✅ |
| GHCR | ✅ |
| GitHub Integration | ✅ |
| Backup & Restore | ✅ |
| Maven Integration | ✅ |
| Test Reports | ✅ |
| Code Coverage | ✅ |
| PollSCM | ✅ |
| Webhooks | ✅ |
| Pipeline Libraries | ✅ |
| SSH Agents | ✅ |
| Container Agents | ✅ |
| Deployments | ✅ |

---

# 🏆 Outcome

After completing this unit, students will be able to design, implement, and manage enterprise-grade Jenkins CI/CD pipelines integrated with GitHub, Maven, Docker, Docker Hub, GHCR, and cloud deployment platforms.

---

⭐ This repository serves as a complete study guide, lab manual, viva handbook, and interview preparation resource for **Unit VI – CI/CD with Jenkins (INT332)**.