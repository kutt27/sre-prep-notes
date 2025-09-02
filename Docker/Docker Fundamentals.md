**Docker** is a platform that uses **containers** to create an **isolated**, lightweight **sandbox environment** for applications. It packages everything needed to run an application -including the code, runtime, libraries, and dependencies - into a single unit. This allows for a streamlined workflow of **building**, **shipping**, and **running** applications consistently across different environments.
## Core Concepts

Docker's core function is to solve the problem of "it works on my machine" by ensuring that an application and its environment are bundled together. The key components include:

![Docker Image](docker_instance.png)

- **Images:** A **Docker image** is a read-only template that contains the application and all its dependencies. It's essentially a blueprint for a container. You can think of it as a class in object-oriented programming.
- **Containers:** A **Docker container** is a runnable instance of an image. It's the lightweight, isolated environment where the application actually runs. Multiple containers can run from the same image, each with its own state and isolated resources.
- **Docker Engine:** This is the client-server application that builds and runs containers. It consists of the Docker daemon (the server), a REST API, and a command-line interface (CLI) client.

## How it Works

Docker utilizes a technology called **containerization**, which is a form of operating-system-level virtualization. Unlike traditional virtual machines (VMs) that virtualize the entire hardware stack and include a full guest operating system, containers share the host machine's OS kernel. This makes them significantly more lightweight, faster to start, and more efficient in terms of resource utilization.

The **build, ship, run** workflow mentioned in the image is central to Docker's value proposition:

1. **Build 🏗️:** A developer creates a **Dockerfile**, a simple text file that contains instructions for building a Docker image. The **Docker build** command processes this file and creates the image.
    
2. **Ship 🚀:** The built image can be pushed to a **container registry** (like Docker Hub), which acts as a central repository. From there, it can be easily pulled and deployed to any other server or machine with Docker installed.
    
3. **Run ✅:** The **Docker run** command takes the image from the registry and starts it as an isolated container. The application runs exactly as it was built, regardless of the underlying host's configuration.

# Containers vs Virtual Machines

Both containers and virtual machines (VMs) are forms of virtualization that allow us to run isolated environments on a single physical host, but they do so in fundamentally different ways. The key distinction lies in their architecture, which impacts their efficiency, portability, and level of isolation.

![[virtual_machine_vs_containers.png]]

---

### Virtual Machines (VMs)

A VM is an abstraction of an entire physical server. It runs on top of a **hypervisor**, a piece of software that virtualizes the hardware (CPU, memory, disk, network) of the host machine. Each VM contains a full-fledged **guest operating system (OS)**, its own kernel, and all the binaries and libraries required by the application.

This full-stack virtualization provides **strong isolation** because each VM is completely separate from the host OS and other VMs. However, this comes with significant overhead. VMs are large, can take several minutes to boot, and consume a lot of resources because each one has to run its *own complete OS*.

---

### Containers

A container, like those created by Docker, is an abstraction at the application layer. Instead of virtualizing the hardware, containers virtualize the operating system. They run on a **container engine** (like Docker Engine) and **share the host OS kernel** with other containers. Each container only contains the application and its necessary dependencies, not a full OS.

This shared-kernel architecture makes containers extremely **lightweight** and **efficient**. They are much smaller than VMs (often in megabytes), start up in seconds, and use fewer resources. This efficiency makes them ideal for microservices and continuous integration/continuous deployment (CI/CD) pipelines.

---

### Key Differences at a Glance

|Feature|Containers (e.g., Docker)|Virtual Machines (VMs)|
|---|---|---|
|**Architecture**|OS-level virtualization. Shares the host OS kernel.|Hardware virtualization. Each VM has its own guest OS and kernel.|
|**Isolation**|Lightweight isolation. Processes are isolated from each other but share the same kernel, which can pose a security risk if the kernel is compromised.|Strong isolation. Each VM is completely independent from the host and other VMs.|
|**Efficiency**|Highly efficient. Very little overhead.|Less efficient. Significant overhead due to the guest OS.|
|**Resource Usage**|Low. They only package the application and its dependencies.|High. They require a full OS, which consumes a lot of CPU, RAM, and disk space.|
|**Startup Time**|Fast. Start in seconds.|Slow. Can take minutes to boot up.|
|**Portability**|Highly portable. The container image can run on any system with a compatible container engine.|Less portable. VMs are tied to a specific hypervisor and can be large and cumbersome to move.|

# Issues with non-containerized applications

Without containerization, developers and sysadmins face several significant challenges when deploying and managing applications. The image you provided illustrates a few of these key issues, including environment inconsistencies and difficulty with scalability.

![[issues_with_non_containers.png]]

---
### 1. "It Works on My Machine" Problem 💻

This is perhaps the most famous issue. A non-containerized application often depends on the specific configuration of the developer's environment (e.g., a certain version of a library, a specific OS patch, or a unique file path). When the application is moved to another environment—such as a testing server, staging server, or production—these subtle differences can cause the application to fail.

- **Dependency Conflicts:** If multiple applications are running on the same host, they might require different, and sometimes incompatible, versions of a library. Upgrading a library for one application can inadvertently break another.
- **Manual Setup:** Every time a new environment is needed, a sysadmin must manually install the OS, runtime, libraries, and dependencies, a process that is not only time-consuming but also prone to human error.

---

### 2. Difficulty with Scaling 📈

Scaling a non-containerized application is a complex and often inefficient process.

- **Resource Overhead:** To scale an application, you typically have to spin up a new virtual machine or a physical server. This is resource-intensive because each new instance requires a full operating system and its associated overhead, wasting CPU and RAM.
- **Slow Deployment:** Deploying a new instance involves a slow, multi-step process: provisioning the VM, installing the OS and software, configuring the environment, and finally deploying the application. This makes it difficult to respond quickly to sudden increases in traffic or demand.

---

### 3. Inconsistent Environments and Lack of Portability 🌍

The lack of a standardized packaging format leads to inconsistency across the development, testing, and production environments.

- **Limited Portability:** An application is tightly coupled to its host operating system and environment. Moving an application to a different OS or a cloud provider can require significant re-engineering and configuration changes.
- **Integration Challenges:** When different components of a service (e.g., a web server, a database, and a backend service) are deployed on different machines, managing their communication and ensuring consistent network configurations becomes a complex task.

In summary, non-containerized applications are difficult to develop and deploy reliably, they are inefficient to scale, and they suffer from a lack of portability due to their tight coupling with the underlying infrastructure. Containers solve these issues by providing a consistent, isolated, and portable environment.

# With Containers

![[with_containers.png]]

# Simple docker flow

![[docker_flow.png]]

### Step 1: The Dockerfile

The process begins with a **Dockerfile**. This is a simple text file that contains a series of instructions on how to build a Docker image. It's the "recipe" for our application's environment. For example, a Dockerfile might specify the base operating system, the software to install, the application code to copy, and the command to run when the container starts.

### Step 2: Build the Docker Image

Using the `docker build` command, we take the Dockerfile and use it to create a **Docker Image**. An image is a read-only, static snapshot of your application and its dependencies. It's a single, self-contained package that can be used to create a running container. Think of it as a blueprint for your application.

### Step 3: Push to a Registry

Once the image is built, we **push** it to a **Registry**. A registry is a centralized, online repository for Docker images. The most popular one is Docker Hub, but organizations can also have private registries. Pushing the image makes it accessible to anyone with the right permissions, which is crucial for sharing it across different teams and environments.

### Step 4: Pull and Run in Different Environments

This is where the true power of Docker becomes apparent. The same exact image can be **pulled** and **run** in any environment that has a Docker engine installed, ensuring consistency across the entire software development lifecycle.

- **Development (Dev):** The developer pulls the image from the registry and runs it as a container on their local machine to test changes. The application runs exactly as it will in other environments, eliminating the "it works on my machine" problem.
- **Test (Test):** The testing team pulls the same image (dev environment) to a testing server. They can run automated or manual tests, confident that any bugs are in the application code, not due to environment inconsistencies.
- **Production (Prod):** Finally, the operations team pulls the same, proven image and runs it as a container in the production environment. This guarantees that the application behaves exactly as it did in development and testing.

By following this flow, Docker ensures that the same packaged application runs reliably and predictably, regardless of where it is deployed. This simple, repeatable process is the foundation of modern DevOps and CI/CD pipelines.

# Docker Architecture

![[docker_architecture.png]]

#### 1. The Client Sends a Command

The flow begins with the **Docker Client**. This is the command-line interface (CLI) we use to interact with Docker by typing commands like `docker build`, `docker pull`, or `docker run`. The client's job is to translate your human-readable commands into REST API requests.

#### 2. The Daemon Performs the Action

These requests are then sent to the **Docker Daemon**, which is a persistent background process running on the host machine. The daemon is the "engine" that does all the heavy lifting. It's responsible for managing Docker objects such as images, containers, networks, and volumes.

#### 3. The Daemon Interacts with the Registry

The daemon communicates with a **Docker Registry**, which is a central, public or private repository for storing and sharing Docker images.

- **When we run `docker pull <image>`**, the daemon checks if the image exists locally. If not, it requests and downloads the image from the registry.
- **When we run `docker push <image>`**, the daemon uploads the image to the registry, making it available for others to pull.

#### 4. The Daemon Manages Images and Containers

Once an image is on the host, the daemon manages its lifecycle.

- **Building an Image:** If we run `docker build`, the daemon reads a **Dockerfile** and builds a new image on the host.
- **Running a Container:** If we run `docker run`, the daemon creates a new, runnable **container** instance from the specified image. This container is the isolated environment where your application runs.
    
### 5. Output is Sent Back to the Client

The result of the daemon's action, whether it's the output of a running container or a simple confirmation message, is then streamed back to the Docker Client for us to see in our terminal. This completes the cycle, providing a seamless experience for building, shipping, and running applications.