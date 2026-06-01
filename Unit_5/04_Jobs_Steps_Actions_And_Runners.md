# Jobs, Steps, Actions & Runners in GitHub Actions

![GitHub Actions](https://img.shields.io/badge/GitHub-Actions-black)
![CI/CD](https://img.shields.io/badge/CI/CD-Automation-blue)
![DevOps](https://img.shields.io/badge/DevOps-Pipeline-green)

---

# 📚 Table of Contents

- Introduction
- What are Jobs?
- What are Steps?
- Shell Commands in Steps
- What are Actions?
- Types of Actions
- Marketplace Actions
- Language-Specific Actions
- What are Runners?
- GitHub Hosted Runners
- Self Hosted Runners
- Complete Workflow Example
- Execution Flow
- Quick Revision Notes
- Viva Questions
- Interview Questions

---

# Introduction

GitHub Actions workflows are built using four major components:

```text
Workflow
   ↓
Jobs
   ↓
Steps
   ↓
Actions / Commands
```

And everything runs on:

```text
Runner
```

Understanding these components is essential for building CI/CD pipelines.

---

# GitHub Actions Architecture

```text
Workflow
   │
   ├── Job
   │      ├── Step
   │      ├── Step
   │      └── Step
   │
   └── Job
          ├── Step
          └── Step
```

---

# What is a Job?

A Job is a collection of steps executed on a runner.

---

## Definition

> A Job is a set of tasks that execute on the same runner.

---

# Example

```yaml
jobs:

  build:

    runs-on: ubuntu-latest
```

Here:

```text
build
```

is a Job.

---

# Job Characteristics

✔ Runs on a runner

✔ Contains multiple steps

✔ Can run independently

✔ Can depend on other jobs

---

# Single Job Example

```yaml
jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - run: echo "Building Project"
```

---

# Multiple Jobs Example

```yaml
jobs:

  build:

  test:

  deploy:
```

---

# Job Execution

By default:

```text
Jobs run in parallel
```

---

# Example

```text
Build Job
       ↘
         Parallel
       ↗
Test Job
```

---

# Job Dependencies

Sometimes one job must finish first.

---

# Example

```yaml
deploy:

  needs: build
```

Meaning:

```text
Deploy waits for Build
```

---

# Job Dependency Diagram

```text
Build
   ↓
Test
   ↓
Deploy
```

---

# What are Steps?

A Step is an individual task within a job.

---

## Definition

> A Step performs a single operation.

---

# Examples

```text
Checkout Code
Install Java
Build Application
Run Tests
```

Each is a step.

---

# Example

```yaml
steps:

  - run: echo "Hello"

  - run: echo "Building"
```

---

# Step Flow

```text
Job
 │
 ├── Step 1
 ├── Step 2
 ├── Step 3
 └── Step 4
```

---

# Step Types

Two major types:

1. Run Commands
2. Use Actions

---

# Shell Commands in Steps

Run commands execute directly on runner.

---

# Example

```yaml
steps:

  - name: Print Message

    run: echo "Hello GitHub Actions"
```

---

# Multiple Commands

```yaml
steps:

  - name: Multiple Commands

    run: |

      pwd

      ls

      echo "Build Started"
```

---

# Linux Commands

```yaml
run: |

  mkdir build

  cd build

  ls
```

---

# Windows Commands

```yaml
runs-on: windows-latest

steps:

  - run: dir
```

---

# Example Java Build

```yaml
- name: Build

  run: mvn clean package
```

---

# Example Node.js Build

```yaml
- name: Install Packages

  run: npm install
```

---

# What are Actions?

Actions are reusable automation units.

Instead of writing everything manually:

```yaml
run: git clone ...
```

we use:

```yaml
uses: actions/checkout
```

---

## Definition

> Actions are reusable applications for GitHub workflows.

---

# Action Diagram

```text
Action

Reusable

Automation

Component
```

---

# Example

```yaml
- uses: actions/checkout@v4
```

This action:

```text
✔ Clones Repository
✔ Downloads Source Code
✔ Prepares Workspace
```

---

# Types of Actions

| Type | Description |
|--------|------------|
| GitHub Actions | Official Actions |
| Marketplace Actions | Community Actions |
| Custom Actions | User-created Actions |

---

# Official GitHub Actions

Provided by GitHub.

Examples:

```text
actions/checkout
actions/setup-java
actions/setup-node
actions/cache
```

---

# Marketplace Actions

GitHub Marketplace contains thousands of actions.

Official site:

:contentReference[oaicite:0]{index=0}

---

# Popular Marketplace Actions

| Action | Purpose |
|----------|----------|
| actions/checkout | Clone repo |
| actions/setup-java | Install Java |
| actions/setup-node | Install Node.js |
| docker/login-action | Docker login |
| docker/build-push-action | Build Docker images |
| actions/cache | Dependency caching |

---

# Example

```yaml
- name: Checkout

  uses: actions/checkout@v4
```

---

# Example

```yaml
- name: Setup Java

  uses: actions/setup-java@v4

  with:

    distribution: temurin

    java-version: 17
```

---

# Language-Specific Actions

GitHub provides actions for various programming languages.

---

# Java

```yaml
uses: actions/setup-java@v4
```

---

# Node.js

```yaml
uses: actions/setup-node@v4
```

---

# Python

```yaml
uses: actions/setup-python@v5
```

---

# .NET

```yaml
uses: actions/setup-dotnet@v4
```

---

# Go

```yaml
uses: actions/setup-go@v5
```

---

# Example Node.js Workflow

```yaml
steps:

  - uses: actions/checkout@v4

  - uses: actions/setup-node@v4

    with:

      node-version: 20

  - run: npm install

  - run: npm test
```

---

# Example Python Workflow

```yaml
steps:

  - uses: actions/checkout@v4

  - uses: actions/setup-python@v5

    with:

      python-version: "3.11"

  - run: pip install -r requirements.txt

  - run: pytest
```

---

# What is a Runner?

A Runner is the machine that executes workflow jobs.

---

## Definition

> Runner is the server or machine where workflow jobs run.

---

# Runner Diagram

```text
Workflow
     ↓
Runner
     ↓
Job
     ↓
Step
```

---

# Types of Runners

1. GitHub Hosted Runner
2. Self Hosted Runner

---

# GitHub Hosted Runner

Provided by GitHub.

---

# Supported Platforms

```text
ubuntu-latest
windows-latest
macos-latest
```

---

# Example

```yaml
runs-on: ubuntu-latest
```

---

# Benefits

✔ Easy Setup

✔ Maintained by GitHub

✔ Automatic Updates

✔ Secure Environment

---

# Self Hosted Runner

Managed by organization.

Can run on:

- Physical Server
- VM
- Cloud Server
- Kubernetes Cluster

---

# Example

```yaml
runs-on: self-hosted
```

---

# Benefits

✔ Full Control

✔ Custom Software

✔ Private Network Access

✔ Internal Resources Access

---

# Runner Comparison

| Feature | GitHub Hosted | Self Hosted |
|-----------|------------|------------|
| Setup | Easy | Manual |
| Cost | GitHub | Organization |
| Maintenance | GitHub | Organization |
| Customization | Limited | Full |
| Security Control | Medium | High |

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

      - name: Build Application

        run: mvn clean package

      - name: Run Tests

        run: mvn test
```

---

# Execution Flow

```text
Push Code
      ↓
Workflow Trigger
      ↓
Runner Starts
      ↓
Job Starts
      ↓
Checkout Action
      ↓
Setup Java Action
      ↓
Build Command
      ↓
Test Command
      ↓
Workflow Complete
```

---

# Real-World Pipeline

```text
Developer Push
      ↓
GitHub Actions
      ↓
Runner
      ↓
Checkout Code
      ↓
Install Dependencies
      ↓
Build Project
      ↓
Run Tests
      ↓
Publish Results
```

---

# Advantages

| Component | Benefit |
|------------|-----------|
| Jobs | Organize workflow |
| Steps | Modular execution |
| Actions | Reusable automation |
| Runners | Flexible execution environment |

---

# Quick Revision Notes

## Job

```text
Collection of steps
```

---

## Step

```text
Single task
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

# Component Hierarchy

```text
Workflow
   ↓
Job
   ↓
Step
   ↓
Action / Command
```

---

# Viva Questions

### 1. What is a Job?

Collection of steps executed on a runner.

---

### 2. What is a Step?

Single task inside a job.

---

### 3. What is an Action?

Reusable automation component.

---

### 4. What is a Runner?

Machine that executes workflows.

---

### 5. Name two official GitHub Actions.

- actions/checkout
- actions/setup-java

---

### 6. Can jobs run in parallel?

Yes.

---

### 7. What keyword is used for actions?

```yaml
uses:
```

---

### 8. What keyword is used for shell commands?

```yaml
run:
```

---

# Interview Questions

## Q1. Difference between Job and Step?

Job = Collection of steps

Step = Individual task

---

## Q2. Difference between run and uses?

run:

```text
Executes shell commands
```

uses:

```text
Executes reusable actions
```

---

## Q3. Why use Actions instead of shell scripts?

Actions are reusable, maintained, and easier to manage.

---

## Q4. What is a Runner?

Execution environment for workflows.

---

## Q5. Difference between GitHub Hosted and Self Hosted Runner?

GitHub Hosted:

- Managed by GitHub

Self Hosted:

- Managed by organization

---

# Key Terms

| Term | Meaning |
|--------|----------|
| Job | Group of steps |
| Step | Single task |
| Action | Reusable automation |
| Runner | Execution machine |
| run | Execute commands |
| uses | Execute action |

---

# Summary

GitHub Actions workflows are built using:

```text
Workflow
   ↓
Jobs
   ↓
Steps
   ↓
Actions
```

and executed on:

```text
Runners
```

Understanding Jobs, Steps, Actions, and Runners is essential for creating professional CI/CD pipelines, Docker workflows, cloud deployments, and enterprise DevOps automation.
