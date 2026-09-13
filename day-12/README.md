# Top 15 AWS Services Every DevOps Engineer Should Learn

AWS provides many cloud services that are widely used in **DevOps, Cloud Computing, CI/CD, automation, monitoring, and infrastructure management**.

## Top 15 AWS Services

| #  | AWS Service        | What It Is Used For           |
| -- | ------------------ | ----------------------------- |
| 1  | **EC2**            | Virtual servers               |
| 2  | **S3**             | Object/file storage           |
| 3  | **IAM**            | Users, roles, and permissions |
| 4  | **VPC**            | Network infrastructure        |
| 5  | **CloudWatch**     | Monitoring and logs           |
| 6  | **CloudFormation** | Infrastructure as Code        |
| 7  | **ECR**            | Store Docker container images |
| 8  | **ECS**            | Run and manage containers     |
| 9  | **EKS**            | Managed Kubernetes            |
| 10 | **Lambda**         | Serverless computing          |
| 11 | **RDS**            | Managed relational databases  |
| 12 | **Route 53**       | DNS and domain management     |
| 13 | **ELB**            | Load balancing                |
| 14 | **CodePipeline**   | CI/CD automation              |
| 15 | **CodeBuild**      | Build and test applications   |

## 1. EC2

**Amazon EC2 (Elastic Compute Cloud)** provides virtual servers in the cloud.

Common DevOps uses:

* Deploy applications
* Host web servers
* Run automation tools
* Create test environments

## 2. S3

**Amazon S3 (Simple Storage Service)** provides scalable object storage.

Used for:

* Backups
* Logs
* Static websites
* Terraform state files
* Application files

## 3. IAM

**IAM (Identity and Access Management)** manages AWS access.

Used for:

* Users
* Groups
* Roles
* Policies
* Permissions

## 4. VPC

**VPC (Virtual Private Cloud)** provides an isolated network environment.

Important concepts:

* Subnets
* Route tables
* Internet Gateway
* NAT Gateway
* Security Groups

## 5. CloudWatch

Used for **monitoring and logging** AWS resources.

```text
EC2 → CloudWatch → Metrics / Logs / Alarms
```

## 6. CloudFormation

AWS **Infrastructure as Code (IaC)** service used to create and manage AWS resources using templates.

## 7. ECR

**Elastic Container Registry** stores Docker container images.

```text
Docker Build → ECR → ECS/EKS
```

## 8. ECS

**Elastic Container Service** is used to run and manage Docker containers on AWS.

## 9. EKS

**Elastic Kubernetes Service** provides managed Kubernetes clusters.

Used for:

* Container orchestration
* Scaling applications
* Microservices

## 10. Lambda

**AWS Lambda** runs code without managing servers.

Common uses:

* Automation
* Event-driven tasks
* Serverless applications

## 11. RDS

**Relational Database Service** provides managed databases such as:

* MySQL
* PostgreSQL
* MariaDB
* Oracle
* SQL Server

## 12. Route 53

Used for **DNS and domain management**.

```text
Domain
   ↓
Route 53
   ↓
AWS Resource
```

## 13. Elastic Load Balancer

Distributes incoming traffic across multiple servers.

```text
          Load Balancer
          /     |     \
        EC2    EC2    EC2
```

## 14. CodePipeline

AWS CI/CD service used to automate the software delivery process.

```text
Code → Build → Test → Deploy
```

## 15. CodeBuild

Used to **compile, test, and package application code** as part of a CI/CD pipeline.

## DevOps Learning Order

For beginners, a good learning order is:

```text
IAM
 ↓
EC2
 ↓
S3
 ↓
VPC
 ↓
CloudWatch
 ↓
CloudFormation
 ↓
ECR → ECS/EKS
 ↓
CodeBuild → CodePipeline
```

## Key Takeaways

* **EC2** → Compute
* **S3** → Storage
* **IAM** → Security & permissions
* **VPC** → Networking
* **CloudWatch** → Monitoring
* **CloudFormation** → IaC
* **ECR/ECS/EKS** → Containers
* **CodeBuild/CodePipeline** → CI/CD

