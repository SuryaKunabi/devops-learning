# Ansible Installation, Passwordless Authentication, Playbooks & Roles

This guide covers the basics of **Ansible installation, SSH passwordless authentication, writing playbooks, and creating Ansible roles**.

## 1. Ansible Installation

Ansible is installed on the **Control Node**.

### Ubuntu/Debian

```bash
sudo apt update
sudo apt install ansible -y
```

Check the installation:

```bash
ansible --version
```

### Architecture

```text
Ansible Control Node
        |
       SSH
        |
   ┌────┴────┐
   ↓         ↓
Server 1   Server 2
```

## 2. Passwordless Authentication

Ansible commonly uses **SSH keys** to connect to Linux managed nodes without entering a password every time.

### Generate SSH Key

On the control node:

```bash
ssh-keygen
```

### Copy Public Key

```bash
ssh-copy-id user@<SERVER-IP>
```

Test the connection:

```bash
ssh user@<SERVER-IP>
```

If it connects without asking for a password, passwordless authentication is configured.

### Ansible Ping Test

```bash
ansible all -i inventory -m ping
```

## 3. Creating and Writing Playbooks

An **Ansible Playbook** is a YAML file containing tasks that Ansible executes on managed servers.

Example: `nginx.yml`

```yaml
- name: Install Nginx
  hosts: webservers
  become: yes

  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
        update_cache: yes

    - name: Start Nginx
      service:
        name: nginx
        state: started
        enabled: yes
```

Run the playbook:

```bash
ansible-playbook -i inventory nginx.yml
```

### Basic Playbook Structure

```text
Playbook
   ↓
Play
   ↓
Tasks
   ↓
Modules
   ↓
Managed Server
```

## 4. Ansible Roles

An **Ansible Role** organizes automation into a reusable directory structure.

Create a role:

```bash
ansible-galaxy role init nginx
```

### Role Structure

```text
roles/
└── nginx/
    ├── tasks/
    │   └── main.yml
    ├── handlers/
    │   └── main.yml
    ├── templates/
    ├── files/
    ├── vars/
    │   └── main.yml
    ├── defaults/
    │   └── main.yml
    └── README.md
```

### Using a Role

```yaml
- name: Configure Web Server
  hosts: webservers
  become: yes

  roles:
    - nginx
```

Run it:

```bash
ansible-playbook -i inventory site.yml
```

## Key Takeaways

* **Ansible Installation** → Install Ansible on the control node.
* **Passwordless Authentication** → Use SSH keys for secure access.
* **Playbooks** → Automate tasks using YAML.
* **Roles** → Organize and reuse Ansible automation.
* **Inventory** → Defines the managed servers.
* **Modules** → Perform specific tasks on servers.

