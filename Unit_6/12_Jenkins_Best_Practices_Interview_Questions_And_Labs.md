
# Jenkins Agents and CI/CD Deployment Flows

![Jenkins](https://img.shields.io/badge/Jenkins-Agents-red)
![CI/CD](https://img.shields.io/badge/CI/CD-Deployment-blue)
![DevOps](https://img.shields.io/badge/DevOps-Automation-green)
![Cloud](https://img.shields.io/badge/Cloud-Deployments-orange)

---

# 📚 Table of Contents

- What are Jenkins Agents?
- Why Agents are Needed
- Jenkins Master-Agent Architecture
- Types of Jenkins Agents
- SSH Agents
- SFTP Agents
- Container-Based Agents
- Agent Labels
- PollSCM
- Webhooks
- Shared Pipeline Libraries
- Deployment Flows
- Deploying to Servers
- Deploying to Cloud
- Backup & Restore
- Pipeline Best Practices
- Quick Revision Notes
- Viva Questions
- Interview Questions

---

# What are Jenkins Agents?

A Jenkins Agent is a machine that performs build, test, and deployment tasks on behalf of Jenkins.

Instead of executing everything on the Jenkins Controller:

```text
Jenkins Controller
        ↓
    Agent
        ↓
Build/Test/Deploy
```

---

# Why Agents are Needed?

Large organizations have:

- Multiple Projects
- Multiple Teams
- Different Technologies

Examples:

```text
Java Project
Node.js Project
Python Project
Docker Project
```

Running all jobs on one machine becomes inefficient.

---

# Master-Agent Architecture

```text
          Jenkins Controller
                   │
      ┌────────────┼────────────┐
      │            │            │
      ▼            ▼            ▼
   Agent-1      Agent-2      Agent-3
   (Java)       (Node)      (Docker)
```

---

# Responsibilities

## Jenkins Controller

- Manage Jobs
- Schedule Builds
- Store Configurations
- Manage Plugins
- Manage Users

---

## Jenkins Agents

- Build Code
- Run Tests
- Deploy Applications
- Execute Pipeline Steps

---

# Types of Jenkins Agents

1. SSH Agents
2. SFTP Agents
3. Container-Based Agents
4. Cloud Agents
5. Windows Agents
6. Linux Agents

---

# SSH Agents

Most common agent type.

Controller connects using:

```text
SSH
```

---

# Architecture

```text
Jenkins
    │
 SSH Connection
    │
Remote Linux Server
```

---

# Requirements

Agent Machine:

```bash
Java Installed
SSH Enabled
```

---

# Add SSH Agent

Navigate:

```text
Manage Jenkins
      ↓
Nodes
      ↓
New Node
```

---

# Configure Agent

```text
Name:
linux-agent

Type:
Permanent Agent
```

---

# Connection Method

```text
Launch Agent via SSH
```

---

# Required Information

```text
Host IP
SSH Credentials
Remote Directory
```

---

# Example

```text
IP: 192.168.1.10
User: ubuntu
Port: 22
```

---

# Advantages

✔ Easy Setup

✔ Secure

✔ Common in Enterprises

---

# SFTP-Based Deployments

Used for:

```text
File Transfers
```

---

# Example

```text
Jenkins
    ↓
SFTP
    ↓
Remote Server
```

---

# Common Usage

Deploy:

```text
JAR Files
WAR Files
ZIP Files
```

to remote servers.

---

# Container-Based Agents

Modern DevOps environments prefer:

```text
Docker Agents
```

---

# Architecture

```text
Jenkins
    ↓
Docker Container
    ↓
Build
```

---

# Example Pipeline

```groovy
pipeline {

    agent {

        docker {

            image 'maven:3.9'

        }

    }

}
```

---

# Benefits

✔ Consistent Environment

✔ Easy Cleanup

✔ No Dependency Conflicts

✔ Reproducible Builds

---

# Agent Labels

Labels help Jenkins choose agents.

Example:

```text
java
docker
linux
windows
```

---

# Example

```groovy
agent {

    label 'docker'

}
```

Jenkins executes job only on Docker agents.

---

# PollSCM

PollSCM checks repository changes periodically.

---

# Example

```groovy
triggers {

    pollSCM('H/5 * * * *')

}
```

Meaning:

```text
Check Every 5 Minutes
```

---

# PollSCM Flow

```text
Jenkins
     ↓
Check GitHub
     ↓
Changes Found?
     ↓
Trigger Build
```

---

# Drawback

Consumes resources because Jenkins continuously checks repositories.

---

# Webhooks

Preferred alternative.

GitHub directly informs Jenkins.

---

# Architecture

```text
GitHub Push
      ↓
Webhook
      ↓
Jenkins
      ↓
Build
```

---

# Benefits

✔ Instant Trigger

✔ Lower Resource Usage

✔ Faster Builds

---

# PollSCM vs Webhook

| Feature | PollSCM | Webhook |
|----------|----------|----------|
| Speed | Delayed | Instant |
| Resource Usage | Higher | Lower |
| Recommended | No | Yes |

---

# Shared Pipeline Libraries

Large organizations use reusable code.

---

# Problem

Multiple pipelines contain repeated code.

Example:

```groovy
Build
Test
Deploy
```

repeated everywhere.

---

# Solution

Shared Libraries.

---

# Architecture

```text
Pipeline
     ↓
Shared Library
     ↓
Reusable Functions
```

---

# Example

```groovy
@Library('company-lib') _
```

---

# Benefits

✔ Reusable

✔ Easier Maintenance

✔ Standardization

---

# Deployment Flows

After successful build:

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

# Deployment Targets

- Linux Servers
- Virtual Machines
- Docker Containers
- Kubernetes
- AWS
- Azure
- GCP

---

# Deployment to Linux Server

Architecture:

```text
Jenkins
     ↓
SSH
     ↓
Linux Server
```

---

# Example

```groovy
stage('Deploy') {

    steps {

        sh 'scp app.jar ubuntu@server:/opt/apps'

    }

}
```

---

# Deployment Flow

```text
Build JAR
     ↓
Transfer File
     ↓
Restart Application
```

---

# Docker Deployment

Pipeline:

```groovy
stage('Deploy') {

    steps {

        sh 'docker pull company/app:v1'

        sh 'docker run -d company/app:v1'

    }

}
```

---

# Cloud Deployment

Supported Platforms:

- AWS
- Azure
- Google Cloud

---

# AWS Example

```text
GitHub
   ↓
Jenkins
   ↓
Build
   ↓
Docker Image
   ↓
AWS EC2
```

---

# Azure Example

```text
Build
 ↓
Push Image
 ↓
Azure Container Apps
```

---

# Kubernetes Deployment

Pipeline:

```text
Build
 ↓
Docker Image
 ↓
Kubernetes Cluster
```

---

# Example

```groovy
sh 'kubectl apply -f deployment.yaml'
```

---

# Complete Enterprise Flow

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
        ↓
Docker Build
        ↓
Docker Hub
        ↓
Production Deployment
```

---

# Backup and Restore

Critical Jenkins Administration Task.

---

# Why Backup?

Protect:

- Jobs
- Credentials
- Plugins
- Pipelines
- Build History

---

# Important Directory

```text
JENKINS_HOME
```

Example:

```text
/var/lib/jenkins
```

---

# Backup Example

```bash
tar -czvf jenkins_backup.tar.gz /var/lib/jenkins
```

---

# Restore Example

```bash
tar -xzvf jenkins_backup.tar.gz
```

---

# Backup Components

```text
Jobs
Users
Plugins
Credentials
Pipeline Configurations
```

---

# Backup Plugins

Popular Plugin:

```text
ThinBackup Plugin
```

---

# Backup Strategy

```text
Daily Backup
Weekly Full Backup
Monthly Archive Backup
```

---

# Pipeline Best Practices

## Use Jenkinsfile

Store pipelines as code.

---

## Use Webhooks

Avoid PollSCM whenever possible.

---

## Keep Stages Small

Example:

```text
Build
Test
Deploy
```

---

## Use Agents Properly

Separate workloads by labels.

---

## Use Shared Libraries

Avoid duplicate code.

---

## Archive Artifacts

Store build outputs.

---

## Store Credentials Securely

Use:

```text
Jenkins Credentials Store
```

---

## Backup Jenkins Regularly

Protect critical configurations.

---

# Quick Revision Notes

## Agent

```text
Machine That Executes Jobs
```

---

## SSH Agent

```text
Remote Machine Connected Through SSH
```

---

## Docker Agent

```text
Container-Based Build Environment
```

---

## PollSCM

```text
Periodic Repository Checking
```

---

## Webhook

```text
Instant GitHub Notification
```

---

## Shared Library

```text
Reusable Pipeline Code
```

---

## Backup

```text
Copy Of Jenkins Configuration
```

---

# Viva Questions

### 1. What is a Jenkins Agent?

A machine that executes Jenkins jobs.

---

### 2. Why use Agents?

To distribute workloads and improve scalability.

---

### 3. What is an SSH Agent?

A remote machine connected using SSH.

---

### 4. What are Docker Agents?

Containers used as Jenkins execution environments.

---

### 5. What is PollSCM?

Periodic checking of source repositories.

---

### 6. What is a Webhook?

An event-based trigger from GitHub.

---

### 7. What are Shared Libraries?

Reusable pipeline code stored centrally.

---

### 8. Where is Jenkins configuration stored?

Inside JENKINS_HOME.

---

### 9. Why is backup important?

To recover Jenkins after failures.

---

### 10. Which is preferred: PollSCM or Webhook?

Webhook.

---

# Interview Questions

## Q1. Explain Jenkins Master-Agent Architecture.

The Jenkins Controller manages jobs while Agents execute builds, tests, and deployments on separate machines.

---

## Q2. Why are Docker Agents popular?

They provide isolated, reproducible, and dependency-free build environments.

---

## Q3. What is the difference between PollSCM and Webhooks?

PollSCM continuously checks repositories while Webhooks trigger builds instantly upon changes.

---

## Q4. What are Shared Libraries?

Reusable pipeline code that helps standardize CI/CD processes across projects.

---

## Q5. How would you back up Jenkins?

By backing up the JENKINS_HOME directory or using plugins like ThinBackup.

---

# Key Takeaways

✔ Jenkins Agents execute builds separately from the Controller.

✔ SSH Agents are the most common enterprise setup.

✔ Docker Agents provide consistent build environments.

✔ Webhooks are preferred over PollSCM.

✔ Shared Libraries improve pipeline maintainability.

✔ Jenkins supports deployments to servers, containers, and cloud platforms.

✔ Regular backups are essential for disaster recovery.

✔ Proper pipeline practices improve scalability and reliability.

---

# Summary

Jenkins Agents enable scalable CI/CD execution by distributing workloads across multiple machines or containers. Combined with Webhooks, Shared Libraries, cloud deployments, and proper backup strategies, Jenkins can support enterprise-grade CI/CD pipelines for modern DevOps environments.