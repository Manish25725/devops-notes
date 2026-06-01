# Container Interaction with Host

![Docker](https://img.shields.io/badge/Docker-ContainerInteraction-blue)
![Containers](https://img.shields.io/badge/Containers-HostCommunication-green)
![Linux](https://img.shields.io/badge/Linux-Terminal-orange)
![DevOps](https://img.shields.io/badge/DevOps-DockerCLI-red)
![Storage](https://img.shields.io/badge/Storage-FileTransfer-purple)

---

# 📚 Table of Contents

- [Overview](#-overview)
- [Why Container Interaction is Needed](#-why-container-interaction-is-needed)
- [docker exec](#-docker-exec)
- [docker attach](#-docker-attach)
- [docker exec vs docker attach](#-docker-exec-vs-docker-attach)
- [docker cp](#-docker-cp)
- [Copying Files Between Host and Container](#-copying-files-between-host-and-container)
- [Container Monitoring Commands](#-container-monitoring-commands)
- [Container Inspection](#-container-inspection)
- [Lab Exercise](#-lab-exercise)
- [Practical Examples](#-practical-examples)
- [Common Errors](#-common-errors)
- [Best Practices](#-best-practices)
- [Quick Revision Notes](#-quick-revision-notes)
- [Viva Questions](#-viva-questions)
- [Interview Questions](#-interview-questions)
- [Conclusion](#-conclusion)

---

# 📖 Overview

Containers are isolated environments, but developers often need to:
- Enter containers
- Run commands
- Debug applications
- View logs
- Transfer files
- Monitor resource usage

Docker provides special commands for:
- container interaction
- debugging
- file sharing
- monitoring

This topic explains:
- `docker exec`
- `docker attach`
- `docker cp`
- monitoring commands
- inspection commands

---

# 🎯 Why Container Interaction is Needed

Developers frequently need to:

```text
✔ Debug applications
✔ Check logs
✔ Modify files
✔ Install packages
✔ Monitor resource usage
✔ Transfer data
```

---

# Example Scenarios

| Task | Docker Command |
|---|---|
| Open terminal | docker exec |
| Connect to running process | docker attach |
| Copy files | docker cp |
| View logs | docker logs |
| Monitor CPU/RAM | docker stats |

---

# ⚙️ docker exec

---

# What is docker exec?

> `docker exec` runs commands inside an already running container.

---

# Main Purpose

```text
✔ Open shell
✔ Run commands
✔ Debug applications
✔ Manage files
✔ Execute scripts
```

---

# Basic Syntax

```bash
docker exec [OPTIONS] <container> <command>
```

---

# Open Interactive Bash Terminal

```bash
docker exec -it <id> bash
```

---

# Example

```bash
docker exec -it myubuntu bash
```

---

# Result

```text
Interactive bash shell opens inside container
```

---

# Alpine Linux Containers

Alpine images usually do NOT have bash.

Use:

```bash
docker exec -it <id> sh
```

---

# Example

```bash
docker exec -it alpine-container sh
```

---

# Run Single Command

```bash
docker exec -it <id> ls /
```

---

# Example

```bash
docker exec -it myubuntu ls /
```

---

# Result

```text
Lists root directory inside container
```

---

# Check Operating System

```bash
docker exec -it <id> cat /etc/os-release
```

---

# Example Output

```text
NAME="Ubuntu"
VERSION="22.04"
```

---

# Run Multiple Commands

```bash
docker exec -it <id> sh -c "echo 'Hello' > /data/test.txt"
```

---

# Explanation

| Part | Meaning |
|---|---|
| sh -c | Execute shell command |
| echo | Write text |
| > | Redirect output |

---

# 🚩 docker exec Flags

| Flag | Purpose |
|---|---|
| -i | Interactive input |
| -t | Allocate terminal |
| -d | Run in background |

---

# Interactive Example

```bash
docker exec -it myubuntu bash
```

---

# Detached Example

```bash
docker exec -d myubuntu touch /tmp/test.txt
```

---

# Benefits of docker exec

```text
✔ Safe
✔ Creates new process
✔ Easy debugging
✔ Does not affect main container process
```

---

# 🔗 docker attach

---

# What is docker attach?

> `docker attach` connects your terminal directly to the main process (PID 1) of a running container.

---

# Syntax

```bash
docker attach <container>
```

---

# Example

```bash
docker attach myubuntu
```

---

# Important Warning ⚠️

Pressing:

```text
Ctrl + C
```

will:
- stop the container

because you are attached to:
- main process

---

# Safe Detach Method

Use:

```text
Ctrl + P
then
Ctrl + Q
```

---

# Result

```text
Detach safely without stopping container
```

---

# 🆚 docker exec vs docker attach

| Feature | docker exec | docker attach |
|---|---|---|
| Creates New Process | ✔ | ✘ |
| Connects to Main Process | ✘ | ✔ |
| Safe Exit | ✔ | ⚠️ Risky |
| Used for Debugging | ✔ | Limited |
| Multiple Sessions | ✔ | Limited |
| Recommended | ✔ | Rarely |

---

# Summary

---

# docker exec

```text
✔ Safe
✔ Preferred
✔ Opens new shell
✔ Easy debugging
```

---

# docker attach

```text
✔ Connects to PID 1
✔ Dangerous if Ctrl+C used
✔ Mainly for process interaction
```

---

# 📂 docker cp

---

# What is docker cp?

> `docker cp` copies files between host system and containers.

---

# Main Purpose

```text
✔ Export logs
✔ Upload configuration files
✔ Backup data
✔ Transfer scripts
```

---

# Basic Syntax

```bash
docker cp <source> <destination>
```

---

# 📤 Copy FROM Container → TO Host

---

# Syntax

```bash
docker cp <container>:/path/in/container /host/path
```

---

# Example

```bash
docker cp mycontainer:/app/app.log ~/Desktop/app.log
```

---

# Result

```text
Log file copied to Desktop
```

---

# 📥 Copy FROM Host → TO Container

---

# Syntax

```bash
docker cp /host/path <container>:/path/in/container
```

---

# Example

```bash
docker cp ~/Desktop/config.json mycontainer:/app/config.json
```

---

# Result

```text
Config file copied into container
```

---

# Windows Example

```bash
docker cp mycontainer:/data/test.txt C:\Users\HP\Desktop\
```

---

# Result

```text
File copied to Windows Desktop
```

---

# 🌟 Benefits of docker cp

```text
✔ No need to enter container
✔ Quick file transfer
✔ Useful for debugging
✔ Easy backups
```

---

# 📊 Container Monitoring Commands

Docker provides commands for:
- monitoring
- debugging
- inspection

---

# Live Resource Usage

```bash
docker stats <id>
```

---

# Shows

```text
✔ CPU usage
✔ Memory usage
✔ Network I/O
✔ Disk I/O
```

---

# Example

```bash
docker stats myubuntu
```

---

# Running Processes Inside Container

```bash
docker top <id>
```

---

# Example

```bash
docker top myubuntu
```

---

# Result

```text
Shows active processes
```

---

# 📋 Container Inspection

---

# Full Container Configuration

```bash
docker inspect <id>
```

---

# Example

```bash
docker inspect myubuntu
```

---

# Output

```text
✔ Network settings
✔ Mount points
✔ Volumes
✔ Environment variables
✔ Resource limits
✔ IP addresses
```

---

# Output Format

```text
JSON
```

---

# 📜 Container Logs

---

# View Logs

```bash
docker logs <id>
```

---

# Follow Logs Live

```bash
docker logs -f <id>
```

---

# Example

```bash
docker logs -f mynginx
```

---

# Result

```text
Real-time application output
```

---

# 🧪 Lab Exercise

---

# Step 1: Run Container

```bash
docker run -d --name myubuntu ubuntu sleep 300
```

---

# Explanation

| Part | Meaning |
|---|---|
| -d | Detached mode |
| sleep 300 | Keep container alive |

---

# Step 2: Enter Container

```bash
docker exec -it myubuntu /bin/bash
```

---

# Step 3: Create Files Inside

```bash
mkdir /data

echo "Hello Docker" > /data/test.txt
```

---

# Exit Container

```bash
exit
```

---

# Step 4: Attach and Detach Safely

```bash
docker attach myubuntu
```

---

# Safe Detach

```text
Ctrl + P
Ctrl + Q
```

---

# Step 5: Copy File from Container → Host

```bash
docker cp myubuntu:/data/test.txt ~/Desktop/
```

---

# Step 6: Copy File from Host → Container

```bash
docker cp ~/Desktop/test.txt myubuntu:/data/sample.txt
```

---

# Step 7: Verify Files

```bash
docker exec -it myubuntu ls /data
```

---

# View File Content

```bash
docker exec -it myubuntu cat /data/sample.txt
```

---

# 🌍 Practical Examples

---

# Example 1: Check OS

```bash
docker exec -it myubuntu cat /etc/os-release
```

---

# Example 2: Create Directory

```bash
docker exec -it myubuntu mkdir /app
```

---

# Example 3: Monitor Resources

```bash
docker stats myubuntu
```

---

# Example 4: Export Logs

```bash
docker cp mycontainer:/var/log/app.log ~/Desktop/
```

---

# Example 5: Import Config File

```bash
docker cp config.json mycontainer:/app/
```

---

# ⚠️ Common Errors

---

# Error 1: Container Not Running

```text
Error response from daemon:
Container is not running
```

---

# Solution

Start container first:

```bash
docker start <id>
```

---

# Error 2: bash Not Found

```text
exec: "bash": executable file not found
```

---

# Solution

Use:

```bash
sh
```

instead of:
```bash
bash
```

---

# Error 3: Permission Denied

---

# Solution

Use:
- sudo
- proper permissions

---

# 🛡️ Best Practices

---

# 1️⃣ Prefer docker exec Over attach

---

# Why?

```text
✔ Safer
✔ More flexible
✔ Does not affect main process
```

---

# 2️⃣ Use Named Containers

---

# Good

```bash
docker run --name webserver nginx
```

---

# Bad

Using random container IDs.

---

# 3️⃣ Avoid Running as Root

Use:
- non-root users
inside containers.

---

# 4️⃣ Use Logs Instead of attach

---

# Recommended

```bash
docker logs -f myapp
```

---

# 5️⃣ Clean Unused Containers

```bash
docker container prune
```

---

# 📌 Quick Revision Notes

| Command | Purpose |
|---|---|
| docker exec | Run command inside container |
| docker attach | Attach to main process |
| docker cp | Copy files |
| docker logs | View logs |
| docker stats | Monitor resources |
| docker top | View processes |
| docker inspect | Full configuration |

---

# 🧠 Important Keywords

- docker exec
- docker attach
- docker cp
- docker logs
- docker inspect
- docker stats
- Interactive Terminal
- PID 1
- Container Debugging
- File Transfer

---

# ❓ Viva Questions

1. What is docker exec?
2. Difference between exec and attach?
3. What does docker cp do?
4. Why use docker stats?
5. What is docker inspect?
6. What is PID 1?
7. Why is Ctrl+C dangerous with attach?
8. How to safely detach from container?
9. What is interactive mode?
10. How to copy files into container?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| Difference between exec and attach? | exec creates new process, attach joins main process |
| Why use docker exec? | Debugging and interaction |
| What does docker inspect show? | Full JSON configuration |
| How to monitor container resources? | docker stats |
| How to transfer files? | docker cp |

---

# 📌 Key Takeaway

Docker provides multiple commands for:
- interacting with containers
- monitoring applications
- debugging systems
- transferring files

Important commands:

```text
✔ docker exec
✔ docker attach
✔ docker cp
✔ docker logs
✔ docker stats
✔ docker inspect
```

These commands are essential for:
- DevOps
- debugging
- troubleshooting
- container management

---

# ✅ Conclusion

Container interaction commands help developers:
- access running containers
- debug applications
- transfer files
- monitor performance
- inspect configurations

`docker exec` is the safest and most commonly used method for container interaction.

Commands like:
- `docker cp`
- `docker stats`
- `docker logs`
- `docker inspect`

are essential tools for modern:
- Docker workflows
- DevOps operations
- cloud-native debugging
