# Docker Compose

## What is Docker Compose?

**Docker Compose** is a tool used to define and run multiple Docker containers as a single application.

Instead of running each container separately, we can define all the services in a `compose.yaml` file and start them using one command.

### Example

```text
Docker Compose
      |
      ├── Web Container
      ├── Backend Container
      └── Database Container
```

---

## Why use Docker Compose?

Docker Compose is useful when an application requires multiple containers.

For example:

```text
Frontend
   |
Backend
   |
Database
```

Docker Compose allows us to configure these services in one YAML file.

### Benefits

- Run multiple containers with one command
- Easy configuration using YAML
- Creates a network between services automatically
- Easy to start and stop the application
- Useful for development and testing
- Supports volumes, ports, environment variables, and dependencies

---

# Basic Docker Compose Example

Create a file named:

```text
compose.yaml
```

Add the following configuration:

```yaml
services:

  web:
    image: nginx
    ports:
      - "8080:80"

  redis:
    image: redis
```

This configuration creates two services:

```text
web
 ↓
Nginx

redis
 ↓
Redis
```

---

# Run the Application

Open CMD or PowerShell in the directory containing `compose.yaml`.

### Start containers

```bash
docker compose up
```

### Run in background

```bash
docker compose up -d
```

The `-d` option runs the containers in detached mode.

---

# Check Running Containers

```bash
docker compose ps
```

You can also use:

```bash
docker ps
```

---

# Access the Web Application

The example maps:

```text
localhost:8080 → Nginx port 80
```

Open:

```text
http://localhost:8080
```

You should see the Nginx welcome page.

---

# View Logs

To view logs:

```bash
docker compose logs
```

To continuously watch the logs:

```bash
docker compose logs -f
```

Press `Ctrl + C` to stop watching the logs.

---

# Stop the Application

To stop and remove the containers:

```bash
docker compose down
```

---

# Important Commands

| Command | Purpose |
|---|---|
| `docker compose up` | Start services |
| `docker compose up -d` | Start services in background |
| `docker compose down` | Stop and remove services |
| `docker compose ps` | Show running services |
| `docker compose logs` | View logs |
| `docker compose logs -f` | Follow logs |
| `docker compose restart` | Restart services |
| `docker compose stop` | Stop services |
| `docker compose start` | Start stopped services |
| `docker compose build` | Build images |

---







