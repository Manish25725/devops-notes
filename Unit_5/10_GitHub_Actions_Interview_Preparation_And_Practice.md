# GitHub Actions Interview Preparation & Practice

![GitHub Actions](https://img.shields.io/badge/GitHub-Actions-black)
![Interview](https://img.shields.io/badge/Interview-Preparation-blue)
![CI/CD](https://img.shields.io/badge/CI/CD-DevOps-green)
![Practice](https://img.shields.io/badge/Practice-Lab-orange)

---

# 📚 Table of Contents

- Unit V Quick Revision
- GitHub Actions Cheat Sheet
- Workflow Anatomy Revision
- Common YAML Mistakes
- Workflow Debugging
- Practice Exercises
- Hands-On Labs
- Viva Questions
- Interview Questions
- End-Term Quick Notes

---

# 🚀 Unit V Quick Revision

## Continuous Integration (CI)

Continuous Integration is a software development practice where code changes are automatically:

```text
Build
↓
Test
↓
Validated
```

whenever developers push code to a repository.

---

## GitHub Actions

GitHub Actions is GitHub's built-in CI/CD platform used to automate:

```text
Build
Test
Package
Deploy
```

---

## Workflow Location

```text
.github/
└── workflows/
```

Example:

```text
.github/workflows/ci.yml
```

---

# GitHub Actions Architecture

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

---

# GitHub Actions Cheat Sheet

## Workflow

```yaml
name: My Workflow
```

---

## Trigger

```yaml
on:
  push
```

---

## Job

```yaml
jobs:
  build:
```

---

## Runner

```yaml
runs-on: ubuntu-latest
```

---

## Step

```yaml
steps:
```

---

## Run Command

```yaml
run: echo "Hello"
```

---

## Use Action

```yaml
uses: actions/checkout@v4
```

---

# Common Workflow Template

```yaml
name: CI Pipeline

on:
  push:

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v4

      - run: echo "Build Started"
```

---

# Common YAML Mistakes

## Wrong Indentation

❌ Wrong

```yaml
jobs:
build:
runs-on:
```

---

✅ Correct

```yaml
jobs:

  build:

    runs-on: ubuntu-latest
```

---

## Missing Colon

❌ Wrong

```yaml
name Build
```

---

✅ Correct

```yaml
name: Build
```

---

## Incorrect Action Version

❌ Wrong

```yaml
uses: actions/checkout
```

---

✅ Correct

```yaml
uses: actions/checkout@v4
```

---

## Wrong Branch Name

❌ Wrong

```yaml
branches:
  - master
```

If repository uses:

```text
main
```

workflow won't trigger.

---

# Debugging GitHub Actions

---

## Check Logs

```text
Actions Tab
      ↓
Workflow Run
      ↓
Logs
```

---

## Enable Debug Logging

Repository Secret:

```text
ACTIONS_RUNNER_DEBUG=true
```

---

## Print Variables

```yaml
- run: env
```

---

## Check Current Directory

```yaml
- run: pwd
```

---

## List Files

```yaml
- run: ls -la
```

---

# Practice Exercise 1

Create workflow that:

✔ Runs on push

✔ Prints Hello World

---

### Solution

```yaml
name: Hello

on:
  push

jobs:

  test:

    runs-on: ubuntu-latest

    steps:

      - run: echo "Hello World"
```

---

# Practice Exercise 2

Create workflow that:

✔ Runs on pull request

✔ Prints repository name

---

### Solution

```yaml
name: PR Workflow

on:
  pull_request

jobs:

  test:

    runs-on: ubuntu-latest

    steps:

      - run: echo ${{ github.repository }}
```

---

# Practice Exercise 3

Create workflow using Java 21.

---

### Solution

```yaml
steps:

  - uses: actions/setup-java@v4

    with:

      distribution: temurin

      java-version: 21
```

---

# Practice Exercise 4

Create workflow using Node.js 20.

---

### Solution

```yaml
steps:

  - uses: actions/setup-node@v4

    with:

      node-version: 20
```

---

# Practice Exercise 5

Build Maven project.

---

### Solution

```yaml
- run: mvn clean package
```

---

# Hands-On Lab 1

## Build Java Application

Workflow:

```yaml
name: Java Build

on:
  push

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v4

      - uses: actions/setup-java@v4

        with:

          distribution: temurin

          java-version: 21

      - run: mvn clean package
```

---

# Hands-On Lab 2

## Build Node Application

```yaml
name: Node Build

on:
  push

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4

        with:

          node-version: 20

      - run: npm install

      - run: npm test
```

---

# Hands-On Lab 3

## Docker Build

```yaml
name: Docker Build

on:
  push

jobs:

  docker:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v4

      - run: docker build -t myapp .
```

---

# Hands-On Lab 4

## Docker Hub Push

```yaml
- uses: docker/login-action@v3

  with:

    username: ${{ secrets.DOCKER_USERNAME }}

    password: ${{ secrets.DOCKER_PASSWORD }}
```

---

# Hands-On Lab 5

## Deploy to Server

```yaml
- uses: appleboy/ssh-action@v1

  with:

    host: ${{ secrets.HOST }}

    username: ${{ secrets.USERNAME }}

    key: ${{ secrets.SSH_PRIVATE_KEY }}
```

---

# 50 Viva Questions

### 1. What is CI?

Continuous Integration.

### 2. What is GitHub Actions?

GitHub's CI/CD platform.

### 3. Where are workflows stored?

`.github/workflows`

### 4. Which language is used?

YAML

### 5. What starts a workflow?

Trigger

### 6. What is a job?

Collection of steps.

### 7. What is a step?

Single task.

### 8. What is an action?

Reusable automation component.

### 9. What is a runner?

Machine executing workflows.

### 10. What is a workflow?

Automation process.

### 11. What is push trigger?

Runs on code push.

### 12. What is pull_request trigger?

Runs on PR events.

### 13. What is workflow_dispatch?

Manual trigger.

### 14. What is schedule trigger?

Time-based trigger.

### 15. What is cron?

Scheduling format.

### 16. What is matrix strategy?

Multiple configurations execution.

### 17. What is needs?

Job dependency keyword.

### 18. What is artifact?

File shared between jobs.

### 19. What is cache?

Stored dependencies.

### 20. What is cache hit?

Cache found.

### 21. What is cache miss?

Cache not found.

### 22. What is setup-java?

Java installation action.

### 23. What is setup-node?

Node.js installation action.

### 24. What is setup-python?

Python installation action.

### 25. What is checkout action?

Repository clone action.

### 26. What is Docker Hub?

Container registry.

### 27. What is GHCR?

GitHub Container Registry.

### 28. What is Docker Buildx?

Advanced Docker builder.

### 29. What is image tagging?

Versioning Docker images.

### 30. What are GitHub Secrets?

Secure credential storage.

### 31. What is ubuntu-latest?

GitHub hosted Linux runner.

### 32. What is windows-latest?

GitHub hosted Windows runner.

### 33. What is self-hosted runner?

Organization-managed runner.

### 34. Why use CI?

Early bug detection.

### 35. Why automate builds?

Consistency.

### 36. Why automate deployment?

Speed and reliability.

### 37. What is Docker login action?

Registry authentication.

### 38. What is workflow file extension?

.yml

### 39. What is build stage?

Compile/package application.

### 40. What is test stage?

Validate functionality.

### 41. What is deployment stage?

Release application.

### 42. What is VPS?

Virtual Private Server.

### 43. What is EC2?

AWS Virtual Machine.

### 44. What is Azure VM?

Microsoft cloud virtual machine.

### 45. What is SSH?

Secure Shell.

### 46. What is rolling deployment?

Gradual update.

### 47. What is blue-green deployment?

Dual environment deployment.

### 48. What is canary deployment?

Small-user rollout.

### 49. What is CI/CD?

Automated software delivery.

### 50. Why use GitHub Actions?

Integrated automation platform.

---

# 30 Interview Questions

## Q1. Explain GitHub Actions architecture.

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

---

## Q2. Difference between Job and Step?

Job = collection of steps

Step = individual task

---

## Q3. Difference between run and uses?

run = execute commands

uses = execute actions

---

## Q4. Explain Matrix Strategy.

Run same job across multiple configurations.

---

## Q5. What is artifact sharing?

Passing files between jobs.

---

## Q6. How does caching improve performance?

Avoids downloading dependencies repeatedly.

---

## Q7. What are GitHub-hosted runners?

Managed by GitHub.

---

## Q8. What are self-hosted runners?

Managed by organization.

---

## Q9. Explain Docker integration in GitHub Actions.

Build → Push → Deploy containers automatically.

---

## Q10. What is GHCR?

GitHub Container Registry.

---

## Q11. Why use GitHub Secrets?

Secure credential management.

---

## Q12. Explain workflow triggers.

Events that start workflows.

---

## Q13. Difference between CI and CD?

CI = Build/Test

CD = Deploy

---

## Q14. Explain Docker Buildx.

Multi-platform image builder.

---

## Q15. What is deployment automation?

Automatic application release.

---

## Q16–30 (Short Answers)

- Explain pull_request trigger.
- Explain workflow_dispatch.
- What is schedule trigger?
- What is cron syntax?
- What is Docker Hub?
- What is EC2?
- What is Azure VM?
- Explain SSH deployment.
- Explain Blue-Green deployment.
- Explain Rolling deployment.
- Explain Canary deployment.
- What are Marketplace Actions?
- What is checkout action?
- What is setup-java action?
- Explain dependency caching.

---

# End-Term Quick Notes

```text
Workflow → Jobs → Steps → Actions

Triggers:
push
pull_request
schedule
workflow_dispatch

Runners:
GitHub Hosted
Self Hosted

Docker:
Build
Push
Deploy

Registries:
Docker Hub
GHCR

Deployments:
VPS
AWS EC2
Azure VM

Strategies:
Rolling
Blue-Green
Canary
```

---

# 🎯 Unit V Summary

By completing Unit V, you have learned:

✅ Continuous Integration (CI)

✅ GitHub Actions Workflows

✅ Triggers & Events

✅ Jobs, Steps & Actions

✅ Matrix Strategies

✅ Caching

✅ GitHub Hosted & Self-Hosted Runners

✅ Docker Integration

✅ Docker Hub & GHCR

✅ Automated Deployments

✅ Cloud Deployments

✅ Deployment Strategies

This unit provides the foundation for modern DevOps CI/CD pipelines used in companies like Amazon, Netflix, Google, Microsoft, and GitHub.