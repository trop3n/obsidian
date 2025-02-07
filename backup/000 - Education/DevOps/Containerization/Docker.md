#containerization #docker #educativeio #virtualenvironments 
# About the Course

## Who is this Course For?

This is a course about Docker and containers; no prior knowledge required. So, if you want to work with cloud and cloud-native technologies, then this course is for you.
### Why Should I Care About Docker?

Docker is here, and it's changed the world. If you want the best jobs working with the best technologies, you need to know Docker and containers. They're even central to Kubernetes, and a strong Docker skill set will help you lean Kubernetes. Docker and containers are also well-positioned for emerging cloud technologies such as WebAssembly and AI workloads. 
### What if I'm Not a Developer?

Most applications, even modern cloud-native microservices, need high-performance production-grade infrastructure. If you think traditional developers will take care of this, think again. To cut a long story short, if you want to thrive in the modern cloud-first world, you must know Docker. But don't stress, this course will give you all the skills you need.
## Course Organization

The course is divided into two main sections: 

1. The big picture stuff
2. The technical stuff
### The Big Picture Stuff

This section gets you up to speed with things like: 

- What is Docker?
- Why do we have containers?
- The fundamental jargon such as "cloud-native", "microservices", and "orchestration".
### The Technical Stuff

This section covers everything you need to know about images, containers, multi-container microservices apps, and the increasingly important topic of orchestration. 

![](https://i.imgur.com/2PvWm0K.png)
### Breakdown of Chapters

Each chapter covers theory and includes plenty of commands and examples. Most of the chapters in the *technical stuff* section are divided into three parts:

1. **The TLDR**: Provides you with two or three paragraphs that you can use to explain the topic during the coffee break. They're also a great way to remind yourself what something is about. 
2. **The Deep Dive**: It explains how things work and gives examples.
3. **The Commands**: It lists all relevant commands in an easy-to-read list with brief reminders of what each one does. 

> [!NOTE]
> We’ve set up version 27.3.1 of the docker released on September 20, 2024, in the playgrounds provided to you.
### Playgrounds

For most of the lessons, we provide you with playgrounds, like the one given below, at the end of the lesson to help you implement what you have learned so far. 

You don’t need to configure anything in the playground. You will be all set to go. Any additional instructions needed for a playground will be provided beforehand.
# Containers from 30,000 Feet

## Towards Virtual Machines

Containers have taken over the world. In this chapter, we will learn:

- why we have containers
- what they do for us
- where we can use them
### The Bad Old Days

Applications are the powerhouse of every modern business. When applications break, businesses break. Most applications run on servers, and in the past, we were limited to running one app per server. 

As a result, the story went something like this: every time a business needed a new application, it had to buy a new server. Unfortunately, we weren't very good at modeling the performance requirements of new applications, and the IT departments had to guess. This often resulted in businesses buy very expensive servers with a lot more performance capability than the apps needed. After all, nobody wanted underpowered servers incapable of handling the app, resulting in unhappy customers and lost revenue. 

As a result, companies ended up with racks and racks of overpowered systems, operating as low as 5-10% of their potential capacity. **A tragic waste of company capital and environmental resources**.
### Hello VMWare!

Amid all this, VMWare, Inc. gave the world a gift -- the virtual machine (VM). As soon as VMware came along, the world became much better. We finally had a technology that allowed us to safely run multiple business applications on a single server. 

It was a game-changer. Businesses could run new apps on the spare capacity of existing servers, spawning a golden age of maximizing the value of existing assets. 
### VMwarts

But... and there's always a but. As great as VMs are, they're far from perfect.

A feature of the VM model is every VM needing its own dedicated operating system (OS). Unfortunately, this has several drawbacks, including:
- Every OS consumes CPU, RAM and other resources we'd rather use on applications
- Every VM and OS needs patching
- Every VM and OS needs monitoring

The VM model has other challenges too. VMs are slow to boot, and portability isn't great, migrating and moving VM workloads between hypervisors and cloud platforms is harder than it needs to be. 
## Hello Containers!

While most of us were reaping the benefits of VMs, web scalers like Google had already moved on from VMs and were using containers.

A feature of the container model is that every container shares the OS of the host it's running on. This means a single host can run more containers than VMs. For example, a host that can run 10 VMs might be able to run 50 containers, making containers far more efficient VMs. Containers are also faster and more portable than VMs.
### Linux Containers

Modern computers started in the Linux world and are the product of incredible work from many people over many years. For example, Google contributed many container-related technologies to the Linux kernel. It's thanks to many contributions like these that we have containers today. 

Some of the major technologies behind modern containers include: *kernel namespaces*, *control groups*, (cgroups), *capabilities* and more. 

However, despite all this great work, containers were incredibly complicated, and it wasn't until Docker came along that they became accessible for the masses.

> [!NOTE]
> **Note:** There are many container-like technologies that pre-date Docker and modern containers. However, none of them changed the world the way Docker has.
### Hello, Docker!

Docker was the magic that made Linux containers easy and brought them to the masses. We'll talk a lot more about Docker in the next chapter. 
### Docker and Windows

Microsoft worked hard to bring Docker and container technologies to the Windows platform. At the time of writing, Windows desktop and server platforms support both the following:

- Windows containers
- Linux containers

*Windows Containers* run Windows apps and require a host system with a Windows kernel. Windows 10, Windows 11 and all modern versions of Windows Server natively support Windows containers. 

Windows systems can also run Linux containers via the *WSL 2 (Windows Subsystem for Linux* subsystem. This means Windows 10 and Windows 11 are great platforms for developing and testing Windows **and** Linux containers.

However, despite all the work developing *Windows Containers*, almost all containers are Linux containers. This is because Linux containers are smaller and faster, and more tooling exists for Linux. _In this course all examples are based on Linux containers._ 
## Running Containers

Understand the basics of running containers.
### Windows Containers vs. Linux Containers

It's vital to understand that containers *share the kernel of the host they're running on*. This means containerized Windows apps need a host with a Windows kernel, whereas containerized Linux apps need a host with a Linux kernel. However, as mentioned, you can run Linux containers on Windows systems that have the WSL 2 backend installed. 
### What about Mac Containers?

There is no such thing as "Mac Containers". However, Macs are great platforms for working with containers. 

The most popular way of working with containers on a Mac is *Docker Desktop*. It works by running Docker inside a lightweight Linux VM on your Mac. Other tools, such as `Podman` and `Rancher Desktop`, are also great for working with containers on Mac.
### What about WebAssembly?

**WebAssembly (Wasm)** is a modern binary instruction set that builds applications that are smaller, faster, more secure and more portable than containers. You write your app in your favorite language and compile it as a ***Wasm binary***, and it'll run anywhere you have a ***Wasm Runtime***. 

However, Wasm apps have many limitations, and we're still developing many of the standards. As a result, containers remain the dominant model for cloud-native applications. The container ecosystem is also much richer and more mature than the Wasm ecosystem. 

Docker and the container ecosystem are adapting to work with Wasm apps, and you should expect a future where VMs, containers, and Wasm apps run side-by-side most cloud applications. 
### What about Kubernetes?

Kubernetes is the industry standard platform for deploying and managing containerized apps. 

> [!NOTE]
> A **containerized app** is an application running as a container.

Older versions of Kubernetes used Docker to start and stop containers. However, newer versions use `containerd`, which is a stripped down version of Docker optimized for use by Kubernetes and other platforms. 

The important thing to know is that *all Docker containers work on Kubernetes*. 
## Chapter Summary

We used to live in a world where every time the business needed a new application, we had to buy a brand-new server. VMware came along and allowed us to drive more value out of new and existing servers. However, following the success of VMware and hypervisors came a newer, more efficient, and portable virtualization technology called **containers**. However, containers were complex and hard to implement until Docker came along and made them easy. WebAssembly is powering a third wave of cloud computing, but Docker and the container ecosystem are evolving to work with WebAssembly.
# Docker and Container-related Standards and Projects
## Introduction to Docker

An introduction to the company and Docker technology.
### Docker

Docker is at the heart of the container ecosystem. However, the term Docker can mean two things:

1. The Docker platform
2. Docker, Inc.

The Docker platform is a neatly packages collection of technologies for creating, managing, and orchestrating containers. Docker, Inc. is the company that created the Docker platform and continues to be the driving force behind developing new features. 
### Docker Inc. 

Docker Inc. is a technology company based our of Palo Alto and founded by French-born American developer and entrepreneur Solomon Hykes. Solomon is no longer at the company. 

The company started as a *platform as a service (PaaS)* provider called *dotCloud*. Behind the scenes, dotCloud delivered their services on top of containers and had an in-house tool to help them deploy and manage those containers. They called this in-house tool *Docker*. 

The word Docker is a British expression meaning **dock worker** that refers to a person who loads and unloads cargo from ships. 

In 2013, dotCloud dropped the struggling PaaS side of the business, rebranded as Docker, Inc and focused on bring Docker and containers to the world. 
## The Docker Technology

The Docker platform is designed to make it as easy as possible to *build*, *ship* and *run* containers. 
### Docker's High Level Components

At a high level, there are two major parts to the Docker platform:

- The CLI (client)
- The Engine (server)

The *CLI* is the familiar `docker` command-line tool for deploying and managing containers. It converts multiple commands into API requests and sends them to the engine.

The *engine* comprises all the server-side components that run and manage containers. 

Below figure shows the high-level architecture. The client and engine can be on the same host or connected over the network. 

![](https://i.imgur.com/jyaffAg.png)

In the later chapters you'll find that the client and engine are complex and comprise a lot of small specialized parts. The figure below gives you an idea of some of the complexity behind the engine. However, the client hides all this complexity so you don't have to care. For example, you type friendly `docker` commands into the CLI, the CLI converts them to API requests and sends them to the daemon, and the daemon takes care of everything else. 

![](https://i.imgur.com/kx2uN21.png)
## Container-Related Standards and Projects

Let's switch focus and briefly look at some standards and governance bodies.

There are several important standards and governance bodies influencing the development of containers and the container ecosystem. Some of these include:

- The OCI
- The CNCF
- The Moby Project
### The Open Container Initiative (OCI)

The [Open Container Initiative (OCI)](https://www.opencontainers.org) is a governance council responsible for low-level container-related standards. It operates under the umbrella of the [Linux Foundation](https://www.linuxfoundation.org/projects) and was founded in the early days of the container ecosystem when some of the people at a company called CoreOS didn't like the way Docker was dominating the ecosystem. In response, CoreOS created an open standard called _[appc](https://github.com/appc/spec/)_ that defined specifications for thing such as image format and container runtime. They also created a reference implementation called *rkt* (pronounced "rocket"). The `appc` standard did things differently from Docker and put the ecosystem in an awkward position with two competing *standards*. 

While competition is usually a good thing, *competing standards* are generally bad, as they generate confusion that slows down user adoption. Fortunately, the main players in the ecosystem came together and formed the OCI as a vendor-neutral lightweight council to govern container standards. This allowed us to archive the `appc` project and place all low-level container-related specifications under OCI's governance.
#### OCI Standards

At the time of writing, the OCI maintains three standards called *specs*:

- The [image-spec](https://github.com/opencontainers/image-spec)
- The [runtime-spec](https://github.com/opencontainers/runtime-spec)
- The [distribution-spec](https://github.com/opencontainers/distribution-spec)

We often use a *rail tracks* analogy when explaining the OCI standards:

When the size and properties of rail tracks were standardized, it gave entrepreneurs in the rail industry confidence the trains, carriages, signaling systems, platforms and other rail infrastructure they built would work with the standardized tracks -- nobody wanted competing standards for track sizes.

The OCI specifications did the same thing for the container ecosystem and it's flourished ever since. Docker has also changed a lot since the formation of the OCI, and all modern verisons of Docker implement all three OCI specs. For example:

- The Docker builder (BuildKit) creates _OCI compliant-images_
- Docker uses an _OCI-compliant runtime_ to create _OCI-compliant containers_
- Docker Hub implements the OCI distribution spec and is an _OCI-compliant registry_

Docker, Inc. and many other companies have people on the technical oversight board of the OCI.
### The CloudNative Computing Foundation (CNCF)

The [Cloud Native Computing Foundation (CNCF)](https://www.cncf.io/) is another Linux Foundation project that is influential in the container ecosystem. It was founded in 2015 with the goal of "...advancing container technologies... and making cloud native computing ubiquitous".

Instead of creating and maintaining container-related specifications, the CNCF *hosts* important projects such as Kubernetes, containerd, Notary, Prometheus, Cilium, and more. 
#### CNCF Project Lifecycle

When we say the CNCF *hosts* these projects, we mean it provides a space, structure, and support for projects to grow and mature. For example, all CNCF projects pass through the following three phases or stages:

- Sandbox
- Incubating
- Graduated

Each phase increases a project's **maturity level** by requiring higher governance standards, documentation, auditing, contribution tracking, marketing, community engagement, and more. For example, new projects accepted as sandbox projects may have great ideas and great technology but need help and resources to create strong governance, etc. The CNCF helps with all of that.

Graduated projects are considered *ready for production* and are guaranteed to have strong governance and implement good practices.

If you see the figure below you'll see that Docker uses at least two CNCF technologies -- containerd and Notary.
### Moby Project

Docker created the *Moby project* as a community-led place for developers to build specialized tools for building container platforms. 

Platform builders can pick the specific Moby tools they need to build their container platform. They can even compose their platforms from a mix of Moby tools, in-house tools, and tools from other projects. Docker, Inc. originally created the Moby project, but it now has members including Microsoft, Mirantis, and Nvidia. The Docker platform is built using tools from various projects, including the Moby project, the CNCF and the OCI.
## Chapter Summary

This chapter introduced Docker and some of the major influences in the container ecosystem.

- Docker, Inc., is a technology company based in Palo Alto that is changing the way we develop software. They were the first movers and instigators of the modern container revolution.
- The Docker platform focuses on running and managing application containers. It runs on Linux and Windows, can be installed almost anywhere, and offers a variety of free and paid-for products.
- The Open Container Initiative (OCI) governs low-level container standards and maintains specifications for runtimes, image format, and registries.
- The CNCF hosts important cloud-native projects and helps them mature into production-grade tools.
- The Moby project hosts low-level tools developers can use to build container platforms.
# The Big Picture
## Introduction to DevOps

An overview of DevOps in today's world.

The aim of this chapter is to quickly paint a big-picture of what Docker is all about before we dive deeper into later chapters. 

This chapter will give you some hands-on experience and a high-level view of images and containers. The goal is to prepare you for more detail in the upcoming chapters. 

We'll break this into two parts:

- The Ops Perspective
- The Dev Perspective

The ops perspective focusing on starting, stopping, deleting containers, and executing commands inside them.

The dev perspective focuses on the application side of things and runs through taking application source code, building it into a container image, and running it as a container.

These two perspective will give you a good idea of what Docker is all about and how the major components fit together.

Don't worry if some of the stuff we do here is totally new. We're not trying to become an expert in this chapter. This about giving a *feel* for things, setting us up to that when we get into the details in later chapters, we have an idea of how the pieces fit together. 
### Running Docker

To follow along with this course, we will be provided with a Linux environment in Educative's terminal widgets. The environment has Docker pre-installed. 

> If you want to follow along locally, see the installation instructions in the “Installing Docker” section.

As we progress through the chapter, we may use the terms “Docker host” and “Docker node” interchangeably. Both refer to the system that you are running Docker on.
## The Ops Perspective

In this and the next three lessons, we'll complete the following:

- Check Docker is working
- Download an image
- Start a container from the image
- Execute a command inside the cont:
- Delete the container

Let's start with verifying that Docker is properly installed in the environment.
### Verifying the Installation

A typical Docker installation installs the client and the engine on the same machine and configures them to talk to each other. 

In the terminal provided below, run a `docker version` command to ensure both are installed and running. Check the Docker installation in the terminal below:

If the response from the client and server looks like the output below, we're good to go:

```bash
$ docker version
                                   
Client:                                   <<---- Start of client response 
 Version:           27.3.1                  -----┐
 API version:       1.43                         | Client info block
 Go version:        go1.21.1                     |
 OS/Arch:           darwin/arm64                 |
 Context:           desktop-linux           -----┘

Server: Docker Engine - Community.          <<---- Start of server response
 Engine:                                    -----┐
  Version:          24.0.5                       |
  API version:      1.3 (minimum version 1.12)   |
  Go version:       go1.20.6                     |
  OS/Arch:          linux/arm64                  |
 containerd:                                     | Server block
  Version:          1.6.31                       |
 runc:                                           |
  Version:          1.1.12                       |
 docker-init:                                    |
  Version:          0.19.0                  -----┘
```
### Instructions for Linux

If you're trying locally on a Linux system and get a `permission denied while trying to connect to the Docker daemon...` error, run the command again with `sudo` privileges. 
## Docker Images

An overview of Docker images and how to download them.
### What are Docker Images?

Images are objects that contain everything an app needs to run. This includes an OS filesystem, the application, and all dependencies. If you work in operations, they're similar to VM templates. If you're a developer, they're similar to *classes*.

At the end of this lesson, a terminal is provided where you can run the commands.

Run the `docker image` command on your Docker host. 

```
docker images
```

You should get the following output after running the command.

```
$ docker images 

REPOSITORY    TAG        IMAGE ID       CREATED       SIZE
```

If you are working with a clean installation, you'll have no images, and your output will be the same as the one given above. If you're working with Multipass, you might see an image called `protainer/protainer-ce`.
### Download an Image

Copying new images onto your Docker host is called *pulling*. Pull the `ubuntu:latest` image.

```
docker pull ubuntu:latest
```

Below is the output of `docker pull ubuntu:latest` command:

```
$ docker pull ubuntu:latest

latest: Pulling from library/ubuntu
31e907dcc94a: Pull complete 
Digest: sha256:8a37d68f4f73ebf3d4efafbcf66379bf3728902a8038616808f04e34a9ab63ee
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest
```

Run another `docker images` to confirm your *pull* command worked. 

```
docker images
```
### Inside a Docker Image

We'll discuss the details of where the image is stored and what's inside it in later chapters. For now, all you need to know is that images contain enough of an operating system and all the code and dependencies required to run the application. The Ubuntu image we pulled includes a stripped-down version of the Ubuntu Linux file system and a few of the standard Linux utilities that ship with Ubuntu.

If you pull an *application container*, such as `nginx:latest`, you'll get an image with a minimal OS **and** the code to run the NGINX app.
## Managing Containers

Learn how to run a container and exit from it without killing it.
### Start a Container from the Image

If you've been following along, you'll have a copy of the `ubuntu:latest` image on your Docker host, and you can use the `docker run` command to start a container from it. 

Run the following `docker run` command to start a new container called `test` from the `ubuntu:latest` image. 

```
$ docker run --name test -it ubuntu:latest bash

root@bbd2e5ad1817:/#
```

Notice how the prompt has changed. This is because the container is already running and the shell is attached to it.
### The `docker run` Command

Let's quickly examine that `docker run` command. 

`docker run` tells Docker to start a new container. The `--name` flag told Docker to call this container `test`. Next, the `-it` flags told Docker to make the container interactive and to attach your shell to the container's terminal. After that, it told Docker to base the container on the `ubuntu:latest` image. Finally, it told Docker to start a Bash shell as the container's main app.

Run a `ps` command from inside the container to list all running processes.

```
root@bbd2e5ad1817:/# ps -elf
```

There are only two processes: 

```
root@bbd2e5ad1817:/# ps -elf

F S UID    PID  PPID   NI ADDR SZ WCHAN  STIME TTY      TIME CMD
4 S root     1     0    0 -  4560 -      13:38 pts/0    00:00:00 /bin/bash
0 R root     9     1    0 -  8606 -      13:38 pts/0    00:00:00 ps -elf
```

- PID 1 is the Bash process that we told the container to run
- PID 9 is the `ps -elf` command we ran to list the running processes

The presence of the `ps -elf` process in the output can be a bit misleading as it is a short-lived process that exits as soon as the `ps` command completes. This means the only long-running process inside the container is the `/bin/bash` process.

Press `Ctrl-PQ` to exit the container without terminating it. This will land your shell back at your local terminal, and your shell prompt will revert. 
### See the Running Containers

In a previous step, you pressed `Ctrl-PQ` to exit from the container. Doing this from inside of a container will exit you from the container without killing it.

Run the following command to verify your `test` container is still running.

```
$ docker ps

CONTAINER ID   IMAGE          COMMAND       CREATED  STATUS    NAMES
bbd2e5ad1817   ubuntu:latest  "/bin/bash"   7 mins   Up 7 min  test
```

The output shows your `test` container
## Attaching to Running Containers

Learn to attach your shell to a running container.
### The `docker attach` Command

You can use the `docker attach` command to attach your shell to the container's main process. Run the following command to attach your shell to the Bash process inside the container.

```
$ docker attach test

root@bbd2e5ad1817:/# 
```

Make sure your shell prompt changes, indicating you successfully connected to a container. Exit the container again by typing `Ctrl-c` and verify your shell prompt reverts to your local machine.
### Delete the Container

Run another `docker ps` to verify your container is still running. Stop and kill the container using the `docker stop` and `docker rm` commands. 

```
docker stop test

test
```

It can take a few seconds for the container to stop.

```
docker rm test

test
```

Verify the container was successfully deleted by running the `docker ps` command with the `-a` flag to list all containers, even those in the stopped state.

```
$ docker ps

CONTAINER ID   IMAGE          COMMAND       CREATED  STATUS    NAMES
bbd2e5ad1817   ubuntu:latest  "/bin/bash"   7 mins   Up 7 min  test
```

Congratulations, you've pulled a Docker image, started a container from it, logged in to it, executed a command inside it, stopped, and deleted it.
## The Dev Perspective

Learn how to clone an app from GitHub, containerize it using Docker, and run it as a container.

Containers are all about applications. You'll complete all the following steps in this lesson:

- Clone an app from a GitHub repo. We will use [this repository](https://github.com/nigelpoulton/psweb.git) to demonstrate the cloning process
- Inspect the app's Dockerfile
- Containerize the app
- Run the app as a container
### Running Commands

Run the following command to make a local clone of the repo. This will copy the application code to your machine so you can containerize it in a future step. 

```
git clone https://github.com/nigelpoulton/psweb.git
```

Change into the `psweb` directory and list its contents. 

```
cd psweb
ls -l
```

The app is a simple Node.js web app running some static HTML.
### Inspect the app's Dockerfile

The **Dockerfile** is a plain-text document that tells Docker how to build the app and dependencies into an image.

```
FROM alpine
LABEL maintainer="nigelpoulton@hotmail.com"
RUN apk add --update nodejs npm curl
COPY . /src
WORKDIR /src
RUN  npm install
EXPOSE 8080
ENTRYPOINT ["node", "./app.js"]
```

You'll learn more about Dockerfiles later in the course. Right now, all you need to know is that each line represents an instruction Docker executes to build the app into an image.
### Containerizing the Application

Run the following `docker build` command to create a new image based on the instructions in the Dockerfile. It will create a new Docker image called `test:latest`.

Be sure to run the command from within the `psweb` directory.

```
docker build -t test:latest .
```

Once the build is complete, check that you have an image called `test:latest`.

```
docker images
```

Congratulations, you've *containerized* an app. That's jargon for building it into a container image that contains the app and dependencies.
### Run the App as a Container

Run the following command to start a container called `web1` from the image. 

```
docker run -d --name web1 --publish 8080:8080 test:latest
```

Open a web browser and navigate to the DNS name or IP address of your Docker host on port 8080. If you're following along on Docker desktop, connect to `localhost:8080` or `127.0.0.1:8080`. If you're following along on Multipass, connect your Multipass VM's `192` address on port `8080`. Run an `ip a | grep 192` command from within the Multipass VM, or run a `multipass ls` from your local machine to find the address.

Congratulations. You've copied some application code from a remote Git repo, built it into a Docker image, and run it as a container. We call this *containerizing* an app. 
### Clean Up

Run the following commands to terminate the container and delete the image.

```
docker rm web1 -f

docker rmi test:latest
```
## Chapter Summary

In the Ops section of the chapter, we downloaded a Docker image, launched a container from it, logged into the container, executed a command inside it, and then stopped and deleted the container.

In the Dev section, we containerized a simple application by pulling source code from GitHub and building it into an image using instructions in a Dockerfile. We then ran the app as a container.

The concepts learned in this chapter will help us in the upcoming chapters.
# The Docker Engine

## Introduction to the Docker Engine

> Get a high level overview of the Docker Engine.

In this chapter, we'll look under the hood of the Docker Engine. This chapter has a strong operations focus.

You can use Docker without knowing everything you're about to learn. However, to truly master something, you need to understand what's going on under the hood. So, if you want to **master Docker**, you should read this chapter.

Let's learn about the Docker Engine.
### Docker Engine - The TLDR

*Docker Engine* is jargon for the server-side components of Docker that run and manage containers. If you've every worked with VMWare, the Docker Engine is similar to ESXi.

The Docker Engine is modular and build from many specialized components pulled from projects such as the OCI, the CNCF and the Moby project.

In many ways, the Docker Engine is like a car engine:

- A car engine is made from many specialized parts that work together to make a car drive -- intake manifolds, throttle bodies, cylinders, pistons, spark plugs, exhaust manifolds, and more. 
- The Docker Engine is made from many specialized tools that work together to create and run containers -- the API, image builder, high-level runtime, low-level runtime, shims, etc.

The figure below shows the components of the Docker Engine that create and run containers. Other components exist, but this simplified diagram focuses on the components that start and run containers. 

![](https://i.imgur.com/G30oyZi.png)

> [!NOTE]
> **Note:** Throughout the book, we’ll refer to `runc` and `containerd` with lowercase `r` and `c`, which is how they’re both written in the official project documentation. This means sentences starting with either `runc` or `containerd` will not begin with a capital letter.
## The Deep Dive

A deep dive into the Docker engine.

When Docker was first released, the Docker Engine had two major components:

- The Docker daemon (sometimes referred to as just "the daemon")
- LXC

The daemon was a monolithic binary containing all the code for the API, image builders, container execution, volumes, networking, and more.

LXC did the hard work of interfacing with the Linux kernel and constructing the required namespaces and cgroups to build and start the containers.
### Replacing LXC

Relying on LXC posed several problems for the Docker project:

- First, LXC is Linux-specific, and Docker had aspirations about being multi-platform.
- Second, Docker was evolving fast, and there was no way of ensuring LXC evolved in the ways Docker needed.

To improve the experience and help the project evolve more quickly, Docker replaced LXC with its own tool, *libcontainer*. The goal of libcontainer was to be a platform-agnostic tool that gave Docker access to the fundamental container building blocks in the host kernel. Libcontainer replaced LXC in Docker a very long time ago.
### Breaking Up the Monolithic Docker Daemon

As previously mentioned, the Docker Engine was originally a monolith with almost all functionality coded into the *daemon*. However, as time passed, this became more and more problematic for the following reasons:

1. It got slower
2. It wasn't what the ecosystem wanted
3. It's hard to innovate on monolithic software

The project recognized these challenges and bena an long-running program to break apart and refactor the Engine so that every feature became it's own specialized tool. Platform builders could then re-use these tools to build other platforms.

This work of breaking apart the Docker daemon is an ongoing process, and all of the code for building images and executing containers has been removed and refactored into small, specialized tools. Notable examples include removing the high-level and low-level runtime functionality and re-implementing them in separate tools called `containerd` and `runc`, both of which are used by many different projects including Docker, Kubernetes, Firecracker, and Fargate. More recently starting with Docker Desktop 4.27.0, Docker has removed image management from the daemon and now uses containerd's image management capabilities.

The figure below shows another view of the main components of the Docker Engine that run containers and lists each component's primary responsibilities.

![](https://i.imgur.com/TnpdSEk.png)
## The Influence of the Open Container Initiative (OCI)

Let's talk about the role of OCI in defining container-related specifications.

Around the same time that Docker, Inc. was refactoring the Engine, the OCI was in the process of defining two container-related standards:

1. Image Specification - [(image-spec)](https://github.com/opencontainers/image-spec)
2. Runtime Specification [(runtime-spec)](https://github.com/opencontainers/runtime-spec)

Both specifications were released as version 1.0 in July 2017 and are still vital today. They've even added a third specification called Distribution Specification [(distribution-spec)](https://github.com/opencontainers/distribution-spec) governing how images are distributed via registries.

At the time of writing, the runtime-spec is at version 1.1.0, the image-spec is at version 1.0.2, and the distribution-spec is at 1.0.1. However, plans are underway for version 1.1 of both the image-spec and distribution-spec. We mentioned this to highlight the slow-and-steady nature of these low-level specifications that are heavily relied upon by so many other projects - stability is the name of the game for low-level OCI specs.

Docker, Inc. was a founding member of the OCI and was heavily involved in defining the specifications. It continues to be involved by contributing code and helping guide the specifications.

All versions of Docker since 2016 have implemented the OCI specifications. For example, Docker uses `runc`, the reference implementation of the OCI runtime-spec, to create OCI-compliant containers. It also uses BuildKit to build OCI-compliant images (image-spec), and Docker Hub is an OCI-compliant registry (registry-spec).
### `runc`

As previously mentioned, [`runc`](https://github.com/opencontainers/runc) (pronounced “run see” and always written with a lowercase `r`) is the reference implementation of the OCI runtime-spec. Docker, Inc. was heavily involved in defining the spec and contributed the initial code for `runc`. 

`runc` is a lightweight CLI wrapper for libcontainer that you can download and use to manage OCI-compliant containers. However, it's a very low-level tool and lacks almost all of the features and add-ons you get with the Docker Engine.

Fortunately, as shown in the figure below, Docker uses `runc` as its low-level runtime. This means you get OCI-compliant containers and the feature-rich Docker user experience. 

![](https://i.imgur.com/lIZ5IiD.png)

On the jargon front, we sometimes say that `runc` operates at the *OCI Layer*, and we often refer to it as a *low-level runtime*. Docker and Kubernetes both use `runc` as their default low-level runtime, and both pair it with the containerd high-level runtime:

- `containerd` operates as the high-level runtime *managing* lifecycle events
- `runc` operates as the low-level runtime *executing* lifecycle events by interfacing with the kernel to do the work of actually building containers and deleting them.
### `containerd`

`condtainerd` (pronounced "container dee") and always written with a lowercase `c` is another tools that Docker created while stripping functionality out of the daemon.

We refer to `containerd` as a *high-level runtime* as it *manages* lifecycle events such as starting, stopping and deleting containers. However, it needs a low-level runtime to perform the actual work. Most of the time, `containerd` is paired with `runc` as its low-level runtime. However, as you see in the figure below, it uses `shims` that make it possible to replace `runc` with other low-level runtimes.

![](https://i.imgur.com/AWZNRF6.png)

The original plan was for `containerd` to be a small specialized tool for managing container lifecycle events. However, it has since grown to include the ability to manage images, networks and volumes.

One reason for adding more functionality is for projects such as Kubernetes that want `containerd` to be able to push and pull images. Fortunately, this extra functionality is modular, meaning projects like Kubernetes can include `containerd` but only take the pieces they need.

`containerd` was originally developed by Docker, Inc. and donated to the Cloud Native Computing Foundation (CNCF). At the time of writing, `containerd` is a graduated CNCF project, meaning it's stable and production-ready. You can see the latest releases [here](https://github.com/containerd/containerd/releases).
## Starting a New Container

Learn about how to start new container using Docker CLI.

Now that you have a view of the big picture, let's see how to use Docker to create a new container.
### Starting Containers using the Docker CLI

The most common way of starting containers is using the Docker CLI. Run the following command to start a new container called `ctr1` based on the `nginx` image.

```
docker run -d --name crt1 nginx
```

Run a `docker ps` command to see if the container is running.

```
docker ps
```

When you run commands like this, the Docker client converts them into API requests and sends them to the API exposed by the daemon. The daemon can expose the API on a local socket or over the network. On Linux, the local socket is `/var/run/docker.sock` and on Windows it's `\pipe\docker_engine`.

The daemon receives the request, interprets it as a request to create a new container, and passes it to `containerd`. Remember that the daemon no longer contains any code to create containers.

The daemon communicates with `containerd` via a CRUD-style API over [gRPC](https://grpc.io/). Despite its name, even `containerd` cannot create containers. It converts the required Docker image into an *OCI Bundle* and tells `runc` to use this to create a new container.

![](https://i.imgur.com/CDmHvpL.png)
### One Huge Benefit of This Model

Decoupling the container creation and management from the Docker daemon and implementing it in `containerd` and `runc` makes it possible to stop, restart, and even update the daemon without impacting running containers. We sometimes call this *daemonless containers*.

If you started the NGINX container earlier, you should delete it using the following command.

```
docker rm ctr1 -f
```
### What's this Shim all About?

Some of the diagrams in this chapter have shown a shim component. Shims are a popular software engineering pattern, and the Docker Engine uses them in between `containerd` and the OCI layer, bringing the following benefits:

- Daemonless containers
- Improves efficiency
- Makes the OCI layer pluggable

We've already mentioned daemonless containers.

On the efficiency front, containerd forks a shim and a `runc` process for every new container. However, each `runc` process exits as soon as the container starts running, leaving the shim process as the container's parent process. The shim is lightweight and sits between `containerd` and the container. It reports on the container's status and performs low-level tasks such as keeping the container's STDIN and STDOUT streams open.

Shims also make it possible to replace `runc` with other low-level runtimes.
### How It's Implemented on Linux

On a Linux system, Docker implements the components we've discussed as the following separate binaries:

- `/usr/bin/dockerd` (the Docker daemon)
- `/usr/bin/containerd`
- `/usr/bin/containerd-shim-runc-v2`
- `/usr/bin/runc`

You can see all of these on a Linux-based Docker host by running a `ps` command. Some of the processes will only be present when the system has running containers, and you can't see them if you're using Docker Desktop on a Mac because the Docker Engine is running inside a VM.
### Do We Still Need the Daemon?

At the time of writing, Docker has stripped most of the functionality out of the daemon, leaving the daemon to focus on serving the API.
## Chapter Summary

Summary of the contents covered in this chapter.

- The Docker Engine is a platform that makes it easy to build, ship, and run containers. It implements the OCI standards and is a modular app comprising many small, specialized components.
- The _Docker daemon_ implements the Docker API, but most other functionality has been stripped out and implemented as standalone composable tools such as `containerd` and `runc`.
- `containerd` performs image management tasks and oversees container lifecycle management, such as starting, stopping, and deleting containers. Docker, Inc. originally wrote it and then contributed to the CNCF. It’s classed as a high-level runtime and used by many other projects, including Kubernetes, Firecracker, and Fargate.
- `containerd` relies on a low-level runtime called `runc` to interface with the host kernel and build containers. `runc` is the reference implementation of the OCI runtime-spec and expects to start containers from OCI-compliant bundles. `containerd` talks to `runc` and ensures Docker images are presented to `runc` as OCI-compliant bundles.
- `runc` is based on code from libcontainer, we can run it as a standalone CLI tool to create containers, and it’s used almost everywhere that `containerd` is used. Shims make it possible to use `containerd` with other low-level runtimes.
# Working with Docker Images


