# 🚀 Unit I — Basics of DevOps Infrastructure

Complete notes, commands, architecture diagrams, practicals, and Docker fundamentals for Unit I.

---

# 📚 Topics Covered

## 1️⃣ DevOps Basics

📄 `01_DevOps.md`

Topics:
- Introduction to DevOps
- Why DevOps?
- DevOps lifecycle
- DevOps tools
- CI/CD basics
- DevOps benefits

---

## 2️⃣ Virtual Machines vs Containers

📄 `02_Virtual_Machines_VS_Containers.md`

Topics:
- Evolution from VMs to containers
- Monolithic vs microservices
- VM limitations
- Container advantages
- Docker vs Virtual Machines

---

## 3️⃣ Container Runtime

📄 `03_Container_Runtime.md`

Topics:
- What is container runtime?
- runc
- containerd
- OCI
- Runtime workflow
- Runtime vs Hypervisor

---

## 4️⃣ Process Isolation & Namespaces

📄 `04_Process_Isolation_Namespaces.md`

Topics:
- Linux namespaces
- PID namespace
- Network namespace
- Mount namespace
- IPC namespace
- UTS namespace
- User namespace

---

## 5️⃣ cgroups

📄 `05_Cgroups.md`

Topics:
- Resource control
- CPU limits
- Memory limits
- Disk I/O control
- Network limits
- Process limits

---

## 6️⃣ Container Images & Layers

📄 `06_Container_Images_And_Layers.md`

Topics:
- Docker images
- Image layers
- Copy-on-Write
- Layer caching
- OverlayFS

---

## 7️⃣ Image Registries & Distribution

📄 `07_Image_Registeries.md`

Topics:
- Docker Hub
- GHCR
- AWS ECR
- Image push/pull
- Registry authentication
- Image tagging

---

## 8️⃣ Docker Architecture

📄 `08_Docker_Architecture.md`

Topics:
- Docker daemon
- Docker CLI
- Docker workflow
- Build-Ship-Run model
- Container lifecycle

---

## 9️⃣ Basic Docker Commands

📄 `09_Basic_Docker_Commands.md`

Topics:
- Image commands
- Container commands
- Network commands
- Volume commands
- Cleanup commands

---

## 🔟 Docker Object Types

📄 `10_Docker_Object_Types.md`

Topics:
- Images
- Containers
- Networks
- Volumes
- OverlayFS
- Docker filesystem

---

## 1️⃣1️⃣ Container Interaction

📄 `11_Container_Interaction.md`

Topics:
- docker exec
- docker attach
- docker cp
- docker logs
- docker inspect
- docker stats

---

## 1️⃣2️⃣ Docker Practice Questions

📄 `13_Docker_Practice_Questions.md`

Topics:
- Resource isolation
- cgroups
- namespaces
- networking
- troubleshooting
- Apache deployment

---

# 🎯 Learning Outcomes

After completing this unit, you will understand:

✅ DevOps fundamentals  
✅ Virtualization and containers  
✅ Linux namespaces and cgroups  
✅ Docker architecture and workflow  
✅ Docker images and layers  
✅ Container runtime and OCI  
✅ Docker networking and volumes  
✅ Docker commands and troubleshooting  
✅ Container interaction with host system  
✅ Practical Docker deployment examples  

---

# 🛠️ Technologies Covered

| Technology | Purpose |
|---|---|
| Docker | Containerization |
| Linux Namespaces | Isolation |
| cgroups | Resource control |
| OverlayFS | Layered filesystem |
| Docker Hub | Image registry |
| containerd | Container runtime |
| runc | Low-level runtime |

---

# 📌 Important Docker Commands

## Pull Image

```bash
docker pull nginx
```

---

## Run Container

```bash
docker run -d -p 8080:80 nginx
```

---

## View Running Containers

```bash
docker ps
```

---

## Open Terminal Inside Container

```bash
docker exec -it <container_id> bash
```

---

## View Logs

```bash
docker logs <container_id>
```

---

## Stop Container

```bash
docker stop <container_id>
```

---

# 📊 Docker Workflow

```text
Dockerfile
     ↓
Build Image
     ↓
Push to Registry
     ↓
Pull Image
     ↓
Run Container
```

---

# 🌟 Core Concepts

| Concept | Description |
|---|---|
| Container | Lightweight isolated environment |
| Image | Read-only template |
| Namespace | Isolation mechanism |
| cgroups | Resource control |
| Volume | Persistent storage |
| Network | Container communication |
| Runtime | Executes containers |

---

# 📖 Recommended Learning Path

```text
DevOps Basics
      ↓
VMs vs Containers
      ↓
Namespaces + cgroups
      ↓
Container Runtime
      ↓
Images + Layers
      ↓
Docker Architecture
      ↓
Docker Commands
      ↓
Networking + Volumes
      ↓
Practice Questions
```

---

# 💡 Best Use Cases

These notes are useful for:

✅ University exams  
✅ Viva preparation  
✅ DevOps interviews  
✅ Docker fundamentals  
✅ Lab practicals  
✅ GitHub portfolio projects  

---

# 👨‍💻 Author

Komal Joshi  
B.Tech CSE — 2027  
DevOps & Cloud Computing Notes

---

# ⭐ Final Note

This Unit I repository provides:
- theory
- commands
- practicals
- architecture
- interview preparation
- troubleshooting

for mastering:
- Docker
- Containers
- DevOps Infrastructure Fundamentals