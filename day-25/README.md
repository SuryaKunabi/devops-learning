# Docker Networking

Docker networking allows Docker containers to communicate with each other, with the host machine, and with external networks.

For example, a web application may need to communicate with a database:

```text
        Docker Network
   ┌──────────────────────┐
   │                      │
   │  Web Container       │
   │        │             │
   │        ↓             │
   │  Database Container  │
   │                      │
   └──────────────────────┘
```

Docker provides different networking drivers and allows us to create custom networks according to the application's requirements.

---

# 1. Why Do You Need Networking in Docker?

Containers are isolated environments. However, applications running inside containers often need to communicate with other services.

For example, consider a web application:

```text
Browser
   │
   ↓
Web Container
   │
   ↓
Database Container
```

The web container needs a way to communicate with the database container.

Docker networking provides this communication.

### Common use cases

Docker networking is required for:

* Container-to-container communication
* Container-to-host communication
* Container-to-internet communication
* Connecting applications with databases
* Connecting microservices
* Exposing applications to users
* Isolating containers from each other

### Example

Suppose you have:

```text
Frontend Container
       │
       ↓
Backend Container
       │
       ↓
Database Container
```

All these containers need networking to communicate.

---

# 2. How Does Docker Networking Work?

When Docker starts a container, Docker provides networking for that container.

A simplified view:

```text
                    Host Machine
                         │
                  Docker Engine
                         │
          ┌──────────────┼──────────────┐
          │              │              │
      Container 1    Container 2    Container 3
          │              │              │
          └──────────────┼──────────────┘
                         │
                    Docker Network
```

Docker creates network interfaces and networking rules that allow containers to communicate.

### Container IP Address

Containers can have their own IP addresses inside a Docker network.

For example:

```text
Container A
IP: 172.x.x.x

Container B
IP: 172.x.x.x
```

However, applications generally should not depend on container IP addresses because container IPs can change.

Instead, on a user-defined network, containers can communicate using **container names**.

For example:

```text
Web Container
     │
     │ connects to
     ↓
database
```

The application can use:

```text
database
```

as the hostname.

Docker provides DNS-based service discovery on user-defined networks. 
---

# 3. What Are the Different Types of Networking in Docker?

Docker provides several network drivers.

The commonly used ones are:

```text
bridge
host
none
overlay
ipvlan
macvlan
```

You can see available networks using:

```bash
docker network ls
```

---

## 3.1 Bridge Network

The **bridge** driver is commonly used when containers run on the same Docker host.

Example:

```text
          Docker Host
               │
        Bridge Network
        ┌──────┴──────┐
        │             │
   Container A   Container B
```

Containers connected to the same user-defined bridge network can communicate with each other.
Example:

```bash
docker network create my-network
```

---

## 3.2 Host Network

With the `host` network, the container shares the host's network namespace.

```text
Docker Host
     │
     └── Container
         uses host networking
```

Example:

```bash
docker run --network host nginx
```

This removes network isolation between the container and the Docker host for that network namespace.

---

## 3.3 None Network

The `none` network provides the container with no network connectivity except the loopback interface.

Example:

```bash
docker run --network none alpine
```

This can be useful when a container does not need network access. 

---

## 3.4 Overlay Network

An **overlay** network is designed to connect containers or services across multiple Docker hosts.

Simplified example:

```text
Docker Host 1              Docker Host 2

Container A                Container B
     │                          │
     └──────── Overlay ─────────┘
              Network
```

Overlay networking is commonly associated with Docker Swarm and multi-host container communication.

## 3.5 Macvlan

The `macvlan` driver allows containers to appear as devices on the physical network with their own MAC addresses.

It is useful for certain network integration scenarios where containers need to appear directly on the physical network.

---

## 3.6 IPvlan

The `ipvlan` driver provides another way to connect containers to external networks while controlling how IP addressing is handled.

It is useful in specific advanced networking environments. 

---

# 4. Which Networking Is Default and Out of the Box?

When Docker is installed, Docker normally creates default networks.

Run:

```bash
docker network ls
```

You will commonly see:

```text
NETWORK ID     NAME      DRIVER
xxxxxx         bridge    bridge
xxxxxx         host      host
xxxxxx         none      null
```

The **default bridge network** is the standard network provided by Docker for containers that don't specify another network. 
For example:

```bash
docker run -d --name container1 nginx
```

Because no network was specified, the container is connected to Docker's default `bridge` network.

You can verify this with:

```bash
docker inspect container1
```

---

# 5. Play With Docker Containers and Inspect Their Networks

Now let's perform some basic hands-on experiments.

## Step 1: Create Two Containers

Run:

```bash
docker run -d --name container1 nginx
```

Run another:

```bash
docker run -d --name container2 nginx
```

Check the containers:

```bash
docker ps
```

---

## Step 2: Check Docker Networks

Run:

```bash
docker network ls
```

You should see the default networks.

---

## Step 3: Inspect the Default Bridge Network

Run:

```bash
docker network inspect bridge
```

Docker will show information such as:

* Network ID
* Driver
* Subnet
* Gateway
* Connected containers

---

## Step 4: Inspect a Container

Run:

```bash
docker inspect container1
```

Look for the `Networks` section.

You can find information such as:

```text
Network
IP Address
Gateway
MAC Address
```

---

## Step 5: Check the Container IP

You can use:

```bash
docker inspect -f "{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}" container1
```

This displays the container's IP address.

---

# 6. Create a Custom Bridge Network

Instead of using Docker's default bridge network, we can create our own network.

Create one:

```bash
docker network create my-network
```

Check it:

```bash
docker network ls
```

You should see:

```text
my-network
```

The default driver for this command is `bridge`.

---

# 7. Run Containers on the Custom Network

Create the first container:

```bash
docker run -d \
  --name web \
  --network my-network \
  nginx
```

Create another:

```bash
docker run -d \
  --name database \
  --network my-network \
  redis
```

Now both containers are connected to:

```text
my-network
```

Architecture:

```text
              my-network
        ┌─────────────────────┐
        │                     │
        │   web               │
        │    │                │
        │    │                │
        │    ↓                │
        │  database           │
        │                     │
        └─────────────────────┘
```

---

# 8. Container-to-Container Communication

One important advantage of a **user-defined bridge network** is that containers can communicate using container names.

For example:

```text
web → database
```

The application inside the `web` container can use:

```text
database
```

as the hostname.

It does not need to manually find the database container's IP address.

Docker provides automatic DNS resolution for containers on user-defined bridge networks. 
---

# 9. Isolating Containers Using Custom Networks

Custom networks can also help isolate applications.

Suppose you have two groups:

```text
Network A
┌───────────────────┐
│ frontend          │
│ backend           │
└───────────────────┘


Network B
┌───────────────────┐
│ test-app          │
│ test-db           │
└───────────────────┘
```

Containers on separate networks are not automatically connected to each other.

For example:

```bash
docker network create app-network
```

Run:

```bash
docker run -d \
  --name app \
  --network app-network \
  nginx
```

Create another network:

```bash
docker network create test-network
```

Run:

```bash
docker run -d \
  --name test \
  --network test-network \
  nginx
```

Now:

```text
app
 │
 └── app-network


test
 │
 └── test-network
```

They are attached to different networks.

This provides **network-level isolation** between the two groups.

> Important: Network isolation is not the same as complete application security. Proper application authentication, authorization, firewall rules, secrets management, and other security controls may still be required.

---

# 10. Connect a Container to Multiple Networks

A container can be connected to more than one Docker network.

For example:

```text
              Network A
                 │
                 ↓
              Backend
                 ↑
                 │
              Network B
```

Create networks:

```bash
docker network create frontend-network
docker network create backend-network
```

Run a container:

```bash
docker run -d \
  --name app \
  --network frontend-network \
  nginx
```

Connect it to another network:

```bash
docker network connect backend-network app
```

Inspect:

```bash
docker inspect app
```

The container will now have connections to both networks.

---

# 11. Remove a Network

First stop and remove the containers connected to the network:

```bash
docker stop web database
```

```bash
docker rm web database
```

Then remove the network:

```bash
docker network rm my-network
```

---

---

# 13. Complete Learning Flow

```text
Docker Container
       │
       ↓
Default Bridge Network
       │
       ↓
Inspect Network
       │
       ↓
Create Custom Bridge Network
       │
       ↓
Connect Containers
       │
       ↓
Container-to-Container Communication
       │
       ↓
Network Isolation
```

## Key Points

* Docker networking allows containers to communicate.
* Docker provides default networks when installed.
* `bridge` is the common default network driver for ordinary containers.
* User-defined bridge networks are useful for application-specific container communication.
* Containers on a user-defined bridge network can use container names for communication.
* Different networks can be used to isolate groups of containers.
* `docker network inspect` is an important command for understanding container networking.
* A container can be connected to multiple networks when required.

