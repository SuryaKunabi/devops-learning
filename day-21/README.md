# Introduction to Containers

## 1. What is a Container?

A **container** is a lightweight, isolated environment used to package and run an application along with all the dependencies required by that application.

A container can include:

* Application code
* Libraries
* Dependencies
* Runtime
* Configuration

The goal is to make the application behave consistently across different environments.

```text
Application + Dependencies
           ↓
       Container
           ↓
     Runs consistently
```

---

## 2. Why Do We Need Containers?

Consider an application developed on a developer's laptop.

It works on the developer's machine but fails on another machine because of:

* Different Python/Node.js versions
* Missing libraries
* Different operating systems
* Different configurations
* Dependency conflicts

Containers help solve this problem by packaging the application and its required environment together.

```text
Developer Machine
       ↓
   Same Image
       ↓
Testing Environment
       ↓
   Same Image
       ↓
Production
```

This helps reduce the common:

> **"It works on my machine!"**

problem.

---

## 3. Containers vs Virtual Machines

Containers and Virtual Machines both provide isolation, but they work differently.

### Virtual Machine

A VM contains a complete guest operating system.

```text
┌─────────────────────┐
│    Application      │
├─────────────────────┤
│    Libraries        │
├─────────────────────┤
│    Guest OS         │
├─────────────────────┤
│    Hypervisor       │
├─────────────────────┤
│    Host OS          │
└─────────────────────┘
```

### Container

Containers share the host operating system's kernel.

```text
┌─────────────────────┐
│    Application      │
├─────────────────────┤
│    Dependencies     │
├─────────────────────┤
│ Container Runtime   │
├─────────────────────┤
│    Host OS          │
└─────────────────────┘
```

Because containers don't normally require a separate full guest OS, they are generally:

* Lightweight
* Faster to start
* More resource efficient

---

## 4. What is Docker?

**Docker** is a platform used to build, package, distribute, and run applications using containers.

Docker provides tools for:

* Creating images
* Running containers
* Managing networks
* Managing storage
* Building application environments

Basic workflow:

```text
Dockerfile
    ↓
Docker Image
    ↓
Docker Container
    ↓
Running Application
```

---

## 5. Docker Image

A **Docker image** is a read-only template used to create containers.

For example:

```text
nginx
python
node
ubuntu
redis
postgres
```

You can download an image using:

```bash
docker pull nginx
```

One image can be used to create multiple containers.

```text
             Nginx Image
             /    |    \
            ↓     ↓     ↓
        Container Container Container
```

---

## 6. Docker Container

A **container** is a running instance of a Docker image.

For example:

```bash
docker run nginx
```

Docker uses the Nginx image to create and start a container.

You can check running containers using:

```bash
docker ps
```

---

## 7. Dockerfile

A **Dockerfile** contains instructions for building a Docker image.

Example:

```dockerfile
FROM python:3.12

WORKDIR /app

COPY . .

CMD ["python", "app.py"]
```

Basic flow:

```text
Dockerfile
    ↓
docker build
    ↓
Docker Image
    ↓
docker run
    ↓
Container
```

---

## 8. Container Networking

Containers often need to communicate with each other.

For example:

```text
┌─────────────┐
│ Web App     │
│ Container   │
└──────┬──────┘
       │
       ↓
┌─────────────┐
│ Database    │
│ Container   │
└─────────────┘
```

Docker provides networking features that allow containers to communicate.

For example, an application container could communicate with a PostgreSQL container through a Docker network.

---

## 9. Container Storage

Containers are often treated as temporary environments.

If important data needs to survive container removal, Docker **volumes** can be used.

```text
Container
    │
    ↓
Docker Volume
    │
    ↓
Persistent Data
```

For example, databases commonly use volumes to preserve their data.

---

## 10. Port Mapping

A container can run an application on a specific port.

For example:

```bash
docker run -d -p 8080:80 nginx
```

Here:

```text
Host Machine             Container
localhost:8080  ───────→ port 80
```

You can access the application using:

```text
http://localhost:8080
```

---

## 11. Multiple Containers

Modern applications often contain multiple services.

For example:

```text
                 Nginx
                   ↓
                Node.js
                /     \
               ↓       ↓
          PostgreSQL   Redis
```

Managing each container separately can become difficult.

This is where **Docker Compose** is useful.

```text
Docker Compose
      │
      ├── Nginx
      ├── Node.js
      ├── PostgreSQL
      └── Redis
```

You can start the complete application with:

```bash
docker compose up
```

---

## 12. Containers in DevOps

Containers are widely used in DevOps because they provide a consistent application environment.

A typical workflow is:

```text
Developer
    ↓
Git Repository
    ↓
Dockerfile
    ↓
Docker Image
    ↓
Container Registry
    ↓
CI/CD Pipeline
    ↓
Deployment
```

For example, a CI/CD pipeline can:

1. Get source code from Git
2. Build a Docker image
3. Run tests
4. Push the image to a registry
5. Deploy the application

---

## 13. Containers and Kubernetes

When applications become larger and require many containers, managing them manually becomes difficult.

**Kubernetes** is a container orchestration platform.

It can help with:

* Container deployment
* Scaling
* Service discovery
* Load balancing
* Self-healing
* Rolling updates

A simplified progression is:

```text
Docker
   ↓
Containers
   ↓
Docker Compose
   ↓
Multiple Containers
   ↓
Kubernetes
   ↓
Container Orchestration
```

---

## 14. Advantages of Containers

### Lightweight

Containers generally use fewer resources than virtual machines.

### Fast

Containers can start quickly because they don't normally need to boot a complete guest operating system.

### Portable

A container image can be used across different environments that support the required container runtime.

### Consistent

The application and its dependencies can be packaged together.

### Isolated

Applications running in different containers are isolated from one another.

### Scalable

Multiple container instances can be created when additional capacity is needed.

### DevOps Friendly

Containers work well with:

* Git
* CI/CD
* Docker Compose
* Kubernetes
* Cloud platforms
---

## 17. Key Takeaway

The main idea behind containers is:

```text
Application
     +
Dependencies
     ↓
Docker Image
     ↓
Container
     ↓
Consistent Environment
```




