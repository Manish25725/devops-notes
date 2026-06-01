# Docker Practice Questions & Solutions

![Docker](https://img.shields.io/badge/Docker-Practice-blue)
![DevOps](https://img.shields.io/badge/DevOps-Labs-green)
![Containers](https://img.shields.io/badge/Containers-Exercises-orange)
![Linux](https://img.shields.io/badge/Linux-Docker-red)

---

# 📚 Table of Contents

- [Task 1 – Resource Mismanagement in Containers](#-task-1--resource-mismanagement-in-containers)
- [Task 2 – Container Resource & Isolation](#-task-2--container-resource--isolation)
- [Task 3 – Run Ubuntu Container in Interactive Mode](#-task-3--run-ubuntu-container-in-interactive-mode)
- [Task 4 – Troubleshoot a Running Container](#-task-4--troubleshoot-a-running-container)
- [Task 5 – Create and Verify Docker Network](#-task-5--create-and-verify-docker-network)
- [Task 6 – Deploy Apache HTTP Server using Docker](#-task-6--deploy-apache-http-server-using-docker)

---

# 🧠 Task 1 – Resource Mismanagement in Containers

## ❓ Q1. Which container feature was misconfigured or missing?

### ✅ Answer:
cgroups (memory limits not set)

### Example

```bash
docker run -d --name app_container nginx
```

- No memory limit specified
- Container can consume unlimited RAM

---

## ❓ Q2. Which kernel mechanism should have prevented this?

### ✅ Answer:
cgroups (memory control)

### Correct Command

```bash
docker run -d \
  --memory="512m" \
  --memory-swap="512m" \
  --name app_container \
  nginx
```

### Result

```text
✔ Maximum memory = 512MB
✔ Prevents excessive RAM usage
✔ Protects host system
```

---

## ❓ Q3. Would namespaces alone solve this issue? Why?

### ✅ Answer:
NO

### Example

```bash
docker run -d --name isolated_container nginx
```

### Explanation

Namespaces provide:
- Process isolation
- Network isolation
- Filesystem isolation

BUT:

```text
Namespaces do NOT limit resources
```

Resource control requires:
- cgroups

---

# 🧠 Task 2 – Container Resource & Isolation

## ❓ Q1. Which Linux feature prevents Container A from consuming all CPU?

### ✅ Answer:
cgroups (CPU control)

### Example

```bash
docker run -d \
  --cpus="1.0" \
  --name containerA \
  ubuntu
```

### Result

```text
✔ CPU usage restricted
✔ Fair resource sharing
✔ Prevents CPU starvation
```

---

## ❓ Q2. Which feature ensures Container B cannot see processes of Container C?

### ✅ Answer:
PID Namespace

### Example

```bash
docker run -d \
  --name containerB \
  ubuntu
```

### Result

```text
✔ Separate process space
✔ Isolated process IDs
✔ Secure process isolation
```

---

## ❓ Q3. Which namespace allows all three containers to use port 80 internally?

### ✅ Answer:
Network Namespace

---

# Example

## Container A

```bash
docker run -d -p 8081:80 nginx
```

## Container B

```bash
docker run -d -p 8082:80 nginx
```

## Container C

```bash
docker run -d -p 8083:80 nginx
```

---

# Explanation

```text
✔ All containers internally use port 80
✔ Each container has isolated network stack
✔ Different host ports avoid conflict
```

---

# 🧠 Task 3 – Run Ubuntu Container in Interactive Mode

## ❓ Question

A student wants to practice Linux commands inside Docker.

Run an Ubuntu container in interactive mode using bash and exit safely after execution.

---

# ✅ Commands

```bash
docker run -it ubuntu bash
```

---

# Exit Container

```bash
exit
```

---

# Explanation

| Flag | Purpose |
|---|---|
| -i | Interactive mode |
| -t | Terminal mode |

---

# 🧠 Task 4 – Troubleshoot a Running Container

## ❓ Question

You need to troubleshoot a running container by:

- Opening bash inside container
- Viewing logs
- Showing running processes

---

# ✅ Commands

## Open Bash

```bash
docker exec -it <container_id> bash
```

---

## View Logs

```bash
docker logs <container_id>
```

---

## Show Running Processes

```bash
docker top <container_id>
```

---

# 🧠 Task 5 – Create and Verify Docker Network

## ❓ Question

Create a custom Docker network named `mynetwork` and verify its configuration.

---

# ✅ Commands

## Create Network

```bash
docker network create mynetwork
```

---

## List Networks

```bash
docker network ls
```

---

## Inspect Network

```bash
docker network inspect mynetwork
```

---

# Result

```text
✔ Network created
✔ Configuration displayed
✔ Connected containers visible
```

---

# 🧠 Task 6 – Deploy Apache HTTP Server using Docker

## ❓ Question

Deploy Apache HTTP Server (httpd) using Docker for testing a static website.

Perform the following:

- Pull Apache image
- Verify image
- Run container in detached mode
- Map port 8081 → 80
- Check running containers
- Access web server

---

# ✅ Step 1: Pull Apache Image

```bash
docker pull httpd
```

---

# ✅ Step 2: Verify Image

```bash
docker images
```

---

# ✅ Step 3: Run Apache Container

```bash
docker run -d -p 8081:80 --name apache-web httpd
```

---

# Explanation

| Option | Purpose |
|---|---|
| -d | Detached mode |
| -p 8081:80 | Port mapping |
| --name | Container name |

---

# ✅ Step 4: Check Running Containers

```bash
docker ps
```

---

# ✅ Step 5: Access Web Server

Open browser:

```text
http://localhost:8081
```

---

# 🌟 Expected Result

Apache default webpage appears successfully.

---

# 📌 Quick Revision Notes

| Topic | Key Concept |
|---|---|
| cgroups | Resource control |
| Namespaces | Isolation |
| docker exec | Enter container |
| docker logs | View logs |
| docker network | Networking |
| docker run -it | Interactive container |
| Port Mapping | Host ↔ Container communication |

---

# 🧠 Important Keywords

- cgroups
- Namespaces
- PID Namespace
- Network Namespace
- docker exec
- docker logs
- docker network
- Apache HTTP Server
- Resource Isolation
- Port Mapping

---

# ❓ Viva Questions

1. What are cgroups?
2. What are namespaces?
3. Difference between cgroups and namespaces?
4. What does docker exec do?
5. What is port mapping?
6. What is docker network?
7. Why use detached mode?
8. What is PID namespace?
9. What is Network namespace?
10. How do containers communicate?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| What controls CPU and memory in Docker? | cgroups |
| What provides process isolation? | PID namespace |
| Why can containers use same internal ports? | Network namespace |
| What does docker exec do? | Run command inside container |
| What is docker network create used for? | Custom networking |

---

# ✅ Conclusion

These Docker practice tasks help understand:

```text
✔ Resource management
✔ Container isolation
✔ Interactive containers
✔ Networking
✔ Troubleshooting
✔ Apache deployment
```

They are extremely useful for:
- practical labs
- viva preparation
- DevOps interviews
- Docker fundamentals