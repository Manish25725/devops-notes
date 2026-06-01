# Docker Networking

![Docker](https://img.shields.io/badge/Docker-Networking-blue)
![Containers](https://img.shields.io/badge/Containers-Communication-green)
![DevOps](https://img.shields.io/badge/DevOps-Networks-orange)
![Linux](https://img.shields.io/badge/Linux-Namespace-red)

---

# 📚 Table of Contents

- Introduction
- Why Docker Networking is Needed
- Docker Network Architecture
- Types of Docker Networks
- Bridge Network
- Host Network
- None Network
- Overlay Network
- DNS Inside Docker
- Linking Containers
- Port Mapping
- Container Communication
- Network Commands
- Practical Examples
- Best Practices
- Summary

---

# 📖 Introduction

Containers need networking to:
- communicate with each other
- communicate with external systems
- expose applications to users

Docker provides built-in networking features for:
- isolation
- communication
- scalability

---

# 🧠 Why Docker Networking is Needed

Without networking:
- containers cannot communicate
- applications remain isolated
- users cannot access services

---

# Example

```text
Frontend Container
        ↓
Backend Container
        ↓
Database Container
```

All require networking.

---

# 🌐 Docker Network Architecture

Each container gets:
- virtual network interface
- IP address
- DNS entry

Docker uses:
- Linux network namespaces
- virtual bridges
- NAT (Network Address Translation)

---

# Networking Workflow

```text
Container A
    ↓
Docker Network
    ↓
Container B
```

---

# 🏗️ Types of Docker Networks

Docker supports multiple network drivers.

---

# Main Network Types

| Network Type | Purpose |
|---|---|
| Bridge | Default local networking |
| Host | Uses host network directly |
| None | No networking |
| Overlay | Multi-host networking |

---

# 🌉 Bridge Network

## Most Common Network

Default network type in Docker.

---

# Characteristics

```text
✔ Private internal network
✔ Containers communicate via IP/name
✔ Isolated from host
✔ Supports port mapping
```

---

# Default Bridge Network

Docker automatically creates:

```text
bridge
```

---

# View Networks

```bash
docker network ls
```

---

# Example

```bash
docker run -d --name web nginx

docker run -d --name db mysql
```

Both connected to:
- default bridge network

---

# ⚠️ Limitation of Default Bridge

Containers communicate using:
- IP addresses only

Better approach:
- custom bridge network

---

# 🌟 Custom Bridge Network

---

# Create Network

```bash
docker network create mynetwork
```

---

# Run Containers on Network

```bash
docker run -d --network mynetwork --name web nginx

docker run -d --network mynetwork --name db mysql
```

---

# Benefits

```text
✔ Automatic DNS resolution
✔ Better isolation
✔ Easier communication
✔ Production-friendly
```

---

# Example Communication

Inside container:

```bash
ping db
```

Works using:
- container names

---

# 🖥️ Host Network

Container shares:
- host machine network

---

# Characteristics

```text
✔ No network isolation
✔ Faster performance
✔ Direct host access
✔ No port mapping needed
```

---

# Example

```bash
docker run --network host nginx
```

---

# Result

Nginx directly uses:
- host port 80

---

# ⚠️ Drawbacks

```text
✘ Less isolation
✘ Port conflicts possible
✘ Lower security
```

---

# 🚫 None Network

Disables networking completely.

---

# Example

```bash
docker run --network none ubuntu
```

---

# Result

Container has:
- no internet
- no communication
- only loopback interface

---

# Use Cases

```text
✔ Security-sensitive workloads
✔ Isolated batch jobs
✔ Testing
```

---

# 🌍 Overlay Network

Used for:
- multi-host container communication

Mainly used in:
- Docker Swarm
- Kubernetes

---

# Characteristics

```text
✔ Cross-host communication
✔ Distributed networking
✔ Scalable microservices
```

---

# Example

```text
Server A Container ↔ Server B Container
```

through overlay network.

---

# 🔍 DNS Inside Docker

Docker provides:
- built-in DNS resolution

Containers communicate using:
- container names

---

# Example

```bash
docker network create appnet

docker run -d --network appnet --name database mysql

docker run -it --network appnet ubuntu bash
```

Inside Ubuntu container:

```bash
ping database
```

---

# Result

Docker resolves:
- `database` → container IP

---

# 🔗 Linking Containers

Older Docker method for container communication.

---

# Example

```bash
docker run -d --name db mysql

docker run -it --link db:mysql ubuntu
```

---

# Problem

`--link` is:
- legacy
- deprecated

Modern approach:
- custom bridge networks

---

# 🌐 Port Mapping

Containers are isolated.

Need port mapping to access applications externally.

---

# Syntax

```bash
docker run -p HOST_PORT:CONTAINER_PORT image
```

---

# Example

```bash
docker run -d -p 8080:80 nginx
```

---

# Workflow

```text
Browser → localhost:8080
          ↓
Docker Host
          ↓
Container Port 80
```

---

# Multiple Port Mapping

```bash
docker run -d -p 8080:80 -p 8443:443 nginx
```

---

# 📡 Container Communication

Containers on same network:
- communicate directly

---

# Example

```bash
docker network create backend_net
```

---

# Run Database

```bash
docker run -d \
  --network backend_net \
  --name mysql_db \
  mysql:8
```

---

# Run Backend App

```bash
docker run -d \
  --network backend_net \
  --name backend \
  node-app:v1
```

---

# Backend Connects Using

```text
mysql_db:3306
```

instead of:
- localhost

---

# 🛠️ Docker Network Commands

---

# List Networks

```bash
docker network ls
```

---

# Create Network

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

# Connect Container to Network

```bash
docker network connect mynetwork container1
```

---

# Disconnect Container

```bash
docker network disconnect mynetwork container1
```

---

# 📊 Practical Example

---

# Step 1: Create Network

```bash
docker network create appnet
```

---

# Step 2: Run MySQL

```bash
docker run -d \
  --network appnet \
  --name mysql_db \
  -e MYSQL_ROOT_PASSWORD=root123 \
  mysql:8
```

---

# Step 3: Run Backend

```bash
docker run -d \
  --network appnet \
  --name backend \
  node-app:v1
```

---

# Step 4: Test Communication

```bash
docker exec -it backend ping mysql_db
```

---

# Result

```text
✔ Containers communicate successfully
✔ DNS resolution works
✔ Same network communication enabled
```

---

# 🌟 Multi-Container Architecture

```text
Frontend Container
        ↓
Backend Container
        ↓
Database Container
```

All connected using:
- Docker bridge network

---

# 🔐 Networking Security

Docker networks provide:
- isolation boundaries

Best practice:
- separate frontend/backend networks

---

# Example

```text
frontend_net
backend_net
database_net
```

---

# Benefits

```text
✔ Better security
✔ Reduced attack surface
✔ Controlled communication
```

---

# ⚡ Best Practices

---

# Use Custom Networks

✅ Good

```bash
docker network create appnet
```

---

# Avoid Legacy Linking

❌ Avoid

```bash
--link
```

---

# Use Container Names

Instead of:
- hardcoded IPs

---

# Separate Application Tiers

```text
Frontend
Backend
Database
```

on separate networks.

---

# Minimize Exposed Ports

Expose only:
- necessary services

---

# 📌 Quick Revision Notes

| Concept | Meaning |
|---|---|
| Bridge Network | Default local networking |
| Host Network | Uses host networking |
| None Network | No networking |
| Overlay Network | Multi-host networking |
| Port Mapping | Host ↔ container access |
| DNS Resolution | Container-name communication |

---

# 🧠 Important Keywords

- Bridge Network
- Host Network
- Overlay Network
- Port Mapping
- Docker DNS
- Network Namespace
- Container Communication
- docker network
- NAT
- Virtual Bridge

---

# ❓ Viva Questions

1. Why is Docker networking needed?
2. What is bridge network?
3. Difference between bridge and host network?
4. What is overlay network?
5. What is port mapping?
6. What is Docker DNS?
7. Why use custom bridge networks?
8. What is network namespace?
9. Difference between localhost and container communication?
10. Why is --link deprecated?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| Default Docker network type? | Bridge |
| What does -p do? | Port mapping |
| How do containers communicate? | Same Docker network |
| Why use custom bridge networks? | DNS + isolation |
| What is overlay network used for? | Multi-host communication |

---

# ✅ Conclusion

Docker networking enables:
- container communication
- service discovery
- external access
- scalable architectures

Using:
- bridge networks
- DNS resolution
- port mapping
- overlay networking

Docker supports:
- modern microservices
- distributed applications
- cloud-native DevOps infrastructure

These concepts are essential for:
- Docker Compose
- Kubernetes
- CI/CD pipelines
- container orchestration