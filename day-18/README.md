# Jenkins on EC2 with Docker Agents

## Project Overview

This project demonstrates how to **install Jenkins on an AWS EC2 instance, configure Jenkins for external access, and use Docker containers as Jenkins build agents** instead of running jobs directly on the Jenkins VM.

The project covers the basic concepts of Jenkins, EC2, Docker Agents, and the advantages of containerized build environments.


## 🏗️ Project Architecture

```text
                    Internet
                       │
                       ▼
                ┌──────────────┐
                │   Jenkins    │
                │  EC2 Server  │
                └──────┬───────┘
                       │
                       │ Docker
                       ▼
                ┌──────────────┐
                │ Docker Agent │
                │  Container   │
                └──────────────┘
                       │
                       ▼
                 Build / Test
                    Jobs
```

## 🛠️ Technologies Used

* **AWS EC2**
* **Jenkins**
* **Docker**
* **Linux/Ubuntu**
* **Git/GitHub**
* **Jenkins Pipeline**


# 1. Install Jenkins on EC2

### Step 1: Launch an EC2 Instance

Create an Ubuntu EC2 instance in AWS.

Configure the Security Group to allow:

| Port | Purpose               |
| ---- | --------------------- |
| 22   | SSH                   |
| 8080 | Jenkins Web Interface |

> For production environments, restrict access to trusted IP addresses instead of opening ports to everyone.

### Step 2: Connect to EC2

```bash
ssh -i your-key.pem ubuntu@<EC2-PUBLIC-IP>
```

### Step 3: Update Packages

```bash
sudo apt update
sudo apt upgrade -y
```

### Step 4: Install Java

Jenkins requires Java.

```bash
sudo apt install fontconfig openjdk-21-jre -y
```

Check Java:

```bash
java -version
```

### Step 5: Install Jenkins

Add the Jenkins repository and install Jenkins:

```bash
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
```

```bash
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | \
  sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

```bash
sudo apt update
sudo apt install jenkins -y
```

### Step 6: Start Jenkins

```bash
sudo systemctl enable --now jenkins
```

Check the service:

```bash
sudo systemctl status jenkins
```

# 2. Configure Jenkins and Expose It to the Outside World

Jenkins normally runs on:

```text
http://<EC2-PUBLIC-IP>:8080
```

### Step 1: Get the Initial Admin Password

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Copy the password.

### Step 2: Open Jenkins

Open your browser:

```text
http://<EC2-PUBLIC-IP>:8080
```

Enter the initial administrator password.

### Step 3: Complete Jenkins Setup

* Install suggested plugins
* Create the Jenkins administrator account
* Configure Jenkins URL
* Open the Jenkins dashboard

### Security Note

For learning purposes, port `8080` can be opened in the EC2 Security Group.

For production, Jenkins should normally be protected using measures such as:

* HTTPS
* Reverse proxy
* Restricted Security Group rules
* Authentication
* Network controls


# 3. Use Docker as Jenkins Agents

Instead of running every Jenkins job directly on the Jenkins EC2 VM, Docker can be used to provide isolated build environments.

### VM Approach

```text
Jenkins
   │
   ▼
EC2 VM
   │
   ├── Build
   ├── Test
   └── Deploy
```

### Docker Agent Approach

```text
Jenkins EC2
    │
    ▼
 Docker
    │
    ├── Agent Container 1 → Build
    │
    ├── Agent Container 2 → Test
    │
    └── Agent Container 3 → Other Job
```

### Install Docker

```bash
sudo apt update
sudo apt install docker.io -y
```

Start Docker:

```bash
sudo systemctl enable --now docker
```

Check Docker:

```bash
docker --version
```

### Allow Jenkins to Use Docker

Add the Jenkins user to the Docker group:

```bash
sudo usermod -aG docker jenkins
```

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

You may need to log out and reconnect to the server for group membership changes to take effect.

# 4. Jenkins Pipeline Using Docker Agent

A simple Jenkins pipeline can use a Docker container as its execution environment.

Example `Jenkinsfile`:

```groovy
pipeline {
    agent {
        docker {
            image 'ubuntu:latest'
        }
    }

    stages {
        stage('Hello') {
            steps {
                sh 'echo "Hello from Docker Agent!"'
            }
        }

        stage('Check Environment') {
            steps {
                sh 'cat /etc/os-release'
            }
        }
    }
}
```

This allows the Jenkins pipeline to execute inside a Docker-based environment rather than directly on the Jenkins VM.


# 5. Advantages of Using Docker as Jenkins Agents

### 🔹 1. Isolation

Each job can run inside its own container, reducing conflicts between different builds.

### 🔹 2. Consistent Environment

The same Docker image can provide the same tools and dependencies across different builds.

### 🔹 3. Easy Dependency Management

Different projects can use different Docker images.

For example:

```text
Project A → Python Docker Image
Project B → Node.js Docker Image
Project C → Java Docker Image
```

### 🔹 4. Faster Setup

Docker containers can be created quickly compared with provisioning complete virtual machines.

### 🔹 5. Clean Build Environment

Containers can be removed after a build, helping avoid leftover dependencies and configuration changes.

### 🔹 6. Scalability

Multiple containers can be used as agents for different Jenkins jobs.

### 🔹 7. Reproducibility

Using a defined Docker image helps make builds more predictable and repeatable.


# Project Structure

```text
jenkins-docker-agent/
│
├── Jenkinsfile
└── README.md
```


# Keytakeways

* Installing Jenkins on an AWS EC2 instance
* Configuring Jenkins
* Accessing Jenkins from outside the EC2 server
* Understanding Jenkins agents
* Installing and configuring Docker
* Running Jenkins jobs using Docker-based agents
* Understanding container isolation and reproducible build environments
* Basic Jenkins Pipeline concepts



