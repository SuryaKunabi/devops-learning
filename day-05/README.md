# AWS CLI Full Guide | EC2 Connection | AWS CloudFormation

# 1. What is AWS CLI?

**AWS Command Line Interface (AWS CLI)** is a command-line tool that allows you to interact with AWS services using commands.

Instead of using the AWS Management Console, you can manage AWS resources from a terminal.

### AWS Console vs AWS CLI

```text
AWS Console
     |
     ↓
Web Browser
     |
     ↓
AWS Resources
```

```text
AWS CLI
     |
     ↓
Terminal
     |
     ↓
AWS API
     |
     ↓
AWS Resources
```

# 2. Install AWS CLI

After installing AWS CLI, verify the installation:

```bash
aws --version
```

Example:

```text
aws-cli/2.x.x Python/3.x.x Linux/x86_64
```

# 3. Configure AWS CLI

Use:

```bash
aws configure
```

You will be asked for:

```text
AWS Access Key ID:
AWS Secret Access Key:
Default region name:
Default output format:
```

Example:

```text
AWS Access Key ID: ********
AWS Secret Access Key: ********
Default region name: ap-south-1
Default output format: json
```

> **Security:** Never upload AWS access keys or secret keys to GitHub.

# 4. Verify AWS CLI Connection

Check your configured identity:

```bash
aws sts get-caller-identity
```

Example output:

```json
{
    "UserId": "AIDAXXXXXXXXX",
    "Account": "123456789012",
    "Arn": "arn:aws:iam::123456789012:user/example"
}
```

This confirms that the AWS CLI is authenticated.

# 5. Useful AWS CLI Commands

### List S3 Buckets

```bash
aws s3 ls
```

### List EC2 Instances

```bash
aws ec2 describe-instances
```

### List EC2 Instances in a readable format

```bash
aws ec2 describe-instances \
--query "Reservations[].Instances[].{ID:InstanceId,State:State.Name,IP:PublicIpAddress}" \
--output table
```

### List IAM Users

```bash
aws iam list-users
```

### List Lambda Functions

```bash
aws lambda list-functions
```

# 6. Connect to EC2 from AWS Console UI

You can connect to a supported EC2 instance directly from the AWS Management Console.

### Steps

```text
AWS Console
     ↓
EC2
     ↓
Instances
     ↓
Select Instance
     ↓
Connect
     ↓
Choose Connection Method
```

Depending on the instance and configuration, AWS may provide options such as:

* EC2 Instance Connect
* Session Manager
* SSH client

For EC2 Instance Connect, choose the appropriate connection option and select **Connect**.


# 7. Connect to EC2 from Terminal Using SSH

For a Linux EC2 instance, SSH is a common way to connect from a terminal.

### Step 1 — Change key permissions

On Linux/macOS:

```bash
chmod 400 mykey.pem
```

### Step 2 — Connect using SSH

```bash
ssh -i mykey.pem ubuntu@YOUR_EC2_PUBLIC_IP
```

Example:

```bash
ssh -i mykey.pem ubuntu@13.234.XX.XX
```

The username depends on the AMI. For example, Ubuntu AMIs commonly use:

```text
ubuntu
```

Amazon Linux commonly uses:

```text
ec2-user
```

# 8. EC2 SSH Connection Flow

```text
Your Computer
     |
     | SSH
     ↓
Internet
     |
     ↓
EC2 Security Group
     |
     | Port 22
     ↓
EC2 Instance
     |
     ↓
Linux Terminal
```

For SSH access, the instance's network configuration and security group must allow the connection.


# 9. Important EC2 Information

Before connecting, you generally need:

| Requirement          | Purpose                     |
| -------------------- | --------------------------- |
| Public IP/DNS        | Identifies the EC2 instance |
| Private key (`.pem`) | SSH authentication          |
| Username             | OS login account            |
| Port 22              | SSH connection              |
| Security Group       | Controls inbound traffic    |

---

# 10. What is AWS CloudFormation?

**AWS CloudFormation (CFT)** is an Infrastructure as Code (IaC) service used to create and manage AWS resources using templates.

Instead of manually creating resources through the AWS Console, you define them in a template.

```text
CloudFormation Template
        ↓
CloudFormation
        ↓
AWS Resources
```

For example:

```text
Template
   ↓
VPC
   ↓
Subnet
   ↓
Security Group
   ↓
EC2
```

# 11. CloudFormation Template

CloudFormation templates can be written in **YAML** or **JSON**.

Example:

```yaml
AWSTemplateFormatVersion: '2010-09-09'

Description: Create a simple EC2 instance

Resources:

  MyEC2Instance:
    Type: AWS::EC2::Instance

    Properties:
      ImageId: ami-xxxxxxxx
      InstanceType: t2.micro

      Tags:
        - Key: Name
          Value: CloudFormation-EC2
```

> Replace `ami-xxxxxxxx` with a valid AMI ID for your AWS region.


# 12. CloudFormation Walkthrough

### Step 1 — Create Template

Create a file:

```bash
touch ec2.yml
```

Add your CloudFormation configuration.


### Step 2 — Open CloudFormation

AWS Console:

```text
AWS Console
     ↓
CloudFormation
     ↓
Create Stack
```

Select the option to create a stack with existing resources (standard workflow), then provide your template.


### Step 3 — Upload Template

```text
CloudFormation
      ↓
Create Stack
      ↓
Upload Template
      ↓
Choose File
      ↓
ec2.yml
```


### Step 4 — Enter Stack Name

Example:

```text
Stack Name:
my-ec2-stack
```

### Step 5 — Review Configuration

Review:

* Template
* Stack name
* Parameters
* Resources
* Permissions

Then create the stack.

# 13. CloudFormation Stack

CloudFormation creates a **stack** containing the resources defined in your template.

```text
             CloudFormation Stack
                     |
          ┌──────────┼──────────┐
          ↓          ↓          ↓
        EC2         S3         IAM
      Instance     Bucket       Role
```

You can manage these resources through the stack.


# 14. CloudFormation Using AWS CLI

You can also create a stack using the AWS CLI.

```bash
aws cloudformation create-stack \
--stack-name my-ec2-stack \
--template-body file://ec2.yml
```

Check the stack:

```bash
aws cloudformation describe-stacks \
--stack-name my-ec2-stack
```

List stacks:

```bash
aws cloudformation list-stacks
```

# 15. Delete CloudFormation Stack

When you no longer need the resources:

```bash
aws cloudformation delete-stack \
--stack-name my-ec2-stack
```

Check the stack status:

```bash
aws cloudformation describe-stacks \
--stack-name my-ec2-stack
```

Deleting the stack can also delete resources managed by that stack, depending on their configuration and deletion policies.


# 16. AWS CLI vs CloudFormation

| Feature             | AWS CLI                      | CloudFormation            |
| ------------------- | ---------------------------- | ------------------------- |
| Type                | Command-line tool            | IaC service               |
| Interaction         | Commands                     | Template                  |
| Automation          | Yes                          | Yes                       |
| Repeatability       | Moderate                     | High                      |
| Resource Management | Individual commands          | Stack-based               |
| Configuration       | CLI commands/options         | YAML/JSON                 |
| Best Use            | Quick operations & scripting | Infrastructure deployment |


# 17. Complete Workflow

```text
                 AWS
                  |
       ┌──────────┴──────────┐
       ↓                     ↓
   AWS Console            AWS CLI
       |                     |
       ↓                     ↓
    EC2 UI              AWS Commands
       |                     |
       └──────────┬──────────┘
                  ↓
              EC2 Instance
                  |
                  ↓
              SSH / Session
                  |
                  ↓
              EC2 Server
```

For infrastructure automation:

```text
CloudFormation Template
          ↓
    CloudFormation
          ↓
    AWS Resources
          ↓
       EC2 / S3
       VPC / IAM
```

# 18. Key Takeaways

* **AWS CLI** allows you to manage AWS services from the terminal.
* `aws configure` is used to configure CLI credentials and defaults.
* `aws sts get-caller-identity` can verify the current AWS identity.
* EC2 Linux instances can commonly be accessed using **SSH**.
* AWS Console provides browser-based EC2 connection options.
* **CloudFormation** is an AWS Infrastructure as Code service.
* CloudFormation templates can be written in **YAML or JSON**.
* A CloudFormation **stack** manages the resources defined by the template.
* AWS CLI and CloudFormation can both be used to automate AWS operations.

