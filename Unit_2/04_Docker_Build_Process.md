# Docker Build Process

![Docker](https://img.shields.io/badge/Docker-BuildProcess-blue)
![Images](https://img.shields.io/badge/Images-Automation-green)
![DevOps](https://img.shields.io/badge/DevOps-CI/CD-orange)
![Containers](https://img.shields.io/badge/Containers-Layering-red)

---

# 📚 Table of Contents

- Introduction
- What is docker build?
- Build Process Workflow
- Docker Build Context
- .dockerignore
- Build Stages
- Layer Creation
- Layer Caching
- Build Output
- Image Tagging During Build
- Build Logs
- Multi-Stage Builds
- Build Optimization
- Common Errors
- Best Practices
- Complete Examples
- Summary

---

# 📖 Introduction

Docker images are created using:
- `docker build`

The build process:
- reads Dockerfile
- executes instructions
- creates image layers
- stores final image locally

---

# 🧠 What is docker build?

> `docker build` creates Docker images from Dockerfile instructions.

---

# Basic Syntax

```bash
docker build [OPTIONS] PATH
```

---

# Example

```bash
docker build -t myapp:v1 .
```

---

# Explanation

| Part | Meaning |
|---|---|
| docker build | Build image |
| -t | Tag image |
| myapp:v1 | Image name + version |
| . | Current directory as build context |

---

# 🏗️ Docker Build Workflow

```text
Dockerfile
      ↓
Build Context Sent
      ↓
Instructions Executed
      ↓
Layers Created
      ↓
Image Built
      ↓
Stored Locally
```

---

# 🔥 Step-by-Step Build Process

---

# Step 1️⃣ Read Dockerfile

Docker searches for:
- `Dockerfile`

inside build context.

---

# Example

```bash
docker build .
```

Docker checks:

```text
./Dockerfile
```

---

# Step 2️⃣ Send Build Context

Docker sends:
- files
- folders
- source code

to Docker daemon.

---

# Build Context Example

```text
project/
 ├── Dockerfile
 ├── app.js
 ├── package.json
 └── node_modules/
```

---

# Problem

Large folders:
- slow builds
- increase image size

---

# 🚫 .dockerignore

Used to exclude unnecessary files.

---

# Example

```text
node_modules
.git
.env
*.log
```

---

# Benefits

```text
✔ Faster builds
✔ Smaller images
✔ Better security
✔ Reduced context size
```

---

# Step 3️⃣ Execute Instructions

Docker executes instructions:
- sequentially

---

# Example

```dockerfile
FROM ubuntu

RUN apt-get update

COPY . /app
```

Execution order:
1. FROM
2. RUN
3. COPY

---

# Step 4️⃣ Create Layers

Each instruction creates:
- immutable image layer

---

# Example

| Instruction | Layer |
|---|---|
| FROM ubuntu | Base layer |
| RUN apt-get update | Layer 2 |
| COPY . /app | Layer 3 |

---

# Step 5️⃣ Cache Layers

Docker stores layers in cache.

---

# Benefit

Future builds reuse unchanged layers.

---

# Example

If app code changes only:
- dependency layers reused

---

# Step 6️⃣ Final Image Created

Docker combines all layers into:
- final image

---

# Image Stored Locally

Check images:

```bash
docker images
```

---

# ⚡ Layer Caching

Docker caching improves:
- build speed

---

# Example Dockerfile

```dockerfile
FROM node:18

COPY package.json .

RUN npm install

COPY . .
```

---

# Why This Order?

Dependencies install only when:
- package.json changes

---

# Result

```text
✔ Faster rebuilds
✔ Cached npm install layer reused
```

---

# ❌ Bad Dockerfile Order

```dockerfile
COPY . .

RUN npm install
```

---

# Problem

Any code change:
- invalidates cache
- reinstall dependencies

---

# 📦 Build Output

---

# Example Command

```bash
docker build -t myapp:v1 .
```

---

# Output Example

```text
Step 1/4 : FROM ubuntu
 ---> 2ca708c1c9cc

Step 2/4 : RUN apt-get update
 ---> Running in abc123

Step 3/4 : COPY . /app
 ---> xyz789

Successfully built 12345abc
Successfully tagged myapp:v1
```

---

# 🏷️ Image Tagging During Build

Tag image while building.

---

# Syntax

```bash
docker build -t image:tag .
```

---

# Examples

```bash
docker build -t myapp:v1 .

docker build -t nginx-custom:latest .
```

---

# Multiple Tags

```bash
docker build -t myapp:v1 -t myapp:latest .
```

---

# 📜 Build Logs

Docker displays:
- build progress
- layer creation
- cache usage
- errors

---

# Example

```text
Using cache
```

means:
- cached layer reused

---

# 🌟 Multi-Stage Builds

Used to:
- reduce image size
- separate build/runtime environments

---

# Example

```dockerfile
FROM node:18 AS build

WORKDIR /app

COPY . .

RUN npm install

RUN npm run build

FROM nginx:alpine

COPY --from=build /app/dist /usr/share/nginx/html
```

---

# Benefits

```text
✔ Smaller production image
✔ Better security
✔ Faster deployment
✔ No unnecessary build tools
```

---

# ⚡ Build Optimization Techniques

---

# 1️⃣ Use Small Base Images

✅ Good

```dockerfile
FROM alpine
```

---

# 2️⃣ Combine RUN Commands

✅ Good

```dockerfile
RUN apt-get update && apt-get install -y curl
```

---

# 3️⃣ Use .dockerignore

Avoid copying:
- logs
- secrets
- node_modules

---

# 4️⃣ Cache Dependencies Properly

Copy dependency files first.

---

# 5️⃣ Use Multi-Stage Builds

Reduces production image size.

---

# ⚠️ Common Build Errors

---

# Error 1: Dockerfile Not Found

```text
unable to prepare context
```

---

# Solution

Ensure:
- Dockerfile exists
- correct directory used

---

# Error 2: COPY Failed

```text
COPY failed: file not found
```

---

# Solution

Check:
- file exists
- correct path

---

# Error 3: Permission Denied

---

# Solution

Use:
- proper file permissions
- sudo if needed

---

# Error 4: Large Build Context

---

# Solution

Use:
- .dockerignore

---

# 🌍 Complete Example

---

# Project Structure

```text
node-app/
 ├── Dockerfile
 ├── package.json
 ├── server.js
 └── .dockerignore
```

---

# Dockerfile

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 3000

CMD ["node", "server.js"]
```

---

# .dockerignore

```text
node_modules
.git
.env
```

---

# Build Image

```bash
docker build -t node-app:v1 .
```

---

# Verify Image

```bash
docker images
```

---

# Run Container

```bash
docker run -d -p 3000:3000 node-app:v1
```

---

# 📌 Quick Revision Notes

| Concept | Meaning |
|---|---|
| docker build | Create image |
| Build Context | Files sent to daemon |
| Layer | Immutable snapshot |
| Cache | Reuse previous layers |
| .dockerignore | Exclude unnecessary files |
| Multi-stage Build | Smaller production images |

---

# 🧠 Important Keywords

- docker build
- Build Context
- Dockerfile
- Layer Caching
- Multi-stage Build
- .dockerignore
- Image Tagging
- Docker Daemon
- Build Logs

---

# ❓ Viva Questions

1. What is docker build?
2. What is build context?
3. Why use .dockerignore?
4. What creates image layers?
5. What is layer caching?
6. Why is Docker build fast?
7. What is multi-stage build?
8. How to tag images during build?
9. Why use small base images?
10. What happens during build process?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| What is build context? | Files sent during build |
| Why use .dockerignore? | Reduce build size |
| What is layer caching? | Reuse unchanged layers |
| Why are multi-stage builds useful? | Smaller production images |
| What does docker build -t do? | Build and tag image |

---

# ✅ Conclusion

Docker build process automates:
- image creation
- layer generation
- application packaging

Using:
- layer caching
- multi-stage builds
- .dockerignore
- optimized Dockerfiles

developers can create:
- efficient
- scalable
- production-ready container images

These concepts are essential for:
- DevOps pipelines
- CI/CD workflows
- containerized applications