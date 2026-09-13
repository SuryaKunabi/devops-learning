
# How to Create Virtual Machines

A **Virtual Machine (VM)** can be created using virtualization software, cloud platforms, or infrastructure automation tools.

There are several ways to create and manage Virtual Machines depending on the environment and requirements.


## 1. Create a VM Using VirtualBox

**Oracle VirtualBox** is a Type 2 hypervisor that allows you to create and run VMs on your local computer.

### Requirements

* Windows, Linux, or macOS host
* Oracle VirtualBox
* Operating System ISO file
* Sufficient RAM and storage

### Steps

```text
Install VirtualBox
       ↓
Create New VM
       ↓
Select OS / ISO
       ↓
Allocate CPU & RAM
       ↓
Create Virtual Disk
       ↓
Start VM
       ↓
Install Operating System
```

### Basic Process

1. Install VirtualBox.
2. Open VirtualBox.
3. Click **New**.
4. Enter the VM name.
5. Select the operating system.
6. Allocate RAM and CPU.
7. Create a virtual hard disk.
8. Attach the OS ISO file.
9. Start the VM.
10. Install the operating system.

Example:

```text
Windows Host
     |
     ↓
VirtualBox
     |
     ↓
Ubuntu VM
```


## 2. Create a VM Using VMware

**VMware Workstation** can be used to create VMs on a local computer.

### Steps

1. Install VMware Workstation.
2. Select **Create a New Virtual Machine**.
3. Select the OS ISO file.
4. Choose the VM name and location.
5. Allocate CPU and RAM.
6. Configure the virtual disk.
7. Start the VM.
8. Install the operating system.

Example:

```text
Windows / Linux Host
        |
        ↓
VMware Workstation
        |
        ↓
     Ubuntu VM
```


## 3. Create a VM Using Hyper-V

**Microsoft Hyper-V** is Microsoft's virtualization platform and is available on supported Windows editions.

### Basic Process

```text
Enable Hyper-V
      ↓
Open Hyper-V Manager
      ↓
New Virtual Machine
      ↓
Configure CPU & RAM
      ↓
Create Virtual Disk
      ↓
Attach ISO
      ↓
Start VM
```

Hyper-V can also be used to manage multiple VMs on a Windows system or server.


## 4. Create a VM Using AWS EC2

Cloud platforms allow you to create virtual servers without purchasing physical hardware.

In AWS, an **EC2 instance** is a virtual server that runs in the AWS cloud.

### Basic Process

```text
AWS Console
     ↓
EC2
     ↓
Launch Instance
     ↓
Select AMI
     ↓
Select Instance Type
     ↓
Configure Storage
     ↓
Configure Network
     ↓
Create/Select Key Pair
     ↓
Launch Instance
```

### Important Components

| Component      | Purpose                   |
| -------------- | ------------------------- |
| AMI            | Operating system/template |
| Instance Type  | CPU and RAM               |
| EBS            | Virtual storage           |
| Key Pair       | Secure login              |
| Security Group | Network access rules      |
| VPC            | Network environment       |

Example:

```text
AWS Cloud
    |
   EC2
    |
    ↓
Ubuntu Virtual Server
```

---

## 5. Create a VM Using Azure

Microsoft Azure provides virtual machines through **Azure Virtual Machines**.

### Basic Process

```text
Azure Portal
     ↓
Virtual Machines
     ↓
Create VM
     ↓
Select OS Image
     ↓
Select VM Size
     ↓
Configure Network
     ↓
Configure Authentication
     ↓
Create VM
```

Example:

```text
Azure Cloud
     |
     ↓
Azure VM
     |
     ↓
Linux / Windows
```

---

## 6. Create a VM Using Google Cloud

Google Cloud provides virtual machines through **Compute Engine**.

### Basic Process

```text
Google Cloud
      ↓
Compute Engine
      ↓
Create Instance
      ↓
Select Machine Type
      ↓
Select OS Image
      ↓
Configure Storage
      ↓
Configure Network
      ↓
Create Instance
```

---

## 7. Create VMs Using Infrastructure as Code

VMs can also be created automatically using **Infrastructure as Code (IaC)** tools.

One popular tool is **Terraform**.

Instead of manually creating a VM through a cloud console, you define the infrastructure in configuration files.

Example:

```text
Terraform Configuration
        ↓
terraform init
        ↓
terraform plan
        ↓
terraform apply
        ↓
Cloud Provider
        ↓
Virtual Machine
```

Example Terraform configuration:

```hcl
resource "aws_instance" "example" {
  ami           = "ami-xxxxxxxx"
  instance_type = "t2.micro"

  tags = {
    Name = "Terraform-VM"
  }
}
```

The exact AMI ID and instance type depend on the AWS region and current availability.

---

# Different Ways to Create Virtual Machines

| Method       | Environment    | Example          |
| ------------ | -------------- | ---------------- |
| VirtualBox   | Local computer | Ubuntu VM        |
| VMware       | Local computer | Linux/Windows VM |
| Hyper-V      | Windows        | Windows/Linux VM |
| AWS          | Cloud          | EC2              |
| Azure        | Cloud          | Azure VM         |
| Google Cloud | Cloud          | Compute Engine   |
| Terraform    | Automated/IaC  | Cloud VM         |

---

# Local VM vs Cloud VM

### Local VM

```text
Your Computer
     |
Hypervisor
     |
Virtual Machine
```

Examples:

* VirtualBox
* VMware
* Hyper-V

You provide the physical hardware.

### Cloud VM

```text
Cloud Provider
      |
Virtualization
      |
Virtual Machine
```

Examples:

* AWS EC2
* Azure VM
* Google Compute Engine

The cloud provider manages the underlying physical infrastructure.

---

# Manual vs Automated VM Creation

### Manual

```text
User
 ↓
Cloud Console
 ↓
Configure VM
 ↓
Create VM
```

### Automated

```text
Terraform Code
      ↓
terraform apply
      ↓
Cloud Provider
      ↓
VM Created
```

Automation is especially useful in **DevOps** because infrastructure can be created consistently and repeatedly.

# Key Takeaways

* VMs can be created on **local computers** using hypervisors.
* VirtualBox, VMware, and Hyper-V are common local virtualization solutions.
* Cloud providers such as AWS, Azure, and Google Cloud provide virtual servers.
* AWS uses **EC2 instances** as virtual servers.
* VMs can be created manually through cloud consoles.
* Tools such as **Terraform** can automate VM creation using Infrastructure as Code.
* The best approach depends on the environment, cost, scalability, and automation requirements.
