# Jenkins Pipeline Syntax & Jenkinsfile

![Jenkins](https://img.shields.io/badge/Jenkins-Pipeline-red)
![CI/CD](https://img.shields.io/badge/CI/CD-Automation-blue)
![Groovy](https://img.shields.io/badge/Groovy-Scripting-green)
![DevOps](https://img.shields.io/badge/DevOps-Pipeline-orange)

---

# 📚 Table of Contents

- What is a Jenkins Pipeline?
- Why Pipelines?
- What is a Jenkinsfile?
- Pipeline Architecture
- Declarative Pipeline
- Scripted Pipeline
- Declarative vs Scripted Pipeline
- Jenkinsfile Structure
- Agents
- Stages
- Steps
- Environment Variables
- Parameters
- Post Actions
- Multi-Branch Pipelines
- Real-World Pipeline Example
- Best Practices
- Quick Revision Notes
- Viva Questions
- Interview Questions

---

# What is a Jenkins Pipeline?

A Jenkins Pipeline is a collection of automated steps that define the entire CI/CD process.

Instead of manually configuring builds:

```text
Build
 ↓
Test
 ↓
Package
 ↓
Deploy
```

everything is written as code.

---

# Why Pipelines?

Traditional builds required:

- Manual execution
- Repetitive configuration
- Difficult maintenance

Pipelines solve this by providing:

✔ Automation

✔ Reusability

✔ Version Control

✔ Scalability

✔ Pipeline as Code

---

# What is a Jenkinsfile?

A Jenkinsfile is a text file that defines a Jenkins Pipeline.

Stored inside:

```text
Project Repository
```

Example:

```text
Project
│
├── src
├── pom.xml
└── Jenkinsfile
```

---

# Benefits of Jenkinsfile

✔ Version Controlled

✔ Easy Collaboration

✔ Reproducible Builds

✔ Auditable Changes

✔ Portable Pipelines

---

# Pipeline Architecture

```text
GitHub Repository
        ↓
     Jenkinsfile
        ↓
      Pipeline
        ↓
Checkout
        ↓
Build
        ↓
Test
        ↓
Deploy
```

---

# Types of Jenkins Pipelines

Jenkins supports two pipeline styles:

## 1. Declarative Pipeline

Modern and recommended.

---

## 2. Scripted Pipeline

Advanced and flexible.

---

# Declarative Pipeline

Introduced to simplify pipeline creation.

Structure is predefined.

Example:

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

                echo 'Building Application'

            }

        }

    }

}
```

---

# Declarative Pipeline Structure

```text
Pipeline
   ↓
Agent
   ↓
Stages
   ↓
Steps
```

---

# Scripted Pipeline

More flexible.

Written using Groovy scripting.

Example:

```groovy
node {

    stage('Build') {

        echo 'Building Application'

    }

}
```

---

# Scripted Pipeline Characteristics

✔ Flexible

✔ Dynamic

✔ Supports Logic

✔ Advanced Customization

---

# Declarative vs Scripted Pipeline

| Feature | Declarative | Scripted |
|----------|-------------|-----------|
| Complexity | Easy | Advanced |
| Syntax | Structured | Flexible |
| Learning Curve | Low | High |
| Recommended | Yes | Advanced Users |
| Readability | Better | Moderate |

---

# Declarative Pipeline Components

Main components:

```text
pipeline
agent
stages
stage
steps
post
environment
parameters
```

---

# Basic Jenkinsfile

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

                echo 'Hello Jenkins'

            }

        }

    }

}
```

---

# Pipeline Block

Top-level block.

```groovy
pipeline {

}
```

Everything must be inside.

---

# Agent Block

Defines where pipeline executes.

Example:

```groovy
agent any
```

Meaning:

```text
Run On Any Available Agent
```

---

# Specific Agent Example

```groovy
agent {

    label 'linux'

}
```

Runs only on:

```text
Linux Agent
```

---

# Stages

Pipeline is divided into stages.

Example:

```groovy
stages {

}
```

---

# Why Stages?

Provide:

✔ Visibility

✔ Organization

✔ Easier Debugging

---

# Example

```groovy
stages {

    stage('Build') {

    }

    stage('Test') {

    }

}
```

---

# Stage Block

Represents a logical phase.

Example:

```groovy
stage('Build')
```

---

# Typical Stages

```text
Checkout
Build
Test
Package
Deploy
```

---

# Steps

Actual commands executed.

Example:

```groovy
steps {

    echo 'Building'

}
```

---

# Shell Commands

Linux:

```groovy
steps {

    sh 'mvn clean package'

}
```

---

# Windows Commands

```groovy
steps {

    bat 'dir'

}
```

---

# Complete Build Example

```groovy
pipeline {

    agent any

    stages {

        stage('Checkout') {

            steps {

                git 'https://github.com/user/project.git'

            }

        }

        stage('Build') {

            steps {

                sh 'mvn clean package'

            }

        }

    }

}
```

---

# Environment Variables

Used for configuration.

Example:

```groovy
environment {

    APP_ENV = 'production'

}
```

---

# Access Environment Variable

```groovy
steps {

    echo "${APP_ENV}"

}
```

Output:

```text
production
```

---

# Multiple Variables

```groovy
environment {

    APP_ENV='prod'
    VERSION='1.0'

}
```

---

# Built-In Variables

Examples:

```groovy
BUILD_NUMBER
JOB_NAME
BUILD_ID
WORKSPACE
```

---

# Example

```groovy
steps {

    echo "${BUILD_NUMBER}"

}
```

---

# Parameters

Allow user input before build starts.

---

# String Parameter

```groovy
parameters {

    string(
        name: 'ENV',
        defaultValue: 'dev'
    )

}
```

---

# Using Parameter

```groovy
echo "${params.ENV}"
```

---

# Choice Parameter

```groovy
parameters {

    choice(
        name: 'ENV',
        choices: ['dev','test','prod']
    )

}
```

---

# Boolean Parameter

```groovy
parameters {

    booleanParam(
        name: 'DEPLOY',
        defaultValue: true
    )

}
```

---

# Post Actions

Executed after stages complete.

---

# Success Action

```groovy
post {

    success {

        echo 'Build Successful'

    }

}
```

---

# Failure Action

```groovy
post {

    failure {

        echo 'Build Failed'

    }

}
```

---

# Always Action

```groovy
post {

    always {

        cleanWs()

    }

}
```

---

# Complete Example

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

                echo 'Building'

            }

        }

    }

    post {

        success {

            echo 'Success'

        }

        failure {

            echo 'Failed'

        }

    }

}
```

---

# Multi-Branch Pipelines

Used when project has:

```text
main
develop
feature/*
```

branches.

---

# Traditional Pipeline Problem

One pipeline:

```text
One Branch
```

---

# Multi-Branch Solution

Jenkins automatically discovers:

```text
main
develop
feature/login
feature/payment
```

and creates pipelines.

---

# Multi-Branch Architecture

```text
GitHub Repo
      ↓
Multibranch Pipeline
      ↓
main
develop
feature/*
```

---

# Benefits

✔ Automatic Branch Discovery

✔ PR Validation

✔ Branch Isolation

✔ Enterprise Friendly

---

# Real-World Pipeline Example

```text
Developer Push
       ↓
GitHub
       ↓
Jenkinsfile
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

# Enterprise Jenkinsfile Example

```groovy
pipeline {

    agent any

    environment {

        APP_ENV = 'prod'

    }

    stages {

        stage('Checkout') {

            steps {

                git 'https://github.com/company/project.git'

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

        stage('Deploy') {

            steps {

                echo 'Deploying Application'

            }

        }

    }

}
```

---

# Best Practices

## Use Declarative Pipelines

Recommended by Jenkins.

---

## Store Jenkinsfile in Git

Benefits:

```text
Version Control
Audit Trail
Code Review
```

---

## Use Separate Stages

Example:

```text
Build
Test
Deploy
```

---

## Avoid Hardcoding Secrets

Use:

```text
Jenkins Credentials
```

---

## Keep Pipelines Small

Reusable stages improve maintenance.

---

# Quick Revision Notes

## Jenkinsfile

```text
Pipeline Definition File
```

---

## Declarative Pipeline

```text
Structured & Recommended
```

---

## Scripted Pipeline

```text
Flexible & Advanced
```

---

## Stage

```text
Logical Build Phase
```

---

## Step

```text
Command Execution Unit
```

---

## Agent

```text
Execution Environment
```

---

## Environment Variable

```text
Configuration Value
```

---

## Parameter

```text
User Input
```

---

# Viva Questions

### 1. What is a Jenkins Pipeline?

Automated CI/CD workflow.

---

### 2. What is a Jenkinsfile?

File that defines a Jenkins Pipeline.

---

### 3. Which pipeline type is recommended?

Declarative Pipeline.

---

### 4. What language is used in Jenkins pipelines?

Groovy.

---

### 5. What is an Agent?

Machine executing pipeline tasks.

---

### 6. What is a Stage?

Logical phase of a pipeline.

---

### 7. What is a Step?

Actual command execution.

---

### 8. What are Environment Variables?

Configuration values available during builds.

---

### 9. What are Parameters?

User inputs provided before build execution.

---

### 10. What is a Multi-Branch Pipeline?

Pipeline that automatically builds multiple Git branches.

---

# Interview Questions

## Q1. Difference between Declarative and Scripted Pipelines?

Declarative is structured and easy; Scripted is flexible and advanced.

---

## Q2. Why should Jenkinsfiles be stored in Git?

Version control, collaboration, and reproducibility.

---

## Q3. What are the key components of a Jenkins Pipeline?

Agent, Stages, Steps, Environment, Parameters, and Post Actions.

---

## Q4. What is the purpose of Multi-Branch Pipelines?

Automatic discovery and execution of pipelines for Git branches.

---

## Q5. How are environment variables used in Jenkins?

To provide configuration without hardcoding values.

---

# Key Takeaways

✔ Jenkins Pipelines automate CI/CD workflows.

✔ Jenkinsfiles store pipeline definitions as code.

✔ Declarative Pipelines are the recommended approach.

✔ Scripted Pipelines offer advanced flexibility.

✔ Environment variables and parameters improve reusability.

✔ Multi-Branch Pipelines support modern Git workflows.

✔ Jenkinsfiles should always be version-controlled.

---

# Summary

Jenkins Pipelines provide a powerful way to automate software delivery workflows. Using Jenkinsfiles, teams can define Build, Test, Package, and Deployment processes as code. Declarative Pipelines simplify pipeline development, while Scripted Pipelines offer advanced customization. Combined with Multi-Branch Pipelines, parameters, and environment variables, Jenkins enables scalable and maintainable CI/CD automation.