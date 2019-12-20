---
layout: post
title:  "Get Acquainted With Containerized Stack"
date:   2019-12-10 18:00:00 +0200
categories: learning
---

Quotes and notes from reading up the new tech stack I’m working with. I often find Wikipedia useful for starting to build a mental modal of what stuff is.

| [Docker](https://en.wikipedia.org/wiki/Docker_(software)) | is a set of platform as a service (PaaS) products that use OS-level virtualization to deliver software in containers |
| [Kubernetes](https://en.wikipedia.org/wiki/Kubernetes)<br>k8s | is an open-source container-orchestration system for automating application deployment, scaling, and management |
| [OpenShift](https://en.wikipedia.org/wiki/OpenShift) | is a family of containerization software developed by Red Hat |
| [OpenShift Origin](https://docs.okd.io/) (aka OKD) | is the upstream community project, built around a core of Docker container packaging and Kubernetes container cluster management |
| [Minishift](https://www.okd.io/minishift/) | is a tool that helps you run OKD locally by launching a single-node OKD cluster inside a virtual machine |
| [Docker Machine](https://docs.docker.com/machine/overview/) | is a tool to install Docker Engine on virtual hosts, and manage the hosts with docker-machine commands |
| [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) | is a command-line tool to run commands against Kubernetes clusters |
| [Ansible](https://en.wikipedia.org/wiki/Ansible_(software)) | is an open-source software provisioning, configuration management, and application-deployment tool |
| [nodemon](https://www.npmjs.com/package/@a1motion/nodemon) | a tool that helps develop node.js based applications by automatically restarting the node application when file changes in the directory are detected |
| [nodeshift](https://nodeshift.dev/nodeshift/) | an opinionated command line application and programmable API that you can use to deploy Node.js projects to OpenShift |


### “What’s the difference between Docker Engine and Docker Machine?”
> When people say “Docker” they typically mean Docker Engine, the client-server application made up of the Docker daemon, a REST API that specifies interfaces for interacting with the daemon, and a command line interface (CLI) client that talks to the daemon (through the REST API wrapper).

> Docker Machine is a tool for provisioning and managing your Dockerized hosts (hosts with Docker Engine on them). Typically, you install Docker Machine on your local system.

– [docs.docker.com/machine/overview/](https://docs.docker.com/machine/overview/)

Pssst… Useful link to [Download Docker CE without logging in](https://github.com/docker/docker.github.io/issues/6910#issuecomment-405216460)


### nodeshift breaking change

* [Same Nodeshift, different default s2i Image](https://github.com/nodeshift/nodeshift/releases/tag/v4.0.0)
* 3.1.1 uses nodeshift/centos7-s2i-nodejs
* 4.0.0 uses ubi7/nodejs-10

---

## Reading up more on concepts

### [What is a Container?](https://www.docker.com/resources/what-container)

> A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. A&nbsp;Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.

### [Virtual machine](https://en.wikipedia.org/wiki/Virtual_machine)

> is an emulation of a computer system. Virtual machines are based on computer architectures and provide functionality of a physical computer. Their implementations may involve specialized hardware, software, or a combination.

### [kernel](https://en.wikipedia.org/wiki/Kernel_(operating_system))

>  is a computer program that is the core of a computer's operating system, with complete control over everything in the system. The kernel facilitates interactions between hardware and software components.

### [OS-level virtualization](https://en.wikipedia.org/wiki/OS-level_virtualization)

> refers to an operating system paradigm in which the kernel allows the existence of multiple isolated user space instances. Such instances, called containers, Zones, virtual private servers, partitions, virtual environments, virtual kernel, or jails, may look like real computers from the point of view of programs running in them.
