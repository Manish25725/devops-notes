
# Docker Compose — Building Blocks

![Docker](https://img.shields.io/badge/Docker-Compose-blue)
![YAML](https://img.shields.io/badge/Configuration-YAML-green)
![DevOps](https://img.shields.io/badge/DevOps-Automation-orange)
![Microservices](https://img.shields.io/badge/Microservices-MultiContainer-red)
![Containers](https://img.shields.io/badge/Containers-Orchestration-purple)

---

# 📚 Table of Contents

- [Overview](#-overview)
- [Basic Structure of docker-compose.yml](#-basic-structure-of-docker-composeyml)
- [YAML Basics](#-yaml-basics)
- [Version](#-version)
- [Services](#-services)
- [image vs build](#-image-vs-build)
- [Ports](#-ports)
- [Volumes](#-volumes)
- [Networks](#-networks)
- [depends_on](#-depends_on)
- [Environment Variables](#-environment-variables)
- [Restart Policies](#-restart-policies)
- [Health Checks](#-health-checks)
- [Additional Important Attributes](#-additional-important-attributes)
- [Complete Docker Compose Example](#-complete-docker-compose-example)
- [Best Practices](#-best-practices)
- [Quick Revision Notes](#-quick-revision-notes)
- [Viva Questions](#-viva-questions)
- [Interview Questions](#-interview-questions)
- [Conclusion](#-conclusion)

---

# 📖 Overview

Docker Compose uses a YAML configuration file called:

```text
docker-compose.yml
```

This file defines:
- Services
- Networks
- Volumes
- Environment Variables
- Dependencies

used in multi-container applications.

---

# 🏗️ Basic Structure of docker-compose.yml

```yaml
version: "3.9"

services:

  web:
    image: nginx

volumes:

  myvolume:

networks:

  mynetwork:
```

---

# 📌 YAML Basics

YAML is:
- Human-readable
- Indentation-sensitive

---

# Important Rule

✅ Use spaces  
❌ Do not use tabs

---

# Correct Indentation

```yaml
services:
  web:
    image: nginx
```

---

# Wrong Indentation

```yaml
services:
web:
image: nginx
```

---

# 🧩 Main Components of Docker Compose

```text
docker-compose.yml
        ↓
--------------------------------
| version                     |
| services                    |
| volumes                     |
| networks                    |
--------------------------------
```

---

# 🔢 Version

Defines Compose file version.

---

# Example

```yaml
version: "3.9"
```

---

# Popular Versions

| Version | Features |
|---|---|
| 3.0 | Basic support |
| 3.5 | Improved networking |
| 3.8 | Modern features |
| 3.9 | Latest stable |

---

# Recommendation

```text
Use Version 3.8 or 3.9
```

---

# ⚙️ Services

Services define containers.

---

# Example

```yaml
services:

  web:
    image: nginx

  database:
    image: postgres
```

---

# Service Concept

```text
Service = Blueprint
Container = Running Instance
```

---

# Example

```text
Service:
    web
        ↓
Creates Container:
    web_1
```

---

# 🆚 image vs build

---

# 🔹 image

Uses existing Docker images.

---

# Example

```yaml
image: nginx:latest
```

---

# Used For

| Example | Purpose |
|---|---|
| nginx | Web server |
| mysql | Database |
| redis | Cache |
| ubuntu | Base OS |

---

# 🔹 build

Builds custom image using Dockerfile.

---

# Example

```yaml
build: .
```

---

# Advanced Example

```yaml
build:
  context: ./app
  dockerfile: Dockerfile
```

---

# When to Use build

```text
✔ Custom application
✔ Own source code
✔ Custom dependencies
```

---

# image vs build Comparison

| Feature | image | build |
|---|---|---|
| Uses Existing Image | ✔ | ✘ |
| Uses Dockerfile | ✘ | ✔ |
| Faster Startup | ✔ | ✘ |
| Customization | Limited | Full |
| Best For | Official Images | Custom Apps |

---

# 🔌 Ports

Ports expose container services to the host machine.

---

# Syntax

```yaml
ports:
  - "HOST:CONTAINER"
```

---

# Example

```yaml
ports:
  - "8080:80"
```

---

# Explanation

```text
Host Port 8080
        ↓
Container Port 80
```

---

# Real Example

```text
Browser → localhost:8080
        ↓
Nginx Container Port 80
```

---

# Multiple Ports

```yaml
ports:
  - "8080:80"
  - "8443:443"
```

---

# 📦 Volumes

Volumes store persistent data.

---

# Problem Without Volumes

```text
Container deleted
        ↓
Data lost
```

---

# Solution

```yaml
volumes:
  - db-data:/var/lib/mysql
```

---

# Volume Types

| Type | Purpose |
|---|---|
| Named Volume | Persistent storage |
| Bind Mount | Share local files |
| Read-Only Volume | Configuration files |

---

# 🔹 Named Volume Example

```yaml
volumes:
  - db-data:/var/lib/mysql
```

---

# 🔹 Bind Mount Example

```yaml
volumes:
  - ./src:/app/src
```

---

# Benefits of Volumes

```text
✔ Data persistence
✔ Backup support
✔ Development convenience
✔ File sharing
```

---

# 🌐 Networks

Networks enable communication between services.

---

# Automatic Networking

Docker Compose automatically creates a network.

---

# Example

```yaml
services:

  backend:
    image: node

  database:
    image: postgres
```

---

# Result

```text
backend → database
```

Containers communicate using service names.

---

# Custom Networks

```yaml
networks:
  frontend:
  backend:
```

---

# Service Network Example

```yaml
services:

  web:
    networks:
      - frontend

  api:
    networks:
      - frontend
      - backend
```

---

# Benefits

| Benefit | Description |
|---|---|
| Isolation | Separate environments |
| Security | Restricted communication |
| Organization | Better architecture |

---

# 🔄 depends_on

Controls service startup order.

---

# Example

```yaml
depends_on:
  - database
```

---

# Workflow

```text
Database starts first
        ↓
Backend starts after database
```

---

# Important Note

```text
depends_on ensures startup order
NOT service readiness
```

---

# ❤️ Health Checks

Health checks verify service availability.

---

# Example

```yaml
healthcheck:
  test: ["CMD", "pg_isready"]
  interval: 10s
  retries: 5
```

---

# Benefits

```text
✔ Better reliability
✔ Prevent startup failures
✔ Service monitoring
```

---

# 🌍 Environment Variables

Environment variables configure containers dynamically.

---

# Example

```yaml
environment:
  DB_HOST: postgres
  DB_USER: admin
  DB_PASSWORD: secret
```

---

# Using .env File

---

# .env File

```env
DB_HOST=postgres
DB_USER=admin
DB_PASSWORD=secret
```

---

# docker-compose.yml

```yaml
environment:
  DB_HOST: ${DB_HOST}
```

---

# Benefits

```text
✔ Cleaner configuration
✔ Better security
✔ Easy environment switching
```

---

# 🔁 Restart Policies

Control container restart behavior.

---

# Policies

| Policy | Description |
|---|---|
| no | Do not restart |
| always | Always restart |
| on-failure | Restart on errors |
| unless-stopped | Restart unless manually stopped |

---

# Example

```yaml
restart: always
```

---

# 🛠️ Additional Important Attributes

---

# container_name

```yaml
container_name: myapp
```

Custom container name.

---

# command

```yaml
command: npm start
```

Override default command.

---

# working_dir

```yaml
working_dir: /usr/src/app
```

Set working directory.

---

# mem_limit

```yaml
mem_limit: 512m
```

Limit memory usage.

---

# cpus

```yaml
cpus: 1.5
```

Limit CPU usage.

---

# user

```yaml
user: appuser
```

Run container as specific user.

---

# 🏛️ Complete Docker Compose Example

```yaml
version: "3.9"

services:

  web:
    image: nginx
    ports:
      - "8080:80"

    volumes:
      - ./html:/usr/share/nginx/html

    depends_on:
      - database

    restart: unless-stopped

    networks:
      - app-network

  database:
    image: postgres:15

    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: secret

    volumes:
      - db-data:/var/lib/postgresql/data

    networks:
      - app-network

volumes:
  db-data:

networks:
  app-network:
```

---

# 🔄 Docker Compose Workflow

```text
Write docker-compose.yml
            ↓
docker-compose up
            ↓
Services Created
            ↓
Networks Created
            ↓
Volumes Mounted
            ↓
Application Running
```

---

# 📊 Most Important Building Blocks

| Component | Purpose |
|---|---|
| version | Compose version |
| services | Define containers |
| image | Use existing image |
| build | Build custom image |
| ports | Port mapping |
| volumes | Persistent storage |
| networks | Communication |
| depends_on | Startup order |
| environment | Configuration |
| restart | Restart behavior |

---

# 🚀 Best Practices

---

# 1️⃣ Use Named Volumes

For databases and persistent storage.

---

# 2️⃣ Avoid Hardcoding Secrets

Use:
- .env files
- Docker secrets

---

# 3️⃣ Use Custom Networks

Improve security and isolation.

---

# 4️⃣ Keep Services Independent

Each service should perform one responsibility.

---

# 5️⃣ Use Health Checks

Improve reliability.

---

# 6️⃣ Use Specific Image Versions

## Good

```yaml
image: postgres:15
```

---

## Bad

```yaml
image: latest
```

---

# 📌 Quick Revision Notes

| Topic | Key Point |
|---|---|
| services | Define containers |
| image | Existing image |
| build | Build custom image |
| ports | Host-to-container mapping |
| volumes | Persistent storage |
| networks | Communication |
| depends_on | Startup order |
| environment | Configuration values |
| restart | Restart policy |

---

# 🧠 Important Keywords

- Docker Compose
- YAML
- Services
- Volumes
- Networks
- Environment Variables
- depends_on
- Healthcheck
- Restart Policy
- Port Mapping

---

# ❓ Viva Questions

1. What is docker-compose.yml?
2. What are services?
3. Difference between image and build?
4. What are volumes?
5. Why are networks used?
6. What is depends_on?
7. What are environment variables?
8. What is port mapping?
9. What are restart policies?
10. What is a health check?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| Purpose of services? | Define containers |
| Why use volumes? | Persistent storage |
| Difference between image and build? | Existing vs custom image |
| Why use networks? | Service communication |
| Why use .env files? | External configuration |

---

# 📌 Key Takeaway

Docker Compose building blocks help developers create:

```text
✔ Organized applications
✔ Multi-container systems
✔ Scalable environments
✔ Persistent storage
✔ Automated networking
```

These components form the foundation of:
- Microservices
- DevOps
- Cloud-native applications

---

# ✅ Conclusion

Docker Compose building blocks simplify application deployment by organizing:
- Containers
- Networking
- Storage
- Dependencies
- Configuration

Using these components developers can build:
- Full-stack applications
- Microservices systems
- Development environments
- Production-ready setups

Docker Compose makes multi-container management:
- Easier
- Faster
- More reliable

---

# 🔗 Next Topic

➡️ Docker Compose Commands