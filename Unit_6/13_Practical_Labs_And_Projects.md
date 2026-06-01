
# Practical Labs and Projects using Jenkins

![Jenkins](https://img.shields.io/badge/Jenkins-Practical_Labs-red)
![CI/CD](https://img.shields.io/badge/CI/CD-Projects-blue)
![Docker](https://img.shields.io/badge/Docker-Integration-green)
![GitHub](https://img.shields.io/badge/GitHub-Automation-orange)

---

# 📚 Table of Contents

- Lab 1: First Freestyle Job
- Lab 2: GitHub Integration
- Lab 3: Maven Build Automation
- Lab 4: Jenkins Pipeline
- Lab 5: GitHub Webhook Trigger
- Lab 6: Docker Build using Jenkins
- Lab 7: Push Docker Image to Docker Hub
- Lab 8: Push Docker Image to GHCR
- Mini Project 1: Java CI Pipeline
- Mini Project 2: Dockerized Spring Boot App
- Mini Project 3: Complete CI/CD Pipeline
- Viva Questions
- Interview Questions

---

# Lab 1: First Freestyle Job

## Objective

Create and run a simple Jenkins job.

---

## Step 1

Navigate:

```text
Dashboard
 ↓
New Item
 ↓
Freestyle Project
```

Name:

```text
hello-jenkins
```

---

## Step 2

Add Build Step

```text
Execute Shell
```

Command:

```bash
echo "Hello Jenkins"
date
hostname
```

---

## Step 3

Click:

```text
Build Now
```

---

## Output

```text
Hello Jenkins
Mon May 25
jenkins-server
```

---

# Lab 2: GitHub Integration

## Objective

Connect Jenkins with GitHub Repository.

---

## Repository Example

```text
https://github.com/username/demo-app.git
```

---

## Steps

Create Job

```text
Freestyle Project
```

---

Configure:

```text
Source Code Management
 ↓
Git
```

Enter:

```text
Repository URL
```

---

Build Job

Jenkins clones repository automatically.

---

# Lab 3: Maven Build Automation

## Objective

Build Java project using Maven.

---

## Prerequisites

Configure:

```text
JDK
Maven
```

inside Jenkins.

---

## Build Command

```bash
mvn clean package
```

---

## Freestyle Configuration

```text
Build
 ↓
Invoke Top-Level Maven Targets
```

Goals:

```text
clean package
```

---

## Output

```text
target/app.jar
```

---

# Lab 4: Jenkins Pipeline

## Objective

Create first Jenkins Pipeline.

---

## Create Pipeline Job

```text
Dashboard
 ↓
New Item
 ↓
Pipeline
```

---

## Pipeline Script

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

                echo 'Building Application'

            }

        }

        stage('Test') {

            steps {

                echo 'Testing Application'

            }

        }

    }

}
```

---

## Execute

```text
Build Now
```

---

# Lab 5: GitHub Webhook Trigger

## Objective

Automatically trigger Jenkins after GitHub push.

---

## Configure Jenkins

Enable:

```text
GitHub hook trigger for GITScm polling
```

---

## Configure GitHub

Navigate:

```text
Repository
 ↓
Settings
 ↓
Webhooks
```

---

## Payload URL

```text
http://JENKINS_IP/github-webhook/
```

---

## Event

```text
Push Event
```

---

## Test

Push code:

```bash
git add .
git commit -m "Webhook Test"
git push
```

---

## Result

```text
GitHub Push
 ↓
Webhook
 ↓
Jenkins Build
```

---

# Lab 6: Docker Build using Jenkins

## Objective

Build Docker image automatically.

---

## Dockerfile

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html
```

---

## Pipeline

```groovy
pipeline {

    agent any

    stages {

        stage('Docker Build') {

            steps {

                sh 'docker build -t demo:v1 .'

            }

        }

    }

}
```

---

## Verify

```bash
docker images
```

Output:

```text
demo:v1
```

---

# Lab 7: Push Docker Image to Docker Hub

## Objective

Push image from Jenkins to Docker Hub.

---

## Login

Store credentials:

```text
dockerhub-creds
```

---

## Pipeline

```groovy
pipeline {

    agent any

    stages {

        stage('Push') {

            steps {

                sh 'docker push username/demo:v1'

            }

        }

    }

}
```

---

## Verify

Open:

```text
https://hub.docker.com
```

Image visible under repositories.

---

# Lab 8: Push Docker Image to GHCR

## Objective

Push image to GitHub Container Registry.

---

## Login

```bash
docker login ghcr.io
```

Use:

```text
GitHub PAT
```

---

## Tag Image

```bash
docker tag demo:v1 ghcr.io/username/demo:v1
```

---

## Push

```bash
docker push ghcr.io/username/demo:v1
```

---

## Verify

GitHub Profile:

```text
Packages
```

---

# Mini Project 1: Java CI Pipeline

## Objective

Build Java Application Automatically.

---

## Workflow

```text
GitHub
 ↓
Jenkins
 ↓
Maven Build
 ↓
JUnit Tests
 ↓
Artifact
```

---

## Jenkinsfile

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

                sh 'mvn clean package'

            }

        }

    }

}
```

---

## Output

```text
target/app.jar
```

---

# Mini Project 2: Dockerized Spring Boot Application

## Objective

Build and Dockerize Spring Boot Application.

---

## Workflow

```text
GitHub
 ↓
Jenkins
 ↓
Maven Build
 ↓
Docker Build
 ↓
Docker Hub
```

---

## Jenkinsfile

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

                sh 'docker build -t spring-app:v1 .'

            }

        }

    }

}
```

---

# Mini Project 3: Complete CI/CD Pipeline

## Objective

Implement Full DevOps Pipeline.

---

## Architecture

```text
Developer
     ↓
GitHub
     ↓
Webhook
     ↓
Jenkins
     ↓
Build
     ↓
Test
     ↓
Docker Build
     ↓
Docker Hub
     ↓
Production Server
```

---

## Jenkinsfile

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

                sh 'mvn clean package'

            }

        }

        stage('Test') {

            steps {

                sh 'mvn test'

            }

        }

        stage('Docker Build') {

            steps {

                sh 'docker build -t company/app:v1 .'

            }

        }

        stage('Docker Push') {

            steps {

                sh 'docker push company/app:v1'

            }

        }

    }

}
```

---

# Complete CI/CD Flow

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

# Viva Questions

### 1. What is a Freestyle Job?

GUI-based Jenkins job.

---

### 2. What is a Jenkins Pipeline?

Code-based CI/CD workflow.

---

### 3. What is a Webhook?

GitHub event that triggers Jenkins builds.

---

### 4. Why integrate Docker with Jenkins?

To automate container builds and deployments.

---

### 5. What is GHCR?

GitHub Container Registry.

---

### 6. What is Maven used for?

Java project build automation.

---

### 7. What is a Jenkinsfile?

Pipeline definition stored in source code.

---

### 8. Why use Docker Hub?

To store and distribute container images.

---

### 9. What is Continuous Integration?

Automatic building and testing of code changes.

---

### 10. What is Continuous Deployment?

Automatic deployment after successful builds.

---

# Interview Questions

## Q1. Explain a complete Jenkins CI/CD pipeline.

GitHub → Jenkins → Build → Test → Package → Docker Build → Docker Hub → Deployment.

---

## Q2. How do Webhooks improve CI/CD?

They trigger builds instantly when code changes.

---

## Q3. How does Jenkins build Docker images?

Using docker build commands in pipeline stages.

---

## Q4. How can Jenkins deploy applications automatically?

Using SSH, Docker, Kubernetes, or cloud deployment commands.

---

## Q5. Which Jenkins project type is preferred?

Pipeline Jobs because they support Pipeline as Code.

---

# Key Takeaways

✔ Jenkins automates software delivery.

✔ GitHub integration enables automatic builds.

✔ Maven builds Java applications.

✔ Docker integration enables containerized deployments.

✔ Webhooks provide instant build triggering.

✔ Jenkins Pipelines are the industry standard.

✔ End-to-end CI/CD pipelines combine GitHub, Jenkins, Maven, Docker, and deployment platforms.

---

# Summary

These practical labs and projects cover the complete Jenkins workflow from creating Freestyle Jobs to implementing enterprise-grade CI/CD pipelines. By combining GitHub, Maven, Docker, Jenkins Pipelines, Webhooks, Docker Hub, and GHCR, learners gain hands-on experience with real-world DevOps automation practices.