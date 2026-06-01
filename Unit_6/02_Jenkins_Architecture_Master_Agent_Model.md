# Jenkins Architecture (Master-Agent Model)

![Jenkins](https://img.shields.io/badge/Jenkins-Architecture-red)
![CI/CD](https://img.shields.io/badge/CI/CD-Automation-blue)
![Master-Agent](https://img.shields.io/badge/Master-Agent-green)
![DevOps](https://img.shields.io/badge/DevOps-Pipeline-orange)

---

# 📚 Table of Contents

- What is Jenkins Architecture?
- Why Jenkins Uses Master-Agent Model
- Components of Jenkins Architecture
- Jenkins Controller (Master)
- Jenkins Agent (Slave)
- Communication Between Controller and Agents
- Build Execution Flow
- Distributed Builds
- Agent Types
- Advantages of Master-Agent Architecture
- Real-World Example
- Architecture Diagram
- Quick Revision Notes
- Viva Questions
- Interview Questions

---

# What is Jenkins Architecture?

Jenkins follows a **Master-Agent Architecture** (formerly called Master-Slave Architecture).

It allows Jenkins to:

✔ Distribute workloads

✔ Execute builds on multiple machines

✔ Scale CI/CD pipelines

✔ Improve performance

✔ Support multiple platforms

---

# Why Jenkins Uses Master-Agent Model?

Imagine a company with:

```text
500 Developers
100 Projects
Thousands of Builds Daily
```

Running everything on one machine would:

❌ Slow down builds

❌ Consume resources

❌ Cause failures

❌ Reduce scalability

Jenkins solves this using:

```text
Controller (Master)
          ↓
      Multiple Agents
```

---

# Basic Architecture

```text
Developer
    ↓
GitHub
    ↓
Jenkins Controller
    ↓
 ┌───────────────┐
 │               │
 ▼               ▼
Agent 1       Agent 2
(Linux)      (Windows)
```

---

# Main Components

Jenkins architecture contains:

1. Controller (Master)
2. Agent Nodes
3. Build Executors
4. Jobs
5. Workspace
6. Plugins
7. Pipelines

---

# Jenkins Controller (Master)

The Controller is the central brain of Jenkins.

Responsibilities:

✔ Manage Jenkins UI

✔ Schedule Builds

✔ Manage Agents

✔ Manage Users

✔ Store Configuration

✔ Manage Plugins

✔ Trigger Pipelines

---

# Controller Responsibilities

```text
Receive Build Request
        ↓
Assign Agent
        ↓
Monitor Build
        ↓
Collect Results
```

---

# Controller Example

Suppose:

Developer pushes code.

Controller:

```text
Receives Trigger
Chooses Agent
Starts Build
Collects Logs
Shows Results
```

---

# Jenkins Agent

An Agent is a worker machine that performs actual build tasks.

The Controller delegates work to Agents.

---

# Agent Responsibilities

✔ Build Applications

✔ Run Tests

✔ Create Artifacts

✔ Execute Scripts

✔ Deploy Applications

---

# Agent Example

```text
Controller:
"Build Java Project"

Agent:
Runs Maven Build
Runs Tests
Creates JAR
Returns Result
```

---

# Master-Agent Diagram

```text
             Jenkins Controller
                     │
     ┌───────────────┼───────────────┐
     │               │               │
     ▼               ▼               ▼

 Linux Agent   Windows Agent   Docker Agent

     │               │               │

 Build Java     Build .NET      Build Containers
```

---

# Why Use Agents?

Different projects require different environments.

Example:

| Project | OS Required |
|----------|------------|
| Java | Linux |
| .NET | Windows |
| iOS | macOS |

Instead of one huge server:

Use specialized agents.

---

# Communication Between Controller and Agents

Communication occurs securely.

Controller sends:

```text
Build Instructions
Pipeline Steps
Scripts
```

Agent sends:

```text
Build Logs
Test Results
Artifacts
Status
```

---

# Communication Flow

```text
Controller
     ↓
Assign Job
     ↓
Agent
     ↓
Execute Build
     ↓
Send Result
     ↓
Controller
```

---

# Build Execution Flow

Step 1

Developer pushes code.

```text
GitHub
```

---

# Step 2

Webhook triggers Jenkins.

---

# Step 3

Controller receives build request.

---

# Step 4

Controller selects available agent.

---

# Step 5

Agent checks out source code.

---

# Step 6

Agent executes build.

---

# Step 7

Agent runs tests.

---

# Step 8

Agent generates artifact.

---

# Step 9

Controller receives result.

---

# Build Flow Diagram

```text
GitHub
   ↓
Jenkins Controller
   ↓
Agent
   ↓
Build
   ↓
Test
   ↓
Artifact
   ↓
Success/Failure
```

---

# What is an Executor?

Executor = build slot.

Each executor can run one build at a time.

Example:

```text
Agent
 ├── Executor 1
 ├── Executor 2
 └── Executor 3
```

Can run:

```text
3 Builds Simultaneously
```

---

# Example

Agent:

```text
4 CPU Cores
```

Executors:

```text
4
```

Possible:

```text
4 Parallel Builds
```

---

# Distributed Builds

Distributed Builds mean:

```text
Multiple Agents
Running Builds
At Same Time
```

Example:

```text
Project A → Linux Agent

Project B → Windows Agent

Project C → Docker Agent
```

All run simultaneously.

---

# Advantages of Distributed Builds

✔ Faster Execution

✔ Better Resource Usage

✔ Scalability

✔ Parallel Processing

✔ Fault Isolation

---

# Agent Types

Jenkins supports multiple agent types.

---

## Permanent Agent

Always running.

Example:

```text
Dedicated Linux Server
```

---

## Dynamic Agent

Created when needed.

Example:

```text
Docker Containers
Kubernetes Pods
```

---

## Cloud Agent

Provisioned from cloud.

Examples:

- AWS EC2
- Azure VM
- Google Cloud

---

# Docker-Based Agents

Modern Jenkins often uses:

```text
Docker Containers
```

as agents.

Advantages:

✔ Lightweight

✔ Fast Startup

✔ Easy Cleanup

---

# Docker Agent Architecture

```text
Controller
     ↓
Docker Agent
     ↓
Build
     ↓
Destroy Container
```

---

# Kubernetes Agents

Enterprise Jenkins commonly uses:

```text
Kubernetes Pods
```

as temporary agents.

Benefits:

✔ Auto Scaling

✔ Better Isolation

✔ Resource Efficiency

---

# Workspace

Workspace is a directory where Jenkins stores:

```text
Source Code
Artifacts
Build Files
Logs
```

Example:

```text
/workspace/my-project
```

---

# Real-World Example

Company:

```text
Amazon
```

Projects:

```text
Java Application
Node.js API
Dockerized Service
```

Jenkins Setup:

```text
Controller
      ↓

Linux Agent → Java Build

Docker Agent → Docker Build

Node Agent → Node Build
```

Each project builds independently.

---

# Advantages of Master-Agent Architecture

| Advantage | Benefit |
|------------|---------|
| Scalability | More agents can be added |
| Faster Builds | Parallel execution |
| Resource Optimization | Workload distribution |
| Isolation | Build failures isolated |
| Flexibility | Different OS support |
| Reliability | Reduced controller load |

---

# Limitations

| Limitation | Description |
|------------|------------|
| Initial Setup | More configuration |
| Maintenance | Multiple machines |
| Networking | Agent connectivity required |
| Security | Agent access must be managed |

---

# Jenkins Architecture Summary

```text
Developer
     ↓
GitHub
     ↓
Jenkins Controller
     ↓
Agent
     ↓
Build
     ↓
Test
     ↓
Artifact
     ↓
Deployment
```

---

# Quick Revision Notes

## Controller

```text
Brain of Jenkins
```

---

## Agent

```text
Worker Machine
```

---

## Executor

```text
Build Slot
```

---

## Workspace

```text
Build Directory
```

---

## Distributed Build

```text
Parallel Builds Across Agents
```

---

## Dynamic Agent

```text
Created When Needed
```

---

# Viva Questions

### 1. What is Jenkins Architecture?

Master-Agent Architecture.

---

### 2. What is Jenkins Controller?

Central management node.

---

### 3. What is a Jenkins Agent?

Worker machine executing builds.

---

### 4. Why use Agents?

To distribute workloads.

---

### 5. What is an Executor?

A build execution slot.

---

### 6. What is a Workspace?

Directory used during build execution.

---

### 7. What are Distributed Builds?

Builds executed across multiple agents.

---

### 8. Can Jenkins work without agents?

Yes, controller can execute builds itself.

---

### 9. What is a Dynamic Agent?

Agent created temporarily.

---

### 10. Which modern platforms provide dynamic agents?

Docker and Kubernetes.

---

# Interview Questions

## Q1. Explain Jenkins Master-Agent Architecture.

Controller manages Jenkins and delegates build execution to agents.

---

## Q2. Why are agents used?

To improve scalability and performance.

---

## Q3. What is the role of executors?

Allow parallel build execution.

---

## Q4. What are the advantages of distributed builds?

Parallelism, scalability, and better resource utilization.

---

## Q5. Why are Docker agents popular?

Because they are lightweight, isolated, and easy to create.

---

# Key Takeaways

✔ Jenkins uses a Controller-Agent architecture.

✔ Controller manages jobs and agents.

✔ Agents execute builds and tests.

✔ Executors enable parallel builds.

✔ Distributed builds improve performance.

✔ Docker and Kubernetes are commonly used as modern Jenkins agents.

---

# Summary

The Jenkins Master-Agent Architecture is designed for scalability and efficient workload distribution. The Controller manages jobs and infrastructure, while Agents perform actual build and deployment tasks. This architecture enables Jenkins to support large-scale CI/CD pipelines used in modern enterprise environments.