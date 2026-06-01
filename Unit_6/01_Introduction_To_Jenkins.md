# Introduction to Jenkins

![Jenkins](https://img.shields.io/badge/Jenkins-CI/CD-red)
![DevOps](https://img.shields.io/badge/DevOps-Automation-blue)
![Automation](https://img.shields.io/badge/Build-Automation-green)
![Open Source](https://img.shields.io/badge/Open_Source-Free-orange)

---

# 📚 Table of Contents

- What is Jenkins?
- Why Jenkins Was Created
- Problems Before Jenkins
- Need for Continuous Integration
- Jenkins in DevOps
- Features of Jenkins
- Jenkins Ecosystem
- Jenkins Workflow
- Advantages of Jenkins
- Limitations of Jenkins
- Real-World Use Cases
- Jenkins vs GitHub Actions
- Jenkins Terminology
- Quick Revision Notes
- Viva Questions
- Interview Questions

---

# What is Jenkins?

**Jenkins** is an open-source automation server used to automate the software development lifecycle.

It helps developers automate:

- Building applications
- Running tests
- Packaging software
- Deploying applications
- Monitoring delivery pipelines

Jenkins is one of the most popular tools used in **Continuous Integration (CI)** and **Continuous Delivery (CD)**.

---

# Definition

> Jenkins is an open-source automation tool written in Java that helps automate building, testing, and deploying software applications.

---

# Why Jenkins Was Created?

Before Jenkins, software development teams faced many challenges:

### Traditional Workflow

```text
Developer Writes Code
        ↓
Manual Build
        ↓
Manual Testing
        ↓
Manual Deployment
```

Problems:

❌ Slow releases

❌ Human errors

❌ Repetitive tasks

❌ Difficult collaboration

❌ Delayed bug detection

---

# Problems Before Jenkins

## Problem 1: Manual Builds

Developers had to manually compile projects.

Example:

```bash
javac Main.java
```

For large projects:

```text
Hundreds of Files
Thousands of Dependencies
```

Manual builds became difficult.

---

## Problem 2: Delayed Testing

Testing occurred only after major development milestones.

Result:

```text
More Bugs
Long Debugging Cycles
```

---

## Problem 3: Integration Issues

Multiple developers worked on different modules.

When code was merged:

```text
Code Conflicts
Build Failures
Dependency Problems
```

---

## Problem 4: Slow Deployment

Deployment involved:

- Copying files manually
- Configuring servers manually
- Restarting services manually

Result:

```text
Slow Releases
```

---

# Need for Continuous Integration (CI)

Continuous Integration (CI) is a development practice where code changes are automatically:

```text
Integrated
Built
Tested
Validated
```

whenever developers commit code.

---

# CI Workflow

```text
Developer Pushes Code
          ↓
Source Repository
          ↓
Automatic Build
          ↓
Automatic Test
          ↓
Feedback
```

---

# What Jenkins Solves

Jenkins automates:

✔ Build Process

✔ Testing

✔ Packaging

✔ Deployment

✔ Notifications

✔ Monitoring

---

# Jenkins in DevOps

DevOps aims to improve collaboration between:

```text
Development Team
        +
Operations Team
```

Jenkins acts as the automation engine.

---

# DevOps Pipeline

```text
Plan
 ↓
Code
 ↓
Build
 ↓
Test
 ↓
Release
 ↓
Deploy
 ↓
Operate
 ↓
Monitor
```

Jenkins automates:

```text
Build
Test
Release
Deploy
```

---

# Jenkins Ecosystem

Jenkins integrates with many tools.

```text
GitHub
GitLab
Docker
Maven
Gradle
Kubernetes
AWS
Azure
SonarQube
Ansible
Terraform
```

---

# Jenkins Integration Architecture

```text
Developer
     ↓
GitHub
     ↓
Jenkins
     ↓
Build
     ↓
Test
     ↓
Docker
     ↓
Deploy
```

---

# Features of Jenkins

## 1. Open Source

Jenkins is completely free.

Benefits:

- No license cost
- Large community
- Continuous updates

---

## 2. Platform Independent

Runs on:

- Windows
- Linux
- macOS

Because Jenkins is Java-based.

---

## 3. Plugin Ecosystem

One of Jenkins' biggest strengths.

More than:

```text
2000+ Plugins
```

available.

Examples:

- Git Plugin
- Docker Plugin
- Maven Plugin
- Pipeline Plugin
- Kubernetes Plugin

---

## 4. Automation

Automates repetitive tasks:

```text
Build
Test
Deploy
```

---

## 5. Continuous Integration

Automatically builds code after commits.

---

## 6. Continuous Delivery

Deploys applications automatically.

---

## 7. Distributed Builds

Can use multiple machines.

```text
Master
   ↓
Agents
```

Allows faster builds.

---

## 8. Pipeline as Code

Pipeline definitions stored in:

```text
Jenkinsfile
```

Benefits:

✔ Version Controlled

✔ Reproducible

✔ Easy Collaboration

---

# Jenkins Workflow

## Step 1

Developer pushes code.

```text
GitHub
```

---

## Step 2

Jenkins detects changes.

---

## Step 3

Build starts.

Example:

```bash
mvn clean package
```

---

## Step 4

Tests execute.

Example:

```bash
mvn test
```

---

## Step 5

Artifact generated.

Example:

```text
app.jar
```

---

## Step 6

Deployment starts.

---

# Jenkins Pipeline Flow

```text
Code Commit
      ↓
Jenkins Trigger
      ↓
Checkout Code
      ↓
Build
      ↓
Test
      ↓
Package
      ↓
Deploy
```

---

# Real-World Example

Consider an E-Commerce Website.

Developers push code:

```text
GitHub
```

Jenkins automatically:

```text
Builds Project
Runs Tests
Creates Docker Image
Pushes Docker Image
Deploys Application
```

Without manual effort.

---

# Advantages of Jenkins

| Advantage | Description |
|------------|------------|
| Open Source | Free to use |
| Automation | Reduces manual work |
| Large Plugin Ecosystem | Supports many tools |
| Platform Independent | Works everywhere |
| CI/CD Support | Full automation |
| Scalability | Supports large projects |
| Community Support | Huge ecosystem |

---

# Limitations of Jenkins

| Limitation | Description |
|------------|------------|
| Complex Setup | Initial setup may be difficult |
| Plugin Management | Too many plugins can create issues |
| Maintenance Required | Server updates needed |
| UI Can Feel Outdated | Compared to modern platforms |

---

# Jenkins vs GitHub Actions

| Feature | Jenkins | GitHub Actions |
|----------|----------|----------|
| Open Source | Yes | No |
| Hosting | Self-hosted | GitHub |
| Plugins | 2000+ | Marketplace |
| Flexibility | Very High | High |
| Maintenance | Required | Minimal |
| Cost | Free | Usage-based |
| Enterprise Use | Very Common | Growing |

---

# Where Jenkins is Used?

Industries using Jenkins:

- Banking
- Healthcare
- E-Commerce
- FinTech
- Telecom
- Cloud Computing

Companies:

- Netflix
- Adobe
- LinkedIn
- IBM
- Cisco

---

# Common Jenkins Use Cases

## Build Automation

```bash
mvn clean package
```

---

## Test Automation

```bash
mvn test
```

---

## Docker Image Creation

```bash
docker build -t app:v1 .
```

---

## Deployment

```bash
docker run app:v1
```

---

## Monitoring Build Status

```text
Success
Failed
Aborted
Running
```

---

# Jenkins Terminology

| Term | Meaning |
|---------|----------|
| Job | Task executed by Jenkins |
| Build | Execution of a Job |
| Pipeline | CI/CD Workflow |
| Jenkinsfile | Pipeline definition |
| Plugin | Jenkins extension |
| Node | Machine running Jenkins |
| Agent | Worker machine |
| Artifact | Generated build file |
| Workspace | Build directory |

---

# Quick Revision Notes

## Jenkins

```text
Open Source Automation Server
```

---

## Purpose

```text
Build + Test + Deploy Automation
```

---

## Language

```text
Java
```

---

## CI

```text
Continuous Integration
```

---

## CD

```text
Continuous Delivery
```

---

## Pipeline

```text
Automated Workflow
```

---

## Jenkinsfile

```text
Pipeline as Code
```

---

# Viva Questions

### 1. What is Jenkins?

An open-source automation server used for CI/CD.

---

### 2. In which language is Jenkins written?

Java.

---

### 3. What is Continuous Integration?

Automatically building and testing code after changes.

---

### 4. What is Continuous Delivery?

Automated software delivery process.

---

### 5. What is a Jenkins Job?

A task executed by Jenkins.

---

### 6. What is a Build?

Execution instance of a job.

---

### 7. What is a Pipeline?

Automated CI/CD workflow.

---

### 8. What is Jenkinsfile?

Pipeline definition stored as code.

---

### 9. Why is Jenkins popular?

Large plugin ecosystem and flexibility.

---

### 10. Is Jenkins free?

Yes.

---

# Interview Questions

## Q1. Why do organizations use Jenkins?

To automate building, testing, and deployment.

---

## Q2. How does Jenkins fit into DevOps?

It automates CI/CD processes.

---

## Q3. What are the benefits of Jenkins?

Automation, scalability, plugin support, CI/CD integration.

---

## Q4. Difference between Jenkins and GitHub Actions?

Jenkins is self-hosted and highly customizable, while GitHub Actions is GitHub-managed.

---

## Q5. What problems does Jenkins solve?

- Manual builds
- Delayed testing
- Integration issues
- Slow deployment

---

# Key Takeaways

✔ Jenkins is an open-source automation server.

✔ It automates building, testing, packaging, and deployment.

✔ Jenkins is one of the most widely used CI/CD tools.

✔ Jenkins integrates with GitHub, Docker, Maven, Kubernetes, AWS, and many other technologies.

✔ Jenkins is a core tool in modern DevOps pipelines.

---

# Summary

Jenkins is a powerful automation platform that enables Continuous Integration and Continuous Delivery by automating software development workflows. It reduces manual effort, improves software quality, accelerates releases, and forms the backbone of many modern DevOps pipelines.