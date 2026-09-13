# Terraform Use-Cases

Terraform is an **Infrastructure as Code (IaC)** tool used to create, manage, and automate cloud infrastructure using configuration files.

Project link : https://github.com/SuryaKunabi/Terraform-projects.git

## Topics Covered

* Terraform Use-Cases
* Terraform Lifecycle
* First Terraform Project
* Terraform State File
* Terraform Best Practices
* Terraform Modules

## 1. Terraform Use-Cases

Terraform can be used to:

* Create AWS EC2 instances
* Create VPCs, subnets, and security groups
* Manage S3 buckets
* Create databases
* Manage cloud infrastructure
* Automate infrastructure deployment
* Create consistent development and production environments

```text
Terraform Code
      ↓
   Provider
      ↓
Cloud Infrastructure
```

# 2. Terraform Lifecycle

Terraform follows a simple workflow:

```text
Write Code
    ↓
terraform init
    ↓
terraform validate
    ↓
terraform plan
    ↓
terraform apply
    ↓
Infrastructure
    ↓
terraform destroy
```

### Important Commands

```bash
terraform init
terraform validate
terraform plan
terraform apply
terraform destroy
```

* **init** → Initializes the Terraform project.
* **validate** → Checks the configuration.
* **plan** → Shows proposed changes.
* **apply** → Creates or updates infrastructure.
* **destroy** → Removes managed infrastructure.

---

# 3. Write Your First Terraform Project

### Project Structure

```text
terraform-project/
├── main.tf
├── variables.tf
├── outputs.tf
└── README.md
```

### `main.tf`

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

### Run the Project

```bash
terraform init
terraform validate
terraform plan
terraform apply
```

After completing the project, infrastructure can be removed using:

```bash
terraform destroy
```

# 4. Terraform State File

Terraform uses a **state file** to keep track of the infrastructure it manages.

The default state file is:

```text
terraform.tfstate
```

### How It Works

```text
Terraform Configuration
        ↓
Terraform State
        ↓
AWS Resources
```

The state file helps Terraform understand:

* Which resources exist
* Resource IDs
* Current configuration
* Changes that need to be made

### Remote State

For team environments, state can be stored remotely, such as in an **Amazon S3 bucket**.

# 5. Terraform Best Practices

Some important practices are:

* Use variables instead of hardcoding values.
* Use `.tfvars` files for variable values.
* Use modules for reusable infrastructure.
* Store Terraform code in Git.
* Use remote state for team projects.
* Do not commit sensitive information.
* Use meaningful resource names.
* Run `terraform fmt` regularly.
* Run `terraform validate` before applying changes.
* Review `terraform plan` before `terraform apply`.

Example:

```bash
terraform fmt
terraform validate
terraform plan
terraform apply
```

# 6. Terraform Modules

A **Terraform module** is a collection of Terraform configuration files that can be reused.

Modules help organize large Terraform projects and avoid repeating code.

### Example Structure

```text
terraform-project/
├── main.tf
├── variables.tf
├── outputs.tf
└── modules/
    └── ec2/
        ├── main.tf
        ├── variables.tf
        └── outputs.tf
```

### Using a Module

```hcl
module "web_server" {
  source = "./modules/ec2"

  instance_type = "t2.micro"
}
```

### Module Workflow

```text
Root Module
     ↓
EC2 Module
     ↓
AWS EC2 Instance
```

## Key Takeaways

* **Terraform** → Infrastructure as Code.
* **Lifecycle** → init → validate → plan → apply → destroy.
* **State File** → Tracks managed infrastructure.
* **Best Practices** → Use variables, modules, Git, remote state, and validation.
* **Modules** → Make Terraform code reusable and organized.

