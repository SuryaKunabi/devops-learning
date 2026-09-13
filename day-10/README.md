# Git Flow Branching Strategy

Git Flow is a Git branching model used to organize **development, releases, and production fixes**.

## Branch Structure

```text
main/master
    │
    ├── hotfix
    │
    └── develop
          │
          ├── feature/login
          ├── feature/payment
          │
          └── release/v1.0
```

## Main Branches

### 1. Main / Master

* Contains stable, production-ready code.
* Used for production releases.

### 2. Develop

* Main development branch.
* Features are integrated here before release.

## Supporting Branches

### 3. Feature Branch

Used to develop new features.

```text
feature/login
feature/payment
```

Usually created from `develop` and merged back into `develop`.

### 4. Release Branch

Used to prepare and test a new version.

```text
release/v1.0
```

After testing, it is merged into `main` and `develop`.

### 5. Hotfix Branch

Used to fix critical production issues quickly.

```text
hotfix/login-error
```

Usually created from `main` and merged back into `main` and `develop`.

## Git Flow

```text
Feature → Develop → Release → Main
                         ↓
                      Production

Main → Hotfix → Main
          ↓
       Develop
```

## Common Commands

```bash
# Create feature branch
git switch -c feature/login

# Create release branch
git switch -c release/v1.0

# Create hotfix branch
git switch -c hotfix/login-error

# Push branch
git push -u origin feature/login

# Merge branch
git switch develop
git merge feature/login
```

## Key Takeaways

* **Main/Master** → Production
* **Develop** → Development
* **Feature** → New features
* **Release** → Release preparation
* **Hotfix** → Critical production fixes

