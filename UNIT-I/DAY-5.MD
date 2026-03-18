🐳 Docker Desktop – Complete Notes
🔹 What is Docker Desktop?

Docker Desktop is a GUI-based application that allows you to build, run, and manage Docker containers on your local machine.

👉 It includes:

Docker Engine

Docker CLI

Docker Compose

Kubernetes (optional)

🔹 Why Docker Desktop?

Without Docker Desktop:

You need to manually install Docker Engine

Configure environment (Linux VM, networking, etc.)

With Docker Desktop:

Everything comes pre-configured

Easy to use via GUI + CLI

🔹 Key Features
1. 🖥️ User Interface (Dashboard)

View running containers

Start/Stop containers

Inspect logs

Manage images and volumes

2. ⚙️ Docker Engine

Core backend that runs containers

Uses:

Namespaces

cgroups (resource control)

3. 💻 Docker CLI

Used in terminal:

docker run nginx
docker ps
docker images
4. 📦 Docker Compose

Run multi-container apps using a YAML file

Example:

version: "3"
services:
  web:
    image: nginx
  db:
    image: mongo

Run:

docker-compose up
5. ☸️ Kubernetes (Optional)

Built-in support for Kubernetes cluster

Used for container orchestration

6. 🔄 Automatic Updates

Keeps Docker updated automatically

🔹 Architecture (Simple)
Docker Desktop
   │
   ├── Docker CLI (user commands)
   │
   ├── Docker Engine (core)
   │       ├── Containers
   │       ├── Images
   │       └── Volumes
   │
   └── OS (Windows/Mac uses Linux VM)

👉 On Windows/Mac:

Docker runs inside a Linux virtual machine

🔹 How Docker Desktop Works

You run a command:

docker run nginx

Docker Desktop:

Pulls image from Docker Hub

Creates container

Runs it inside Linux VM

🔹 Important Components
🔸 Image

Blueprint of container

Example: nginx, node

🔸 Container

Running instance of image

🔸 Volume

Persistent storage

🔸 Network

Communication between containers

🔹 Advantages

✔ Easy setup
✔ Beginner-friendly GUI
✔ Cross-platform (Windows/Mac)
✔ Integrated tools
✔ Faster development workflow

🔹 Disadvantages

❌ Uses more RAM (because of VM)
❌ Slower than native Linux Docker
❌ Limited control compared to manual setup

🔹 Common Commands (Must Know)
docker ps              # running containers
docker ps -a           # all containers
docker images          # list images
docker run nginx       # run container
docker stop <id>       # stop container
docker rm <id>         # delete container
docker rmi <id>        # delete image
🔹 Docker Desktop vs Docker Engine
Feature	Docker Desktop	Docker Engine
GUI	Yes	No
Setup	Easy	Manual
OS Support	Windows/Mac	Linux
Performance	Slightly slower	Faster