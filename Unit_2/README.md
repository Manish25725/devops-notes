# 🐳 Unit II — Image Building & Container Management

Complete notes and practicals for Docker Image Building, Container Management, Networking, Storage, Registries, and DevOps workflows.

![Docker](https://img.shields.io/badge/Docker-Containerization-blue)
![DevOps](https://img.shields.io/badge/DevOps-Automation-green)
![Containers](https://img.shields.io/badge/Containers-Virtualization-orange)
![CI/CD](https://img.shields.io/badge/CI/CD-Pipelines-red)

---

# 📚 Unit II Syllabus Coverage

This repository covers the complete Unit II syllabus:

✔ Dockerfile Core Concepts  
✔ Image Layering  
✔ Build Context & `.dockerignore`  
✔ Dockerfile Instructions (`FROM`, `RUN`, `COPY`, `ADD`, `CMD`, `ENTRYPOINT`, `WORKDIR`, `ENV`, `EXPOSE`, `VOLUME`)  
✔ Docker Build Process  
✔ Image Tagging & Versioning  
✔ Docker Networking  
✔ Bridge, Host & Overlay Networks  
✔ DNS Inside Docker  
✔ Linking Containers  
✔ Port Mapping  
✔ Docker Storage  
✔ Volumes vs Bind Mounts  
✔ Copy-on-Write Mechanism  
✔ Docker Hub & GHCR  
✔ Private Registries  
✔ Authentication & Access Tokens  
✔ Practical Docker Projects  

---

# 📂 Repository Structure

| File | Topic |
|---|---|
| `01_Dockerfile_Core_Concepts.md` | Dockerfile fundamentals & image layering |
| `02_Dockerfile_Instructions.md` | Important Dockerfile instructions |
| `03_Image_Building_And_Management.md` | Docker build process & image management |
| `04_Docker_Layering_And_Filesystem.md` | Docker layers & Copy-on-Write |
| `05_Build_Context_And_Dockerignore.md` | Build context & `.dockerignore` |
| `06_Docker_Networking.md` | Docker networking concepts |
| `07_Docker_Storage_Volumes_Bind_Mounts.md` | Volumes & bind mounts |
| `08_Environment_Variables_And_Port_Mapping.md` | Environment variables & networking |
| `09_Registries_And_GHCR.md` | Docker Hub, GHCR & registries |
| `10_Docker_Practical_Projects.md` | Hands-on Docker projects |
| `11_Docker_Best_Practices_And_Interview_Preparation.md` | Best practices & interview prep |

---

# 🚀 Learning Path

## Step 1 — Learn Dockerfile Basics

Start with:
- Docker architecture
- Image layering
- Build process

📄 Read:
`01_Dockerfile_Core_Concepts.md`

---

## Step 2 — Learn Dockerfile Instructions

Understand:
- `FROM`
- `RUN`
- `COPY`
- `CMD`
- `ENTRYPOINT`
- `ENV`
- `WORKDIR`

📄 Read:
`02_Dockerfile_Instructions.md`

---

## Step 3 — Build & Manage Images

Learn:
- `docker build`
- image tagging
- image history
- optimization

📄 Read:
`03_Image_Building_And_Management.md`

---

## Step 4 — Understand Docker Layers

Learn:
- Copy-on-Write
- OverlayFS
- layer caching

📄 Read:
`04_Docker_Layering_And_Filesystem.md`

---

## Step 5 — Build Context & .dockerignore

Learn:
- build optimization
- secure builds
- reducing image size

📄 Read:
`05_Build_Context_And_Dockerignore.md`

---

## Step 6 — Learn Docker Networking

Understand:
- bridge networks
- host networks
- overlay networks
- DNS resolution

📄 Read:
`06_Docker_Networking.md`

---

## Step 7 — Learn Docker Storage

Understand:
- Docker volumes
- bind mounts
- persistent storage

📄 Read:
`07_Docker_Storage_Volumes_Bind_Mounts.md`

---

## Step 8 — Environment Variables & Ports

Learn:
- dynamic configuration
- `.env`
- port mapping

📄 Read:
`08_Environment_Variables_And_Port_Mapping.md`

---

## Step 9 — Registries & GHCR

Learn:
- Docker Hub
- GitHub Container Registry
- image push/pull
- authentication

📄 Read:
`09_Registries_And_GHCR.md`

---

## Step 10 — Practice Projects

Build:
- Nginx website
- Node.js apps
- MySQL database
- Multi-container systems

📄 Read:
`10_Docker_Practical_Projects.md`

---

## Step 11 — Interview Preparation

Learn:
- best practices
- optimization
- troubleshooting
- interview questions

📄 Read:
`11_Docker_Best_Practices_And_Interview_Preparation.md`

---

# 🧠 Important Docker Concepts Covered

| Topic | Description |
|---|---|
| Dockerfile | Instructions to build image |
| Docker Image | Read-only application template |
| Docker Container | Running instance of image |
| Volumes | Persistent storage |
| Bind Mounts | Host-to-container mapping |
| Networking | Container communication |
| Port Mapping | Host ↔ container connectivity |
| Registries | Image storage systems |
| GHCR | GitHub Container Registry |
| Layering | Efficient image storage |
| CoW | Copy-on-Write mechanism |

---

# 🛠️ Common Docker Commands

## Build Image

```bash
docker build -t myapp:v1 .
```

---

## Run Container

```bash
docker run -d -p 8080:80 nginx
```

---

## List Containers

```bash
docker ps
```

---

## View Logs

```bash
docker logs container_id
```

---

## Open Terminal Inside Container

```bash
docker exec -it container_id bash
```

---

## Create Volume

```bash
docker volume create myvolume
```

---

## Create Network

```bash
docker network create mynetwork
```

---

## Push Image to Docker Hub

```bash
docker push username/myapp:v1
```

---

## Push Image to GHCR

```bash
docker push ghcr.io/username/myapp:v1
```

---

# 🌍 Practical Projects Included

✔ Custom Nginx Website  
✔ Node.js Express App  
✔ MySQL Persistent Database  
✔ Multi-Container Application  
✔ Bind Mount Development Workflow  
✔ GitHub Container Registry Deployment  

---

# 📈 Skills You Will Gain

After completing this unit, you will understand:

```text
✔ Docker Architecture
✔ Dockerfile Writing
✔ Image Building
✔ Container Management
✔ Docker Networking
✔ Docker Storage
✔ Registry Management
✔ GHCR Integration
✔ CI/CD Basics
✔ Production Best Practices
✔ Docker Troubleshooting
```

---

# 💼 Interview Preparation

This repository also includes:

✔ Viva Questions  
✔ Interview Questions  
✔ Best Practices  
✔ Real-world Examples  
✔ Production Concepts  
✔ Troubleshooting Scenarios  

---

# 🔐 Best Practices Summary

✔ Use Alpine images  
✔ Use `.dockerignore`  
✔ Avoid `latest` tag  
✔ Use volumes for databases  
✔ Use bind mounts for development  
✔ Avoid running containers as root  
✔ Use environment variables  
✔ Use custom Docker networks  
✔ Keep images small and optimized  

---

# 📖 Recommended Learning Order

```text
Docker Basics
      ↓
Dockerfile
      ↓
Images & Containers
      ↓
Networking
      ↓
Storage
      ↓
Registries
      ↓
Projects
      ↓
Docker Compose
      ↓
Kubernetes
```

---

# 🎯 Future Learning

After Docker:

```text
Docker Compose
      ↓
Kubernetes
      ↓
Helm
      ↓
CI/CD Pipelines
      ↓
Cloud Deployments
```

---

# 👩‍💻 Author

**Komal Joshi**  
B.Tech CSE  
DevOps & Cloud Computing Enthusiast 🚀

---

# ⭐ Conclusion

This repository provides:
- complete Docker theory
- practical implementations
- DevOps workflows
- production concepts
- interview preparation

It is designed for:
- university preparation
- lab practice
- DevOps beginners
- Docker learners
- interview preparation

Mastering these topics builds a strong foundation for:
- Docker Compose
- Kubernetes
- CI/CD
- Cloud-native DevOps
- modern infrastructure engineering

---

# 📌 References

- :contentReference[oaicite:0]{index=0}
- :contentReference[oaicite:1]{index=1}
- :contentReference[oaicite:2]{index=2}
- :contentReference[oaicite:3]{index=3}

---