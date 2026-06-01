
# Docker Compose — Essential Commands

![Docker](https://img.shields.io/badge/Docker-Compose-blue)
![Commands](https://img.shields.io/badge/Linux-Commands-green)
![DevOps](https://img.shields.io/badge/DevOps-Automation-orange)
![Containers](https://img.shields.io/badge/Containers-Management-red)
![CLI](https://img.shields.io/badge/Tool-CLI-purple)

---

# 📚 Table of Contents

- [Overview](#-overview)
- [Command Syntax](#-command-syntax)
- [Initialization Commands](#-initialization-commands)
- [Starting Services](#-starting-services)
- [Stopping Services](#-stopping-services)
- [Monitoring and Debugging](#-monitoring-and-debugging)
- [Executing Commands Inside Containers](#-executing-commands-inside-containers)
- [Advanced Docker Compose Commands](#-advanced-docker-compose-commands)
- [Development Workflow](#-development-workflow)
- [Production Workflow](#-production-workflow)
- [Testing Workflow](#-testing-workflow)
- [Troubleshooting](#-troubleshooting)
- [Best Practices](#-best-practices)
- [Quick Revision Notes](#-quick-revision-notes)
- [Viva Questions](#-viva-questions)
- [Interview Questions](#-interview-questions)
- [Conclusion](#-conclusion)

---

# 📖 Overview

Docker Compose provides commands to:
- Create containers
- Start services
- Stop services
- Restart applications
- Monitor logs
- Execute commands inside containers

These commands simplify multi-container application management.

---

# 🧠 Command Syntax

---

# Modern Syntax

```bash
docker compose COMMAND
```

---

# Old Syntax

```bash
docker-compose COMMAND
```

---

# Example

```bash
docker compose up
```

Both syntaxes work similarly.

---

# 🚀 Initialization Commands

---

# Check Docker Compose Version

```bash
docker compose version
```

---

# Example Output

```text
Docker Compose version v2.20.0
```

---

# Validate YAML File

```bash
docker compose config
```

---

# Purpose

```text
✔ Check YAML syntax
✔ Detect errors
✔ Validate configuration
```

---

# List Services

```bash
docker compose config --services
```

---

# Example Output

```text
frontend
backend
database
```

---

# Create Compose File

---

# Windows

```bash
notepad docker-compose.yml
```

---

# Linux/Mac

```bash
touch docker-compose.yml
nano docker-compose.yml
```

---

# ▶️ Starting Services

---

# Start Services (Foreground Mode)

```bash
docker compose up
```

---

# Result

```text
✔ Creates containers
✔ Starts services
✔ Displays live logs
```

---

# Start Services in Background

```bash
docker compose up -d
```

---

# Benefits

```text
✔ Terminal remains free
✔ Services run in background
```

---

# Build and Start Containers

```bash
docker compose up --build
```

---

# Used When

```text
✔ Dockerfile changed
✔ Application code updated
```

---

# Build Images Only

```bash
docker compose build
```

---

# Rebuild Without Cache

```bash
docker compose build --no-cache
```

---

# Scale Services

```bash
docker compose up --scale web=3
```

---

# Result

```text
web_1
web_2
web_3
```

---

# Pull Latest Images

```bash
docker compose pull
```

---

# Pull Specific Service

```bash
docker compose pull web
```

---

# ⏹️ Stopping Services

---

# Stop and Remove Everything

```bash
docker compose down
```

---

# Removes

```text
✔ Containers
✔ Networks
```

---

# Keeps

```text
✔ Volumes
✔ Persistent data
```

---

# Remove Everything Including Volumes

```bash
docker compose down -v
```

---

# Warning

```text
⚠ Deletes all stored data
```

---

# Stop Containers Only

```bash
docker compose stop
```

---

# Restart Stopped Containers

```bash
docker compose start
```

---

# Restart Running Containers

```bash
docker compose restart
```

---

# Remove Stopped Containers

```bash
docker compose rm
```

---

# 📊 Monitoring and Debugging

---

# View Running Containers

```bash
docker compose ps
```

---

# Example Output

```text
NAME            STATUS      PORTS
web_1           Up          8080:80
db_1            Up          5432:5432
```

---

# View Logs

```bash
docker compose logs
```

---

# Stream Logs in Real Time

```bash
docker compose logs -f
```

---

# View Logs of Specific Service

```bash
docker compose logs web
```

---

# Last 100 Log Lines

```bash
docker compose logs --tail 100
```

---

# Logs with Timestamps

```bash
docker compose logs -f -t
```

---

# Logs Since Last 10 Minutes

```bash
docker compose logs --since 10m
```

---

# 🖥️ Executing Commands Inside Containers

---

# Open Interactive Shell

```bash
docker compose exec web bash
```

---

# Result

```text
Inside running container shell
```

---

# Example Commands

```bash
ls
pwd
env
```

---

# Run Single Command

```bash
docker compose exec app npm test
```

---

# Access Database

```bash
docker compose exec db psql -U postgres
```

---

# Run Without Interactive Terminal

```bash
docker compose exec -T app npm test
```

---

# Run Command as Root User

```bash
docker compose exec -u root app bash
```

---

# ⚙️ Advanced Docker Compose Commands

---

# View Full Configuration

```bash
docker compose config
```

---

# List Images Used

```bash
docker compose images
```

---

# Pause Running Containers

```bash
docker compose pause
```

---

# Resume Paused Containers

```bash
docker compose unpause
```

---

# Force Stop Containers

```bash
docker compose kill
```

---

# Push Images to Registry

```bash
docker compose push
```

---

# 📊 Most Important Commands Summary

| Command | Purpose |
|---|---|
| docker compose up | Start services |
| docker compose up -d | Start in background |
| docker compose down | Stop and remove |
| docker compose down -v | Remove including volumes |
| docker compose ps | View running containers |
| docker compose logs | View logs |
| docker compose restart | Restart services |
| docker compose build | Build images |
| docker compose exec | Execute inside container |

---

# 🔄 Development Workflow

---

# Step 1: Clone Project

```bash
git clone project-url
```

---

# Step 2: Start Application

```bash
docker compose up -d
```

---

# Step 3: Check Running Containers

```bash
docker compose ps
```

---

# Step 4: Monitor Logs

```bash
docker compose logs -f
```

---

# Step 5: Stop Application

```bash
docker compose down
```

---

# 🚀 Production Workflow

---

# Pull Latest Code

```bash
git pull origin main
```

---

# Build Updated Images

```bash
docker compose build
```

---

# Start Updated Containers

```bash
docker compose up -d
```

---

# Verify Deployment

```bash
docker compose ps
```

---

# 🧪 Testing Workflow

---

# Remove Old Environment

```bash
docker compose down -v
```

---

# Start Fresh Environment

```bash
docker compose up -d
```

---

# Run Tests

```bash
docker compose exec app npm test
```

---

# Cleanup

```bash
docker compose down
```

---

# 🛠️ Troubleshooting

---

# Container Not Starting

## Check Logs

```bash
docker compose logs service-name
```

---

# Port Already in Use

## Example Error

```text
Port 8080 already allocated
```

---

# Solution

```bash
netstat -ano
```

OR

Change port mapping.

---

# Services Cannot Communicate

## Check Network

```bash
docker compose ps
```

---

# Test Connection

```bash
docker compose exec web ping db
```

---

# Data Lost

## Reason

```bash
docker compose down -v
```

removes volumes.

---

# Solution

Avoid using:

```bash
-v
```

in production.

---

# 🛡️ Best Practices

---

# 1️⃣ Use Detached Mode in Production

```bash
docker compose up -d
```

---

# 2️⃣ Validate Compose File

```bash
docker compose config
```

---

# 3️⃣ Use Health Checks

Ensure services are ready before starting dependent services.

---

# 4️⃣ Avoid Hardcoding Secrets

Use:
- .env files
- Docker secrets

---

# 5️⃣ Monitor Logs Regularly

```bash
docker compose logs -f
```

---

# 6️⃣ Use Specific Image Versions

## Good

```yaml
image: postgres:15
```

---

## Bad

```yaml
image: latest
```

---

# 7️⃣ Use Named Volumes

Prevent accidental data loss.

---

# 📈 Docker Compose Command Workflow

```text
Write docker-compose.yml
            ↓
docker compose build
            ↓
docker compose up -d
            ↓
docker compose ps
            ↓
docker compose logs -f
            ↓
docker compose restart
            ↓
docker compose down
```

---

# 📌 Quick Revision Notes

| Command | Purpose |
|---|---|
| up | Start services |
| up -d | Start in background |
| down | Stop and remove |
| ps | View containers |
| logs | View logs |
| restart | Restart containers |
| exec | Run commands inside container |
| build | Build images |
| pull | Download latest images |

---

# 🧠 Important Keywords

- Docker Compose
- CLI Commands
- Multi-container
- Logs
- Restart
- Volumes
- Scaling
- Build
- Detached Mode
- Container Shell

---

# ❓ Viva Questions

1. What is docker compose up?
2. Difference between up and up -d?
3. What does docker compose down do?
4. What is docker compose logs?
5. How to execute commands inside a container?
6. What is detached mode?
7. Why use docker compose ps?
8. How to rebuild images?
9. What is scaling in Docker Compose?
10. Why use health checks?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| How to start services in background? | docker compose up -d |
| Command to stop all services? | docker compose down |
| How to view logs? | docker compose logs |
| Command to restart services? | docker compose restart |
| How to scale containers? | docker compose up --scale |

---

# 📌 Key Takeaway

Docker Compose commands simplify:

```text
✔ Container management
✔ Multi-service deployment
✔ Monitoring
✔ Scaling
✔ Debugging
✔ Automation
```

These commands are essential for:
- DevOps Engineers
- Backend Developers
- Cloud Engineers
- Docker Administrators

---

# ✅ Conclusion

Docker Compose commands provide a powerful way to:
- Build applications
- Deploy services
- Monitor containers
- Debug issues
- Scale applications

By mastering these commands developers can efficiently manage:
- Full-stack applications
- Microservices
- CI/CD environments
- Cloud-native systems

Docker Compose significantly improves:
- Productivity
- Automation
- Reliability
- Deployment speed

---

# 🔗 Next Topic

➡️ Practical Multi-Container Deployments