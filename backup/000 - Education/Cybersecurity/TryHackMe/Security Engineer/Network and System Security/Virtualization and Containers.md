
As computing has become more prevalent in daily life, the need for computing resources, and extensibility is larger than ever. With access to computing resources limited, technology has needed to adapt to allow those without direct access to resources to still access modern technology. 

Thus, cloud computing and virtualization have come to the forefront of technology as a solution for individuals, small and large businesses, and everything in between.

Apart from cloud computing, virtualization can also be used to partition and create virtual machines (VMs). This allows for atomic testing, development, research, and other uses that we will expand upon throughout this room.

### Learning Objectives

- Understand what virtualization is, how and why it is used.
- Learn common virtualization technologies, including hypervisors and containers.
- Use virtualization technologies practically and understand their applications to security and modern computing.

This room is designed to teach high-level concepts from the ground up and requires no prerequisites.

# What is Virtualization?

At its most basic level, virtualization is the concept of *encapsulating the capabilities and features of a physical machine in a virtual environment*, known as a **virtual machine**.

But why is virtualization needed? For most organizations and individuals, virtualization comes from a need of the following:

- **Decrease expenses**: Physical servers can be expensive, and virtualization can decrease the number of server or other hardware, or even completely remove physical hardware from a company's infrastructure.
- **Scale**: Without properly implemented DevOps, it may be hard for a company to scale resources as server usage increases. Virtualization makes this process easier and can delegate a server's resources to virtual machines as needed based on usage.
- **Efficiency**: Like scaling, virtualization can also make it easier to decrease the resources allocated to a virtual machine if there is reduced usage.

## Virtualization Technology

At this point, you may be asking yourself how virtualization is possible; while this is an intricate question, in this room, we will break down different technologies and platforms, briefly looking at how they interact with the underlying host operating system.

To answer the above question, we need to expand the definition of virtualization. Formally, virtualization abstracts or creates an **abstraction layer** over computer hardware. An abstraction layer allows a single device to be divided into multiple virtual computers, also known as virtual machines.

In simpler terms, this means that the virtual machine will have access to *logical resources* that are abstracted away from the *physical resources*.

## Virtualization Structure

Virtualization is implemented using an *engine-machine format*, which means that a software or system creates an abstraction layer and allocates resources, while an operating system or application can then be installed on top of this virtualized environment. The operating system is installed in a virtual machine known as a guest OS, as opposed to the host OS on which the virtualization engine is running.

# Hypervisors

In the previous task, we introduced the concept of virtualization at a high level and briefly discussed the structure of virtualization. In this task, we will present our first type of virtualization engine: **hypervisors**.

A hypervisor provides the ability to create the abstraction layer between hardware and software. A hypervisor will also generally include some form of management application or software to provide an interface between the end user and the abstraction layer to create or load virtual machines.

Hypervisors are separated into two categories that are determined by their position relative to the hardware. They can either directly create a lightweight operating system on top of the hardware that is the hypervisor or add a hypervisor as an application on top of a pre-existing operating system.

## Type 1 Hypervisors

**Type 1 Hypervisors**, also known as **bare metal hypervisors**, create an abstraction layer directly between the hardware and virtual machines without a common operating system between them. Instead, the hypervisor is the operating system and is often *headless*, with only a web-based management portal remotely accessed. These hypervisors are designed for scale and to deploy a large number of virtual machines at once. They are extremely lightweight to dedicate the most resources to virtual machines.

Below is a diagram of a type 1 hypervisor architecture.
![](https://i.imgur.com/k51mtp8.png)
> Examples of type 1 hypervisors include **VMware ESXi**, **Proxmox**, **VMware vSphere**, **Xen** and **KVM**.

## Type 2 Hypervisors

**Type 2 Hypervisors**, also known as **hosted hypervisors**, create an abstraction layer from a software application built on top of a pre-existing operating system. Unlike type 1 hypervisors, type 2 hypervisors are often managed directly from the application through a GUI. These hypervisors are often designed for end-users or individuals such as developers and are not strictly designed to run a large number of virtual machines at scale. 

![](https://i.imgur.com/H2GH0Bu.png)

> Examples of type 2 hypervisors include VMware Workstation, VMware Fusion, VirtualBox, Parallels, and QEMU.

# Containers

Hypervisors work as expected for a large number of use cases but begin to encounter issues when scaling lightweight applications. *Microservices* give us a good example of an application architecture that encounters issues when deployed from a hypervisor. 

A microservice is an application structure that is broken up into smaller services that are scalable and use lightweight protocols and features. The lightweight nature of the architecture poses obvious issues to hypervisors that require a large number of virtual machines each with high resource usage.

**Containers** are the current solution to the issues encountered with hypervisors at scale.

## What Are Containers?

Containers have a lot in common with virtual machines, but instead of being completely abstracted from the host operating system, containers share some properties with the host operating system. 

Containers have their own filesystem, a portion of computing resources (CPU, RAM), a process space, and more. 

Container engines are our second type of virtualization. As virtual machines use a hypervisor to create an abstraction layer for virtulization, containers use a container engine to create an abstraction layer using logical resources.

# Docker

If someone is familiar with containers, Docker is likely the first name that comes to mind. Docker is a container platform and engine that is used to run Docker "images" as containers. 

Each Docker image is built of a base image, such as Alpine or Ubuntu, that is specifically built for use in containers and is lightweight. To build a Docker image, a Dockerfile must be created, which defines the base image for a container and any commands to be run.

For more information about Docker, check out the [Intro to Docker](https://tryhackme.com/room/introtodockerk8pdqk) room.

## Running and Interacting with a Docker Container

Docker Hub is a remote repository for Docker images, similar to GitHub - a remote repository for Git. Using Docker Hub, we can pull Docker images created by others or push our own. 

```
docker pull <user>/<image>
```

Alternatively, a container image can be automatically pulled when running the container for the first time. Once a container is pulled for the first time, it will be cached locally, and Docker will look for it locally before attempting to download it.

```
docker run <user>/<image>
```

Once the image is started, we can verify that the Docker engine is running the container by listing the processes running in Docker using the below command.

```
docker ps
```

From the above command, you may notice that the container will be assigned a random identifier, IP address, and network interface. 

## Hands-On Application

To get hands-on with containers and Docker, we will deploy a Flask web server in a Docker container. Before starting the Docker container, we must first introduce two new flags that must be used with the `run` command to allow the container to detach from the current terminal(`-d`) and expose ports externally (`-p`). Below is the required syntax to start the example Flask app in a Docker container, exposing the webserver to port 5000.

```
docker run -p 5000:5000 -d cyrillic/thm_example_app
```


To verify that the webserver is running in the Docker container, we can scan the container or access the designated port in a web browser.

**Note:** Certain special characters may not be visible on the provided VM. When doing a copy-and-paste, it will still copy all characters.

# Kubernetes

Through the user of hypervisors and containers, most problems associated with traditional computing are resolved, such as *cost* and *efficiency*. This still leaves the question, what if we need a faster and more scalable solution? That is, as load or other criteria changes, the resources or the number of instances allocated to the application or service increase or decrease on the fly as needed.

**Kubernetes**, also shortened to **K8s**, is one such solution known as an **orchestration platform**. An orchestration platform aims to integrate into other products, such as Docker, and extend their capabilities or "synchronize" them with other products or applications. 

Kubernetes relies on these traditional virtualization models like hypervisors and containers and extends their uses, features and capabilities. 

These capabilities and features include the following:

- **Horizontal Scaling**: Unlike traditional "vertical" scaling, "horizontal" scaling refers to adding devices or machines to handle increased workload, rather than adding logic resources such as CPU or RAM.
- **Extensibility**: Clusters can be modified dynamically without affecting containers outside of the intended group. 
- **Self-Healing**: K8s can automatically restart, replace, reschedule and kill containers that are not properly functioning based on user-defined health checks.
- **Automated Rollouts and Rollbacks**: K8s can progressively roll out changes to containers. As changes are made, it will monitor the application's health and decide whether to continue the rollout or rollback. This ensures the constant uptime of your cluster even if some clusters fail.

## Hands-On Application

