---
date: "2025-07-14"
draft: false
title: 'Virtual machine vs Container vs Sandbox'
author: 'King Jin'
tags: ['Virtual machine','Container','Sandbox']
showtoc: true
---
Recently, I tried Distrobox, a tool that enables us to run different operating systems within the host OS. I've noticed it's different from a virtual machine, as it uses containerization instead. Over the past year, I've heard a lot about containers (like Docker), sandboxes, and virtual machines, and I'd like to understand the distinctions between them.

## Virtualization
#### How virtualization work
Virtualization is the technology that allows a single physical machine, known as the **host**, to run multiple virtual machines or **guests**.

The key of virtualization is hypervisor. It's the software that create and manages the virtual machines.
- Type 1 (Bare-Metal): This hypervisor is installed directly onto the host's hardware, acting as the operating system itself. Examples include VMware vSphere, Hyper-V. This type is common in data centers due to its high performance and efficiency
- Type 2 (Hosted): This hypervisor runs as an application on top of a conventional operating system(Like Windows, Linux). Examples include VMware Workstaion and Oracle VirtualBox. This approach is often used for desktop virtualization and development purposes.

Once the hypervisor is in place, you can create one or more VMs. This involves 
- Allocating resources(CPU cores, RAM, storage)
- Configuring virtual hardware(virtual network adapter, virtual storage controllers, virtual BIOS)
- Installing a guest OS, the guest os is unaware that it's running in a virtualized environment.
![virtualization mechanism graph](/Hand_write_note/virtualization.png)
#### How WSL work:
- WSL 1: It did not run a real Linux kernel. Instead, it functioned as a real-time translation layer. It tricked Linux binaries into thinking they were communicating with a Linux kernel, when in reality, they were talking to a clever interpreter connected to the Windows kernel.
- WSL 2: Due to the limitations of translating every single Linux syscall, WSL 2 uses a lightweight, highly optimized type 1 virtual machine.


#### Use case
1. Server consolidation and optimization
2. Development and testing envionments
3. Application isolation and legacy application support

#### Pros and Cons
Pros:
1. Strong isolation
2. Total compatibility

Cons:
1. Heavyweight and slow
2. Inefficient

## Containerization
Containerization works by virtualizing the operating system, allowing an application to run in an isolated user space with all its dependencies, code and libraries. It all runs on a single host operating system and shared host OS's kernel, making containers incredibly lightweight and fast.

#### How containers work
Containers work by creating isolated environments for applications using two key technologies built into the host OS's kernel:
1. Namespaces: This feature provides isolation. Each container gets its own isolated view of resources like the network stack, process IDs, and filesystem mounts. This prevents conbtainers from seeing or interacting with each other or the host system.
2. Control Groups(cgroups): This feature manages resource allocation. It limits and monitors how much of the host's physical resources, such as CPU, RAM, I/O, each container can consume. This ensures no single container can monopolize the host's resources.

#### How container engine work
- Rule: A tool to create, run and manage container. It's the translator/project manager between user and host's OS kernel.
- Workflow:
  - Creating a Dockerfile: A developer creates a text file defining all the steps required to build the application environment.
  - Building an Image: The container engine reads the Dockerfile and packages it into a single, read-only, standardized image. This image serves as a static template for the container.
  - Running a Container: The container engine uses this image to launch one or more container instances. During runtime, it creates an isolated namespace cgroups, while also adding a writable layer on top of the image to make the applications runnable.

![container_graph](/Hand_write_note/containerization.png)
#### Docker vs Kubernetes vs Podman
These are container enginers, but they serve very different purposes.
- Docker: The industry standard, it provides an all-in-one platform that includes a daemon, a client and an image registry(Docker hub). It's easy to get started with and has a mature ecosystem
- Podman: A more security, daemonless alternative. Its command line is highly compatible with Docker's, its run as a non-root user by default, and its architecture is more streamlined.
- Kubernetes: When applications scale up and need to run across hundreds or thousands of containers and multiple servers, Kubernetes is needed. It is a container orchestrator and servers as the brain of a container cluster. Kubernetes is not responsible for the actual running of containers. Instead, it handles higher-level management tasks such as automated deployment, elastic scaling, service discovery, load balancing and self healing.

#### How distrobox works
Distrobox is a clever tool that uses a container negine like Podman to create tightly integrated development environments. Its main purpose is to let you run any Linux distribution inside a container on your host OS but make it feel completely native.

#### Use case
1. Breaking down large, monolithic applications into smaller, independently deployable services
2. Creating consistent and reproducible environments for building, testing and deploying software.

#### Pros and Cons
Pros
1. Lightweight and fast
2. Highly portable

Cons
1. Weaker isolation
2. You can only run containers that are compatible with the host OS kernel.
  
## Sandbox
A sandbox is a secure, isolated environment on a computer where you can run untrusted program without risking harm to your host system.
#### How to create a sandbox
1. Container
2. Virtual machine
3. Using dedicated sandbox software(like Sandboxie-Plus)

#### Use case
1. To be listed on the App Store or Google play store, and application must run in a sandbox. That's why when we open a new app, the user have t approve a list of resources that enable the app to access.
2. Education
3. Browser plugin

#### Pros and Cons
Pros
1. Extremely lightweight  and fast: A sandbox applies rules to an already running process, adding minimal overhead. It's instantaneous
2. Targeted security: It's perfect for its narrow purpose: running a single untrusted application and preventing it from accessing your personal files, network or hardware.

Cons
1. Weakest Isolation: It shares the host OS and kernel.
2. Limited scape: It's purely a security feature, not a deployment or development tool.