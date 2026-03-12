1️⃣ Virtualization
Definition

Virtualization is a technology that allows multiple virtual machines (VMs) to run on a single physical computer.

Each VM behaves like a separate computer with its own:

OS

CPU

RAM

Storage

Applications

How Virtualization Works

There is a layer called Hypervisor between hardware and virtual machines.

Hardware
   ↓
Hypervisor
   ↓
VM1 (OS + Apps)
VM2 (OS + Apps)
VM3 (OS + Apps)
Hypervisor

A Hypervisor is software that manages virtual machines.

Types of Hypervisors
Type 1 (Bare Metal)

Runs directly on hardware.

Examples:

VMware ESXi

Microsoft Hyper-V

Xen

Architecture:

Hardware
   ↓
Hypervisor
   ↓
VMs
Type 2 (Hosted Hypervisor)

Runs on top of an existing OS.

Examples:

Oracle VM VirtualBox

VMware Workstation

Architecture:

Hardware
   ↓
Host OS
   ↓
Hypervisor
   ↓
VMs
Advantages of Virtualization

Better hardware utilization

Isolation between systems

Run multiple OS

Easy testing environments

Cost reduction

Disadvantages

High resource usage

Each VM needs full OS

Slow boot time

2️⃣ Containerization
Definition

Containerization is a lightweight virtualization method where applications run inside containers instead of full virtual machines.

Containers share the same OS kernel.

Container Architecture
Hardware
   ↓
Host OS
   ↓
Container Engine
   ↓
Containers
(App + Dependencies)

Popular container engine:

Docker

Container Characteristics

Containers include:

Application

Libraries

Dependencies

Runtime

But not full OS.

Advantages

Lightweight

Faster startup

Portable

Efficient resource usage

Easy deployment

Example

If we deploy:

Node.js app

Python app

Java app

Each runs inside its own container but shares the same kernel.

3️⃣ Virtualization vs Containerization
Feature	Virtualization	Containerization
OS	Each VM has full OS	Shared OS
Size	Large	Small
Boot time	Minutes	Seconds
Resource usage	High	Low
Isolation	Strong	Medium
4️⃣ Namespaces (Linux)
Definition

A Namespace is a Linux feature that provides isolation for processes.

Namespaces make containers think they are running on a separate system.

What Namespaces Isolate

They isolate:

Processes

Network

Filesystem

Users

Hostname

IPC

Types of Namespaces
Namespace	Function
PID Namespace	Isolates process IDs
Network Namespace	Separate network stack
Mount Namespace	Separate filesystem
User Namespace	Separate users
IPC Namespace	Interprocess communication
UTS Namespace	Hostname isolation
Example

In a container:

Container A → PID 1
Container B → PID 1

Both can have PID 1 because namespaces isolate them.

5️⃣ Container Runtime
Definition

A Container Runtime is software responsible for running containers.

It manages:

Container creation

Container lifecycle

Image pulling

Resource management

Example Container Runtimes

containerd

CRI-O

Docker

Runtime Architecture
Container Engine
     ↓
Container Runtime
     ↓
Containers

Example with Docker:

Docker CLI
   ↓
Docker Daemon
   ↓
containerd
   ↓
runc
   ↓
Containers
6️⃣ What is runc

Low-level runtime

Actually creates containers

Uses Linux namespaces + cgroups

Example runtime:

runc