# Image Tagging & Inspection

![Docker](https://img.shields.io/badge/Docker-Images-blue)
![DevOps](https://img.shields.io/badge/DevOps-Versioning-green)
![Containers](https://img.shields.io/badge/Containers-Inspection-orange)
![Registry](https://img.shields.io/badge/Registry-DockerHub-red)

---

# 📚 Table of Contents

- Introduction
- What is Image Tagging?
- Image Naming Convention
- Tags and Versions
- latest Tag
- Docker Tag Command
- Image Versioning
- Semantic Versioning
- Image Inspection
- docker inspect
- docker history
- docker images
- Layer Inspection
- Image Metadata
- Practical Examples
- Best Practices
- Summary

---

# 📖 Introduction

Docker images require:
- proper naming
- tagging
- versioning

for:
- deployment
- updates
- rollback
- CI/CD pipelines

Docker also provides commands to:
- inspect images
- view layers
- analyze metadata

---

# 🧠 What is Image Tagging?

> Image tagging is the process of assigning a name and version to Docker images.

---

# Purpose of Tags

```text
✔ Identify versions
✔ Manage releases
✔ Deploy correct image
✔ Rollback easily
✔ Track updates
```

---

# 🏷️ Docker Image Naming Convention

---

# Format

```text
repository/image:tag
```

---

# Example

```text
nginx:latest
mysql:8
node-app:v1
komal/myapp:v2
```

---

# Components

| Part | Meaning |
|---|---|
| repository | Registry/project |
| image | Image name |
| tag | Version |

---

# Example Breakdown

```text
komal/node-app:v1
```

| Component | Value |
|---|---|
| Repository | komal |
| Image | node-app |
| Tag | v1 |

---

# 🔖 What are Tags?

Tags represent:
- image versions

---

# Examples

```text
v1
v2
latest
dev
prod
staging
```

---

# Example Usage

```bash
docker pull nginx:latest

docker pull mysql:8

docker run node-app:v1
```

---

# 🌟 latest Tag

If no tag specified:

Docker automatically uses:
- `latest`

---

# Example

```bash
docker pull nginx
```

same as:

```bash
docker pull nginx:latest
```

---

# ⚠️ Important Note

`latest` does NOT mean:
- newest image always

It only means:
- default tag

---

# 🏗️ Docker Tag Command

Used to:
- create new tags
- rename images
- prepare for registry push

---

# Syntax

```bash
docker tag SOURCE_IMAGE TARGET_IMAGE
```

---

# Example

```bash
docker tag myapp:v1 komal/myapp:v1
```

---

# Verify

```bash
docker images
```

---

# 🏷️ Multiple Tags for Same Image

One image can have:
- multiple tags

---

# Example

```bash
docker tag myapp:v1 myapp:latest

docker tag myapp:v1 myapp:production
```

---

# Result

Same image ID:
- different tags

---

# 📦 Image Versioning

Versioning helps manage:
- releases
- updates
- rollback

---

# Example

| Version | Purpose |
|---|---|
| v1 | Initial release |
| v2 | Updated version |
| v3 | Bug fixes |
| latest | Current default |

---

# 🚀 Semantic Versioning

Professional projects use:

```text
MAJOR.MINOR.PATCH
```

---

# Example

```text
1.0.0
1.1.0
1.1.1
2.0.0
```

---

# Meaning

| Part | Description |
|---|---|
| MAJOR | Breaking changes |
| MINOR | New features |
| PATCH | Bug fixes |

---

# Example

```text
v1.2.3
```

- v1 → major
- 2 → minor
- 3 → patch

---

# 🔍 docker images Command

Used to list local images.

---

# Syntax

```bash
docker images
```

---

# Output Example

```text
REPOSITORY   TAG      IMAGE ID
nginx        latest   abc123
mysql        8        xyz789
```

---

# Useful Flags

## Show All Images

```bash
docker images -a
```

---

# Filter Images

```bash
docker images nginx
```

---

# 🧠 docker inspect Command

Used to view:
- detailed image metadata

---

# Syntax

```bash
docker inspect image_name
```

---

# Example

```bash
docker inspect nginx
```

---

# Shows

```text
✔ Environment variables
✔ Volumes
✔ Layers
✔ Entrypoint
✔ CMD
✔ Architecture
✔ OS
✔ Networking
```

---

# Example Output Fields

```json
{
  "Architecture": "amd64",
  "Os": "linux",
  "Env": ["PATH=/usr/local/bin"],
  "Cmd": ["nginx", "-g", "daemon off;"]
}
```

---

# 📜 docker history Command

Used to view:
- image layers
- commands used during build

---

# Syntax

```bash
docker history image_name
```

---

# Example

```bash
docker history nginx
```

---

# Output Shows

```text
✔ Layer sizes
✔ Dockerfile commands
✔ Layer creation time
✔ Layer IDs
```

---

# Example Output

```text
IMAGE          CREATED       SIZE
abc123         2 days ago    50MB
xyz789         3 days ago    20MB
```

---

# 🌟 Why docker history is Useful

```text
✔ Analyze image size
✔ Debug builds
✔ Understand layers
✔ Optimize Dockerfiles
```

---

# 🔬 Layer Inspection

Docker stores images as:
- layered filesystem

---

# View Layers

```bash
docker history nginx
```

---

# Inspect Storage Driver

```bash
docker info
```

---

# Common Drivers

| Driver | Purpose |
|---|---|
| overlay2 | Linux layered storage |
| aufs | Older Linux driver |
| windowsfilter | Windows containers |

---

# 📊 Practical Example

---

# Step 1: Build Image

```bash
docker build -t node-app:v1 .
```

---

# Step 2: Create Additional Tag

```bash
docker tag node-app:v1 node-app:latest
```

---

# Step 3: View Images

```bash
docker images
```

---

# Step 4: Inspect Image

```bash
docker inspect node-app:v1
```

---

# Step 5: View History

```bash
docker history node-app:v1
```

---

# 🗂️ Image Metadata

Metadata includes:

| Metadata | Description |
|---|---|
| Image ID | Unique image identifier |
| Tag | Version |
| Size | Image size |
| Architecture | amd64/arm |
| OS | Linux/Windows |
| CMD | Default startup command |
| ENV | Environment variables |

---

# ⚡ Best Practices

---

# Use Specific Versions

✅ Good

```text
myapp:v1.0.0
```

❌ Bad

```text
myapp:latest
```

---

# Use Semantic Versioning

```text
1.0.0
1.1.0
2.0.0
```

---

# Keep Images Small

Use:
- alpine images
- multi-stage builds

---

# Regularly Remove Old Images

```bash
docker image prune
```

---

# Document Tags Properly

Maintain:
- release history
- deployment mapping

---

# 📌 Quick Revision Notes

| Command | Purpose |
|---|---|
| docker images | List images |
| docker inspect | Detailed metadata |
| docker history | View layers |
| docker tag | Create tags |
| docker image prune | Cleanup images |

---

# 🧠 Important Keywords

- Image Tagging
- Versioning
- Semantic Versioning
- latest Tag
- docker inspect
- docker history
- Image Layers
- Metadata
- Registry

---

# ❓ Viva Questions

1. What is image tagging?
2. Why are tags important?
3. What is semantic versioning?
4. What does latest mean?
5. What is docker inspect?
6. What is docker history?
7. How to create image tags?
8. Why inspect images?
9. Difference between image ID and tag?
10. Why use versioning?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| What is docker tag? | Creates additional image tag |
| What does docker inspect do? | Shows detailed metadata |
| Why use semantic versioning? | Better release management |
| What does docker history show? | Image layers |
| Why avoid latest tag in production? | Unpredictable deployments |

---

# ✅ Conclusion

Image tagging and inspection are essential for:
- image management
- deployment pipelines
- version control
- debugging
- optimization

Using commands like:
- docker tag
- docker inspect
- docker history

developers can:
- manage versions
- inspect layers
- optimize images
- maintain reliable deployments

These concepts are critical in:
- Docker
- CI/CD
- DevOps workflows
- container orchestration