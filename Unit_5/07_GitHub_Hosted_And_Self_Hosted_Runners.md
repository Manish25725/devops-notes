# GitHub Hosted Runners & Self-Hosted Runners

![GitHub Actions](https://img.shields.io/badge/GitHub-Actions-black)
![Runner](https://img.shields.io/badge/Runner-Execution_Environment-blue)
![CI/CD](https://img.shields.io/badge/CI/CD-Automation-green)
![DevOps](https://img.shields.io/badge/DevOps-Infrastructure-orange)

---

# 📚 Table of Contents

- What is a Runner?
- Why Runners are Needed
- GitHub Hosted Runners
- Supported Operating Systems
- Runner Lifecycle
- Self-Hosted Runners
- Installing Self-Hosted Runners
- Runner Security
- Runner Management
- Hosted vs Self-Hosted Comparison
- Enterprise Use Cases
- Best Practices
- Quick Revision Notes
- Viva Questions
- Interview Questions

---

# What is a Runner?

A Runner is a machine that executes GitHub Actions workflows.

Whenever a workflow starts:

```text
Workflow Trigger
       ↓
Runner Starts
       ↓
Jobs Execute
       ↓
Workflow Completes
```

Without runners, workflows cannot execute.

---

# Runner Architecture

```text
Developer Pushes Code
          ↓
GitHub Actions
          ↓
Runner
          ↓
Job
          ↓
Step
          ↓
Result
```

---

# Why Runners are Needed?

GitHub Actions only defines:

```yaml
Workflow
Jobs
Steps
```

But actual execution requires:

```text
CPU
RAM
Storage
Operating System
Network
```

These resources are provided by runners.

---

# Types of Runners

GitHub Actions supports two types:

```text
1. GitHub Hosted Runners

2. Self-Hosted Runners
```

---

# GitHub Hosted Runners

GitHub Hosted Runners are virtual machines provided and managed by GitHub.

You simply write:

```yaml
runs-on: ubuntu-latest
```

GitHub automatically:

```text
Creates VM
Runs Workflow
Deletes VM
```

---

# Hosted Runner Workflow

```text
Workflow Trigger
       ↓
GitHub Creates VM
       ↓
Execute Jobs
       ↓
Destroy VM
```

---

# Example

```yaml
jobs:

  build:

    runs-on: ubuntu-latest
```

---

# Supported GitHub Hosted Runners

## Ubuntu

```yaml
runs-on: ubuntu-latest
```

Most commonly used.

---

## Windows

```yaml
runs-on: windows-latest
```

Used for:

- .NET Applications
- Windows Software

---

## macOS

```yaml
runs-on: macos-latest
```

Used for:

- iOS Development
- Apple Applications

---

# Supported Platforms

| Runner | OS |
|----------|----------|
| ubuntu-latest | Linux |
| windows-latest | Windows |
| macos-latest | macOS |

---

# Preinstalled Software

GitHub Hosted Runners already contain:

```text
Git
Docker
Java
Node.js
Python
Go
.NET SDK
Maven
Gradle
```

Many tools are pre-installed.

---

# Example

```yaml
runs-on: ubuntu-latest
```

Then immediately:

```yaml
run: java --version
```

works without manual installation.

---

# Advantages of GitHub Hosted Runners

## Easy Setup

No infrastructure management.

---

## Automatic Updates

GitHub maintains software updates.

---

## Scalability

GitHub automatically provides runners.

---

## Security

Fresh VM for every workflow run.

---

## Maintenance Free

No patching or monitoring required.

---

# Limitations of Hosted Runners

## Limited Customization

Cannot install permanent software.

---

## Internet Dependency

Must communicate with GitHub.

---

## Usage Limits

Free plans have runner minute limits.

---

## Temporary Environment

Everything deleted after workflow finishes.

---

# Hosted Runner Lifecycle

```text
Start Workflow
      ↓
Create VM
      ↓
Execute Job
      ↓
Upload Logs
      ↓
Delete VM
```

---

# What is a Self-Hosted Runner?

A Self-Hosted Runner is managed by the organization.

Instead of GitHub creating a VM:

```text
Your Server Executes Workflow
```

---

# Self-Hosted Runner Architecture

```text
GitHub Actions
       ↓
Company Server
       ↓
Runner Software
       ↓
Workflow Execution
```

---

# Example

```yaml
runs-on: self-hosted
```

---

# Where Can Self-Hosted Runners Run?

They can be installed on:

- Physical Servers
- Virtual Machines
- AWS EC2
- Azure VMs
- Google Cloud VMs
- Kubernetes Nodes
- Personal Computers

---

# Why Use Self-Hosted Runners?

Sometimes organizations need:

```text
Private Networks
Custom Software
Internal Databases
Special Hardware
```

Hosted runners cannot access these resources.

---

# Example Scenario

Company Database:

```text
10.0.0.5
```

Only accessible from internal network.

GitHub Hosted Runner:

```text
Cannot Access
```

Self-Hosted Runner:

```text
Can Access
```

---

# Installing Self-Hosted Runner

Navigate to:

```text
Repository
      ↓
Settings
      ↓
Actions
      ↓
Runners
      ↓
New Self Hosted Runner
```

---

# GitHub Provides Commands

Example:

```bash
mkdir actions-runner

cd actions-runner
```

---

# Download Runner

```bash
curl -o actions-runner.tar.gz \
https://github.com/actions/runner/releases/latest/download/actions-runner-linux-x64.tar.gz
```

---

# Extract Files

```bash
tar xzf actions-runner.tar.gz
```

---

# Configure Runner

```bash
./config.sh
```

GitHub provides:

```text
Runner URL
Authentication Token
```

---

# Start Runner

```bash
./run.sh
```

Runner becomes available.

---

# Verification

GitHub Repository:

```text
Settings
      ↓
Actions
      ↓
Runners
```

Status:

```text
Online
```

---

# Using Self-Hosted Runner

Workflow:

```yaml
jobs:

  build:

    runs-on: self-hosted
```

---

# Custom Labels

Organizations often create labels.

Example:

```yaml
runs-on:

  - self-hosted

  - linux

  - docker
```

---

# Label Architecture

```text
Self Hosted
      ↓
Linux
      ↓
Docker Installed
```

Workflow selects matching runner.

---

# Runner Security

Security is extremely important.

Self-hosted runners execute arbitrary workflow code.

---

# Security Risks

Potential risks:

```text
Malicious Code
Unauthorized Access
Credential Theft
Data Leakage
```

---

# Security Best Practices

## Use Dedicated Runner Machines

Avoid using personal systems.

---

## Restrict Repository Access

Only trusted repositories should use runners.

---

## Use Firewalls

Protect internal systems.

---

## Rotate Secrets

Regularly update:

```text
Tokens
Passwords
Certificates
```

---

## Monitor Activity

Track workflow execution logs.

---

# Runner Management

Organizations often manage:

```text
10
100
1000+
```

runners.

---

# Management Tasks

- Updates
- Monitoring
- Scaling
- Security
- Resource Allocation

---

# Auto Scaling

Large companies use:

```text
Kubernetes
AWS Auto Scaling
Azure Scale Sets
```

to dynamically create runners.

---

# Runner Groups

GitHub supports Runner Groups.

Example:

```text
Development Runners

Testing Runners

Production Runners
```

---

# Enterprise Architecture

```text
GitHub

      ↓

Runner Group

 ├── Build Runner
 ├── Test Runner
 └── Deploy Runner
```

---

# Hosted vs Self-Hosted Comparison

| Feature | Hosted Runner | Self-Hosted Runner |
|----------|----------|----------|
| Managed By | GitHub | Organization |
| Setup | Easy | Manual |
| Maintenance | GitHub | Organization |
| Cost | Included Minutes | Infrastructure Cost |
| Security Control | Limited | Full |
| Custom Software | Limited | Full |
| Internal Network Access | No | Yes |
| Scalability | Automatic | Manual/Custom |

---

# When to Use Hosted Runners?

Use Hosted Runners when:

✔ Open Source Projects

✔ Small Teams

✔ Learning GitHub Actions

✔ Standard CI/CD Workflows

✔ No Special Infrastructure

---

# When to Use Self-Hosted Runners?

Use Self-Hosted Runners when:

✔ Internal Networks

✔ Enterprise Applications

✔ Custom Hardware

✔ Security Requirements

✔ Private Databases

✔ On-Premise Infrastructure

---

# Real-World Example

## Startup

Uses:

```text
GitHub Hosted Runner
```

Reason:

```text
Simple
Cheap
Easy
```

---

## Enterprise Bank

Uses:

```text
Self Hosted Runner
```

Reason:

```text
Private Network
Compliance
Security
Internal Systems
```

---

# Best Practices

✔ Prefer Hosted Runners initially

✔ Use Self-Hosted only when needed

✔ Secure runner machines

✔ Monitor resource usage

✔ Keep runners updated

✔ Use labels for organization

✔ Separate production runners

---

# Quick Revision Notes

## Runner

```text
Machine executing workflows
```

---

## Hosted Runner

```text
Managed by GitHub
```

---

## Self-Hosted Runner

```text
Managed by organization
```

---

## Hosted Example

```yaml
runs-on: ubuntu-latest
```

---

## Self Hosted Example

```yaml
runs-on: self-hosted
```

---

# Hosted Runner Flow

```text
Workflow
    ↓
Create VM
    ↓
Execute
    ↓
Destroy VM
```

---

# Self Hosted Flow

```text
Workflow
    ↓
Company Server
    ↓
Execute
```

---

# Viva Questions

### 1. What is a Runner?

A machine that executes GitHub Actions workflows.

---

### 2. What are the two types of runners?

- GitHub Hosted Runner
- Self Hosted Runner

---

### 3. Who manages Hosted Runners?

GitHub.

---

### 4. Who manages Self-Hosted Runners?

Organization/User.

---

### 5. Which keyword selects a hosted Linux runner?

```yaml
runs-on: ubuntu-latest
```

---

### 6. Which keyword selects a self-hosted runner?

```yaml
runs-on: self-hosted
```

---

### 7. Can self-hosted runners access internal company networks?

Yes.

---

### 8. Why are hosted runners considered secure?

Because a fresh VM is created for each workflow run.

---

# Interview Questions

## Q1. Difference between Hosted and Self-Hosted Runners?

Hosted:

```text
Managed by GitHub
```

Self-Hosted:

```text
Managed by Organization
```

---

## Q2. Why do enterprises prefer self-hosted runners?

For security, compliance, and internal network access.

---

## Q3. What are the risks of self-hosted runners?

Running untrusted code may compromise systems.

---

## Q4. Can runners be grouped?

Yes.

Using Runner Groups.

---

## Q5. When should you choose hosted runners?

For standard CI/CD pipelines with no special infrastructure requirements.

---

# Key Terms

| Term | Meaning |
|---------|---------|
| Runner | Workflow execution machine |
| Hosted Runner | GitHub-managed runner |
| Self-Hosted Runner | Organization-managed runner |
| Runner Group | Collection of runners |
| Label | Runner identifier |
| Auto Scaling | Dynamic runner creation |

---

# Summary

GitHub Actions workflows execute on runners.

Two options are available:

```text
GitHub Hosted Runner
```

and

```text
Self Hosted Runner
```

Hosted runners are easy, secure, and maintenance-free.

Self-hosted runners provide full control, custom software support, and access to internal infrastructure, making them ideal for enterprise environments.