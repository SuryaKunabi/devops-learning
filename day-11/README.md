# AWS IAM, EC2 & Application Deployment

This project covers the basic process of creating an **IAM user**, launching an **EC2 instance**, accessing it, deploying an application, and making it accessible from the internet.

## Topics Covered

1. Create an IAM User and Login
2. Create an EC2 Instance and follow best practices
3. Access the EC2 Instance
4. Deploy an Application on EC2
5. Expose the Application to the Internet
6. Access the Application from a Laptop

## 1. Create IAM User and Login

IAM (Identity and Access Management) is used to manage users and permissions in AWS.

Basic steps:

```text
AWS Console
    ↓
IAM
    ↓
Create User
    ↓
Assign Permissions
    ↓
Create User
    ↓
Login
```

**Best Practice:**

* Give users only the permissions they need.
* Enable MFA.
* Avoid using the root account for daily activities.
* Use IAM roles for AWS services whenever possible.


## 2. Create an EC2 Instance

EC2 provides virtual servers in AWS.

Basic steps:

```text
AWS Console
    ↓
EC2
    ↓
Launch Instance
    ↓
Choose AMI
    ↓
Choose Instance Type
    ↓
Create/Select Key Pair
    ↓
Configure Security Group
    ↓
Launch Instance
```

### EC2 Best Practices

* Use the appropriate instance size.
* Allow only required ports.
* Use SSH keys instead of passwords.
* Keep the operating system updated.
* Stop or terminate unused instances.
* Use IAM roles instead of storing AWS credentials on the server.


## 3. Access the EC2 Instance

For a Linux EC2 instance, SSH can be used.

```bash
ssh -i my-key.pem ubuntu@<PUBLIC-IP>
```

Example:

```bash
ssh -i aws-key.pem ubuntu@54.123.45.67
```

After successful login:

```bash
whoami
hostname
```


## 4. Deploy an Application on EC2

Example: Deploy a simple web application using Nginx.

### Install Nginx

```bash
sudo apt update
sudo apt install nginx -y
```

### Start Nginx

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

### Check Status

```bash
sudo systemctl status nginx
```

The application/web page can be placed in:

```text
/var/www/html/
```

## 5. Expose the Application to the Internet

Configure the EC2 **Security Group** to allow HTTP traffic.

```text
Internet
   ↓
Port 80
   ↓
Security Group
   ↓
EC2 Instance
   ↓
Nginx
   ↓
Application
```

Example inbound rule:

| Type | Protocol | Port | Source    |
| ---- | -------- | ---: | --------- |
| HTTP | TCP      |   80 | 0.0.0.0/0 |
| SSH  | TCP      |   22 | Your IP   |

> Avoid opening SSH (port 22) to `0.0.0.0/0` unless absolutely necessary.


## 6. Access the Application from Laptop

Open a browser on your laptop and enter:

```text
http://<EC2-PUBLIC-IP>
```

Example:

```text
http://54.123.45.67
```

The request follows:

```text
Laptop
   ↓
Internet
   ↓
EC2 Public IP
   ↓
Security Group
   ↓
Nginx
   ↓
Application
```

## Complete Workflow

```text
IAM User
   ↓
EC2 Instance
   ↓
SSH Access
   ↓
Install Nginx
   ↓
Deploy Application
   ↓
Configure Security Group
   ↓
Expose Port 80
   ↓
Access from Laptop
```

## Key Takeaways

* **IAM** → Manages users and permissions.
* **EC2** → Provides virtual servers.
* **SSH** → Used to access Linux EC2 instances.
* **Nginx** → Can serve web applications.
* **Security Group** → Controls network access.
* **Public IP** → Allows the application to be accessed from the internet.

