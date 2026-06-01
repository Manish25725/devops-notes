# Jenkins and GitHub Integration

![Jenkins](https://img.shields.io/badge/Jenkins-GitHub-red)
![CI/CD](https://img.shields.io/badge/CI/CD-Automation-blue)
![GitHub](https://img.shields.io/badge/GitHub-Integration-green)
![DevOps](https://img.shields.io/badge/DevOps-Webhooks-orange)

---

# 📚 Table of Contents

- Why Integrate Jenkins with GitHub?
- Jenkins + GitHub Architecture
- GitHub Repository Integration
- Git Credentials Configuration
- Webhooks
- Poll SCM
- Automatic Build Triggers
- Jenkinsfile from GitHub
- GitHub Branch Integration
- Multi-Branch Pipelines
- GitHub Pull Request Builds
- Complete CI/CD Flow
- Best Practices
- Quick Revision Notes
- Viva Questions
- Interview Questions

---

# Why Integrate Jenkins with GitHub?

Modern software development revolves around:

```text
GitHub
```

Developers push code to GitHub repositories.

Jenkins automatically:

✔ Detects Changes

✔ Downloads Code

✔ Builds Application

✔ Runs Tests

✔ Deploys Application

Without manual intervention.

---

# Traditional Workflow

```text
Developer Pushes Code
        ↓
Developer Opens Jenkins
        ↓
Clicks Build Manually
```

Problems:

❌ Slow

❌ Manual

❌ Error-Prone

---

# Automated Workflow

```text
Developer Pushes Code
        ↓
GitHub
        ↓
Webhook
        ↓
Jenkins
        ↓
Build Starts Automatically
```

---

# Jenkins + GitHub Architecture

```text
Developer
     ↓
GitHub Repository
     ↓
Webhook
     ↓
Jenkins
     ↓
Build
     ↓
Test
     ↓
Deploy
```

---

# GitHub Repository Integration

Jenkins can connect to:

- Public Repositories
- Private Repositories
- Organization Repositories

Example Repository:

```text
https://github.com/company/app.git
```

---

# Connecting Jenkins to GitHub

Navigate:

```text
Manage Jenkins
     ↓
Plugins
```

Install:

```text
Git Plugin
GitHub Plugin
GitHub Branch Source Plugin
```

---

# Important GitHub Plugins

| Plugin | Purpose |
|----------|----------|
| Git Plugin | Git Integration |
| GitHub Plugin | GitHub Support |
| GitHub Branch Source | Multi-Branch Pipelines |
| GitHub Integration Plugin | Enhanced GitHub Features |

---

# Configure GitHub Repository

Example:

```text
https://github.com/company/project.git
```

Inside Job:

```text
Source Code Management
      ↓
Git
      ↓
Repository URL
```

---

# Git Credentials

Public repositories:

```text
No Credentials Needed
```

Private repositories:

```text
Credentials Required
```

---

# Authentication Options

### Username + Password

Legacy method.

---

### Personal Access Token (PAT)

Recommended.

---

### SSH Keys

Enterprise preferred.

---

# Personal Access Token (PAT)

Generate PAT:

```text
GitHub
  ↓
Settings
  ↓
Developer Settings
  ↓
Personal Access Tokens
```

---

# Store PAT in Jenkins

Navigate:

```text
Manage Jenkins
     ↓
Credentials
```

Add:

```text
Secret Text
```

---

# Example Credential

```text
github-pat
```

---

# Using Credentials

```groovy
git credentialsId: 'github-pat',
url: 'https://github.com/company/app.git'
```

---

# SSH Authentication

Generate SSH Key:

```bash
ssh-keygen -t rsa -b 4096
```

---

# Add Public Key to GitHub

GitHub:

```text
Settings
   ↓
SSH Keys
```

Add:

```text
id_rsa.pub
```

---

# Add Private Key to Jenkins

Store:

```text
id_rsa
```

inside Jenkins Credentials.

---

# Webhooks

Webhook = GitHub notifies Jenkins immediately when code changes.

---

# Without Webhook

```text
GitHub
   ↓
Wait
   ↓
Jenkins Checks Later
```

Slow.

---

# With Webhook

```text
GitHub Push
      ↓
Webhook
      ↓
Jenkins
      ↓
Build Starts
```

Instant.

---

# Webhook Architecture

```text
Developer Push
        ↓
GitHub
        ↓
Webhook
        ↓
Jenkins
```

---

# Configure Webhook

GitHub Repository:

```text
Settings
    ↓
Webhooks
```

---

# Payload URL

Example:

```text
http://your-jenkins-server/github-webhook/
```

---

# Content Type

```text
application/json
```

---

# Events

Choose:

```text
Just the push event
```

or

```text
Send me everything
```

---

# Webhook Flow

```text
Push Code
    ↓
GitHub
    ↓
Webhook
    ↓
Jenkins Trigger
```

---

# Poll SCM

Alternative to webhooks.

Jenkins periodically checks GitHub.

---

# Example

```groovy
pollSCM('* * * * *')
```

Meaning:

```text
Check Every Minute
```

---

# Poll SCM Architecture

```text
Jenkins
    ↓
Check GitHub
    ↓
Changes Found?
    ↓
Build
```

---

# Webhook vs Poll SCM

| Feature | Webhook | Poll SCM |
|----------|----------|----------|
| Trigger Speed | Instant | Delayed |
| Resource Usage | Low | Higher |
| Recommended | Yes | Backup Option |

---

# Automatic Build Triggers

Common triggers:

### Push Event

```text
Developer Push
```

---

### Pull Request

```text
PR Created
```

---

### Merge Event

```text
Code Merged
```

---

### Schedule

```text
Nightly Builds
```

---

# Jenkinsfile from GitHub

Best Practice:

Store Jenkinsfile inside repository.

---

# Repository Structure

```text
Project
│
├── src
├── pom.xml
└── Jenkinsfile
```

---

# Jenkins Configuration

```text
Pipeline
     ↓
Pipeline Script from SCM
     ↓
Git
```

---

# Advantages

✔ Version Controlled

✔ Reusable

✔ Auditable

---

# Multi-Branch Pipelines

Supports:

```text
main
develop
feature/*
release/*
```

Automatically.

---

# Architecture

```text
Repository
     ↓
Branch Discovery
     ↓
Pipeline Per Branch
```

---

# Example

```text
main
develop
feature-login
feature-payment
```

Each branch gets:

```text
Independent Pipeline
```

---

# Benefits

✔ Branch Isolation

✔ PR Validation

✔ Enterprise Ready

---

# GitHub Pull Request Builds

Jenkins can automatically:

```text
Build Pull Requests
```

before merge.

---

# Flow

```text
Developer Creates PR
         ↓
GitHub
         ↓
Jenkins Build
         ↓
Tests Pass
         ↓
Merge Allowed
```

---

# Complete Jenkins + GitHub CI Flow

```text
Developer Push
       ↓
GitHub
       ↓
Webhook
       ↓
Jenkins
       ↓
Checkout
       ↓
Build
       ↓
Test
       ↓
Package
```

---

# Real-World Example

Spring Boot Project:

```text
GitHub Repository
       ↓
Webhook
       ↓
Jenkins
       ↓
Maven Build
       ↓
JUnit Tests
       ↓
Docker Build
       ↓
Deploy
```

---

# Enterprise Workflow

```text
Developer
      ↓
GitHub
      ↓
Pull Request
      ↓
Jenkins Validation
      ↓
Merge
      ↓
Deployment
```

---

# Best Practices

## Use Webhooks

Preferred over Poll SCM.

---

## Store Jenkinsfile in Git

Always use:

```text
Pipeline as Code
```

---

## Use PAT or SSH Keys

Avoid passwords.

---

## Enable PR Validation

Build every pull request.

---

## Protect Main Branch

Require successful Jenkins builds.

---

## Use Multi-Branch Pipelines

For large projects.

---

# Quick Revision Notes

## Webhook

```text
GitHub Notifies Jenkins
```

---

## Poll SCM

```text
Jenkins Checks GitHub
```

---

## PAT

```text
Personal Access Token
```

---

## Multi-Branch Pipeline

```text
Pipeline Per Git Branch
```

---

## Jenkinsfile

```text
Pipeline Definition
```

---

# Viva Questions

### 1. Why integrate Jenkins with GitHub?

To automate CI/CD workflows.

---

### 2. What is a Webhook?

A GitHub notification sent to Jenkins.

---

### 3. What is Poll SCM?

Jenkins periodically checking repositories.

---

### 4. Which is preferred: Webhook or Poll SCM?

Webhook.

---

### 5. What is a PAT?

Personal Access Token.

---

### 6. Where should Jenkinsfile be stored?

Inside Git repository.

---

### 7. What is a Multi-Branch Pipeline?

Pipeline created for each Git branch.

---

### 8. Why use SSH Keys?

Secure repository access.

---

### 9. Can Jenkins build Pull Requests?

Yes.

---

### 10. What plugin is required for Git integration?

Git Plugin.

---

# Interview Questions

## Q1. Explain Jenkins and GitHub integration.

GitHub stores source code while Jenkins automatically builds, tests, and deploys code whenever changes occur.

---

## Q2. What is the difference between Webhooks and Poll SCM?

Webhooks are event-driven and instant, while Poll SCM periodically checks repositories.

---

## Q3. Why should Jenkinsfiles be stored in GitHub?

For version control, auditing, and collaboration.

---

## Q4. How can Jenkins access private GitHub repositories?

Using PATs or SSH Keys stored in Jenkins Credentials.

---

## Q5. What are Multi-Branch Pipelines?

Pipelines automatically created and managed for multiple Git branches.

---

# Key Takeaways

✔ GitHub is commonly used as the source code repository.

✔ Jenkins automates builds after GitHub events.

✔ Webhooks provide instant build triggering.

✔ PATs and SSH Keys enable secure repository access.

✔ Multi-Branch Pipelines support modern Git workflows.

✔ Jenkinsfiles should always be stored in Git repositories.

✔ Pull Request validation improves code quality.

---

# Summary

Jenkins and GitHub integration forms the foundation of modern CI/CD pipelines. Through Webhooks, PATs, SSH Keys, Multi-Branch Pipelines, and Jenkinsfiles stored in repositories, teams can automate software delivery from code commit to deployment while maintaining security, scalability, and collaboration.