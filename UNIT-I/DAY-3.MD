What are Namespaces?

A namespace is a Linux feature that isolates system resources for a group of processes.

👉 In simple words:

Namespaces make one process think it has its own separate system.

So inside a container:

it thinks it has its own processes

its own network

its own file system

its own users

But actually everything is running on the same Linux OS kernel.

Why Namespaces are Important in DevOps

Containers like Docker use namespaces to:

isolate applications

run multiple apps safely

prevent processes from interfering with each other

create lightweight containers

Example:

Server running:

App A container

App B container

App C container

Because of namespaces:

App A cannot see App B processes.

Example Without Namespace

Imagine your system running:

Process 1
Process 2
Process 3
Process 4

All processes can see each other using commands like:

ps aux
Example With Namespace (Containers)

Container 1:

Process A
Process B

Container 2:

Process X
Process Y

Inside Container 1, if you run:

ps aux

You only see:

Process A
Process B

You cannot see X and Y.

This happens because of PID namespace.

Types of Linux Namespaces

Linux provides 6 main namespaces.

1️⃣ PID Namespace

PID = Process ID

It isolates processes.

Example:

Inside container:

PID 1  -> Node server
PID 2  -> worker process

But on host machine:

PID 3421
PID 3422

Container thinks its process is PID 1.

2️⃣ Network Namespace

Each container gets its own network stack.

This includes:

IP address

routing table

network interfaces

ports

Example:

Container A

IP: 172.17.0.2

Container B

IP: 172.17.0.3

Both run:

Port 3000

No conflict.

3️⃣ Mount Namespace

Controls filesystem visibility.

Each container sees its own filesystem.

Example:

Container sees:

/app
/bin
/usr

But it cannot see host directories.

4️⃣ UTS Namespace

UTS = Unix Time Sharing

Controls:

hostname

domain name

Example:

Container 1 hostname:

backend-server

Container 2 hostname:

database-server
5️⃣ IPC Namespace

IPC = Inter Process Communication

Isolates:

message queues

shared memory

semaphores

So processes in one container cannot communicate with another container.

6️⃣ User Namespace

Controls user IDs and permissions.

Example:

Inside container:

root (UID 0)

But on host machine it maps to:

UID 1000

This improves security.

How Namespaces + Containers Work

Containers like:

Docker

Kubernetes

use:

Namespaces  → Isolation
Cgroups     → Resource control

Together they create containers.

Simple Real World Analogy

Imagine an apartment building.

Building = Server
Apartment = Container
Rooms = Processes

Each apartment has:

its own kitchen

its own bathroom

its own electricity

Even though everything is inside one building.

👉 That apartment isolation is like namespaces.

DevOps Interview Definition

If interviewer asks:

What are namespaces?

Answer: