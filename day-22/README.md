## Docker Installation
Windows

For Windows, the easiest approach is to install Docker Desktop.

Download Docker Desktop from:

https://www.docker.com/products/docker-desktop/

After installation, start Docker Desktop.

Verify Installation

Open CMD or PowerShell and run:

docker --version

Example:

Docker version 29.x.x

Check Docker Compose:

docker compose version
Test Docker

Run:

docker run hello-world

Docker will:

Pull hello-world image
        ↓
Create container
        ↓
Run container
        ↓
Display confirmation message

If you see the Docker welcome message, your Docker installation is working.

Basic Commands After Installation

Check Docker:

docker --version

Check running containers:

docker ps

Check all containers:

docker ps -a

List images:

docker images

## Writing Your First Dockerfile

Now let's create a very simple Docker application.

We will create a Python application that prints a message.

Step 1: Create a Project

Create a folder:

docker-first-app

Inside it:

docker-first-app/
│
├── app.py
└── Dockerfile
Step 2: Create app.py

Add:

print("Hello from my first Docker container!")
Step 3: Create Dockerfile

Create a file named exactly:

Dockerfile

Add:

FROM python:3.12

WORKDIR /app

COPY app.py .

CMD ["python", "app.py"]
Understanding Each Instruction
FROM
FROM python:3.12

Specifies the base image.

Here we are using Python 3.12.

Python 3.12 Image
       ↓
Our Application
WORKDIR
WORKDIR /app

Sets /app as the working directory inside the image/container.

Instead of working from the root directory, commands will execute from:

/app
COPY
COPY app.py .

Copies app.py from the build context on your computer into the current working directory inside the image.

Local Computer

app.py
  │
  │ COPY
  ↓
Container Image

/app/app.py
CMD
CMD ["python", "app.py"]

Specifies the default command that runs when the container starts.

In this case:

python app.py

will execute.

Build the Docker Image

Open CMD/PowerShell inside the project folder.

Run:

docker build -t my-first-app .

Docker reads the Dockerfile and creates an image.

Check the image:

docker images

You should see:

REPOSITORY      TAG       IMAGE ID
my-first-app    latest    xxxxxxxx
Run the Container

Run:

docker run --name my-first-container my-first-app

You should see:

Hello from my first Docker container!
Check the Container
docker ps -a

You will see your container.

Because the Python program finishes immediately, the container will show a stopped/exited status.

This is normal.

The container runs the command:

python app.py

The program prints the message and exits.

View Container Logs

You can see the output using:

docker logs my-first-container

Output:

Hello from my first Docker container!
Remove the Container
docker rm my-first-container

Remove the image if required:

docker rmi my-first-app
Complete Flow

The complete process you just learned is:

              app.py
                │
                ↓
            Dockerfile
                │
                ↓
       docker build -t my-first-app .
                │
                ↓
          Docker Image
          my-first-app
                │
                ↓
 docker run my-first-container
                │
                ↓
          Docker Container
                │
                ↓
    "Hello from my first Docker container!"
