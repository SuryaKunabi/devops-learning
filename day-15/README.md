# Infrastructure as Code (IaC) | Terraform

Project link : https://github.com/SuryaKunabi/Terraform-projects.git

## What is Infrastructure as Code?

**Infrastructure as Code (IaC)** is the practice of creating and managing infrastructure using **code instead of manual configuration**.

Instead of manually creating servers, networks, and databases through a cloud console, we define them in configuration files.

### Traditional Approach

```text
AWS Console
    ↓
Create EC2
    ↓
Configure Network
    ↓
Configure Security
```

### IaC Approach

```text
Terraform Code
      ↓
   terraform
      ↓
Cloud Infrastructure
```

## Benefits of IaC

* Automation
* Consistency
* Faster infrastructure creation
* Version control
* Easy to reproduce environments
* Reduced manual errors
* Easy to destroy and recreate infrastructure

# What is Terraform?

**Terraform** is an open-source **Infrastructure as Code tool** developed by HashiCorp.

Terraform allows you to create and manage infrastructure using configuration files written in **HashiCorp Configuration Language (HCL)**.

Terraform can manage resources on:

* AWS
* Azure
* Google Cloud
* Kubernetes
* Other supported platforms


## Terraform Workflow

```text
Write Configuration
        ↓
terraform init
        ↓
terraform plan
        ↓
terraform apply
        ↓
Infrastructure Created
        ↓
terraform destroy
```

## Basic Terraform Project

```text
terraform-project/
├── main.tf
├── variables.tf
├── outputs.tf
└── README.md
```

### main.tf

Example of creating an AWS EC2 instance:

```hcl
provider "aws" {
  region = "ap-south-1"
}

resource "aws_instance" "web" {
  ami           = "ami-xxxxxxxx"
  instance_type = "t2.micro"
}
```

## Important Terraform Commands

### Initialize

```bash
terraform init
```

Downloads required providers and prepares the working directory.

### Validate

```bash
terraform validate
```

Checks whether the configuration is valid.

### Plan

```bash
terraform plan
```

Shows what Terraform is going to create, modify, or delete.

### Apply

```bash
terraform apply
```

Creates or updates the infrastructure.

### Destroy

```bash
terraform destroy
```

Deletes the infrastructure managed by Terraform.

## Terraform State

Terraform maintains a **state file** to track the infrastructure it manages.

```text
Terraform Code
      ↓
terraform.tfstate
      ↓
AWS Resources
```

For team environments, Terraform state can be stored remotely, for example in an **Amazon S3 bucket**.

## Key Takeaways

* **IaC** → Manage infrastructure using code.
* **Terraform** → Popular IaC tool.
* **HCL** → Language used for Terraform configuration.
* `terraform plan` → Preview changes.
* `terraform apply` → Create/update infrastructure.
* `terraform destroy` → Remove infrastructure.
* **State** → Keeps track of managed resources.

