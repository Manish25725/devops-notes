# Basic Docker Commands

![Docker](https://img.shields.io/badge/Docker-Commands-blue)
![Containers](https://img.shields.io/badge/Containers-Management-green)
![DevOps](https://img.shields.io/badge/DevOps-CLI-orange)
![Linux](https://img.shields.io/badge/Linux-Terminal-red)
![Cloud](https://img.shields.io/badge/Cloud-Native-purple)

---

# 📚 Table of Contents

- [Overview](#-overview)
- [Docker Command Structure](#-docker-command-structure)
- [Docker Information Commands](#-docker-information-commands)
- [Docker Image Commands](#-docker-image-commands)
- [Docker Container Lifecycle Commands](#-docker-container-lifecycle-commands)
- [Container Interaction Commands](#-container-interaction-commands)
- [Docker Run Flags](#-docker-run-flags)
- [Port Mapping](#-port-mapping)
- [Volume Commands](#-volume-commands)
- [Network Commands](#-network-commands)
- [Cleanup Commands](#-cleanup-commands)
- [Practical Examples](#-practical-examples)
- [Nginx Example](#-nginx-example)
- [Ubuntu Interactive Example](#-ubuntu-interactive-example)
- [Apache Example](#-apache-example)
- [MySQL Example](#-mysql-example)
- [Quick Revision Notes](#-quick-revision-notes)
- [Viva Questions](#-viva-questions)
- [Interview Questions](#-interview-questions)
- [Conclusion](#-conclusion)

---

# 📖 Overview

Docker commands are used to:
- Manage images
- Create containers
- Run applications
- Configure networking
- Manage storage
- Monitor resource usage

Docker CLI allows developers to:
- interact with Docker daemon
- automate deployments
- manage container lifecycle

---

# ⚙️ Docker Command Structure

General syntax:

```bash
docker <object> <command> <options>
```

---

# Example

```bash
docker container ls
docker image pull nginx
docker volume create myvolume
```

---

# Simplified Commands

Docker also provides shortcuts.

---

# Example

```bash
docker ps
docker run nginx
docker pull ubuntu
```

---

# 🧠 Docker Information Commands

These commands provide:
- Docker installation details
- System information
- Runtime configuration

---

# Check Docker Version

```bash
docker --version
```

---

# Example Output

```text
Docker version 26.0.0
```

---

# Detailed Docker Information

```bash
docker info
```

---

# Shows

```text
✔ Containers count
✔ Images count
✔ Storage driver
✔ CPU information
✔ Memory information
✔ Docker root directory
```

---

# 🖼️ Docker Image Commands

Images are:
- templates for containers

---

# Pull Image

Downloads image from registry.

```bash
docker pull ubuntu
```

---

# Example

```bash
docker pull nginx
docker pull python:3.11
```

---

# List Downloaded Images

```bash
docker images
```

---

# Example Output

```text
REPOSITORY   TAG       IMAGE ID
ubuntu       latest    abc123
nginx        latest    def456
```

---

# View Image History

```bash
docker history httpd
```

---

# Shows

```text
✔ Image layers
✔ Layer size
✔ Build commands
```

---

# Remove Image

```bash
docker rmi ubuntu
```

---

# Force Remove Image

```bash
docker rmi -f <image-id>
```

---

# 📦 Docker Container Lifecycle Commands

Containers move through:
- created
- running
- stopped
- removed states

---

# Create + Run Container

```bash
docker run ubuntu
```

---

# Run Interactive Terminal

```bash
docker run -it ubuntu /bin/bash
```

---

# Explanation

| Flag | Purpose |
|---|---|
| -i | Interactive mode |
| -t | Terminal mode |

---

# Result

```text
Interactive shell opens inside container
```

---

# Run in Detached Mode

```bash
docker run -d nginx
```

---

# Result

```text
Container runs in background
```

---

# Run with Name + Port Mapping

```bash
docker run -d -p 8080:80 --name mynginx nginx
```

---

# Meaning

| Option | Purpose |
|---|---|
| -d | Background mode |
| -p | Port mapping |
| --name | Container name |

---

# Auto Remove Container

```bash
docker run --rm ubuntu echo "Hello"
```

---

# Result

```text
Container automatically deleted after exit
```

---

# List Running Containers

```bash
docker ps
```

---

# List All Containers

```bash
docker ps -a
```

---

# Start Stopped Container

```bash
docker start <container-id>
```

---

# Stop Running Container

```bash
docker stop <container-id>
```

---

# Restart Container

```bash
docker restart <container-id>
```

---

# Pause Container

```bash
docker pause <container-id>
```

---

# Unpause Container

```bash
docker unpause <container-id>
```

---

# Remove Container

```bash
docker rm <container-id>
```

---

# Force Remove Running Container

```bash
docker rm -f <container-id>
```

---

# 🔍 Container Interaction Commands

These commands help interact with running containers.

---

# Open Terminal Inside Container

```bash
docker exec -it <container-id> bash
```

---

# Example

```bash
docker exec -it mynginx bash
```

---

# View Container Logs

```bash
docker logs <container-id>
```

---

# Live Logs

```bash
docker logs -f <container-id>
```

---

# Inspect Container Configuration

```bash
docker inspect <container-id>
```

---

# Output

```text
JSON configuration data
```

---

# Monitor Resource Usage

```bash
docker stats
```

---

# Shows

```text
✔ CPU usage
✔ Memory usage
✔ Network usage
✔ Disk I/O
```

---

# View Running Processes Inside Container

```bash
docker top <container-id>
```

---

# 🌐 Port Mapping

Containers have isolated networking.

Port mapping exposes container services to host system.

---

# Syntax

```bash
-p <HOST_PORT>:<CONTAINER_PORT>
```

---

# Example

```bash
docker run -d -p 8080:80 nginx
```

---

# Meaning

```text
Host Port 8080
        ↓
Container Port 80
```

---

# Access Application

```text
http://localhost:8080
```

---

# 📊 Port Mapping Visualization

```text
Browser
   ↓
localhost:8080
   ↓
Docker Host
   ↓
Container Port 80
   ↓
Nginx Service
```

---

# 🚩 Docker Run Flags

---

# Common Flags

| Flag | Purpose |
|---|---|
| -d | Detached mode |
| -it | Interactive terminal |
| --name | Assign container name |
| --rm | Auto remove |
| -p | Port mapping |
| -e | Environment variables |
| -v | Volume mount |

---

# Example

```bash
docker run -d \
-p 8080:80 \
--name webserver \
nginx
```

---

# 💾 Volume Commands

Volumes provide:
- persistent storage

---

# Create Volume

```bash
docker volume create myvolume
```

---

# List Volumes

```bash
docker volume ls
```

---

# Inspect Volume

```bash
docker volume inspect myvolume
```

---

# Remove Volume

```bash
docker volume rm myvolume
```

---

# 🌐 Network Commands

Docker networking enables:
- container communication

---

# List Networks

```bash
docker network ls
```

---

# Create Custom Network

```bash
docker network create mynetwork
```

---

# Inspect Network

```bash
docker network inspect mynetwork
```

---

# Remove Network

```bash
docker network rm mynetwork
```

---

# 🧹 Cleanup Commands

Cleanup commands remove:
- unused resources
- stopped containers
- dangling images

---

# Stop All Running Containers

```bash
docker stop $(docker ps -aq)
```

---

# Remove All Containers

```bash
docker rm $(docker ps -aq)
```

---

# Remove All Images

```bash
docker rmi $(docker images -q)
```

---

# Remove Unused Resources

```bash
docker system prune -a
```

---

# Remove Everything Including Volumes

```bash
docker system prune -a --volumes
```

---

# ⚠️ Warning

These commands permanently delete data.

---

# 🌍 Practical Examples

---

# 🌐 Nginx Example

---

# Step 1: Pull Image

```bash
docker pull nginx
```

---

# Step 2: Run Container

```bash
docker run -d -p 8080:80 --name mynginx nginx
```

---

# Step 3: Verify Running Container

```bash
docker ps
```

---

# Step 4: Stop Container

```bash
docker stop mynginx
```

---

# Step 5: Start Again

```bash
docker start mynginx
```

---

# Step 6: Remove Container

```bash
docker rm -f mynginx
```

---

# 🌟 Result

Access:

```text
http://localhost:8080
```

---

# 💻 Ubuntu Interactive Example

Run Ubuntu container:

```bash
docker run -it ubuntu bash
```

---

# Inside Container

```bash
echo "Hello from container"
```

---

# Exit Container

```bash
exit
```

---

# 🌐 Apache (httpd) Example

---

# Pull Image

```bash
docker pull httpd
```

---

# Run Apache Container

```bash
docker run -d --name my-apache -p 8080:80 httpd
```

---

# Modify Webpage

```bash
docker exec -it my-apache bash -c \
"echo '<h1>Hello!</h1>' > /usr/local/apache2/htdocs/index.html"
```

---

# Test in Browser

```bash
curl http://localhost:8080
```

---

# 🗄️ MySQL Example

---

# Run MySQL Container

```bash
docker run -d \
-p 3307:3306 \
--name mysql-test \
-e MYSQL_ROOT_PASSWORD=root123 \
-e MYSQL_DATABASE=college \
mysql:8
```

---

# Explanation

| Option | Purpose |
|---|---|
| -e | Environment variable |
| MYSQL_ROOT_PASSWORD | Root password |
| MYSQL_DATABASE | Initial database |

---

# Open Terminal

```bash
docker exec -it mysql-test bash
```

---

# Login to MySQL

```bash
mysql -h 127.0.0.1 -u root -p
```

---

# 📊 Docker Workflow Example

```text
Pull Image
     ↓
Run Container
     ↓
Map Ports
     ↓
Interact with App
     ↓
Stop Container
     ↓
Remove Container
```

---

# 📌 Quick Revision Notes

| Topic | Key Point |
|---|---|
| docker pull | Download image |
| docker run | Create + start container |
| docker ps | List containers |
| docker exec | Enter container |
| docker logs | View logs |
| docker volume | Persistent storage |
| docker network | Container networking |
| docker system prune | Cleanup |

---

# 🧠 Important Keywords

- Docker CLI
- Docker Images
- Containers
- Volumes
- Networking
- Port Mapping
- Detached Mode
- Interactive Mode
- Cleanup
- Environment Variables

---

# ❓ Viva Questions

1. What does docker run do?
2. Difference between docker ps and docker ps -a?
3. What is detached mode?
4. What does -it mean?
5. What is port mapping?
6. What is docker exec?
7. What are Docker volumes?
8. What is docker inspect?
9. Why use docker logs?
10. What does docker system prune do?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| Difference between image and container? | Template vs running instance |
| What does docker run do internally? | Pulls image, creates container, starts process |
| Why use volumes? | Persistent storage |
| What is docker exec? | Run command inside container |
| What is port mapping? | Connect host ports to container ports |

---

# 📌 Key Takeaway

Docker commands help manage:
- images
- containers
- storage
- networking
- resources

Core workflow:

```text
Pull Image
      ↓
Run Container
      ↓
Monitor
      ↓
Stop
      ↓
Remove
```

Docker CLI simplifies:
- container management
- deployment
- automation
- DevOps workflows

---

# ✅ Conclusion

Docker commands form the foundation of:
- container management
- DevOps workflows
- CI/CD pipelines
- cloud-native applications

Using Docker CLI, developers can:
- build images
- run containers
- manage storage
- configure networking
- monitor applications

Mastering Docker commands is essential for:
- DevOps engineers
- cloud engineers
- backend developers
- system administrators

---

# 🔗 Next Topic

➡️ Docker Object Types