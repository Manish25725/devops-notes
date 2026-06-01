# Docker Practical Projects

![Docker](https://img.shields.io/badge/Docker-Projects-blue)
![DevOps](https://img.shields.io/badge/DevOps-HandsOn-green)
![Containers](https://img.shields.io/badge/Containers-Practical-orange)
![CI/CD](https://img.shields.io/badge/CI/CD-Deployment-red)

---

# 📚 Table of Contents

- Introduction
- Project 1 — Custom Nginx Website
- Project 2 — Node.js Express Application
- Project 3 — MySQL Persistent Database
- Project 4 — Multi-Container Application
- Project 5 — Bind Mount Development Workflow
- Project 6 — Push Image to GHCR
- Best Practices
- Summary

---

# 📖 Introduction

Practical Docker projects help understand:

```text
✔ Dockerfiles
✔ Image Building
✔ Containers
✔ Networking
✔ Volumes
✔ Port Mapping
✔ Registries
✔ Environment Variables
```

These projects simulate:
- real DevOps workflows
- production deployments
- CI/CD pipelines

---

# 🌐 Project 1 — Custom Nginx Website

---

# 🎯 Objective

Deploy a custom static website using:
- Nginx container
- Dockerfile
- Port mapping

---

# 📁 Project Structure

```text
nginx-project/
 ├── Dockerfile
 ├── index.html
 └── default.conf
```

---

# 📄 index.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>Docker App</title>
</head>
<body>
    <h1>Welcome to My Docker Nginx App</h1>
</body>
</html>
```

---

# 📄 default.conf

```nginx
server {
    listen 80;

    location / {
        root /usr/share/nginx/html;
        index index.html;
    }
}
```

---

# 📄 Dockerfile

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html

COPY default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
```

---

# 🏗️ Build Image

```bash
docker build -t custom-nginx:v1 .
```

---

# 🚀 Run Container

```bash
docker run -d \
  -p 8080:80 \
  --name nginx-container \
  custom-nginx:v1
```

---

# 🌍 Access Website

```text
http://localhost:8080
```

---

# ✅ Result

```text
✔ Custom website deployed
✔ Docker image created
✔ Port mapping working
```

---

# 🟢 Project 2 — Node.js Express Application

---

# 🎯 Objective

Containerize a Node.js Express server.

---

# 📁 Project Structure

```text
node-app/
 ├── app.js
 ├── package.json
 └── Dockerfile
```

---

# 📄 app.js

```javascript
const express = require("express");

const app = express();

app.get("/", (req, res) => {
  res.send("Docker Node App Running!");
});

app.listen(3000, "0.0.0.0", () => {
  console.log("Server running on port 3000");
});
```

---

# 📄 package.json

```json
{
  "name": "node-docker-app",
  "version": "1.0.0",
  "main": "app.js",
  "dependencies": {
    "express": "^4.18.2"
  }
}
```

---

# 📄 Dockerfile

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package.json .

RUN npm install

COPY app.js .

EXPOSE 3000

CMD ["node", "app.js"]
```

---

# 🏗️ Build Image

```bash
docker build -t node-demo:v1 .
```

---

# 🚀 Run Container

```bash
docker run -d \
  -p 3000:3000 \
  --name node-container \
  node-demo:v1
```

---

# 🌍 Access Application

```text
http://localhost:3000
```

---

# ✅ Result

```text
✔ Node.js app containerized
✔ Docker networking working
✔ Application accessible
```

---

# 🗄️ Project 3 — MySQL Persistent Database

---

# 🎯 Objective

Run MySQL container with:
- environment variables
- persistent volume

---

# 📦 Create Volume

```bash
docker volume create mysql_data
```

---

# 🚀 Run MySQL

```bash
docker run -d \
  --name mysql_db \
  -e MYSQL_ROOT_PASSWORD=root123 \
  -e MYSQL_DATABASE=college \
  -v mysql_data:/var/lib/mysql \
  -p 3307:3306 \
  mysql:8
```

---

# 🔍 Verify

```bash
docker ps
```

---

# 🧠 Connect to MySQL

```bash
docker exec -it mysql_db bash
```

Inside container:

```bash
mysql -u root -p
```

---

# ✅ Result

```text
✔ Persistent database
✔ Environment variables working
✔ Volume persistence enabled
```

---

# 🌐 Project 4 — Multi-Container Application

---

# 🎯 Objective

Create:
- frontend
- backend
- database

containers using Docker networking.

---

# 📡 Create Network

```bash
docker network create app_net
```

---

# 🗄️ Run Database

```bash
docker run -d \
  --name database \
  --network app_net \
  -e MYSQL_ROOT_PASSWORD=root123 \
  mysql:8
```

---

# ⚙️ Run Backend

```bash
docker run -d \
  --name backend \
  --network app_net \
  -e DB_HOST=database \
  backend:v1
```

---

# 🌍 Run Frontend

```bash
docker run -d \
  --name frontend \
  --network app_net \
  -p 8080:80 \
  frontend:v1
```

---

# 🧠 Architecture

```text
Frontend
   ↓
Backend
   ↓
Database
```

---

# ✅ Result

```text
✔ Multi-container communication
✔ Docker networking
✔ Service isolation
✔ Microservices architecture
```

---

# 🔄 Project 5 — Bind Mount Development Workflow

---

# 🎯 Objective

Use bind mounts for:
- live code updates
- development workflow

---

# 📁 Create Project

```bash
mkdir bind-demo

cd bind-demo
```

---

# 📄 Create app.js

```javascript
console.log("Hello Docker");
```

---

# 🚀 Run Container with Bind Mount

```bash
docker run -it \
  -v $(pwd):/app \
  node:18 \
  node /app/app.js
```

---

# ✏️ Modify app.js

```javascript
console.log("Updated Docker App");
```

---

# 🔄 Run Again

```bash
docker run -it \
  -v $(pwd):/app \
  node:18 \
  node /app/app.js
```

---

# ✅ Result

```text
✔ Instant updates
✔ No rebuild required
✔ Fast development cycle
```

---

# ☁️ Project 6 — Push Image to GHCR

---

# 🎯 Objective

Push Docker image to:
- GitHub Container Registry

---

# 📁 Create Project

```bash
mkdir ghcr-demo
```

---

# 📄 index.html

```html
<h1>GHCR Demo Success!</h1>
```

---

# 📄 Dockerfile

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html
```

---

# 🏗️ Build Image

```bash
docker build -t ghcr.io/YOUR_USERNAME/ghcr-demo .
```

---

# 🔐 Login to GHCR

```bash
docker login ghcr.io
```

Use:
- GitHub username
- PAT token

---

# 📤 Push Image

```bash
docker push ghcr.io/YOUR_USERNAME/ghcr-demo
```

---

# 📥 Pull Image

```bash
docker pull ghcr.io/YOUR_USERNAME/ghcr-demo
```

---

# 🚀 Run Container

```bash
docker run -p 8080:80 ghcr.io/YOUR_USERNAME/ghcr-demo
```

---

# 🌍 Verify

```text
http://localhost:8080
```

---

# ✅ Result

```text
✔ Image uploaded to GHCR
✔ Registry workflow completed
✔ Deployment verified
```

---

# 🔐 Best Practices

---

# Use Small Base Images

✅ Good

```dockerfile
FROM alpine
```

---

# Use Volumes for Databases

```bash
-v mysql_data:/var/lib/mysql
```

---

# Use .dockerignore

Avoid unnecessary files.

---

# Use Environment Variables

Avoid hardcoded values.

---

# Use Custom Networks

```bash
docker network create app_net
```

---

# Use Proper Version Tags

```text
v1.0.0
```

---

# 📊 Skills Learned

| Project | Skills |
|---|---|
| Nginx Website | Dockerfile, Port Mapping |
| Node.js App | Application Containerization |
| MySQL Database | Volumes, Persistence |
| Multi-Container App | Networking |
| Bind Mount Workflow | Development Setup |
| GHCR Deployment | Registries, Authentication |

---

# 📌 Quick Revision Notes

| Concept | Example |
|---|---|
| Dockerfile | Build image |
| Port Mapping | -p 8080:80 |
| Volume | Persistent storage |
| Bind Mount | Live development |
| Network | Multi-container communication |
| GHCR | Image registry |

---

# 🧠 Important Keywords

- Dockerfile
- Image Build
- Port Mapping
- Docker Volume
- Bind Mount
- Docker Network
- GHCR
- Multi-Container Application
- Containerization

---

# ❓ Viva Questions

1. What is Dockerfile?
2. Why use Docker volumes?
3. What is bind mount?
4. Why use Docker networking?
5. What is port mapping?
6. How to push image to GHCR?
7. What is environment variable?
8. Why use Docker Compose?
9. Difference between volume and bind mount?
10. What is multi-container architecture?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| Why containerize applications? | Portability and scalability |
| Why use volumes for databases? | Persistent storage |
| What is bind mount useful for? | Development |
| Why use custom networks? | Container communication |
| What is GHCR? | GitHub Container Registry |

---

# ✅ Conclusion

These Docker practical projects demonstrate:
- real-world containerization
- networking
- storage
- deployment workflows
- registry integration

Using:
- Dockerfiles
- Volumes
- Networks
- Environment Variables
- GHCR

developers can build:
- scalable
- portable
- production-ready applications

These projects form the foundation for:
- Docker Compose
- Kubernetes
- CI/CD pipelines
- cloud-native DevOps