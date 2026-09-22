# GitHub Actions

## What is GitHub Actions?

GitHub Actions is a CI/CD and automation platform provided by GitHub. It allows you to automatically build, test, and deploy applications when specific events occur in a GitHub repository.

Common events include:

* Push to a branch
* Pull request
* Release creation
* Scheduled tasks
* Manual workflow execution

---

## Why Use GitHub Actions?

GitHub Actions can be used to:

* Automate build and testing
* Automate application deployment
* Implement CI/CD pipelines
* Run security and code-quality checks
* Automate repetitive tasks
* Integrate with AWS, Azure, Google Cloud, Docker, and other tools
* Manage CI/CD directly from a GitHub repository

### Example CI/CD Flow

```text
Developer
    |
    v
GitHub Repository
    |
    v
GitHub Actions
    |
    +----> Build
    |
    +----> Test
    |
    +----> Deploy
    |
    v
Production
```

---

## When Should You Use GitHub Actions?

GitHub Actions is useful when you need to:

* Run tests automatically after code changes
* Build applications automatically
* Deploy applications to cloud servers
* Build and push Docker images
* Perform security checks
* Automate GitHub repository tasks
* Create CI/CD pipelines for GitHub projects

For example:

```text
Push Code
    |
    v
Run Tests
    |
    v
Build Application
    |
    v
Build Docker Image
    |
    v
Deploy to AWS
```

---

# GitHub Actions vs Jenkins

| Feature            | GitHub Actions                  | Jenkins                                 |
| ------------------ | ------------------------------- | --------------------------------------- |
| Platform           | Integrated with GitHub          | Independent CI/CD server                |
| Setup              | Easy                            | Requires installation and configuration |
| Server Management  | GitHub-hosted runners available | Usually managed by the user             |
| Configuration      | YAML                            | Jenkinsfile / UI                        |
| GitHub Integration | Built-in                        | Requires configuration/plugins          |
| Extensions         | GitHub Marketplace              | Large plugin ecosystem                  |
| Runners/Agents     | GitHub-hosted or self-hosted    | Jenkins agents                          |
| Maintenance        | Lower with hosted runners       | More maintenance required               |
| Best suited for    | GitHub-based projects           | Highly customizable CI/CD environments  |

---

## Basic GitHub Actions Workflow

GitHub Actions workflow files are stored inside:

```text
.github/workflows/
```

Example:

```yaml
name: CI Pipeline

on:
  push:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Run Test
        run: echo "Running tests..."

      - name: Build
        run: echo "Building application..."
```

---

## Important GitHub Actions Concepts

### Workflow

A YAML file that defines an automated process.

### Event

Defines when a workflow should run.

Example:

```yaml
on:
  push:
    branches:
      - main
```

### Job

A group of steps that run together on a runner.

### Step

An individual task inside a job.

### Action

A reusable component that performs a specific task.

Example:

```yaml
uses: actions/checkout@v4
```

### Runner

The machine that executes the workflow.

Common GitHub-hosted runners include:

```text
ubuntu-latest
windows-latest
macos-latest
```

---

## GitHub Actions CI/CD Flow

```text
Developer
    |
    v
Git Push
    |
    v
GitHub Repository
    |
    v
GitHub Actions
    |
    +----> Checkout Code
    |
    +----> Build
    |
    +----> Test
    |
    +----> Docker Build
    |
    +----> Deploy
    |
    v
Production
```

---

## GitHub Actions vs Jenkins - Simple Understanding

### GitHub Actions

```text
GitHub
   |
   v
GitHub Actions
   |
   +----> Build
   |
   +----> Test
   |
   +----> Deploy
```

### Jenkins

```text
GitHub
   |
   v
Jenkins Server
   |
   +----> Controller
   |
   +----> Agents
             |
             +----> Build
             +----> Test
             +----> Deploy
```

---

## Conclusion

GitHub Actions provides CI/CD and automation directly within GitHub. It is useful for automating builds, tests, deployments, and other development tasks.

Jenkins is a separate CI/CD automation server that provides extensive customization and a large plugin ecosystem.

Both GitHub Actions and Jenkins can be used to create CI/CD pipelines depending on the project requirements.

