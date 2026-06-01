# Jenkins Installation & UI Overview

![Jenkins](https://img.shields.io/badge/Jenkins-Installation-red)
![DevOps](https://img.shields.io/badge/DevOps-CI/CD-blue)
![Docker](https://img.shields.io/badge/Docker-Supported-green)
![Open Source](https://img.shields.io/badge/Open_Source-Free-orange)

---

# 📚 Table of Contents

- What is Jenkins Installation?
- Jenkins Requirements
- Installation Methods
- Installing Jenkins using WAR File
- Installing Jenkins using Docker
- Initial Setup
- Unlocking Jenkins
- Plugin Installation
- Creating First Admin User
- Jenkins Dashboard Overview
- Jobs and Build History
- Plugin Manager
- Global Configuration
- Jenkins Home Directory
- Practical Commands
- Quick Revision Notes
- Viva Questions
- Interview Questions

---

# What is Jenkins Installation?

Before Jenkins can automate builds and deployments, it must be installed and configured.

Jenkins can run on:

- Windows
- Linux
- macOS
- Docker Containers
- Cloud Servers

Because Jenkins is Java-based, Java must be installed first.

---

# Jenkins Requirements

## Minimum Requirements

| Component | Requirement |
|------------|-------------|
| RAM | 2 GB |
| CPU | Dual Core |
| Disk | 10 GB |
| Java | Java 17+ |
| OS | Windows/Linux/macOS |

---

# Verify Java Installation

```bash
java --version
```

Example Output:

```text
openjdk 21
```

If Java is not installed:

```text
Jenkins will not start
```

---

# Jenkins Installation Methods

There are multiple ways to install Jenkins:

### 1. WAR File Installation

```text
java -jar jenkins.war
```

---

### 2. Docker Installation

```bash
docker run jenkins/jenkins:lts
```

---

### 3. Native Package Installation

- Windows Installer
- Debian Package
- RPM Package

---

### 4. Cloud Installation

- AWS EC2
- Azure VM
- Google Cloud

---

# Method 1: Jenkins WAR Installation

WAR = Web Application Archive

Official Jenkins package:

```text
jenkins.war
```

---

# Step 1: Download Jenkins

Official Website:

:contentReference[oaicite:0]{index=0}

Download:

```text
jenkins.war
```

---

# Step 2: Verify Java

```bash
java --version
```

---

# Step 3: Run Jenkins

```bash
java -jar jenkins.war
```

---

# What Happens?

Jenkins starts:

```text
Embedded Web Server
```

Default Port:

```text
8080
```

---

# Access Jenkins

Open Browser:

```text
http://localhost:8080
```

---

# WAR Installation Flow

```text
Download WAR
      ↓
Install Java
      ↓
Run WAR
      ↓
Access localhost:8080
```

---

# Method 2: Jenkins using Docker

Most DevOps engineers prefer Docker.

Advantages:

✔ Fast Setup

✔ Portable

✔ Easy Cleanup

✔ Production Friendly

---

# Pull Jenkins Image

```bash
docker pull jenkins/jenkins:lts
```

---

# Verify Image

```bash
docker images
```

---

# Run Jenkins Container

```bash
docker run -d \
-p 8080:8080 \
-p 50000:50000 \
--name jenkins \
jenkins/jenkins:lts
```

---

# Explanation

```text
8080 → Jenkins UI

50000 → Agent Communication
```

---

# Verify Container

```bash
docker ps
```

Expected:

```text
jenkins container running
```

---

# Access Jenkins

Open Browser:

```text
http://localhost:8080
```

---

# Docker Installation Architecture

```text
Docker Host
      ↓
Jenkins Container
      ↓
Port 8080
      ↓
Browser
```

---

# Persistent Jenkins Data

Without volume:

```text
Container Deleted
      ↓
Data Lost
```

---

# Use Docker Volume

```bash
docker run -d \
-p 8080:8080 \
-p 50000:50000 \
-v jenkins_home:/var/jenkins_home \
--name jenkins \
jenkins/jenkins:lts
```

---

# Benefits

```text
Jenkins Configurations
Plugins
Jobs
Users

Persist After Restart
```

---

# Initial Setup

When Jenkins starts first time:

```text
Unlock Jenkins
```

screen appears.

---

# Unlock Jenkins

Jenkins generates:

```text
Initial Admin Password
```

---

# WAR Installation Password

Location:

```text
~/.jenkins/secrets/initialAdminPassword
```

---

# Linux Command

```bash
cat ~/.jenkins/secrets/initialAdminPassword
```

---

# Docker Command

```bash
docker logs jenkins
```

OR

```bash
docker exec -it jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

---

# Example Password

```text
8dbe73e2d8cb4...
```

Copy and paste into Jenkins UI.

---

# Plugin Installation

After unlocking:

Choose:

```text
Install Suggested Plugins
```

Recommended for beginners.

---

# Common Plugins Installed

| Plugin | Purpose |
|----------|----------|
| Git | Git Integration |
| Pipeline | Pipeline Support |
| Maven | Maven Builds |
| Docker | Docker Integration |
| SSH | Remote Deployment |

---

# Plugin Installation Flow

```text
Unlock Jenkins
      ↓
Install Plugins
      ↓
Restart Jenkins
```

---

# Create First Admin User

After plugins:

Create:

```text
Username
Password
Email
```

Example:

```text
admin
```

---

# Jenkins Dashboard

After login:

Main Jenkins Dashboard appears.

---

# Dashboard Components

```text
Dashboard
 ├── New Item
 ├── Build History
 ├── Manage Jenkins
 ├── Credentials
 ├── Nodes
 └── Jobs
```

---

# Dashboard Architecture

```text
Jenkins Dashboard
      ↓
Manage Jenkins
      ↓
Configure System
      ↓
Jobs
```

---

# New Item

Used to create:

- Freestyle Jobs
- Pipeline Jobs
- Multibranch Pipelines

---

# Build History

Shows:

```text
Build Number
Status
Duration
Time
```

---

# Build Status Colors

| Color | Meaning |
|----------|----------|
| Blue/Green | Success |
| Red | Failed |
| Yellow | Unstable |
| Grey | Not Built |

---

# Manage Jenkins

Most important administration section.

Contains:

- Plugin Manager
- Credentials
- Nodes
- System Configuration
- Global Tools

---

# Plugin Manager

Manage plugins.

Options:

```text
Installed Plugins
Available Plugins
Updates
```

---

# Install New Plugin

Steps:

```text
Manage Jenkins
      ↓
Plugins
      ↓
Available Plugins
      ↓
Install
```

---

# Important Plugins

### Git Plugin

Connect Jenkins with GitHub.

---

### Pipeline Plugin

Required for Jenkinsfile.

---

### Docker Plugin

Docker Integration.

---

### Maven Plugin

Maven Builds.

---

### SSH Plugin

Remote Deployment.

---

# Global Tool Configuration

Location:

```text
Manage Jenkins
      ↓
Global Tool Configuration
```

Configure:

- JDK
- Maven
- Git
- Gradle

---

# Example

Install Maven:

```text
Manage Jenkins
      ↓
Global Tool Configuration
      ↓
Maven
```

---

# Jenkins Home Directory

Jenkins stores everything in:

```text
JENKINS_HOME
```

---

# Linux

```text
/var/lib/jenkins
```

---

# Docker

```text
/var/jenkins_home
```

---

# Contents

```text
Jobs
Plugins
Users
Builds
Logs
Credentials
```

---

# Jenkins Directory Structure

```text
JENKINS_HOME
│
├── jobs
├── plugins
├── users
├── workspace
├── builds
└── logs
```

---

# Useful Jenkins Commands

Check Java:

```bash
java --version
```

---

Run Jenkins WAR:

```bash
java -jar jenkins.war
```

---

Pull Jenkins Image:

```bash
docker pull jenkins/jenkins:lts
```

---

Run Jenkins Container:

```bash
docker run -d -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts
```

---

View Logs:

```bash
docker logs jenkins
```

---

Enter Container:

```bash
docker exec -it jenkins bash
```

---

Restart Container:

```bash
docker restart jenkins
```

---

Stop Container:

```bash
docker stop jenkins
```

---

# Real-World Setup

```text
GitHub
    ↓
Jenkins
    ↓
Docker
    ↓
AWS Server
```

Most companies run Jenkins:

```text
Docker Container
```

instead of WAR file.

---

# Quick Revision Notes

## Default Port

```text
8080
```

---

## Agent Port

```text
50000
```

---

## Admin Password

```text
initialAdminPassword
```

---

## Plugin Manager

```text
Manage Jenkins → Plugins
```

---

## Global Tool Config

```text
Manage Jenkins → Global Tool Configuration
```

---

## Jenkins Home

```text
JENKINS_HOME
```

---

# Viva Questions

### 1. What is the default Jenkins port?

8080

---

### 2. Which language is Jenkins written in?

Java

---

### 3. What is required before Jenkins installation?

Java

---

### 4. Which Docker image is commonly used?

```bash
jenkins/jenkins:lts
```

---

### 5. What is Jenkins Home?

Directory storing Jenkins data.

---

### 6. Where is plugin management done?

Plugin Manager.

---

### 7. What port is used for agents?

50000

---

### 8. What is the first step after installation?

Unlock Jenkins.

---

### 9. What is the default admin password called?

initialAdminPassword

---

### 10. Which installation method is most popular today?

Docker Installation.

---

# Interview Questions

## Q1. How do you install Jenkins?

Using WAR, Docker, native packages, or cloud VMs.

---

## Q2. Why is Java required?

Because Jenkins is Java-based.

---

## Q3. How can Jenkins data persist in Docker?

Using Docker Volumes.

---

## Q4. What is JENKINS_HOME?

Directory containing Jenkins configuration and jobs.

---

## Q5. Why do organizations prefer Dockerized Jenkins?

Easy deployment, portability, and scalability.

---

# Key Takeaways

✔ Jenkins can be installed using WAR files or Docker.

✔ Java is required before installation.

✔ Jenkins UI runs on port 8080.

✔ Agent communication uses port 50000.

✔ Plugins extend Jenkins functionality.

✔ JENKINS_HOME stores all Jenkins data.

✔ Docker is the preferred installation method in modern DevOps environments.

---

# Summary

Installing Jenkins is the first step toward building a CI/CD pipeline. Jenkins can be deployed using WAR files, Docker containers, or cloud servers. After installation, administrators configure plugins, users, tools, and jobs through the Jenkins Dashboard, which serves as the central management interface for all CI/CD activities.