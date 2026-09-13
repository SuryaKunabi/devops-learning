# Git and GitHub

# 1. What is Git?

**Git** is a distributed **Version Control System (VCS)** used to track changes in files and source code.

Git allows developers to:

* Track changes
* Create versions of code
* Work on different features using branches
* Revert changes
* Collaborate with other developers
* Maintain project history

Git works locally on your computer, so you can use most Git features without an internet connection.


# 2. What is Version Control?

**Version Control** is a system used to track and manage changes made to files over time.

For example, imagine manually saving files:

```text
project_v1
project_v2
project_final
project_final_new
project_final_latest
```

This becomes difficult to manage.

With Git:

```text
Version 1
   ↓
Version 2
   ↓
Version 3
   ↓
Version 4
```

Git maintains the history of changes and allows you to move between versions when required.


# 3. Why is Version Control Needed?

Version control helps developers:

### Track Changes

You can see what changes were made and when.

### Restore Previous Versions

If a new change causes a problem, you can return to an earlier version.

### Collaboration

Multiple developers can work on the same project.

### Branching

Developers can create separate branches for features or fixes.

### Backup

A remote repository such as GitHub can store a copy of the project.


# 4. What is GitHub?

**GitHub** is a cloud-based platform used to host and collaborate on Git repositories.

Git and GitHub are not the same.

```text
Git
 ↓
Version Control System
 ↓
Runs on your computer
```

```text
GitHub
 ↓
Online platform
 ↓
Hosts Git repositories
 ↓
Collaboration
```

GitHub provides features such as:

* Remote repositories
* Pull Requests
* Issues
* Code Reviews
* Collaboration
* Project management
* GitHub Actions for CI/CD


# 5. Git vs GitHub

| Git                                         | GitHub                                        |
| ------------------------------------------- | --------------------------------------------- |
| Version Control System                      | Git hosting and collaboration platform        |
| Runs locally                                | Primarily cloud-based                         |
| Tracks code changes                         | Hosts Git repositories                        |
| Works without internet for local operations | Requires network access for remote operations |
| Developed as Git software                   | Platform built around Git                     |


# 6. Git Workflow

A basic Git workflow looks like this:

```text
Working Directory
       ↓
      git add
       ↓
Staging Area
       ↓
    git commit
       ↓
Local Repository
       ↓
     git push
       ↓
GitHub Repository
```

# 7. Install Git

Check whether Git is installed:

```bash
git --version
```

Example:

```text
git version 2.x.x
```


# 8. Configure Git

Set your username:

```bash
git config --global user.name "Your Name"
```

Set your email:

```bash
git config --global user.email "your-email@example.com"
```

Check the configuration:

```bash
git config --list
```

# 9. Create a Git Repository

Go to your project directory:

```bash
cd my-project
```

Initialize Git:

```bash
git init
```

This creates a hidden `.git` directory.

```text
my-project/
├── .git/
├── index.html
└── style.css
```

The `.git` directory contains the information Git uses to track the repository.


# 10. Check Repository Status

Use:

```bash
git status
```

This shows:

* Modified files
* New files
* Staged files
* Current branch


# 11. Add Files to Staging

Add a specific file:

```bash
git add index.html
```

Add all files:

```bash
git add .
```

The staging area allows you to select which changes should be included in the next commit.

# 12. Commit Changes

A commit saves a snapshot of your staged changes.

```bash
git commit -m "Add website files"
```

Good commit messages should clearly describe the change.

Examples:

```bash
git commit -m "Add login page"
```

```bash
git commit -m "Update website styling"
```

# 13. View Commit History

Use:

```bash
git log
```

A shorter version:

```bash
git log --oneline
```

Example:

```text
a82f123 Update website styling
b71c456 Add website files
```

# 14. Git Branches

A **branch** allows you to work on changes separately from the main development line.

Example:

```text
             feature-login
                  |
                  ↓
main ─────────────●──────────
                  |
             feature work
```

Create a branch:

```bash
git branch feature-login
```

Switch to it:

```bash
git switch feature-login
```

Or create and switch in one command:

```bash
git switch -c feature-login
```

# 15. Merge

After completing work on a branch, you can merge it into another branch.

Switch to the main branch:

```bash
git switch main
```

Merge the feature branch:

```bash
git merge feature-login
```

Basic workflow:

```text
main
 |
 └── feature-login
       |
       | Development
       ↓
    git merge
       |
       ↓
     main
```

# 16. GitHub Repository

To upload your local project to GitHub:

```text
Local Project
     ↓
   git add
     ↓
 git commit
     ↓
 git push
     ↓
GitHub Repository
```

First create a repository on GitHub.

Then connect your local repository to the remote repository:

```bash
git remote add origin https://github.com/USERNAME/REPOSITORY.git
```

Check the remote:

```bash
git remote -v
```

# 17. Push Code to GitHub

For the first push:

```bash
git push -u origin main
```

After that, you can normally use:

```bash
git push
```

# 18. Clone a Repository

`git clone` downloads an existing Git repository to your computer.

```bash
git clone https://github.com/USERNAME/REPOSITORY.git
```

Example:

```text
GitHub Repository
       ↓
   git clone
       ↓
Local Computer
```

# 19. Pull Changes

`git pull` downloads changes from the remote repository and integrates them into your current branch.

```bash
git pull
```

Basic workflow:

```text
GitHub
  ↓
git pull
  ↓
Local Repository
```

# 20. Git Push vs Git Pull

| Command     | Purpose                                   |
| ----------- | ----------------------------------------- |
| `git push`  | Upload local commits to remote repository |
| `git pull`  | Download and integrate remote changes     |
| `git clone` | Copy an existing remote repository        |
| `git fetch` | Download remote changes without merging   |


# 21. Git Areas

Git mainly works with three areas:

```text
Working Directory
       |
       | git add
       ↓
Staging Area
       |
       | git commit
       ↓
Local Repository
       |
       | git push
       ↓
Remote Repository
```

### Working Directory

Files you are currently working on.

### Staging Area

Files selected for the next commit.

### Local Repository

Commits stored on your computer.

### Remote Repository

Repository hosted on a remote platform such as GitHub.


# 22. Common Git Commands

| Command         | Purpose                        |
| --------------- | ------------------------------ |
| `git init`      | Initialize a repository        |
| `git status`    | Check repository status        |
| `git add .`     | Stage all changes              |
| `git commit`    | Save changes                   |
| `git log`       | View commit history            |
| `git branch`    | Manage branches                |
| `git switch`    | Switch branches                |
| `git merge`     | Merge branches                 |
| `git clone`     | Clone a repository             |
| `git remote -v` | View remote repositories       |
| `git push`      | Upload changes                 |
| `git pull`      | Download and integrate changes |
| `git fetch`     | Download remote changes        |


# 23. Basic Git Workflow Example

```bash
# Create project directory
mkdir my-project

# Enter project
cd my-project

# Initialize Git
git init

# Create a file
touch README.md

# Check status
git status

# Stage the file
git add README.md

# Commit the file
git commit -m "Add README"

# Add GitHub repository
git remote add origin https://github.com/USERNAME/my-project.git

# Push to GitHub
git push -u origin main
```

# 24. Git in DevOps

Git is an important part of DevOps because it provides version control for:

* Application source code
* Infrastructure code
* Configuration files
* Shell scripts
* Ansible playbooks
* Terraform files
* CI/CD configuration

A typical DevOps workflow:

```text
Developer
    ↓
   Git
    ↓
 GitHub
    ↓
 CI/CD Pipeline
    ↓
 Build
    ↓
 Test
    ↓
 Deploy
    ↓
Production
```

# Key Takeaways

* **Git** is a distributed version control system.
* **Version Control** tracks and manages changes to files.
* **GitHub** hosts Git repositories and provides collaboration features.
* `git add` moves changes to the staging area.
* `git commit` saves a snapshot of changes.
* `git push` uploads commits to a remote repository.
* `git pull` downloads and integrates remote changes.
* **Branches** allow developers to work on features independently.
* Git is a fundamental tool in **DevOps and CI/CD**.


