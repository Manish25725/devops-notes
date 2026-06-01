# Matrix Strategies & Multi-Job Workflows

![GitHub Actions](https://img.shields.io/badge/GitHub-Actions-black)
![CI/CD](https://img.shields.io/badge/CI/CD-Automation-blue)
![Matrix](https://img.shields.io/badge/Matrix-Strategy-green)
![DevOps](https://img.shields.io/badge/DevOps-Pipelines-orange)

---

# 📚 Table of Contents

- Introduction
- What is a Matrix Strategy?
- Why Matrix Builds are Needed
- Matrix Workflow Syntax
- Testing Multiple Operating Systems
- Testing Multiple Language Versions
- Multi-Dimensional Matrix
- Matrix Include & Exclude
- What are Multi-Job Workflows?
- Job Dependencies
- needs Keyword
- Parallel vs Sequential Jobs
- Sharing Artifacts Between Jobs
- Real-World CI Pipelines
- Best Practices
- Quick Revision
- Viva Questions
- Interview Questions

---

# Introduction

As projects grow larger, developers need to:

✔ Test multiple environments

✔ Test different language versions

✔ Run jobs in parallel

✔ Build complex CI/CD pipelines

GitHub Actions provides:

```text
Matrix Strategy
```

and

```text
Multi-Job Workflows
```

to solve these challenges.

---

# What is a Matrix Strategy?

A Matrix Strategy allows a job to run multiple times using different configurations.

Instead of writing:

```yaml
Job 1 → Ubuntu
Job 2 → Windows
Job 3 → macOS
```

GitHub automatically generates them.

---

# Matrix Concept

```text
One Job Definition
        ↓
Many Job Executions
```

---

# Example

```yaml
strategy:

  matrix:

    os:

      - ubuntu-latest

      - windows-latest

      - macos-latest
```

---

# Generated Jobs

```text
Build (Ubuntu)

Build (Windows)

Build (macOS)
```

---

# Why Matrix Builds Are Needed

Imagine a Node.js application.

Users run it on:

```text
Windows
Linux
macOS
```

Testing only Linux is risky.

Matrix builds verify compatibility everywhere.

---

# Traditional Approach

```text
Write Separate Job
Write Separate Job
Write Separate Job
```

Large and repetitive.

---

# Matrix Approach

```text
One Job
Multiple Configurations
```

Cleaner and scalable.

---

# Basic Matrix Example

```yaml
jobs:

  build:

    strategy:

      matrix:

        os:

          - ubuntu-latest

          - windows-latest

          - macos-latest

    runs-on: ${{ matrix.os }}

    steps:

      - run: echo "Running on ${{ matrix.os }}"
```

---

# Execution

GitHub automatically creates:

```text
Build (Ubuntu)

Build (Windows)

Build (macOS)
```

---

# Matrix Execution Diagram

```text
Build Job
     │
     ├── Ubuntu
     ├── Windows
     └── macOS
```

---

# Testing Multiple Java Versions

A Java application may support:

```text
Java 17
Java 21
```

---

# Example

```yaml
strategy:

  matrix:

    java:

      - 17

      - 21
```

---

# Complete Example

```yaml
jobs:

  build:

    strategy:

      matrix:

        java:

          - 17

          - 21

    runs-on: ubuntu-latest

    steps:

      - uses: actions/setup-java@v4

        with:

          distribution: temurin

          java-version: ${{ matrix.java }}

      - run: mvn test
```

---

# Generated Jobs

```text
Java 17 Build

Java 21 Build
```

---

# Testing Multiple Node Versions

Example:

```yaml
strategy:

  matrix:

    node:

      - 18

      - 20

      - 22
```

---

# Result

```text
Node 18 Test

Node 20 Test

Node 22 Test
```

---

# Multi-Dimensional Matrix

Matrix can combine variables.

---

# Example

```yaml
strategy:

  matrix:

    os:

      - ubuntu-latest

      - windows-latest

    java:

      - 17

      - 21
```

---

# Generated Jobs

```text
Ubuntu + Java 17

Ubuntu + Java 21

Windows + Java 17

Windows + Java 21
```

---

# Matrix Visualization

```text
           Java17   Java21

Ubuntu        ✔        ✔

Windows       ✔        ✔
```

---

# Include Keyword

Used to add extra configurations.

---

# Example

```yaml
strategy:

  matrix:

    java: [17,21]

    include:

      - java: 23

        experimental: true
```

---

# Generated

```text
Java 17

Java 21

Java 23 Experimental
```

---

# Exclude Keyword

Used to skip combinations.

---

# Example

```yaml
strategy:

  matrix:

    os:

      - ubuntu-latest

      - windows-latest

    java:

      - 17

      - 21

    exclude:

      - os: windows-latest

        java: 21
```

---

# Excluded Combination

```text
Windows + Java 21
```

will not execute.

---

# Matrix Benefits

| Benefit | Description |
|----------|----------|
| Scalability | Easy testing |
| Automation | No duplication |
| Coverage | Multiple environments |
| Reliability | Cross-platform testing |

---

# What are Multi-Job Workflows?

A workflow can contain multiple jobs.

Example:

```text
Build
Test
Deploy
```

Each represented as a separate job.

---

# Multi-Job Architecture

```text
Workflow

│
├── Build
│
├── Test
│
└── Deploy
```

---

# Example

```yaml
jobs:

  build:

  test:

  deploy:
```

---

# Why Use Multiple Jobs?

Different stages require:

```text
Build
Testing
Security Scanning
Packaging
Deployment
```

Keeping them separate improves maintainability.

---

# Job Dependency

By default:

```text
Jobs run in parallel
```

---

# Example

```text
Build

Test

Deploy
```

may start simultaneously.

---

# needs Keyword

Used to create dependencies.

---

# Example

```yaml
test:

  needs: build
```

---

# Meaning

```text
Build finishes
      ↓
Test starts
```

---

# Sequential Pipeline

```yaml
build

test:
  needs: build

deploy:
  needs: test
```

---

# Execution Flow

```text
Build
   ↓
Test
   ↓
Deploy
```

---

# Multiple Dependencies

```yaml
deploy:

  needs:

    - build

    - test
```

---

# Meaning

Deploy waits for:

```text
Build ✔

AND

Test ✔
```

---

# Dependency Diagram

```text
Build
   │
   └─────┐
         │
Test ────┘
         ↓
      Deploy
```

---

# Parallel Jobs

Example:

```yaml
jobs:

  lint:

  build:

  security:
```

---

# Execution

```text
Lint
Build
Security

Run Together
```

---

# Benefits

✔ Faster pipelines

✔ Better resource utilization

---

# Sharing Data Between Jobs

Jobs run on separate runners.

Files are not automatically shared.

---

# Solution

Use:

```text
Artifacts
```

---

# Upload Artifact

```yaml
- name: Upload

  uses: actions/upload-artifact@v4

  with:

    name: app

    path: target/*.jar
```

---

# Download Artifact

```yaml
- name: Download

  uses: actions/download-artifact@v4

  with:

    name: app
```

---

# Artifact Flow

```text
Build Job
      ↓
Upload Artifact
      ↓
Storage
      ↓
Download Artifact
      ↓
Deploy Job
```

---

# Real-World Java Pipeline

```text
Push Code
     ↓
Build Job
     ↓
Unit Test Job
     ↓
Integration Test Job
     ↓
Package Job
     ↓
Deploy Job
```

---

# Example

```yaml
jobs:

  build:

    runs-on: ubuntu-latest

  test:

    needs: build

    runs-on: ubuntu-latest

  deploy:

    needs: test

    runs-on: ubuntu-latest
```

---

# Enterprise Pipeline

```text
Build
   ↓
Code Quality Scan
   ↓
Security Scan
   ↓
Unit Tests
   ↓
Integration Tests
   ↓
Docker Build
   ↓
Deployment
```

---

# Combining Matrix + Multi-Job

```text
Build Matrix

Ubuntu
Windows
macOS

        ↓

Test Job

        ↓

Deploy Job
```

---

# Complete Example

```yaml
jobs:

  build:

    strategy:

      matrix:

        java:

          - 17

          - 21

    runs-on: ubuntu-latest

  deploy:

    needs: build

    runs-on: ubuntu-latest
```

---

# Best Practices

✔ Use matrix for version testing

✔ Use needs for dependencies

✔ Keep jobs small

✔ Use artifacts for sharing

✔ Avoid duplicate workflows

✔ Run independent jobs in parallel

---

# Quick Revision Notes

## Matrix Strategy

```text
One Job
Many Configurations
```

---

## needs

```text
Creates dependency
```

---

## Parallel Jobs

```text
Run simultaneously
```

---

## Sequential Jobs

```text
Run one after another
```

---

## Artifact

```text
Share files between jobs
```

---

# Matrix Example

```yaml
strategy:

  matrix:

    java:

      - 17

      - 21
```

---

# Dependency Example

```yaml
test:

  needs: build
```

---

# Viva Questions

### 1. What is a Matrix Strategy?

A feature that allows one job to run with multiple configurations.

---

### 2. Why use Matrix builds?

To test across multiple environments.

---

### 3. What keyword creates job dependency?

```yaml
needs
```

---

### 4. Do jobs run sequentially by default?

No.

They run in parallel.

---

### 5. How do jobs share files?

Using artifacts.

---

### 6. What is upload-artifact?

Used to store files for later jobs.

---

### 7. What is download-artifact?

Used to retrieve stored artifacts.

---

### 8. Can matrix jobs run simultaneously?

Yes.

---

# Interview Questions

## Q1. Explain Matrix Strategy.

Matrix Strategy automatically creates multiple job executions using different configurations.

---

## Q2. Why use matrix builds in CI?

To verify software compatibility across platforms and versions.

---

## Q3. Difference between parallel and sequential jobs?

Parallel:

```text
Run together
```

Sequential:

```text
Run using needs dependency
```

---

## Q4. How do you create a dependency between jobs?

```yaml
needs:
```

---

## Q5. How can one job use files generated by another?

Using upload-artifact and download-artifact actions.

---

# Key Terms

| Term | Meaning |
|--------|---------|
| Matrix | Multiple configurations |
| Strategy | Job execution plan |
| needs | Job dependency |
| Artifact | Shared file |
| Parallel Job | Simultaneous execution |
| Sequential Job | Dependency-based execution |

---

# Summary

Matrix Strategies enable testing across:

✔ Multiple OS versions

✔ Multiple language versions

✔ Multiple environments

Multi-job workflows allow:

✔ Build pipelines

✔ Testing pipelines

✔ Deployment pipelines

using dependencies and artifacts.

These concepts are fundamental for building enterprise-grade CI/CD systems in GitHub Actions.