
# Docker Containerization

## 1. What is Containerization?

**Containerization** is the process of packaging an application together with everything it needs to run, such as:

* Application code
* Runtime
* Libraries
* Dependencies
* Configuration

This package is created as a **Docker image** and can then be run as a **Docker container**.

The main purpose is to make the application run consistently across different environments.

### Simple Flow

```text
Application
     ↓
Dockerfile
     ↓
Docker Image
     ↓
Docker Container
     ↓
Running Application
```

---

# 2. What is a Container?

A **container** is a running instance of a Docker image.

For example:

```text
Docker Image
     ↓
 docker run
     ↓
Docker Container
     ↓
Application Running
```

A container provides an isolated environment for the application, including its own filesystem, networking, and process environment.

---

# 3. Why Containerize an Application?

Without containerization, an application may require manual installation of:

```text
Python / Node.js / Java
        +
Libraries
        +
Dependencies
        +
Configuration
```

This can cause problems when moving the application to another machine.

With containerization:

```text
Application
    +
Dependencies
    +
Runtime
    ↓
Docker Image
    ↓
Container
```

The application can then be run using the same image in different environments.

---

# 4. How to Create a Container

There are two common situations.

### Using an Existing Image

You can create and start a container directly from an existing image:

```bash
docker run nginx
```

Docker uses the `nginx` image to create and start a container.

Check running containers:

```bash
docker ps
```

Check all containers:

```bash
docker ps -a
```

Stop the container:

```bash
docker stop <container-name-or-id>
```

Remove the container:

```bash
docker rm <container-name-or-id>
```

---

# 5. How to Containerize an Application

To containerize your own application, you normally create a **Dockerfile**.

A Dockerfile contains instructions that Docker uses to build an image.

### Example Python Application

Project:

```text
python-app/
│
├── app.py
├── requirements.txt
└── Dockerfile
```

---

## 6. Create the Application

### `app.py`

```python
print("Hello from my containerized application!")
```

For a web application, the application would normally start a web server instead.

---

# 7. Create a Dockerfile

Create a file named:

```text
Dockerfile
```

Do not add a file extension.

Example:

```dockerfile
FROM python:3.12

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["python", "app.py"]
```

### Dockerfile Explanation

#### `FROM`

```dockerfile
FROM python:3.12
```

Provides the Python runtime that the application needs.

#### `WORKDIR`

```dockerfile
WORKDIR /app
```

Sets the working directory inside the image.

#### `COPY`

```dockerfile
COPY requirements.txt .
```

Copies the dependency file into the image.

```dockerfile
COPY . .
```

Copies the application files into the image.

#### `RUN`

```dockerfile
RUN pip install --no-cache-dir -r requirements.txt
```

Installs the Python dependencies while building the image.

#### `CMD`

```dockerfile
CMD ["python", "app.py"]
```

Defines the default command that runs when the container starts.

---

# 8. Build the Docker Image

Open the terminal inside the project directory:

```bash
cd python-app
```

Build the image:

```bash
docker build -t my-python-app .
```

Explanation:

```text
docker build
     ↓
Build an image

-t my-python-app
     ↓
Name the image

.
     ↓
Current directory
```

Docker reads the Dockerfile and creates the image from it.

Check the image:

```bash
docker images
```

You should see:

```text
REPOSITORY       TAG       IMAGE ID
my-python-app    latest    xxxxxxxxx
```

---

# 9. Create and Run the Container

Now create a container from the image:

```bash
docker run --name my-python-container my-python-app
```

The complete process is:

```text
       app.py
          │
          ↓
     Dockerfile
          │
          ↓
   docker build
          │
          ↓
    Docker Image
          │
          ↓
     docker run
          │
          ↓
 Docker Container
          │
          ↓
 Application Running
```

---

# 10. Containerizing a Web Application

For a web application, the process is similar.

For example:

```text
my-web-app/
│
├── app.py
├── requirements.txt
└── Dockerfile
```

The application might run on port `5000`.

Dockerfile:

```dockerfile
FROM python:3.12

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

Build the image:

```bash
docker build -t my-web-app .
```

Run the container:

```bash
docker run -d -p 5000:5000 --name my-web-container my-web-app
```

The `-p` option maps a port on the host to a port in the container. Docker documents this as publishing the container port to the Docker host.

```text
Your Computer
localhost:5000
      │
      ↓
Docker Container
port 5000
      │
      ↓
Web Application
```

You can then access the application through:

```text
http://localhost:5000
```

---

# 11. Check the Container

List running containers:

```bash
docker ps
```

View container logs:

```bash
docker logs my-web-container
```

Stop the container:

```bash
docker stop my-web-container
```

Start it again:

```bash
docker start my-web-container
```

Remove it:

```bash
docker rm my-web-container
```

---

# 12. Containerization Workflow

The complete containerization workflow is:

```text
1. Develop Application
          ↓
2. Create Dockerfile
          ↓
3. docker build
          ↓
4. Docker Image
          ↓
5. docker run
          ↓
6. Docker Container
          ↓
7. Application Running
```


Repository : https://github.com/SuryaKunabi/docker-projects/tree/main/python-web-app

---


---

