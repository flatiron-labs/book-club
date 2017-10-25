# The Docker Book: Chapter 1

## Introduction
- Not like hypervisor virtualization, where machines run virtually on physical hardware
- containers run in user space on top of OS kernel
- **Q: I don't think I get the difference. Is there a good example or way to illustrate this? How important is understanding this**
- allows multiple isolated user space instances to run on single host
-  benefits of containers: strong isolation, own network and storage stacks, resource management capabilities, limited overhead
- disadvantages of containers: can be complex to set up, have been viewed as less secure

## Introducing Docker
- "Docker is an open-source engine that automates the deployment of applications into containers." (p. 7)
- lots of talk of "lightweight" and "fast"
- "application deployment engine on top of a virtualized container execution environment"
- the good stuff: standardized environments, portable applications, encourages "service-oriented" architecture 
- **Q: Dockerfiles sort of look like a series of instructions. I think I'm missing the part where the app code is/goes...?**

## Docker components
- Docker client and server (Docker Engine)
- Docker Images
- Registries
- Docker Containers

### Docker images
- launch your containers from images
- built using a series of instructions
- the "source code" of containers
- **Q: Cool, but what's in an image?** 
- **Q: Can we talk more about this vs chef? Is it about the time that the series of instructions are run?**

### Registries
- stores the images you build
- public and private
- Docker Hub operates public registry
- can also run your own private registry
- sounds a lot like Git

### Containers
- containers are the running / execution aspect of Docker
- consists of image format, set of standard operations, execution environment
- **Q: For real though, where does your application code go?**


### Compose and Swarm
- running Docker containers in stacks and clusters, called swarms in Docker-speak
- Docker Compose: run stacks of containers to represent application stacks
- Docker Swarm: create clusters of containers for scalable workloads

## Docker with configuration management
- Docker images are lightweight, layered, easy to iterate on

## Technical components
- native Linux container format
- Linux kernel namespaces provide isolation
- filesystem isolation: container has its own root filesystem
- process isolation: container runs in own process environment
- network isolation: separate virtual interfaces and IP addressing between containers
- Resource isolation and grouping: CPU and memory allocated individually to each Docker container using cgroups
- Copy-on-write: ??? (**Q: I don't...get it**)
- Logging: STDOUT, STDERR, STDIN
- interactive shell: can attach to STDIN
