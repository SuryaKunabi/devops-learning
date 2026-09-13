# Configuration Management with Ansible | Puppet vs Ansible

Project link : https://github.com/SuryaKunabi/Ansible-Projects.git 

## What is Configuration Management?

**Configuration Management** is the process of automatically managing and maintaining servers, applications, and system configurations.

It helps ensure that multiple servers have a **consistent and desired configuration**.

### Example

```text
Ansible Controller
       |
       ├── Web Server 1
       ├── Web Server 2
       └── Web Server 3
```

Instead of manually configuring every server, a configuration management tool can automate the process.

## What is Ansible?

**Ansible** is an open-source automation and configuration management tool.

It can be used to:

* Install packages
* Configure servers
* Deploy applications
* Manage files
* Start/stop services
* Automate repetitive tasks

Ansible uses **YAML playbooks** to define tasks.

### Basic Ansible Architecture

```text
        Ansible Controller
               |
        SSH / WinRM
               |
     ┌─────────┼─────────┐
     ↓         ↓         ↓
   Server 1  Server 2  Server 3
```

Ansible is generally **agentless**, meaning an Ansible agent does not need to be installed on managed Linux servers.

---

## What is Puppet?

**Puppet** is also a configuration management and automation tool.

It uses a **client-server architecture** and commonly uses agents on managed nodes.

```text
Puppet Server
     |
     ├── Puppet Agent
     ├── Puppet Agent
     └── Puppet Agent
```

## Puppet vs Ansible

| Feature        | Ansible             | Puppet                              |
| -------------- | ------------------- | ----------------------------------- |
| Architecture   | Agentless           | Agent-based                         |
| Configuration  | YAML                | Puppet DSL                          |
| Communication  | SSH/WinRM           | Puppet protocol                     |
| Learning Curve | Easier              | Comparatively harder                |
| Setup          | Simple              | More setup required                 |
| Automation     | Strong              | Strong                              |
| Common Use     | DevOps & automation | Enterprise configuration management |

## Ansible Example

```yaml
- name: Install Nginx
  hosts: webservers
  become: yes

  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
        update_cache: yes
```

Run the playbook:

```bash
ansible-playbook -i inventory nginx.yml
```

## Key Takeaways

* **Configuration Management** → Maintains consistent server configurations.
* **Ansible** → Simple, agentless automation tool.
* **Puppet** → Agent-based configuration management tool.
* **Ansible uses YAML** for playbooks.
* Both tools help automate infrastructure and reduce manual work.
