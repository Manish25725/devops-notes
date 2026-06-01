# Process Isolation & Namespaces

![Docker](https://img.shields.io/badge/Docker-Containers-blue)
![Linux](https://img.shields.io/badge/Linux-Namespaces-green)
![Security](https://img.shields.io/badge/Security-Isolation-orange)
![Kernel](https://img.shields.io/badge/Kernel-cgroups-red)
![DevOps](https://img.shields.io/badge/DevOps-Infrastructure-purple)

---

# 📚 Table of Contents

- [Overview](#-overview)
- [What is Process Isolation?](#-what-is-process-isolation)
- [Why Isolation is Important](#-why-isolation-is-important)
- [Introduction to Linux Namespaces](#-introduction-to-linux-namespaces)
- [How Namespaces Work](#-how-namespaces-work)
- [Types of Linux Namespaces](#-types-of-linux-namespaces)
- [PID Namespace](#-pid-namespace)
- [Network Namespace](#-network-namespace)
- [Mount Namespace](#-mount-namespace)
- [IPC Namespace](#-ipc-namespace)
- [UTS Namespace](#-uts-namespace)
- [User Namespace](#-user-namespace)
- [How Docker Uses Namespaces](#-how-docker-uses-namespaces)
- [Namespaces + cgroups](#-namespaces--cgroups)
- [Container Isolation Workflow](#-container-isolation-workflow)
- [Security Through Isolation](#-security-through-isolation)
- [Namespace Limitations](#-namespace-limitations)
- [Practical Docker Examples](#-practical-docker-examples)
- [Quick Revision Notes](#-quick-revision-notes)
- [Viva Questions](#-viva-questions)
- [Interview Questions](#-interview-questions)
- [Conclusion](#-conclusion)

---

# 📖 Overview

Containers need isolation to:
- Prevent interference
- Improve security
- Separate applications
- Create independent environments

Linux provides this isolation using:
- Namespaces
- cgroups

Namespaces isolate:
- Processes
- Network
- Filesystem
- Users
- IPC
- Hostnames

---

# 🧠 What is Process Isolation?

> Process Isolation is a kernel-level mechanism that separates processes so they cannot interfere with each other.

---

# Without Isolation

```text
Application A
      ↓
Can access:
✔ Memory of other apps
✔ Files of other apps
✔ Network resources
✔ System processes
```

---

# Problems

```text
✔ Security risks
✔ Application conflicts
✔ System crashes
✔ Poor reliability
```

---

# With Isolation

```text
Application A
      ↓
Runs inside sandbox
      ↓
Cannot access other applications
```

---

# Result

```text
✔ Better security
✔ Stable infrastructure
✔ Independent execution
✔ Fault isolation
```

---

# 🎯 Why Isolation is Important

Modern systems run:
- Multiple applications
- Multiple containers
- Multiple users

Without isolation:
- One application can affect others.

---

# Example

```text
Container A crashes
        ↓
Container B continues running safely
```

---

# 🐧 Introduction to Linux Namespaces

Linux namespaces provide isolation by creating separate views of system resources.

---

# 🧠 Definition

> A Namespace is a Linux kernel feature that isolates system resources for processes.

---

# Core Idea

Instead of one global system view:

```text
One System
      ↓
Multiple Isolated Views
```

---

# Example

```text
Container A sees:
PID 1, 2, 3

Container B sees:
PID 1, 2, 3

Host sees:
PID 5001, 5002, 6001
```

Each container thinks:
- it owns the system.

---

# ⚙️ How Namespaces Work

Namespaces partition:
- Processes
- Network
- Filesystem
- Users

into isolated environments.

---

# Workflow

```text
Linux Kernel
      ↓
Creates Namespace
      ↓
Assigns Process to Namespace
      ↓
Process gets isolated system view
```

---

# 🧩 Types of Linux Namespaces

Linux provides six major namespaces.

---

# Namespace Types

| Namespace | Purpose |
|---|---|
| PID | Process isolation |
| Network | Network isolation |
| Mount | Filesystem isolation |
| IPC | IPC isolation |
| UTS | Hostname isolation |
| User | User/permission isolation |

---

# 1️⃣ PID Namespace

---

# Purpose

Isolates:
- Process IDs
- Process trees

---

# How It Works

Each container gets:
- Separate PID numbering

---

# Example

```text
Container A:
PID 1 → nginx

Container B:
PID 1 → node

Host:
PID 5847 → nginx
PID 6123 → node
```

Same process:
- different PID views.

---

# Why Important?

```text
✔ Process isolation
✔ Clean abstraction
✔ Containers think they own system
```

---

# Verification

Inside container:

```bash
ps aux
echo $$
```

---

# Result

Only container processes are visible.

---

# 2️⃣ Network Namespace

---

# Purpose

Isolates:
- IP addresses
- Network interfaces
- Routing tables
- Ports

---

# Example

```text
Container A:
IP → 172.17.0.2
Port 80 active

Container B:
IP → 172.17.0.3
Port 80 active
```

No conflict because:
- different network namespaces.

---

# Benefits

```text
✔ Independent networking
✔ Multiple containers can use same ports
✔ Better isolation
```

---

# Verification

Inside container:

```bash
ip addr show
netstat -tlnp
ip route
```

---

# Example Communication

```text
Container A
      ↓
Ping 172.17.0.3
      ↓
Container B
```

---

# 3️⃣ Mount Namespace

---

# Purpose

Isolates:
- Filesystems
- Mount points
- Directories

---

# How It Works

Each container gets:
- separate root filesystem

---

# Example

```text
Container A:
/app/data.txt

Container B:
/app/data.txt
```

Different files despite same path.

---

# Benefits

```text
✔ Filesystem isolation
✔ No file conflicts
✔ Independent environments
```

---

# Verification

```bash
ls /
mount
df -h
```

---

# Example

Container A:

```bash
echo "A" > /data.txt
```

Container B:

```bash
echo "B" > /data.txt
```

Two isolated filesystems.

---

# 4️⃣ IPC Namespace

---

# Purpose

Isolates:
- Shared memory
- Message queues
- Semaphores

---

# Why Important?

Processes inside one container:
- communicate internally
- cannot access IPC of other containers

---

# Benefits

```text
✔ Secure inter-process communication
✔ Isolation between containers
```

---

# Verification

```bash
ipcs
ipcs -m
ipcs -q
```

---

# IPC Resources

| Resource | Purpose |
|---|---|
| Shared Memory | Shared data |
| Message Queues | Process messaging |
| Semaphores | Synchronization |

---

# 5️⃣ UTS Namespace

---

# Purpose

Isolates:
- Hostname
- Domain name

---

# Example

Container A:

```text
Hostname → backend-server
```

Container B:

```text
Hostname → frontend-server
```

---

# Benefits

```text
✔ Independent hostnames
✔ Easier identification
✔ Better organization
```

---

# Verification

```bash
hostname
hostname -f
```

---

# Set Custom Hostname

```bash
docker run -h mycontainer ubuntu
```

---

# 6️⃣ User Namespace

---

# Purpose

Isolates:
- User IDs
- Group IDs
- Permissions

---

# Core Security Feature

Container root user:
- NOT real host root.

---

# Example

```text
Inside Container:
UID 0 (root)

Host:
Mapped to UID 100001
```

---

# Benefits

```text
✔ Prevent privilege escalation
✔ Improved security
✔ Safer containers
```

---

# Verification

```bash
id
whoami
```

---

# 🐳 How Docker Uses Namespaces

Docker automatically creates:
- PID namespace
- Network namespace
- Mount namespace
- IPC namespace
- UTS namespace
- User namespace

for every container.

---

# Example

```bash
docker run -it ubuntu bash
```

---

# Docker Internally

```text
✔ Creates namespaces
✔ Assigns container process
✔ Applies isolation
✔ Starts container
```

---

# 🏗️ Complete Container Isolation

---

# Full Isolation Stack

```text
PID Namespace
        +
Network Namespace
        +
Mount Namespace
        +
IPC Namespace
        +
UTS Namespace
        +
User Namespace
        +
cgroups
```

---

# Result

```text
✔ Complete sandbox
✔ Resource control
✔ Security isolation
```

---

# ⚙️ Namespaces + cgroups

Namespaces only provide:
- isolation

They do NOT limit:
- CPU
- Memory
- Disk usage

---

# cgroups Provide

| Resource | Purpose |
|---|---|
| CPU | CPU limits |
| Memory | RAM limits |
| Disk I/O | Storage control |
| Network | Bandwidth control |

---

# Example

```yaml
memory: 512MB
cpu: 1
```

---

# Combined Effect

```text
Namespaces → What container sees
cgroups → What container gets
```

---

# 🔒 Security Through Isolation

Namespaces create security boundaries.

---

# Example Attack Scenario

```text
Malicious Container
        ↓
Attempts access
        ↓
Namespaces block access
```

---

# Protection

| Namespace | Security Benefit |
|---|---|
| PID | Process protection |
| Network | Network isolation |
| Mount | Filesystem protection |
| User | Permission isolation |

---

# 🌐 Shared Kernel Concept

Important:

Containers share:
- Linux kernel

---

# Example

```text
Host Linux Kernel 5.10
        ↓
Shared by all containers
```

---

# Benefits

```text
✔ Fast startup
✔ Low memory usage
✔ Better performance
```

---

# Limitation

```text
Cannot run Windows containers on Linux kernel
```

---

# ⚠️ Namespace Limitations

Namespaces isolate resources but do NOT control:
- CPU usage
- Memory limits
- Disk I/O limits

---

# Solution

Use:
- Namespaces
- cgroups together

---

# 📊 Namespace vs cgroups

| Feature | Namespaces | cgroups |
|---|---|---|
| Isolation | ✔ | ✘ |
| Resource Limits | ✘ | ✔ |
| Security | ✔ | Partial |
| CPU Control | ✘ | ✔ |
| Memory Control | ✘ | ✔ |

---

# 🔍 Verifying Namespaces

---

# List All Namespaces

```bash
lsns
```

---

# Network Namespaces

```bash
ip netns list
```

---

# Inspect Container

```bash
docker inspect container_id
```

---

# Example Output

```json
"IPAddress": "172.17.0.2"
```

---

# 🛠️ Practical Docker Examples

---

# Example 1: PID Isolation

Create container:

```bash
docker run -d --name app1 ubuntu sleep 1000
```

---

# View Processes

```bash
docker exec app1 ps aux
```

---

# Result

Only container processes visible.

---

# Example 2: Network Isolation

```bash
docker run -d -p 8080:80 --name web1 nginx
docker run -d -p 8081:80 --name web2 nginx
```

---

# Result

```text
web1 → localhost:8080
web2 → localhost:8081
```

Both use port 80 internally without conflict.

---

# Example 3: Filesystem Isolation

```bash
docker run -v ~/data:/app/data ubuntu
```

---

# Result

Containers isolated except shared volume.

---

# 📌 Quick Revision Notes

| Topic | Key Point |
|---|---|
| Namespaces | Resource isolation |
| PID Namespace | Process isolation |
| Network Namespace | Network isolation |
| Mount Namespace | Filesystem isolation |
| IPC Namespace | IPC isolation |
| UTS Namespace | Hostname isolation |
| User Namespace | Permission isolation |
| cgroups | Resource control |

---

# 🧠 Important Keywords

- Namespaces
- Process Isolation
- cgroups
- Docker
- Linux Kernel
- PID Namespace
- Network Namespace
- Mount Namespace
- Container Security
- Isolation

---

# ❓ Viva Questions

1. What is process isolation?
2. What are namespaces?
3. Why are namespaces important?
4. What is PID namespace?
5. What is network namespace?
6. What is mount namespace?
7. What is user namespace?
8. Difference between namespaces and cgroups?
9. Why are containers secure?
10. Why do containers share kernel?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| What provides isolation in containers? | Linux namespaces |
| What controls resource limits? | cgroups |
| Why can multiple containers use port 80? | Network namespaces |
| Why are containers lightweight? | Shared kernel |
| What is PID 1 inside container? | Main container process |

---

# 📌 Key Takeaway

Containers achieve isolation using:

```text
✔ PID Namespace
✔ Network Namespace
✔ Mount Namespace
✔ IPC Namespace
✔ UTS Namespace
✔ User Namespace
```

Combined with:
- cgroups

they provide:
- secure
- lightweight
- isolated
- scalable environments

---

# ✅ Conclusion

Process isolation is the foundation of modern containerization.

Linux namespaces allow containers to:
- run independently
- remain isolated
- securely share infrastructure

Combined with cgroups, namespaces create:
- secure containers
- lightweight virtualization
- scalable cloud-native systems

Namespaces and cgroups together form the core technology behind:
- Docker
- Kubernetes
- Modern container platforms

---

# 🔗 Next Topic

➡️ Control Groups (cgroups) and Resource Management