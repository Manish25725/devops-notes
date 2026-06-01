# Control Groups (cgroups)

![Linux](https://img.shields.io/badge/Linux-cgroups-blue)
![Docker](https://img.shields.io/badge/Docker-Containers-green)
![Kernel](https://img.shields.io/badge/Kernel-ResourceControl-orange)
![DevOps](https://img.shields.io/badge/DevOps-Infrastructure-red)
![Containers](https://img.shields.io/badge/Containers-Isolation-purple)

---

# 📚 Table of Contents

- [Overview](#-overview)
- [What are cgroups?](#-what-are-cgroups)
- [Why cgroups are Needed](#-why-cgroups-are-needed)
- [Namespaces vs cgroups](#-namespaces-vs-cgroups)
- [Apartment Building Analogy](#-apartment-building-analogy)
- [Problems Without cgroups](#-problems-without-cgroups)
- [Benefits of cgroups](#-benefits-of-cgroups)
- [Resources Controlled by cgroups](#-resources-controlled-by-cgroups)
- [CPU Control](#-cpu-control)
- [Memory Control](#-memory-control)
- [Disk I/O Control](#-disk-io-control)
- [Network Control](#-network-control)
- [Device Access Control](#-device-access-control)
- [Process Count Control](#-process-count-control)
- [How cgroups Work](#-how-cgroups-work)
- [Docker and cgroups](#-docker-and-cgroups)
- [Soft Limit vs Hard Limit](#-soft-limit-vs-hard-limit)
- [cgroups Workflow](#-cgroups-workflow)
- [Practical Docker Examples](#-practical-docker-examples)
- [Benefits of cgroups](#-benefits-of-cgroups-1)
- [Limitations of cgroups](#-limitations-of-cgroups)
- [Quick Revision Notes](#-quick-revision-notes)
- [Viva Questions](#-viva-questions)
- [Interview Questions](#-interview-questions)
- [Conclusion](#-conclusion)

---

# 📖 Overview

Containers share the same operating system kernel.

Without proper resource control:
- One container can consume all CPU
- Memory may get exhausted
- Disk performance may degrade
- Entire host system may crash

Linux solves this problem using:
- cgroups (Control Groups)

cgroups ensure:
- Fair resource allocation
- Stability
- Predictable performance

---

# 🧠 What are cgroups?

> cgroups (Control Groups) are a Linux kernel feature used to limit, monitor, and control resources for processes and containers.

---

# 🎯 Main Purpose

cgroups control:
- CPU usage
- Memory usage
- Disk I/O
- Network bandwidth
- Process limits
- Device access

---

# Core Idea

```text
Namespaces → Isolation
cgroups → Resource Control
```

---

# ⚠️ Why cgroups are Needed

Without cgroups:

```text
One container uses:
✔ All CPU
✔ All RAM
✔ All disk bandwidth
✔ All network bandwidth
```

---

# Result

```text
✔ Other containers become slow
✔ Applications crash
✔ Host system freezes
✔ Infrastructure instability
```

---

# Example Problem

```text
Container A → Heavy workload
Container B → Starved of resources
Container C → Crashes
Host → Becomes unstable
```

---

# 🏗️ Namespaces vs cgroups

Namespaces and cgroups work together.

---

# Namespaces

Namespaces provide:
- Isolation
- Separate views of resources

---

# Example

```text
Container A sees PID 1
Container B sees PID 1
```

Both isolated from each other.

---

# cgroups

cgroups provide:
- Resource limits
- Fair sharing

---

# Example

```text
Container A → 512MB RAM
Container B → 256MB RAM
```

---

# 📊 Namespaces vs cgroups Comparison

| Feature | Namespaces | cgroups |
|---|---|---|
| Purpose | Isolation | Resource control |
| Controls Visibility | ✔ | ✘ |
| Controls CPU/Memory | ✘ | ✔ |
| Security | ✔ | Partial |
| Resource Allocation | ✘ | ✔ |

---

# 🏢 Apartment Building Analogy

---

# Namespaces

Namespaces are like:
- separate apartments

Each tenant:
- sees only their apartment

---

# cgroups

cgroups are like:
- electricity/water meters

Each apartment gets:
- limited resource usage

---

# Result

```text
✔ Fair usage
✔ No resource abuse
✔ Stable building
```

---

# ❌ Problems Without cgroups

Without cgroups:

---

# Scenario

One container starts heavy processing.

---

# Effects

```text
✔ CPU fully consumed
✔ RAM exhausted
✔ Disk becomes slow
✔ Other containers stop responding
✔ Host crashes
```

---

# Example

```text
Container A → Uses 100% CPU
Container B → No CPU available
Container C → Crashes due to memory shortage
```

---

# Result

```text
Infrastructure becomes unstable
```

---

# ✅ Benefits of cgroups

With cgroups:

```text
✔ Fair resource sharing
✔ Predictable performance
✔ Better stability
✔ Improved security
✔ Controlled scalability
```

---

# Example

```text
Container A → 40% CPU
Container B → 35% CPU
Container C → 25% CPU
```

All containers continue running properly.

---

# 🧩 Resources Controlled by cgroups

cgroups control many system resources.

---

# Resource Types

| Resource | Purpose |
|---|---|
| CPU | CPU time and cores |
| Memory | RAM limits |
| Disk I/O | Disk read/write control |
| Network | Bandwidth control |
| Devices | Hardware access |
| Process Count | Maximum processes |

---

# ⚙️ CPU Control

cgroups control:
- CPU cores
- CPU time
- CPU priorities

---

# Example

```bash
docker run --cpus 1 nginx
```

---

# Result

```text
Container limited to 1 CPU core
```

---

# Benefits

```text
✔ Prevent CPU monopolization
✔ Fair scheduling
✔ Stable performance
```

---

# Example Scenario

```text
Container A → 50% CPU
Container B → 25% CPU
Container C → 25% CPU
```

---

# 🧠 Memory Control

Memory control prevents containers from exhausting RAM.

---

# Example

```bash
docker run -m 512m nginx
```

---

# Result

```text
Maximum RAM = 512MB
```

---

# Benefits

```text
✔ Prevent memory exhaustion
✔ Protect host system
✔ Stable infrastructure
```

---

# Soft Limit vs Hard Limit

| Limit Type | Behavior |
|---|---|
| Soft Limit | Warning/slower performance |
| Hard Limit | Container killed |

---

# Example

```text
Memory exceeds hard limit
        ↓
Kernel kills container
```

---

# 💽 Disk I/O Control

Disk I/O control limits:
- Read operations
- Write operations
- Disk bandwidth

---

# Benefits

```text
✔ Prevent disk saturation
✔ Fair storage performance
```

---

# Example

```text
Container A → Heavy database writes
Container B → Still receives disk access
```

---

# 🌐 Network Control

Network cgroups control:
- Upload speed
- Download speed
- Packet rate

---

# Benefits

```text
✔ Prevent network flooding
✔ Fair bandwidth allocation
```

---

# Example

```text
Container limited to:
100 Mbps bandwidth
```

---

# 🔌 Device Access Control

cgroups restrict:
- Access to hardware devices

---

# Example Devices

| Device | Example |
|---|---|
| Storage | /dev/sda |
| GPU | NVIDIA GPU |
| USB | USB devices |

---

# Benefits

```text
✔ Better security
✔ Prevent unauthorized hardware access
```

---

# 🔢 Process Count Control

Limits:
- Number of processes
- Number of threads

---

# Why Important?

Prevents:
- Fork bombs
- Process abuse

---

# Example

```text
Maximum Processes = 100
```

---

# ⚙️ How cgroups Work

---

# Step 1️⃣

Linux creates a cgroup.

---

# Step 2️⃣

Docker assigns container processes to that cgroup.

---

# Step 3️⃣

Limits are applied.

---

# Step 4️⃣

Kernel continuously monitors usage.

---

# Step 5️⃣

If limits exceeded:
- throttle resources
- kill process
- generate warnings

---

# Workflow

```text
Container Created
        ↓
cgroup Assigned
        ↓
Limits Applied
        ↓
Kernel Monitors Usage
        ↓
Resource Enforcement
```

---

# 🐳 Docker and cgroups

Docker automatically uses cgroups.

---

# Example Commands

---

# Limit Memory

```bash
docker run -m 512m nginx
```

---

# Limit CPU

```bash
docker run --cpus 1 nginx
```

---

# Limit Processes

```bash
docker run --pids-limit 100 nginx
```

---

# Combined Example

```bash
docker run \
-m 512m \
--cpus 1 \
--pids-limit 100 \
nginx
```

---

# Result

```text
✔ 512MB RAM
✔ 1 CPU
✔ 100 processes maximum
```

---

# 📊 Soft Limit vs Hard Limit

---

# Soft Limit

```text
✔ Warning threshold
✔ System tries optimization
✔ Container slowed down
```

---

# Hard Limit

```text
✔ Strict enforcement
✔ Container terminated
✔ Prevents host crash
```

---

# Example

```text
Container exceeds memory limit
        ↓
OOM Killer terminates container
```

---

# 🔄 cgroups Workflow

```text
Container Starts
        ↓
Docker Creates cgroup
        ↓
Limits Configured
        ↓
Kernel Monitors Usage
        ↓
Resource Usage Controlled
```

---

# 🛠️ Practical Docker Examples

---

# Example 1: Limit Memory

```bash
docker run -m 256m ubuntu
```

---

# Example 2: Limit CPU

```bash
docker run --cpus 0.5 ubuntu
```

---

# Example 3: Limit Processes

```bash
docker run --pids-limit 50 ubuntu
```

---

# Example 4: Combined Limits

```bash
docker run \
-m 512m \
--cpus 1 \
--pids-limit 100 \
ubuntu
```

---

# 🌟 Benefits of cgroups

| Benefit | Description |
|---|---|
| Stability | Prevents host crashes |
| Fairness | Equal resource sharing |
| Scalability | Better workload management |
| Security | Restricts abuse |
| Predictability | Controlled performance |

---

# ⚠️ Limitations of cgroups

| Limitation | Description |
|---|---|
| No Isolation | Isolation handled by namespaces |
| Shared Kernel | Containers still share kernel |
| Complex Tuning | Requires optimization |
| Linux Specific | Kernel feature |

---

# 📌 Quick Revision Notes

| Topic | Key Point |
|---|---|
| cgroups | Resource control |
| CPU Limit | Restrict CPU usage |
| Memory Limit | Restrict RAM |
| Disk I/O | Storage control |
| Process Limit | Prevent fork bombs |
| Soft Limit | Warning |
| Hard Limit | Strict enforcement |
| Namespaces | Isolation |

---

# 🧠 Important Keywords

- cgroups
- Linux Kernel
- Resource Limits
- CPU Control
- Memory Control
- Docker
- Namespaces
- OOM Killer
- Process Limits
- Container Stability

---

# ❓ Viva Questions

1. What are cgroups?
2. Why are cgroups needed?
3. Difference between namespaces and cgroups?
4. How does Docker use cgroups?
5. What is memory limiting?
6. What happens when memory limit exceeds?
7. What is CPU throttling?
8. What are soft and hard limits?
9. What is process limit?
10. Why are cgroups important?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| What do cgroups control? | CPU, memory, I/O, network |
| Why use cgroups? | Prevent resource abuse |
| Difference between namespaces and cgroups? | Isolation vs resource control |
| What happens if memory exceeds limit? | Container killed |
| Why are cgroups important in containers? | Stability and fairness |

---

# 📌 Key Takeaway

cgroups are the resource management foundation of containers.

They ensure:

```text
✔ Fair resource sharing
✔ Host stability
✔ Controlled scaling
✔ Predictable performance
✔ Better security
```

Together:

```text
Namespaces → Isolation
cgroups → Resource Control
```

form the core technology behind:
- Docker
- Kubernetes
- Modern cloud-native infrastructure

---

# ✅ Conclusion

Containers need controlled resource allocation to ensure:
- Stability
- Fairness
- Scalability

cgroups solve this problem by limiting:
- CPU
- Memory
- Disk I/O
- Network bandwidth
- Process count

Combined with namespaces, cgroups create:
- secure
- lightweight
- efficient container environments

cgroups are a critical part of:
- Docker
- Kubernetes
- Linux containerization

---

# 🔗 Next Topic

➡️ Container Images and Docker Layering