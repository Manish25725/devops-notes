# Dockerfile Instructions

![Docker](https://img.shields.io/badge/Docker-Dockerfile-blue)
![DevOps](https://img.shields.io/badge/DevOps-Containers-green)
![Images](https://img.shields.io/badge/Images-Building-orange)

---

# 📚 Table of Contents

- Introduction
- Structure of Dockerfile
- FROM
- RUN
- COPY
- ADD
- WORKDIR
- ENV
- EXPOSE
- VOLUME
- CMD
- ENTRYPOINT
- USER
- LABEL
- Dockerfile Execution Flow
- CMD vs ENTRYPOINT
- Best Practices
- Complete Example
- Summary

---

# 📖 Introduction

Dockerfile instructions are commands used to create Docker images.

Each instruction:
- performs a specific task
- creates a new image layer
- builds the final container image

---

# 🏗️ Basic Dockerfile Structure

```dockerfile
FROM ubuntu:22.04

RUN apt-get update

WORKDIR /app

COPY . .

ENV APP_ENV=production

EXPOSE 3000

CMD ["python", "app.py"]
```

---

# 🔹 FROM Instruction

## Purpose

Defines the base image.

---

# Syntax

```dockerfile
FROM image:tag
```

---

# Example

```dockerfile
FROM ubuntu:22.04
```

---

# Notes

```text
✔ First instruction in Dockerfile
✔ Mandatory instruction
✔ Base layer of image
```

---

# 🔹 RUN Instruction

## Purpose

Executes commands during image build process.

---

# Syntax

```dockerfile
RUN command
```

---

# Example

```dockerfile
RUN apt-get update
RUN apt-get install -y nginx
```

---

# Combined Example

```dockerfile
RUN apt-get update && apt-get install -y curl nginx
```

---

# Why Combine RUN Commands?

```text
✔ Fewer image layers
✔ Smaller image size
✔ Faster builds
```

---

# 🔹 COPY Instruction

## Purpose

Copies files from host → image.

---

# Syntax

```dockerfile
COPY source destination
```

---

# Example

```dockerfile
COPY app.py /app/
```

---

# Copy Entire Directory

```dockerfile
COPY . /app
```

---

# 🔹 ADD Instruction

## Purpose

Similar to COPY but with extra features.

---

# Features

```text
✔ Can extract tar files
✔ Can download URLs
✔ Copies files
```

---

# Example

```dockerfile
ADD app.tar.gz /app/
```

---

# COPY vs ADD

| COPY | ADD |
|---|---|
| Simple copy | Extra functionality |
| Preferred | Use only when needed |
| More predictable | More complex |

---

# 🔹 WORKDIR Instruction

## Purpose

Sets default working directory.

---

# Syntax

```dockerfile
WORKDIR /path
```

---

# Example

```dockerfile
WORKDIR /app
```

---

# Benefit

All following commands execute inside `/app`.

---

# Example

```dockerfile
WORKDIR /app

COPY . .

RUN npm install
```

---

# 🔹 ENV Instruction

## Purpose

Sets environment variables.

---

# Syntax

```dockerfile
ENV KEY=value
```

---

# Example

```dockerfile
ENV NODE_ENV=production
ENV PORT=3000
```

---

# Benefits

```text
✔ Dynamic configuration
✔ Runtime flexibility
✔ Environment separation
```

---

# 🔹 EXPOSE Instruction

## Purpose

Documents application port.

---

# Syntax

```dockerfile
EXPOSE port
```

---

# Example

```dockerfile
EXPOSE 3000
```

---

# Important Note

```text
EXPOSE does NOT publish ports.
Use docker run -p for port mapping.
```

---

# 🔹 VOLUME Instruction

## Purpose

Creates mount point for persistent storage.

---

# Syntax

```dockerfile
VOLUME ["/path"]
```

---

# Example

```dockerfile
VOLUME ["/data"]
```

---

# Benefits

```text
✔ Persistent storage
✔ Data survives container deletion
✔ Share data between containers
```

---

# 🔹 CMD Instruction

## Purpose

Defines default command when container starts.

---

# Syntax

```dockerfile
CMD ["executable","param"]
```

---

# Example

```dockerfile
CMD ["python", "app.py"]
```

---

# Important

CMD can be overridden during `docker run`.

---

# Example

```bash
docker run myimage python test.py
```

Overrides default CMD.

---

# 🔹 ENTRYPOINT Instruction

## Purpose

Defines fixed executable for container.

---

# Syntax

```dockerfile
ENTRYPOINT ["executable"]
```

---

# Example

```dockerfile
ENTRYPOINT ["python"]
CMD ["app.py"]
```

---

# Result

Container always starts with:

```bash
python app.py
```

---

# 🔥 CMD vs ENTRYPOINT

| CMD | ENTRYPOINT |
|---|---|
| Default command | Fixed executable |
| Easily overridden | Harder to override |
| Flexible | Strict behavior |

---

# Example

```dockerfile
ENTRYPOINT ["ping"]
CMD ["google.com"]
```

Run:

```bash
docker run image
```

Result:

```bash
ping google.com
```

Override:

```bash
docker run image localhost
```

Result:

```bash
ping localhost
```

---

# 🔹 USER Instruction

## Purpose

Runs container as non-root user.

---

# Example

```dockerfile
RUN useradd appuser

USER appuser
```

---

# Benefits

```text
✔ Better security
✔ Reduced privileges
✔ Production best practice
```

---

# 🔹 LABEL Instruction

## Purpose

Adds metadata to image.

---

# Example

```dockerfile
LABEL maintainer="komal@example.com"
LABEL version="1.0"
```

---

# Dockerfile Execution Flow

```text
FROM
  ↓
RUN
  ↓
COPY
  ↓
WORKDIR
  ↓
ENV
  ↓
EXPOSE
  ↓
CMD / ENTRYPOINT
```

---

# 🚀 Complete Dockerfile Example

## Node.js Application

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

ENV NODE_ENV=production

EXPOSE 3000

CMD ["node", "app.js"]
```

---

# Build Image

```bash
docker build -t node-app:v1 .
```

---

# Run Container

```bash
docker run -d -p 3000:3000 node-app:v1
```

---

# 🌟 Best Practices

## Use Small Images

```dockerfile
FROM alpine
```

---

## Combine RUN Commands

```dockerfile
RUN apt-get update && apt-get install -y curl
```

---

## Avoid Root User

```dockerfile
USER appuser
```

---

## Use Specific Versions

✅ Good

```dockerfile
FROM node:18-alpine
```

❌ Bad

```dockerfile
FROM node:latest
```

---

## Use .dockerignore

Avoid copying:
- node_modules
- logs
- secrets

---

# 📌 Quick Revision Notes

| Instruction | Purpose |
|---|---|
| FROM | Base image |
| RUN | Execute commands |
| COPY | Copy files |
| ADD | Advanced copy |
| WORKDIR | Set working directory |
| ENV | Environment variables |
| EXPOSE | Document ports |
| VOLUME | Persistent storage |
| CMD | Default command |
| ENTRYPOINT | Fixed executable |
| USER | Non-root execution |

---

# ❓ Viva Questions

1. What is Dockerfile?
2. Purpose of FROM instruction?
3. Difference between COPY and ADD?
4. What does RUN do?
5. What is WORKDIR?
6. Difference between CMD and ENTRYPOINT?
7. Why use ENV?
8. Purpose of EXPOSE?
9. Why use USER instruction?
10. What creates Docker layers?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| What is FROM? | Base image instruction |
| Difference between CMD and ENTRYPOINT? | CMD is default command, ENTRYPOINT is fixed executable |
| Why combine RUN commands? | Reduce image layers |
| Why avoid root user? | Better security |
| What is EXPOSE? | Documents container port |

---

# ✅ Conclusion

Dockerfile instructions define:
- how images are built
- how applications run
- how containers behave

Understanding these instructions is essential for:
- Docker image creation
- container deployment
- DevOps automation
- production-ready applications