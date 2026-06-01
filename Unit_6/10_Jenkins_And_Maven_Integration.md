# Jenkins and Maven Integration

![Jenkins](https://img.shields.io/badge/Jenkins-Maven-red)
![CI/CD](https://img.shields.io/badge/CI/CD-Java-blue)
![Maven](https://img.shields.io/badge/Maven-Build-green)
![DevOps](https://img.shields.io/badge/DevOps-Automation-orange)

---

# 📚 Table of Contents

- Why Maven with Jenkins?
- Maven Overview
- Jenkins + Maven Architecture
- Installing Maven in Jenkins
- Global Tool Configuration
- Configuring JDK
- Running Maven Builds
- Maven Build Lifecycle in Jenkins
- Maven Pipelines
- Surefire Plugin Reports
- Code Coverage Reports
- Artifact Management
- Maven + Jenkins CI/CD Flow
- Best Practices
- Quick Revision Notes
- Viva Questions
- Interview Questions

---

# Why Maven with Jenkins?

Java projects require:

- Dependency Management
- Compilation
- Testing
- Packaging

Instead of manually running:

```bash
mvn clean package
```

Jenkins automates the entire Maven build process.

---

# What is Maven?

Maven is a Build Automation Tool primarily used for Java applications.

Main Functions:

✔ Dependency Management

✔ Project Build

✔ Testing

✔ Packaging

✔ Deployment

---

# Maven + Jenkins Architecture

```text
Developer
     ↓
GitHub
     ↓
Jenkins
     ↓
Maven Build
     ↓
Testing
     ↓
Artifact
     ↓
Deployment
```

---

# Why Integrate Maven with Jenkins?

Without Jenkins:

```text
Developer
    ↓
Manual Build
    ↓
Manual Testing
    ↓
Manual Deployment
```

Problems:

❌ Slow

❌ Error-Prone

❌ Inconsistent

---

With Jenkins:

```text
Commit Code
      ↓
Automatic Build
      ↓
Automatic Test
      ↓
Automatic Package
```

---

# Maven Installation in Jenkins

Navigate:

```text
Manage Jenkins
     ↓
Global Tool Configuration
```

---

# Add Maven

```text
Maven Installations
```

Click:

```text
Add Maven
```

Example:

```text
Name: Maven-3.9
Version: 3.9.x
```

---

# Maven Tool Configuration

Example:

```text
Maven Name:
Maven-3.9
```

Jenkins downloads and manages Maven automatically.

---

# Configure Java (JDK)

Maven requires Java.

Navigate:

```text
Manage Jenkins
     ↓
Global Tool Configuration
```

---

# Add JDK

Example:

```text
Name:
JDK-21
```

---

# Verify Configuration

```text
Manage Jenkins
      ↓
Global Tool Configuration
      ↓
JDK
      ↓
Maven
```

---

# Jenkins + Maven Workflow

```text
GitHub
   ↓
Checkout
   ↓
Maven Compile
   ↓
Unit Tests
   ↓
Package
   ↓
Artifact
```

---

# Running Maven in Freestyle Jobs

Create:

```text
Freestyle Project
```

---

# Build Step

Choose:

```text
Invoke Top-Level Maven Targets
```

---

# Example Goal

```bash
clean package
```

---

# What Happens?

```text
Clean
 ↓
Compile
 ↓
Test
 ↓
Package
```

Automatically.

---

# Maven Build Lifecycle

Important phases:

```text
validate
compile
test
package
verify
install
deploy
```

---

# Lifecycle Flow

```text
Validate
    ↓
Compile
    ↓
Test
    ↓
Package
    ↓
Install
```

---

# Compile Example

```bash
mvn compile
```

Creates:

```text
.class files
```

---

# Test Example

```bash
mvn test
```

Executes:

```text
JUnit Tests
```

---

# Package Example

```bash
mvn package
```

Creates:

```text
app.jar
```

or

```text
app.war
```

---

# Install Example

```bash
mvn install
```

Installs artifact into:

```text
Local Maven Repository
```

---

# Deploy Example

```bash
mvn deploy
```

Publishes artifact to:

```text
Artifact Repository
```

Example:

```text
Nexus
Artifactory
```

---

# Jenkins Pipeline Example

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

# Complete Maven Pipeline

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

                sh 'mvn clean compile'

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

# Maven Tool Usage in Pipeline

```groovy
tools {

    maven 'Maven-3.9'

}
```

---

# Example

```groovy
pipeline {

    agent any

    tools {

        maven 'Maven-3.9'

    }

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

# Surefire Plugin

Maven uses:

```text
Maven Surefire Plugin
```

for Unit Testing.

---

# Purpose

Runs:

```text
JUnit
TestNG
```

tests automatically.

---

# Example

```bash
mvn test
```

Triggers:

```text
Surefire Plugin
```

---

# Surefire Report Location

```text
target/surefire-reports/
```

Contains:

```text
XML Reports
```

---

# Publish Test Reports in Jenkins

```groovy
post {

    always {

        junit 'target/surefire-reports/*.xml'

    }

}
```

---

# Benefits

✔ Test Results Dashboard

✔ Failed Test Details

✔ Historical Tracking

---

# Test Reporting Flow

```text
JUnit Tests
      ↓
Surefire Reports
      ↓
Jenkins Dashboard
```

---

# Code Coverage

Code Coverage measures:

```text
How Much Code Was Tested
```

---

# Popular Coverage Tools

| Tool | Language |
|--------|----------|
| JaCoCo | Java |
| Cobertura | Java |
| Istanbul | JavaScript |

---

# JaCoCo Example

Add Plugin:

```xml
<plugin>
  <groupId>org.jacoco</groupId>
  <artifactId>jacoco-maven-plugin</artifactId>
</plugin>
```

---

# Generate Coverage

```bash
mvn test
```

Coverage Report:

```text
target/site/jacoco
```

---

# Publish Coverage

Jenkins Plugin:

```text
JaCoCo Plugin
```

---

# Coverage Flow

```text
Source Code
      ↓
Tests
      ↓
Coverage Report
      ↓
Jenkins Dashboard
```

---

# Artifact Management

Artifacts:

```text
JAR
WAR
ZIP
```

generated after builds.

---

# Archive Artifacts

```groovy
post {

    success {

        archiveArtifacts 'target/*.jar'

    }

}
```

---

# Artifact Flow

```text
Build
   ↓
Artifact
   ↓
Archive
   ↓
Download
```

---

# Enterprise Maven Pipeline

```text
GitHub
   ↓
Checkout
   ↓
Compile
   ↓
Unit Tests
   ↓
Coverage
   ↓
Package
   ↓
Artifact
   ↓
Deploy
```

---

# Spring Boot Example

Build:

```bash
mvn clean package
```

Output:

```text
target/app.jar
```

Jenkins archives:

```text
app.jar
```

for deployment.

---

# Maven + Jenkins CI/CD Flow

```text
Developer Commit
        ↓
GitHub
        ↓
Jenkins
        ↓
Maven Build
        ↓
Unit Tests
        ↓
Coverage Report
        ↓
Package
        ↓
Artifact
        ↓
Deploy
```

---

# Best Practices

## Use Maven Tool Configuration

Avoid hardcoded Maven paths.

---

## Always Run Tests

```bash
mvn test
```

before deployment.

---

## Publish Test Reports

Use:

```groovy
junit
```

---

## Generate Coverage

Use:

```text
JaCoCo
```

---

## Archive Artifacts

Store build outputs.

---

## Fail Fast

Stop deployment if tests fail.

---

# Quick Revision Notes

## Maven

```text
Java Build Automation Tool
```

---

## Surefire

```text
Unit Testing Plugin
```

---

## JaCoCo

```text
Code Coverage Tool
```

---

## Maven Tool Configuration

```text
Global Jenkins Maven Setup
```

---

## Archive Artifacts

```text
Store Build Outputs
```

---

# Viva Questions

### 1. Why integrate Maven with Jenkins?

To automate Java builds.

---

### 2. Where is Maven configured in Jenkins?

Global Tool Configuration.

---

### 3. What command compiles Java code?

```bash
mvn compile
```

---

### 4. What command creates a JAR?

```bash
mvn package
```

---

### 5. What plugin runs unit tests?

Surefire Plugin.

---

### 6. Where are Surefire reports stored?

```text
target/surefire-reports
```

---

### 7. What is JaCoCo?

A Java code coverage tool.

---

### 8. What is an artifact?

Build output like JAR/WAR.

---

### 9. How do you archive artifacts?

Using archiveArtifacts.

---

### 10. Why are test reports important?

They validate application quality.

---

# Interview Questions

## Q1. How do you configure Maven in Jenkins?

Using Global Tool Configuration and Maven Installations.

---

## Q2. What is the purpose of Surefire Plugin?

To execute JUnit/TestNG tests.

---

## Q3. How are Maven builds executed in Jenkins Pipelines?

Using mvn commands inside pipeline stages.

---

## Q4. What is JaCoCo used for?

Generating code coverage reports.

---

## Q5. Why archive Maven artifacts?

To store deployable build outputs for future deployment.

---

# Key Takeaways

✔ Maven automates Java builds.

✔ Jenkins integrates Maven for CI/CD.

✔ Surefire executes automated tests.

✔ JaCoCo generates coverage reports.

✔ Artifacts should be archived after successful builds.

✔ Jenkins dashboards provide test and coverage visibility.

✔ Maven + Jenkins is a standard Java CI/CD stack.

---

# Summary

Jenkins and Maven integration enables fully automated Java application builds, testing, packaging, and deployment. Maven handles dependency management and build lifecycles, while Jenkins orchestrates CI/CD workflows. Together with Surefire, JaCoCo, and artifact management, they form the foundation of enterprise-grade Java DevOps pipelines.