## 1. What is a Server?

A **server** is a computer or system that provides services, resources, or data to other computers called **clients** over a network.

### Examples

* Web Server → Hosts websites
* Database Server → Stores and manages data
* File Server → Stores and shares files
* Application Server → Runs applications
* DNS Server → Converts domain names into IP addresses

### Simple Example

```text
Client
   |
   | Request
   ↓
Server
   |
   | Response
   ↓
Client
```

A server can be a **physical machine** or a **virtual machine**.

---

## 2. What is a Virtual Machine (VM)?

A **Virtual Machine (VM)** is a software-based computer that runs inside a physical computer.

A VM has virtualized:

* CPU
* RAM
* Storage
* Network interface
* Operating system

For example, you can run an **Ubuntu VM** inside a Windows computer.

```text
Physical Computer
        |
   Hypervisor
        |
   ┌────┴─────┐
   ↓          ↓
  VM 1       VM 2
 Ubuntu     Windows
```

Each VM operates like an independent computer.

---

## 3. What is a Hypervisor?

A **hypervisor** is software or firmware that creates and manages Virtual Machines.

It allows multiple VMs to share the resources of a physical computer.

### Main Responsibilities

* Creates and manages VMs
* Allocates CPU and RAM
* Manages virtual storage
* Manages virtual networking
* Isolates VMs from each other

### Types of Hypervisors

#### Type 1 — Bare-Metal Hypervisor

Runs directly on the physical hardware.

```text
Physical Hardware
       ↓
Type 1 Hypervisor
       ↓
 ┌─────┼─────┐
 VM1   VM2   VM3
```

Examples:

* VMware ESXi
* Microsoft Hyper-V
* Xen

Type 1 hypervisors are commonly used in data centers.

#### Type 2 — Hosted Hypervisor

Runs on top of a host operating system.

```text
Physical Hardware
       ↓
Host Operating System
       ↓
Type 2 Hypervisor
       ↓
    Virtual Machines
```

Examples:

* Oracle VirtualBox
* VMware Workstation

---

## 4. Physical Machine vs Virtual Machine

| Feature          | Physical Machine               | Virtual Machine           |
| ---------------- | ------------------------------ | ------------------------- |
| Hardware         | Dedicated physical hardware    | Uses virtual hardware     |
| CPU              | Physical CPU                   | Virtual CPU               |
| RAM              | Physical RAM                   | Allocated virtual RAM     |
| Storage          | Physical disk                  | Virtual disk              |
| Operating System | Installed directly on hardware | Runs through a hypervisor |
| Resource Sharing | Usually dedicated              | Shared with other VMs     |
| Setup            | Takes more time                | Usually faster            |
| Cost             | Higher                         | Lower                     |
| Scalability      | Limited by hardware            | Easy to scale             |
| Migration        | More difficult                 | Easier                    |
| Isolation        | Hardware-level                 | Software-level isolation  |

---

## 5. Advantages of Virtual Machines

### 1. Better Resource Utilization

Multiple VMs can share the resources of a single physical server.

```text
        Physical Server
        CPU + RAM + Storage
              |
       ┌──────┼──────┐
       ↓      ↓      ↓
      VM1    VM2    VM3
```

This reduces unused hardware resources.

### 2. Cost Reduction

Instead of purchasing separate physical servers for different applications, multiple VMs can run on one physical server.

### 3. Easy to Create

VMs can be created and configured much faster than physical servers.

### 4. Isolation

Each VM operates independently.

If one VM experiences a problem, other VMs can continue running.

### 5. Easy Backup and Recovery

VMs can be backed up, copied, or restored more easily than physical machines.

### 6. Scalability

CPU, RAM, and storage can usually be adjusted according to application requirements.

### 7. Testing and Development

Developers and system administrators can create separate VMs for testing different operating systems and applications.

### 8. Easy Migration

Virtual machines can often be moved between compatible physical hosts, depending on the virtualization platform.

---

## 6. Physical Server vs Virtualization

### Without Virtualization

```text
Server 1 → Application 1
Server 2 → Application 2
Server 3 → Application 3
```

This can result in underutilized hardware.

### With Virtualization

```text
             Physical Server
                    |
               Hypervisor
          ┌─────────┼─────────┐
          ↓         ↓         ↓
        VM 1      VM 2      VM 3
     App 1      App 2      App 3
```

Multiple workloads can share the same physical server.

---

## 7. Key Takeaways

* **Server** → Provides services or resources to clients.
* **VM** → A software-based computer running on a physical system.
* **Hypervisor** → Creates and manages virtual machines.
* **Physical Machine** → Uses dedicated physical hardware.
* **Virtual Machine** → Uses virtualized hardware provided by a hypervisor.
* **Virtualization** → Improves resource utilization, scalability, isolation, and flexibility.


