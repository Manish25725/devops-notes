
# Practical Examples with Docker Compose

![Docker](https://img.shields.io/badge/Docker-Compose-blue)
![Microservices](https://img.shields.io/badge/Architecture-Microservices-green)
![DevOps](https://img.shields.io/badge/DevOps-Deployment-orange)
![Containers](https://img.shields.io/badge/Containers-MultiService-red)
![Cloud](https://img.shields.io/badge/Cloud-Native-purple)

---

# 📚 Table of Contents

- [Overview](#-overview)
- [Why Practical Examples Matter](#-why-practical-examples-matter)
- [Example 1: Node.js + MongoDB](#-example-1-nodejs--mongodb)
- [Example 2: WordPress + MySQL](#-example-2-wordpress--mysql)
- [Example 3: React + Spring Boot + PostgreSQL](#-example-3-react--spring-boot--postgresql)
- [Architecture Diagrams](#-architecture-diagrams)
- [Communication Workflow](#-communication-workflow)
- [Common Docker Compose Patterns](#-common-docker-compose-patterns)
- [Best Practices](#-best-practices)
- [Advantages of Multi-Container Applications](#-advantages-of-multi-container-applications)
- [Quick Revision Notes](#-quick-revision-notes)
- [Viva Questions](#-viva-questions)
- [Interview Questions](#-interview-questions)
- [Conclusion](#-conclusion)

---

# 📖 Overview

Docker Compose is widely used for building and managing:
- Full-stack applications
- Multi-container systems
- Microservices architectures
- Development environments

In this topic, we will build real-world applications using:
- Node.js
- MongoDB
- WordPress
- MySQL
- React
- Spring Boot
- PostgreSQL

---

# 🎯 Why Practical Examples Matter

Practical deployments help developers understand:

```text
✔ Service communication
✔ Networking
✔ Volumes
✔ Environment variables
✔ Health checks
✔ Dependency management
✔ Persistent storage
✔ Multi-container orchestration
```

---

# 🟢 Example 1: Node.js + MongoDB

---

# 📌 Scenario

Create a backend application using:
- Node.js
- Express.js
- MongoDB

---

# 🎯 Requirements

```text
✔ Node.js server on port 3000
✔ MongoDB database
✔ Persistent database storage
✔ Automatic networking
✔ Service dependency management
✔ Development workflow support
```

---

# 🏗️ Project Structure

```text
project/
│
├── docker-compose.yml
├── Dockerfile
├── package.json
├── app.js
└── src/
```

---

# 📄 docker-compose.yml

```yaml
version: '3.8'

services:

  app:
    build: .
    container_name: node-app

    ports:
      - "3000:3000"

    environment:
      - MONGO_URL=mongodb://mongo:27017/mydb

    depends_on:
      - mongo

    volumes:
      - .:/usr/src/app

    restart: unless-stopped

  mongo:
    image: mongo:6

    ports:
      - "27017:27017"

    volumes:
      - mongo-data:/data/db

    restart: unless-stopped

volumes:
  mongo-data:
```

---

# 📄 Dockerfile

```dockerfile
FROM node:18-alpine

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

---

# 📄 package.json

```json
{
  "name": "node-app",
  "version": "1.0.0",
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "express": "^4.18.2",
    "mongoose": "^7.0.0"
  }
}
```

---

# 📄 app.js

```javascript
const express = require('express');
const mongoose = require('mongoose');

const app = express();

mongoose.connect(process.env.MONGO_URL)
.then(() => console.log("MongoDB Connected"))
.catch(err => console.log(err));

app.get('/', (req, res) => {
    res.send('Hello from Node.js');
});

app.listen(3000, () => {
    console.log('Server running on port 3000');
});
```

---

# ▶️ Running the Application

```bash
docker compose up -d
```

---

# 📊 Workflow

```text
User Request
      ↓
Node.js Application
      ↓
MongoDB Database
      ↓
Response Returned
```

---

# 🌟 Features Demonstrated

| Feature | Usage |
|---|---|
| build | Custom image |
| image | MongoDB image |
| volumes | Persistent data |
| depends_on | Startup order |
| environment | MongoDB connection |
| ports | Port exposure |

---

# 🟠 Example 2: WordPress + MySQL

---

# 📌 Scenario

Deploy a complete blogging platform using:
- WordPress
- MySQL

---

# 🎯 Requirements

```text
✔ WordPress on port 8080
✔ MySQL database
✔ Persistent storage
✔ Environment variable configuration
✔ Automatic restart
```

---

# 🏗️ Architecture

```text
Browser
    ↓
WordPress Container
    ↓
MySQL Container
```

---

# 📄 docker-compose.yml

```yaml
version: '3.8'

services:

  wordpress:
    image: wordpress:6-apache

    ports:
      - "8080:80"

    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: secret
      WORDPRESS_DB_NAME: wordpress_db

    depends_on:
      - db

    volumes:
      - wordpress-data:/var/www/html

  db:
    image: mysql:5.7

    environment:
      MYSQL_DATABASE: wordpress_db
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: secret
      MYSQL_ROOT_PASSWORD: rootpass

    volumes:
      - db-data:/var/lib/mysql

volumes:
  wordpress-data:
  db-data:
```

---

# ▶️ Start Services

```bash
docker compose up -d
```

---

# 🌐 Access WordPress

```text
http://localhost:8080
```

---

# 🌟 Features Demonstrated

| Feature | Purpose |
|---|---|
| Named Volumes | Persistent database |
| Environment Variables | Database configuration |
| Multi-container | WordPress + MySQL |
| Automatic Networking | Service communication |
| Restart Policy | Better reliability |

---

# 🔵 Example 3: React + Spring Boot + PostgreSQL

---

# 📌 Scenario

Deploy a full-stack application with:
- React frontend
- Spring Boot backend
- PostgreSQL database

---

# 🎯 Requirements

```text
✔ Frontend on port 3000
✔ Backend on port 8080
✔ PostgreSQL database
✔ Service communication
✔ Database initialization
✔ Health checks
```

---

# 🏗️ Architecture Diagram

```text
┌─────────────────────┐
│     React UI        │
│     Port 3000       │
└─────────┬───────────┘
          │ API Calls
          ▼
┌─────────────────────┐
│   Spring Boot API   │
│     Port 8080       │
└─────────┬───────────┘
          │ JDBC
          ▼
┌─────────────────────┐
│   PostgreSQL DB     │
│     Port 5432       │
└─────────────────────┘
```

---

# 📄 docker-compose.yml

```yaml
version: '3.8'

services:

  frontend:
    build: ./frontend

    ports:
      - "3000:3000"

    depends_on:
      - backend

  backend:
    build: ./backend

    ports:
      - "8080:8080"

    environment:
      SPRING_DATASOURCE_URL: jdbc:postgresql://db:5432/appdb
      SPRING_DATASOURCE_USERNAME: postgres
      SPRING_DATASOURCE_PASSWORD: postgres

    depends_on:
      db:
        condition: service_healthy

  db:
    image: postgres:15

    environment:
      POSTGRES_DB: appdb
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres

    ports:
      - "5432:5432"

    volumes:
      - postgres-data:/var/lib/postgresql/data

    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]

volumes:
  postgres-data:
```

---

# 📄 Frontend Dockerfile

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY . .

RUN npm install

EXPOSE 3000

CMD ["npm", "start"]
```

---

# 📄 Backend Dockerfile

```dockerfile
FROM openjdk:17

WORKDIR /app

COPY target/app.jar app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]
```

---

# 📄 init.sql

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100)
);
```

---

# ▶️ Start Full Stack Application

```bash
docker compose up -d
```

---

# 🌐 Access Services

| Service | URL |
|---|---|
| React Frontend | http://localhost:3000 |
| Spring Boot API | http://localhost:8080 |
| PostgreSQL | localhost:5432 |

---

# 🔄 Communication Workflow

```text
User opens React UI
        ↓
React sends API request
        ↓
Spring Boot processes request
        ↓
PostgreSQL stores/retrieves data
        ↓
JSON response returned
        ↓
React updates UI
```

---

# 🌟 Features Demonstrated

| Feature | Purpose |
|---|---|
| Multi-stage architecture | Frontend + Backend + DB |
| Health checks | Reliability |
| depends_on | Service readiness |
| Persistent volumes | Database storage |
| Networks | Inter-service communication |

---

# 🌐 Architecture Diagrams

---

# Node.js + MongoDB

```text
Client
   ↓
Node.js Container
   ↓
MongoDB Container
```

---

# WordPress + MySQL

```text
Browser
   ↓
WordPress
   ↓
MySQL
```

---

# React + Spring Boot + PostgreSQL

```text
React UI
   ↓
Spring Boot API
   ↓
PostgreSQL
```

---

# 📦 Common Docker Compose Patterns

---

# 1️⃣ Database Initialization

```yaml
volumes:
  - ./init.sql:/docker-entrypoint-initdb.d/init.sql
```

---

# 2️⃣ Environment Variables

```yaml
environment:
  DB_HOST: database
```

---

# 3️⃣ Persistent Storage

```yaml
volumes:
  - db-data:/var/lib/postgresql/data
```

---

# 4️⃣ Health Checks

```yaml
healthcheck:
  test: ["CMD", "pg_isready"]
```

---

# 5️⃣ Service Dependencies

```yaml
depends_on:
  - database
```

---

# 🚀 Advantages of Multi-Container Applications

| Advantage | Benefit |
|---|---|
| Service Isolation | Better reliability |
| Scalability | Independent scaling |
| Flexibility | Different technologies |
| Easier Maintenance | Smaller services |
| Faster Deployment | Independent updates |

---

# 🛡️ Best Practices

---

# 1️⃣ Use Specific Image Versions

## Good

```yaml
image: postgres:15
```

---

# 2️⃣ Use Named Volumes

Prevent data loss.

---

# 3️⃣ Externalize Secrets

Use:
- .env files
- Docker secrets

---

# 4️⃣ Add Health Checks

Improve reliability.

---

# 5️⃣ Keep Containers Lightweight

One process per container.

---

# 6️⃣ Use Restart Policies

```yaml
restart: unless-stopped
```

---

# 📊 Practical Examples Comparison

| Example | Technologies | Purpose |
|---|---|---|
| Example 1 | Node.js + MongoDB | Backend API |
| Example 2 | WordPress + MySQL | CMS Platform |
| Example 3 | React + Spring Boot + PostgreSQL | Full-stack Application |

---

# 📌 Quick Revision Notes

| Topic | Key Point |
|---|---|
| Node.js Stack | API + MongoDB |
| WordPress Stack | CMS + MySQL |
| React Stack | Full-stack architecture |
| volumes | Persistent storage |
| depends_on | Startup dependency |
| healthcheck | Service monitoring |
| environment | Dynamic configuration |

---

# 🧠 Important Keywords

- Docker Compose
- Multi-container
- Persistent Volumes
- Health Checks
- Service Dependencies
- Environment Variables
- Full-stack Application
- Microservices
- PostgreSQL
- MongoDB

---

# ❓ Viva Questions

1. Why use Docker Compose for practical applications?
2. What is depends_on?
3. Why are volumes important?
4. What are health checks?
5. Difference between build and image?
6. Why use environment variables?
7. How do containers communicate?
8. Why use PostgreSQL in Docker?
9. What is persistent storage?
10. What are advantages of multi-container apps?

---

# 💼 Interview Questions

| Question | Answer |
|---|---|
| Why use Docker Compose? | Manage multi-container apps |
| Why use volumes? | Persistent storage |
| Purpose of health checks? | Verify service availability |
| Why use environment variables? | Dynamic configuration |
| Why separate frontend/backend/database? | Better scalability and maintenance |

---

# 📌 Key Takeaway

Practical Docker Compose deployments demonstrate:

```text
✔ Real-world application orchestration
✔ Multi-container management
✔ Networking
✔ Persistent storage
✔ Service communication
✔ Full-stack deployment
```

These examples form the foundation of:
- Cloud-native applications
- Microservices
- DevOps workflows
- Modern software deployment

---

# ✅ Conclusion

Docker Compose makes it easy to build and manage:
- Backend APIs
- CMS platforms
- Full-stack applications
- Multi-container systems

Using:
- Containers
- Volumes
- Networks
- Environment variables
- Health checks

developers can create scalable and reliable applications efficiently.

Docker Compose is an essential tool for:
- Developers
- DevOps Engineers
- Cloud Engineers
- System Administrators

---

# 🔗 Next Topic

➡️ Docker Compose Best Practices and Interview Preparation