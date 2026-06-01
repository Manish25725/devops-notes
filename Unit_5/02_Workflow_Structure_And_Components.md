# Workflow Structure & Components in GitHub Actions

![GitHub Actions](https://img.shields.io/badge/GitHub-Actions-black)
![Workflow](https://img.shields.io/badge/Workflow-Automation-blue)
![CI/CD](https://img.shields.io/badge/CI/CD-Pipeline-green)

---

# 📚 Table of Contents

- What is a Workflow?
- Workflow Directory Structure
- YAML Basics
- Workflow Anatomy
- Key Components
- Workflows
- Jobs
- Steps
- Actions
- Runners
- Workflow Execution Flow
- Example Workflow
- Quick Revision
- Viva Questions
- Interview Questions

---

# What is a Workflow?

A Workflow is an automated process defined in a YAML file.

It contains:

- Events (Triggers)
- Jobs
- Steps
- Actions
- Runners

A workflow automatically executes tasks whenever a specified event occurs.

---

## Example

```text
Developer Pushes Code
          ↓
Workflow Starts
          ↓
Build Application
          ↓
Run Tests
          ↓
Deploy
```

---

# Workflow Directory Structure

GitHub Actions workflows must be stored inside:

```text
.github/
└── workflows/
    ├── build.yml
    ├── test.yml
    └── deploy.yml
```

---

# Repository Structure

```text
MyProject/
│
├── src/
├── pom.xml
├── Dockerfile
│
└── .github/
    └── workflows/
        ├── ci.yml
        └── deploy.yml
```

---

# Why This Location?

GitHub automatically scans:

```text
.github/workflows/
```

for workflow files.

Only YAML files inside this directory are treated as GitHub Actions workflows.

---

# YAML Basics

GitHub Actions uses YAML.

YAML = "YAML Ain't Markup Language"

Extension:

```text
.yml
.yaml
```

---

## Example

```yaml
name: My Workflow

on:
  push:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Hello
        run: echo "Hello GitHub Actions"
```

---

# YAML Rules

---

## Key-Value Pairs

```yaml
name: CI Pipeline
```

---

## Lists

```yaml
branches:
  - main
  - dev
```

---

## Indentation

Use spaces only.

```yaml
jobs:
  build:
```

❌ Never use tabs.

---

# Workflow Anatomy

A GitHub Actions workflow contains:

```text
Workflow
   │
   ├── Trigger
   │
   ├── Job
   │     │
   │     ├── Step
   │     ├── Step
   │     └── Step
   │
   └── Job
         │
         ├── Step
         └── Step
```

---

# Key Components

GitHub Actions consists of:

1. Workflow
2. Event
3. Job
4. Step
5. Action
6. Runner

---

# Component Relationship

```text
Workflow
   ↓
Jobs
   ↓
Steps
   ↓
Actions / Commands
```

---

# 1️⃣ Workflow

Workflow = complete automation process.

Stored in:

```text
.github/workflows/
```

Example:

```yaml
name: Java CI
```

---

# Workflow Example

```yaml
name: Build Project
```

This simply names the workflow.

---

# Multiple Workflows

Repository can contain:

```text
build.yml
test.yml
deploy.yml
docker.yml
```

Each workflow performs different tasks.

---

# 2️⃣ Jobs

A Job is a collection of steps.

Each job runs on a runner.

---

## Example

```yaml
jobs:

  build:

    runs-on: ubuntu-latest

  test:

    runs-on: ubuntu-latest
```

---

# Job Diagram

```text
Workflow
   │
   ├── Build Job
   │
   └── Test Job
```

---

# Multiple Jobs

```yaml
jobs:

  build:

  test:

  deploy:
```

---

# Job Characteristics

✔ Independent

✔ Can run in parallel

✔ Can depend on another job

---

# Example

```yaml
deploy:

  needs: build
```

Deploy starts only after build succeeds.

---

# 3️⃣ Steps

A Job contains Steps.

Each step performs one task.

---

## Example

```yaml
steps:

  - name: Checkout

  - name: Build

  - name: Test
```

---

# Step Diagram

```text
Build Job

│
├── Checkout Code
├── Install Dependencies
├── Build Project
└── Run Tests
```

---

# Example

```yaml
steps:

- name: Print Message
  run: echo "Hello World"
```

---

# 4️⃣ Actions

Actions are reusable pieces of automation.

Think of them as:

```text
Pre-written code blocks
```

provided by GitHub or community.

---

# Example

Checkout repository:

```yaml
uses: actions/checkout@v4
```

Instead of writing code manually.

---

# Popular Actions

| Action | Purpose |
|----------|----------|
| actions/checkout | Clone Repository |
| actions/setup-java | Install Java |
| actions/setup-node | Install Node.js |
| docker/login-action | Docker Login |
| docker/build-push-action | Docker Build |

---

# Example

```yaml
- name: Checkout Repository

  uses: actions/checkout@v4
```

---

# 5️⃣ Runners

A Runner is the machine executing the workflow.

---

## Types

### GitHub Hosted Runner

Provided by GitHub.

Examples:

```text
ubuntu-latest
windows-latest
macos-latest
```

---

### Self Hosted Runner

Managed by organization.

Installed on:

- Physical Server
- Virtual Machine
- Cloud Instance

---

# Example

```yaml
runs-on: ubuntu-latest
```

---

# Workflow Execution Flow

```text
Push Event
      ↓
Workflow Trigger
      ↓
Runner Starts
      ↓
Job Executes
      ↓
Step Executes
      ↓
Action Runs
      ↓
Result Generated
```

---

# Complete Workflow Example

```yaml
name: Java CI

on:
  push:

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - name: Checkout Repository

        uses: actions/checkout@v4

      - name: Setup Java

        uses: actions/setup-java@v4

        with:

          distribution: temurin

          java-version: 17

      - name: Build Project

        run: mvn clean package
```

---

# Execution Explanation

Step 1:

```yaml
on:
  push
```

Workflow starts when code is pushed.

---

Step 2:

```yaml
runs-on:
  ubuntu-latest
```

Runner machine starts.

---

Step 3:

```yaml
actions/checkout
```

Repository cloned.

---

Step 4:

```yaml
setup-java
```

Java installed.

---

Step 5:

```yaml
mvn clean package
```

Application built.

---

# Real-World CI Workflow

```text
Developer Push
      ↓
GitHub Event
      ↓
Workflow
      ↓
Runner
      ↓
Checkout Code
      ↓
Install Dependencies
      ↓
Build
      ↓
Test
      ↓
Report
```

---

# Advantages

| Feature | Benefit |
|-----------|-----------|
| Workflow | Complete automation |
| Jobs | Parallel execution |
| Steps | Organized tasks |
| Actions | Reusable automation |
| Runners | Execution environment |

---

# Quick Revision Notes

## Workflow

```text
Complete automation pipeline
```

---

## Job

```text
Collection of steps
```

---

## Step

```text
Single task execution
```

---

## Action

```text
Reusable automation component
```

---

## Runner

```text
Machine executing workflow
```

---

# Architecture Diagram

```text
Workflow
    │
    ├── Job
    │      │
    │      ├── Step
    │      ├── Step
    │      └── Step
    │
    └── Job
           │
           ├── Step
           └── Step
```

---

# Frequently Asked Viva Questions

### 1. What is a workflow?

An automated process defined in YAML.

---

### 2. Where are workflow files stored?

```text
.github/workflows/
```

---

### 3. What is a job?

A collection of steps executed on a runner.

---

### 4. What is a step?

A single task within a job.

---

### 5. What is an action?

Reusable automation code.

---

### 6. What is a runner?

Machine executing the workflow.

---

### 7. Which language is used for workflow files?

YAML.

---

### 8. Can multiple jobs run simultaneously?

Yes.

---

# Interview Questions

## Q1. Explain GitHub Actions architecture.

```text
Workflow
   ↓
Job
   ↓
Step
   ↓
Action
   ↓
Runner
```

---

## Q2. Difference between Job and Step?

Job:

- Collection of steps

Step:

- Individual task

---

## Q3. What are GitHub Hosted Runners?

Machines provided and maintained by GitHub.

---

## Q4. What are Actions?

Reusable automation components that simplify workflow creation.

---

## Q5. Why use actions instead of shell scripts?

Actions are reusable, tested, and easier to maintain.

---

# Key Terms

| Term | Meaning |
|--------|---------|
| Workflow | Complete automation |
| Job | Group of steps |
| Step | Individual task |
| Action | Reusable automation |
| Runner | Execution machine |
| YAML | Workflow configuration language |

---

# Summary

GitHub Actions workflows are stored inside:

```text
.github/workflows/
```

A workflow consists of:

```text
Workflow
   ↓
Jobs
   ↓
Steps
   ↓
Actions
   ↓
Runner
```

Understanding these components is essential before learning workflow triggers, matrix strategies, deployments, Docker integration, and advanced CI/CD pipelines.