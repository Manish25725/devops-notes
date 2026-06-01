# Workflow Triggers in GitHub Actions

![GitHub Actions](https://img.shields.io/badge/GitHub-Actions-black)
![Triggers](https://img.shields.io/badge/Workflow-Triggers-blue)
![Automation](https://img.shields.io/badge/CI-CD-green)

---

# 📚 Table of Contents

- What are Workflow Triggers?
- Why Triggers are Important
- Events in GitHub Actions
- Push Trigger
- Pull Request Trigger
- Schedule Trigger
- Manual Trigger (workflow_dispatch)
- Multiple Triggers
- Branch-Specific Triggers
- Path-Based Triggers
- Real-World Examples
- Trigger Flow Diagrams
- Quick Revision Notes
- Viva Questions
- Interview Questions

---

# What are Workflow Triggers?

A trigger is an event that starts a workflow.

Whenever a specified event occurs, GitHub automatically executes the workflow.

---

## Simple Flow

```text
Event Occurs
      ↓
Trigger Activated
      ↓
Workflow Starts
      ↓
Jobs Execute
```

---

# Why Triggers are Important?

Without triggers:

```text
Developer manually starts build
Developer manually runs tests
Developer manually deploys
```

Lots of manual work.

---

With triggers:

```text
Push Code
     ↓
Build Automatically

Create PR
     ↓
Run Tests Automatically

Every Day
     ↓
Run Scheduled Job
```

---

# GitHub Events

GitHub provides hundreds of events.

Most common:

| Event | Purpose |
|---------|----------|
| push | Code pushed |
| pull_request | PR created/updated |
| schedule | Run at fixed time |
| workflow_dispatch | Manual execution |
| release | Release created |
| issue | Issue created |
| fork | Repository forked |

---

# Trigger Syntax

```yaml
on:
  push
```

Meaning:

```text
Start workflow whenever code is pushed
```

---

# Push Trigger

Push trigger runs workflow whenever code is pushed.

---

## Example

```yaml
on:
  push
```

---

# Workflow

```text
Developer Pushes Code
          ↓
GitHub Detects Push
          ↓
Workflow Starts
```

---

# Example Workflow

```yaml
name: Build Project

on:
  push

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - run: echo "Build Started"
```

---

# Real Use Cases

Push trigger commonly used for:

```text
✔ Build Project
✔ Run Tests
✔ Code Quality Checks
✔ Security Scanning
```

---

# Push Trigger with Branch Filtering

Only run workflow for main branch.

```yaml
on:

  push:

    branches:

      - main
```

---

# Multiple Branches

```yaml
on:

  push:

    branches:

      - main

      - dev
```

Workflow starts only on:

```text
main
dev
```

---

# Ignoring Branches

```yaml
on:

  push:

    branches-ignore:

      - experimental
```

---

# Pull Request Trigger

Runs whenever:

- PR created
- PR updated
- PR reopened

---

## Syntax

```yaml
on:
  pull_request
```

---

# Flow

```text
Developer Creates PR
          ↓
Workflow Starts
          ↓
Tests Execute
          ↓
Merge Decision
```

---

# Example

```yaml
on:

  pull_request:

    branches:

      - main
```

---

# Use Cases

Before merging:

```text
✔ Build
✔ Unit Tests
✔ Integration Tests
✔ Code Analysis
```

---

# Example Pipeline

```text
Create PR
      ↓
Run Tests
      ↓
Pass?
  ↓      ↓
Yes      No
 ↓        ↓
Merge   Reject
```

---

# Schedule Trigger

Runs workflow automatically based on time.

Uses:

```text
Cron Expressions
```

---

# Syntax

```yaml
on:

  schedule:

    - cron: '0 0 * * *'
```

---

# Meaning

```text
Run every day at midnight
```

---

# Cron Format

```text
* * * * *
│ │ │ │ │
│ │ │ │ └── Day of Week
│ │ │ └──── Month
│ │ └────── Day
│ └──────── Hour
└────────── Minute
```

---

# Common Cron Examples

| Expression | Meaning |
|------------|----------|
| `0 0 * * *` | Daily midnight |
| `0 12 * * *` | Every day at noon |
| `0 * * * *` | Every hour |
| `*/15 * * * *` | Every 15 minutes |
| `0 0 * * 0` | Every Sunday |

---

# Example

```yaml
on:

  schedule:

    - cron: '0 0 * * *'
```

---

# Real Use Cases

Schedule trigger often used for:

```text
✔ Nightly Builds
✔ Database Backups
✔ Security Scans
✔ Dependency Updates
✔ Health Checks
```

---

# Manual Trigger

Sometimes we want to start workflow manually.

GitHub provides:

```text
workflow_dispatch
```

---

# Syntax

```yaml
on:

  workflow_dispatch:
```

---

# Flow

```text
Developer
     ↓
Clicks "Run Workflow"
     ↓
Workflow Starts
```

---

# Example

```yaml
name: Manual Deployment

on:

  workflow_dispatch
```

---

# Usage

GitHub Repository

```text
Actions Tab
      ↓
Run Workflow
      ↓
Execute
```

---

# Manual Trigger with Inputs

```yaml
on:

  workflow_dispatch:

    inputs:

      environment:

        description: 'Environment'

        required: true

        default: 'staging'
```

---

# User Chooses

```text
staging
production
testing
```

before execution.

---

# Multiple Triggers

A workflow can have multiple triggers.

---

# Example

```yaml
on:

  push:

  pull_request:

  workflow_dispatch:
```

---

# Meaning

Workflow runs when:

```text
✔ Push Happens

OR

✔ Pull Request Created

OR

✔ Manual Run
```

---

# Real Example

```yaml
on:

  push:

    branches:

      - main

  pull_request:

    branches:

      - main

  workflow_dispatch:
```

---

# Branch-Specific Triggers

---

# Production Branch

```yaml
on:

  push:

    branches:

      - production
```

---

# Development Branch

```yaml
on:

  push:

    branches:

      - dev
```

---

# Multiple Branches

```yaml
on:

  push:

    branches:

      - main

      - dev

      - release
```

---

# Path-Based Triggers

Run workflow only when specific files change.

---

# Example

```yaml
on:

  push:

    paths:

      - 'src/**'
```

---

# Meaning

Workflow starts only if:

```text
src/
```

files change.

---

# Example

```yaml
on:

  push:

    paths:

      - 'Dockerfile'

      - '.github/workflows/**'
```

---

# Real Use Cases

```text
✔ Docker Build only when Dockerfile changes

✔ Java Build only when source code changes

✔ Documentation workflow only when docs change
```

---

# Complete Trigger Example

```yaml
name: CI Pipeline

on:

  push:

    branches:

      - main

  pull_request:

    branches:

      - main

  schedule:

    - cron: '0 0 * * *'

  workflow_dispatch:
```

---

# Workflow Starts When

```text
✔ Code pushed to main

✔ Pull request created

✔ Daily midnight schedule

✔ Manual execution
```

---

# Trigger Execution Diagram

```text
Push Event
      │
      ├── Workflow

Pull Request
      │
      ├── Workflow

Schedule
      │
      ├── Workflow

Manual
      │
      └── Workflow
```

---

# Real-World CI Example

```text
Developer Push
      ↓
Build

Developer Creates PR
      ↓
Run Tests

Every Midnight
      ↓
Security Scan

Manual
      ↓
Deploy Production
```

---

# Advantages of Triggers

| Feature | Benefit |
|-----------|----------|
| Automation | No manual execution |
| Reliability | Consistent workflows |
| Speed | Faster feedback |
| Flexibility | Many event types |
| Scalability | Supports enterprise pipelines |

---

# Quick Revision Notes

## Push Trigger

```yaml
on:
  push
```

Runs on code push.

---

## Pull Request Trigger

```yaml
on:
  pull_request
```

Runs on PR activity.

---

## Schedule Trigger

```yaml
on:

  schedule:

    - cron: '0 0 * * *'
```

Runs periodically.

---

## Manual Trigger

```yaml
on:

  workflow_dispatch
```

Runs manually.

---

# Common Cron Expressions

| Cron | Meaning |
|--------|----------|
| `0 0 * * *` | Daily |
| `0 * * * *` | Hourly |
| `*/15 * * * *` | Every 15 min |
| `0 0 * * 0` | Weekly |

---

# Viva Questions

### 1. What is a trigger?

An event that starts a workflow.

---

### 2. Which trigger runs when code is pushed?

```yaml
push
```

---

### 3. Which trigger runs when PR is created?

```yaml
pull_request
```

---

### 4. Which trigger supports scheduling?

```yaml
schedule
```

---

### 5. Which trigger supports manual execution?

```yaml
workflow_dispatch
```

---

### 6. What is a cron expression?

A schedule format used for timed workflow execution.

---

### 7. Can one workflow have multiple triggers?

Yes.

---

### 8. Can workflows run only on specific branches?

Yes.

Using:

```yaml
branches:
```

---

# Interview Questions

## Q1. Difference between Push and Pull Request triggers?

Push:

```text
Runs after code push.
```

Pull Request:

```text
Runs during merge review.
```

---

## Q2. Why use Pull Request triggers?

To validate code before merging.

---

## Q3. What is workflow_dispatch?

Manual workflow execution trigger.

---

## Q4. How do scheduled workflows work?

Using cron expressions.

---

## Q5. Explain branch filtering.

Allows workflows to run only for specified branches.

---

# Key Terms

| Term | Meaning |
|---------|---------|
| Trigger | Event starting workflow |
| Push | Code pushed |
| Pull Request | PR event |
| Schedule | Time-based execution |
| workflow_dispatch | Manual execution |
| Cron | Scheduling format |

---

# Summary

Workflow triggers determine when GitHub Actions workflows start.

Most commonly used triggers:

```yaml
push
pull_request
schedule
workflow_dispatch
```

Triggers help automate:

✔ Builds

✔ Tests

✔ Security Scans

✔ Deployments

✔ Maintenance Tasks

Understanding triggers is the foundation for building powerful CI/CD pipelines in GitHub Actions.