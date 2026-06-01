# Pipeline Stages and Artifact Management

![Jenkins](https://img.shields.io/badge/Jenkins-Pipeline-red)
![CI/CD](https://img.shields.io/badge/CI/CD-Stages-blue)
![Artifacts](https://img.shields.io/badge/Artifacts-Management-green)
![DevOps](https://img.shields.io/badge/DevOps-Automation-orange)

---

# 📚 Table of Contents

- What are Pipeline Stages?
- Why Use Stages?
- Common Pipeline Stages
- Checkout Stage
- Build Stage
- Test Stage
- Package Stage
- Deploy Stage
- Post Actions
- Artifacts
- Managing Artifacts
- Archiving Artifacts
- Artifact Lifecycle
- Real-World CI/CD Flow
- Best Practices
- Quick Revision Notes
- Viva Questions
- Interview Questions

---

# What are Pipeline Stages?

A Pipeline Stage is a logical section of a Jenkins Pipeline.

Instead of one huge build process:

```text
Build Everything
```

We divide it into:

```text
Checkout
Build
Test
Package
Deploy
```

This improves:

✔ Readability

✔ Debugging

✔ Monitoring

✔ Maintenance

---

# Why Use Stages?

Without stages:

```text
One Large Script
```

Problems:

❌ Hard to Debug

❌ Hard to Monitor

❌ Difficult Maintenance

---

With stages:

```text
Checkout
 ↓
Build
 ↓
Test
 ↓
Package
 ↓
Deploy
```

Easy to track progress.

---

# Pipeline Architecture

```text
GitHub
   ↓
Checkout
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

# Common Pipeline Stages

Most CI/CD pipelines contain:

### 1. Checkout

Download source code.

### 2. Build

Compile application.

### 3. Test

Run automated tests.

### 4. Package

Create deployable artifact.

### 5. Deploy

Deploy application.

---

# Stage 1: Checkout

Purpose:

Retrieve source code from Git repository.

---

# Example

```groovy
stage('Checkout') {

    steps {

        git 'https://github.com/company/project.git'

    }

}
```

---

# What Happens?

```text
GitHub Repository
        ↓
Clone Repository
        ↓
Workspace
```

---

# Checkout Stage Flow

```text
GitHub
   ↓
Clone
   ↓
Workspace
```

---

# Stage 2: Build

Purpose:

Compile source code.

---

# Maven Example

```groovy
stage('Build') {

    steps {

        sh 'mvn compile'

    }

}
```

---

# Java Build Flow

```text
Source Code
      ↓
Compilation
      ↓
.class Files
```

---

# Build Stage Benefits

✔ Detects Syntax Errors

✔ Verifies Compilation

✔ Generates Build Output

---

# Stage 3: Test

Purpose:

Run automated tests.

---

# Maven Test Example

```groovy
stage('Test') {

    steps {

        sh 'mvn test'

    }

}
```

---

# Test Flow

```text
Application
      ↓
Unit Tests
      ↓
Result
```

---

# Benefits

✔ Detect Bugs Early

✔ Improve Quality

✔ Prevent Broken Releases

---

# Stage 4: Package

Purpose:

Generate deployable artifact.

Examples:

```text
JAR
WAR
ZIP
Docker Image
```

---

# Maven Example

```groovy
stage('Package') {

    steps {

        sh 'mvn package'

    }

}
```

---

# Package Flow

```text
Source Code
      ↓
Build
      ↓
JAR File
```

Example Output:

```text
target/app.jar
```

---

# Stage 5: Deploy

Purpose:

Deploy application.

---

# Example

```groovy
stage('Deploy') {

    steps {

        echo 'Deploying Application'

    }

}
```

---

# Deployment Targets

- Linux Server
- AWS EC2
- Azure VM
- Kubernetes
- Docker Containers

---

# Complete Pipeline Example

```groovy
pipeline {

    agent any

    stages {

        stage('Checkout') {

            steps {

                git 'https://github.com/company/project.git'

            }

        }

        stage('Build') {

            steps {

                sh 'mvn compile'

            }

        }

        stage('Test') {

            steps {

                sh 'mvn test'

            }

        }

        stage('Package') {

            steps {

                sh 'mvn package'

            }

        }

    }

}
```

---

# What are Post Actions?

Post Actions run after pipeline completion.

Useful for:

✔ Notifications

✔ Cleanup

✔ Reporting

✔ Logging

---

# Post Action Types

```text
always
success
failure
unstable
aborted
```

---

# Always Block

Runs regardless of result.

```groovy
post {

    always {

        cleanWs()

    }

}
```

---

# Success Block

Runs only if build succeeds.

```groovy
post {

    success {

        echo 'Build Successful'

    }

}
```

---

# Failure Block

Runs only if build fails.

```groovy
post {

    failure {

        echo 'Build Failed'

    }

}
```

---

# Post Action Flow

```text
Pipeline Complete
        ↓
Post Action
        ↓
Notification/Cleanup
```

---

# What are Artifacts?

Artifacts are files generated during a build.

Examples:

```text
app.jar
app.war
report.zip
docker-image
test-report.xml
```

---

# Artifact Examples

Java Project:

```text
target/app.jar
```

Web Application:

```text
target/app.war
```

Reports:

```text
test-report.xml
```

---

# Why Artifacts Matter?

Artifacts are:

✔ Build Outputs

✔ Deployable Files

✔ Reusable Assets

✔ Traceable Build Results

---

# Artifact Lifecycle

```text
Source Code
      ↓
Build
      ↓
Artifact
      ↓
Storage
      ↓
Deployment
```

---

# Archive Artifacts

Jenkins can store artifacts after build.

Example:

```groovy
post {

    success {

        archiveArtifacts artifacts: 'target/*.jar'

    }

}
```

---

# What Happens?

Jenkins stores:

```text
target/app.jar
```

inside build history.

---

# Accessing Artifacts

Navigate:

```text
Build
   ↓
Artifacts
```

---

# Artifact Storage Flow

```text
Build
  ↓
Artifact
  ↓
Archive
  ↓
Build History
```

---

# Multiple Artifacts

```groovy
archiveArtifacts artifacts: 'target/*.jar,target/*.war'
```

---

# Fingerprinting Artifacts

Used for tracking.

Example:

```groovy
archiveArtifacts(
artifacts: 'target/*.jar',
fingerprint: true
)
```

---

# Benefits

✔ Traceability

✔ Version Tracking

✔ Audit Support

---

# Test Reports

Jenkins can publish reports.

Example:

```groovy
junit 'target/surefire-reports/*.xml'
```

---

# Report Flow

```text
Tests
  ↓
XML Reports
  ↓
Jenkins Dashboard
```

---

# Real-World CI/CD Example

```text
Developer Push
        ↓
Checkout
        ↓
Build
        ↓
Unit Test
        ↓
Package
        ↓
Archive Artifact
        ↓
Deploy
```

---

# Enterprise Pipeline Example

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

                sh 'mvn compile'

            }

        }

        stage('Test') {

            steps {

                sh 'mvn test'

            }

        }

        stage('Package') {

            steps {

                sh 'mvn package'

            }

        }

    }

    post {

        success {

            archiveArtifacts artifacts: 'target/*.jar'

        }

    }

}
```

---

# Best Practices

## Separate Stages Clearly

Use:

```text
Checkout
Build
Test
Package
Deploy
```

---

## Archive Important Artifacts

Store:

```text
JAR
WAR
Reports
```

---

## Use Post Actions

Handle:

```text
Cleanup
Notifications
Reporting
```

---

## Publish Test Results

Use:

```groovy
junit
```

---

## Keep Pipelines Modular

Smaller stages improve maintenance.

---

# Quick Revision Notes

## Stage

```text
Logical Pipeline Section
```

---

## Checkout

```text
Download Source Code
```

---

## Build

```text
Compile Application
```

---

## Test

```text
Run Automated Tests
```

---

## Package

```text
Create Deployable Artifact
```

---

## Artifact

```text
Generated Build Output
```

---

## Post Action

```text
Runs After Pipeline Completion
```

---

# Viva Questions

### 1. What is a Pipeline Stage?

A logical phase of a Jenkins Pipeline.

---

### 2. What is the purpose of Checkout?

Retrieve source code.

---

### 3. What happens during Build?

Source code is compiled.

---

### 4. Why is the Test stage important?

It validates application quality.

---

### 5. What is Packaging?

Creating deployable files.

---

### 6. What is an Artifact?

Generated output of a build.

---

### 7. What is archiveArtifacts?

Stores build outputs in Jenkins.

---

### 8. What is a Post Action?

Action executed after pipeline completion.

---

### 9. What does the success block do?

Runs after successful builds.

---

### 10. Why archive artifacts?

For deployment and traceability.

---

# Interview Questions

## Q1. Explain common Jenkins pipeline stages.

Checkout, Build, Test, Package, and Deploy.

---

## Q2. What are artifacts in Jenkins?

Files generated during builds that can be stored and deployed.

---

## Q3. How do you archive artifacts?

Using archiveArtifacts in the pipeline.

---

## Q4. What is the purpose of post actions?

Cleanup, notifications, reporting, and artifact handling.

---

## Q5. Why should pipelines be divided into stages?

For readability, debugging, and maintainability.

---

# Key Takeaways

✔ Pipeline stages organize CI/CD workflows.

✔ Common stages are Checkout, Build, Test, Package, and Deploy.

✔ Artifacts are generated outputs used for deployment.

✔ Jenkins can archive artifacts for future use.

✔ Post Actions improve automation after builds complete.

✔ Structured pipelines are easier to maintain and debug.

---

# Summary

Pipeline Stages divide a Jenkins Pipeline into logical phases such as Checkout, Build, Test, Package, and Deploy. Artifacts generated during these stages can be archived and reused for deployments. Post Actions further enhance automation by enabling cleanup, notifications, reporting, and artifact management after pipeline execution.