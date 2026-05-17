# STAGE 2 — LOCAL REPOSITORY MANAGEMENT 🚀

---

# 📚 Table of Contents

1. Creating Repository
2. Git Lifecycle
3. Basic Commands
4. Understanding Commits
5. File Operations
6. Viewing History
7. .gitignore
8. Practical Tasks
9. Important Interview Questions & Answers
10. Summary
11. Next Stage

---

# 1️⃣ Creating Repository

---

# 📌 What is a Git Repository?

A Git Repository is a directory managed and tracked by Git.

It stores:

✅ Source code  
✅ Commit history  
✅ Branches  
✅ Logs  
✅ Configurations  

---

# 📌 git init

`git init` initializes a new Git repository.

---

# 📌 Command

```bash
git init
```

---

# 📌 What Happens Internally?

Git creates a hidden directory:

```bash
.git/
```

This folder contains:

- Commit objects
- Branches
- References
- Logs
- Metadata

---

# 📌 Repository Structure

```text
devops-git-lab/
│
├── deployment.yaml
├── service.yaml
├── ingress.yaml
└── .git/
```

---

# 📌 Important

Without `.git/`:

❌ Repository history lost  
❌ Git stops working  
❌ Branch information lost  

---

# 📌 Verify Repository

```bash
ls -la
```

---

# 2️⃣ Git Lifecycle

Git tracks files through multiple states.

---

# 📌 Lifecycle Flow

```text
Untracked → Modified → Staged → Committed
```

---

# 📌 Lifecycle Diagram

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
```

---

# 📌 States Explained

| State | Meaning |
|---|---|
| Untracked | Git does not track file |
| Modified | File changed |
| Staged | Ready for commit |
| Committed | Saved in Git history |

---

# 📌 Example

```bash
touch deployment.yaml
git status
```

Git shows:

```text
Untracked files
```

Stage file:

```bash
git add deployment.yaml
```

Commit file:

```bash
git commit -m "Add deployment manifest"
```

---

# 3️⃣ Basic Commands

---

# 📌 git status

Shows current repository state.

```bash
git status
```

Displays:

- Untracked files
- Modified files
- Staged files

---

# 📌 git add

Moves changes to staging area.

---

# Stage All Files

```bash
git add .
```

---

# Stage Specific File

```bash
git add deployment.yaml
```

---

# 📌 git commit

Creates snapshot of staged changes.

```bash
git commit -m "Add nginx deployment"
```

---

# 📌 git log

Shows commit history.

```bash
git log
```

Compact format:

```bash
git log --oneline
```

---

# 📌 git diff

Shows unstaged changes.

```bash
git diff
```

Show staged changes:

```bash
git diff --staged
```

---

# 📌 git show

Displays detailed commit information.

```bash
git show <commit-id>
```

---

# 4️⃣ Understanding Commits

---

# 📌 What is Commit?

A commit is:

> Snapshot of project at a specific point in time.

---

# 📌 Commit Hash

Every commit gets unique identifier.

Example:

```text
e4a1c8b92d6a
```

---

# 📌 SHA-1

Git uses SHA-1 hashing algorithm.

Purpose:

✅ Unique commit IDs  
✅ Integrity verification  
✅ Change tracking  

---

# 📌 Commit Messages

Good commit messages improve:

✅ Debugging  
✅ Collaboration  
✅ Audit tracking  

---

# ❌ Bad Commit Messages

```bash
git commit -m "fix"
git commit -m "update"
git commit -m "asdf"
```

---

# ✅ Good Commit Messages

```bash
git commit -m "fix: resolve ingress routing issue"
```

```bash
git commit -m "feat: add prometheus monitoring"
```

---

# 📌 Atomic Commits

Atomic commit means:

> One commit = One logical change

---

# ❌ Bad Practice

Single commit containing:

- Docker changes
- Kubernetes updates
- README changes
- Bug fixes

---

# ✅ Good Practice

Separate commits:

```bash
feat: add monitoring
fix: resolve ingress issue
docs: update README
```

---

# 📌 Commit Message Convention

| Prefix | Meaning |
|---|---|
| feat: | New feature |
| fix: | Bug fix |
| docs: | Documentation |
| refactor: | Refactoring |
| style: | Formatting |
| test: | Tests |
| chore: | Maintenance |

---

# 5️⃣ File Operations

---

# 📌 git rm

Removes file from Git.

```bash
git rm svc.yaml
```

---

# 📌 git mv

Rename or move file.

```bash
git mv service.yaml svc.yaml
```

---

# 📌 git restore

Restore modified/deleted file.

```bash
git restore deployment.yaml
```

Restore staged changes:

```bash
git restore --staged deployment.yaml
```

---

# 📌 Real DevOps Usage

Useful for:

✅ Rollbacks  
✅ Recovery  
✅ Infrastructure restoration  

---

# 6️⃣ Viewing History

---

# 📌 git log

Detailed commit history.

```bash
git log
```

---

# 📌 git log --oneline

Compact history view.

```bash
git log --oneline
```

---

# 📌 git log --graph

Visual commit graph.

```bash
git log --graph
```

---

# 📌 Full Graph

```bash
git log --all --oneline --graph
```

---

# 📌 git blame

Shows:

- Who changed line
- When changed
- Which commit changed it

```bash
git blame deployment.yaml
```

---

# 📌 Real Production Example

Suppose deployment breaks.

Using:

```bash
git blame deployment.yaml
```

You identify:

✅ Which engineer changed replicas  
✅ Which commit caused issue  
✅ Exact timestamp  

---

# 7️⃣ .gitignore

---

# 📌 Purpose

`.gitignore` tells Git:

> Ignore these files and folders.

---

# 📌 Why Important?

Without `.gitignore`:

❌ Secrets leak  
❌ Large unnecessary files committed  
❌ Build artifacts tracked  

---

# 📌 Common Examples

```bash
.env
*.pem
node_modules/
dist/
.terraform/
.vscode/
```

---

# 📌 Ignoring Secrets

```bash
.env
*.key
*.pem
credentials/
```

---

# 📌 Ignoring Build Artifacts

```bash
dist/
build/
target/
*.jar
```

---

# 📌 Wildcards

Ignore all `.log` files:

```bash
*.log
```

---

# 📌 Real DevOps Risk

If `.env` gets committed:

❌ AWS credentials leak  
❌ Database passwords exposed  
❌ Kubernetes secrets exposed  

This becomes major security issue 🚨

---

# 8️⃣ Practical Tasks

---

# ✅ Task 1 — Create Repository

```bash
mkdir devops-git-lab
cd devops-git-lab
git init
```

Verify:

```bash
ls -la
```

---

# ✅ Task 2 — Create Kubernetes Manifests

```bash
touch deployment.yaml
touch service.yaml
touch ingress.yaml
```

---

# ✅ Task 3 — Check Status and Stage Files

```bash
git status
```

Stage all files:

```bash
git add .
```

Stage specific files:

```bash
git add deployment.yaml service.yaml
```

---

# ✅ Task 4 — Commit Changes

```bash
git commit -m "Initial Kubernetes manifests"
```

View history:

```bash
git log
```

---

# ✅ Task 5 — Modify Files and Check Diff

Check changes:

```bash
git diff
```

Stage changes:

```bash
git add deployment.yaml
```

Check staged changes:

```bash
git diff --staged
```

Commit:

```bash
git commit -m "Add nginx deployment configuration"
```

---

# ✅ Task 6 — Use .gitignore

Create file:

```bash
touch .gitignore
```

Example:

```bash
.env
*.pem
node_modules/
dist/
.terraform/
```

Test:

```bash
echo "SECRET_KEY=abc123" > .env
git status
```

`.env` should not appear.

---

# ✅ Task 7 — File Operations

Rename:

```bash
git mv service.yaml svc.yaml
```

Delete:

```bash
git rm svc.yaml
```

Restore:

```bash
git restore svc.yaml
```

Unstage:

```bash
git restore --staged deployment.yaml
```

---

# 9️⃣ Important Interview Questions & Answers

# 🟢 Beginner Level

---

# 1. What is Git Lifecycle?

## Answer:

Git Lifecycle represents the stages through which files move inside Git.

```text
Untracked → Modified → Staged → Committed
```

---

# 2. What is Staging Area?

## Answer:

Staging Area is temporary preparation area where changes are collected before commit.

---

# 3. Difference between git add and git commit?

## Answer:

| Command | Purpose |
|---|---|
| git add | Move changes to staging area |
| git commit | Save staged changes permanently |

---

# 4. What is .git folder?

## Answer:

`.git/` is hidden folder storing:

- Commit history
- Branches
- Logs
- Configurations

It is the brain of Git repository.

---

# 5. What is .gitignore?

## Answer:

`.gitignore` tells Git which files/folders should not be tracked.

Example:

```bash
.env
node_modules/
*.log
```

---

# 🟡 Intermediate Level

---

# 6. Explain Git Internal Architecture.

## Answer:

```text
Working Directory
       ↓
Staging Area
       ↓
Local Repository
       ↓
Remote Repository
```

---

# 7. What is SHA-1 Hashing?

## Answer:

Git uses SHA-1 hashing to generate unique commit IDs.

Example:

```text
e4a1c8b92d6a
```

---

# 8. Difference between git diff and git show?

## Answer:

| Command | Purpose |
|---|---|
| git diff | Shows changes before commit |
| git show | Shows details of commit |

---

# 9. Explain Atomic Commits.

## Answer:

Atomic Commit means:

> One commit should contain one logical change only.

Benefits:

✅ Easier rollback  
✅ Better debugging  
✅ Clean history  

---

# 10. How does git blame help debugging?

## Answer:

`git blame` shows:

✅ Who changed line  
✅ Which commit changed it  
✅ When change happened  

Useful for production debugging and audit tracking.

---

# 🎯 Summary

After completing this stage, you should understand:

✅ Repository initialization  
✅ Git lifecycle  
✅ Staging and commits  
✅ File operations  
✅ Commit history  
✅ Git architecture  
✅ .gitignore usage  
✅ Debugging with git blame  
✅ Professional commit practices  

---

# 🚀 Senior DevOps Perspective

In production:

Git repositories store:

✅ Kubernetes manifests  
✅ Terraform infrastructure  
✅ Jenkins pipelines  
✅ Docker configurations  
✅ Helm charts  
✅ ArgoCD applications  

Git becomes:

> Infrastructure Source of Truth

Every infrastructure change becomes:

✅ Auditable  
✅ Traceable  
✅ Recoverable  
✅ Version controlled  

# STAGE 2 LAB — LOCAL REPOSITORY MANAGEMENT 🚀

This lab covers hands-on Git operations used daily by DevOps Engineers and Software Developers.

---

# 📚 Lab Objectives

In this lab you will learn:

✅ Initialize Git repository  
✅ Understand Git lifecycle  
✅ Stage and commit changes  
✅ Track modifications using diff  
✅ Use `.gitignore` securely  
✅ Perform file operations  
✅ View commit history  
✅ Practice professional commit messages  

---

# 🧪 Task 1 — Create Repository

---

# 📌 Create Project Directory

```bash
mkdir devops-git-lab
cd devops-git-lab
```

---

# 📌 Initialize Git Repository

```bash
git init
```

---

# 📌 Verify `.git` Directory

```bash
ls -la
```

Expected:

```text
.git/
```

---

# 📌 What Happens Internally?

Git creates hidden folder:

```bash
.git/
```

This folder stores:

- Commit history
- Branches
- Logs
- Configurations
- Metadata

---

# 🧪 Task 2 — Create Kubernetes Manifests

Create Kubernetes YAML files.

```bash
touch deployment.yaml
touch service.yaml
touch ingress.yaml
```

---

# 📌 Verify Files

```bash
ls
```

Expected:

```text
deployment.yaml
service.yaml
ingress.yaml
```

---

# 🧪 Task 3 — Check Status and Stage Files

---

# 📌 Check Status

```bash
git status
```

Expected:

```text
Untracked files:
```

---

# 📌 Stage All Files

```bash
git add .
```

---

# 📌 OR Stage Specific Files

```bash
git add deployment.yaml service.yaml
```

---

# 📌 Check Status Again

```bash
git status
```

Expected:

```text
Changes to be committed
```

---

# 📌 Learning

Files moved from:

```text
Working Directory → Staging Area
```

---

# 🧪 Task 4 — Commit Changes

---

# 📌 Create Commit

```bash
git commit -m "Initial Kubernetes manifests"
```

---

# 📌 View Commit History

```bash
git log
```

---

# 📌 Learning

Git created snapshot of repository state.

Each commit contains:

- Commit ID
- Author
- Timestamp
- Changes

---

# 🧪 Task 5 — Modify Files and Check Diff

---

# 📌 Add Content to deployment.yaml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.21
        ports:
        - containerPort: 80
```

---

# 📌 Check Unstaged Changes

```bash
git diff
```

---

# 📌 Stage Changes

```bash
git add deployment.yaml
```

---

# 📌 Check Staged Changes

```bash
git diff --staged
```

---

# 📌 Commit Changes

```bash
git commit -m "Add nginx deployment configuration"
```

---

# 📌 Learning

Difference between:

| Command | Purpose |
|---|---|
| git diff | Shows unstaged changes |
| git diff --staged | Shows staged changes |

---

# 🧪 Task 6 — Use .gitignore

---

# 📌 Create .gitignore

```bash
cat > .gitignore << 'EOF'
# Secrets and sensitive files
.env
*.pem
*.key
*.crt
secrets/
credentials/

# Dependencies
node_modules/
vendor/
venv/
__pycache__/

# Build artifacts
*.log
dist/
build/
target/
*.jar
*.war

# Terraform
*.tfstate
*.tfstate.*
.terraform/
.terraform.lock.hcl

# Kubernetes
kubeconfig
*.kubeconfig

# IDE and editors
.vscode/
.idea/
*.swp
*.swo
*~
.DS_Store

# OS files
Thumbs.db
EOF
```

---

# 📌 Test .gitignore

Create ignored file:

```bash
echo "SECRET_KEY=abc123" > .env
```

---

# 📌 Verify Ignored File

```bash
git status
```

`.env` should NOT appear.

---

# 📌 Commit .gitignore

```bash
git add .gitignore
git commit -m "Add .gitignore for sensitive files"
```

---

# 📌 Learning

`.gitignore` prevents:

❌ Secret leakage  
❌ Unnecessary files  
❌ Build artifacts tracking  

---

# 🧪 Task 7 — File Operations

---

# 📌 Rename File

```bash
git mv service.yaml svc.yaml
```

Commit:

```bash
git commit -m "Rename service.yaml to svc.yaml"
```

---

# 📌 Delete File

```bash
git rm svc.yaml
```

Commit:

```bash
git commit -m "Remove svc.yaml"
```

---

# 📌 Restore Deleted File

```bash
git restore svc.yaml
```

---

# 📌 Unstage File

```bash
git add deployment.yaml
git restore --staged deployment.yaml
```

---

# 📌 Learning

| Command | Purpose |
|---|---|
| git mv | Rename/move file |
| git rm | Delete tracked file |
| git restore | Restore file changes |

---

# 🧪 Task 8 — Practice Good Commit Messages

---

# ❌ BAD COMMIT MESSAGES

```bash
git commit -m "fixed stuff"
git commit -m "update"
git commit -m "changes"
git commit -m "asdf"
```

---

# ✅ GOOD COMMIT MESSAGES

```bash
git commit -m "fix: resolve nginx ingress path routing issue"

git commit -m "feat: add prometheus monitoring to deployment"

git commit -m "docs: update README with deployment instructions"

git commit -m "refactor: simplify service selector logic"
```

---

# ✅ BEST PRACTICE COMMIT

```bash
git commit -m "fix: resolve nginx ingress path routing issue

- Updated path from /* to /api/*
- Added rewrite-target annotation
- Tested in staging environment
- Resolves issue #123"
```

---

# 📌 Commit Message Convention

| Prefix | Meaning |
|---|---|
| feat: | New feature |
| fix: | Bug fix |
| docs: | Documentation |
| style: | Formatting |
| refactor: | Code restructuring |
| test: | Testing |
| chore: | Maintenance |

---

# 📌 Why Good Commit Messages Matter?

Good commit messages help:

✅ Easier debugging  
✅ Better collaboration  
✅ Audit tracking  
✅ Cleaner history  

---

# 🧪 Task 9 — View History

---

# 📌 Basic Log

```bash
git log
```

---

# 📌 Compact Log

```bash
git log --oneline
```

---

# 📌 Graph Visualization

```bash
git log --oneline --graph --all
```

---

# 📌 Last 5 Commits

```bash
git log -5
```

---

# 📌 Show Specific Commit

```bash
git show <commit-hash>
```

---

# 📌 Show Who Changed Each Line

```bash
git blame deployment.yaml
```

---

# 📌 Learning

| Command | Purpose |
|---|---|
| git log | Full commit history |
| git log --oneline | Compact history |
| git log --graph | Visual branch graph |
| git show | Detailed commit info |
| git blame | Line-by-line author tracking |

---

# 🎯 Important Interview Questions

---

# 🟢 Beginner Level

---

# 1. What is Git Lifecycle?

Git Lifecycle represents file states:

```text
Untracked → Modified → Staged → Committed
```

---

# 2. What is Staging Area?

Temporary area where changes are prepared before commit.

---

# 3. Difference between git add and git commit?

| Command | Purpose |
|---|---|
| git add | Stage changes |
| git commit | Save snapshot |

---

# 4. What is .git folder?

Hidden directory storing:

- Commits
- Branches
- Logs
- Configurations

---

# 5. What is .gitignore?

File telling Git which files/folders to ignore.

---

# 🟡 Intermediate Level

---

# 6. Explain Git Internal Architecture.

```text
Working Directory
       ↓
Staging Area
       ↓
Local Repository
       ↓
Remote Repository
```

---

# 7. What is SHA-1 Hashing?

Git uses SHA-1 to generate unique commit IDs.

---

# 8. Difference between git diff and git show?

| Command | Purpose |
|---|---|
| git diff | Shows unstaged changes |
| git show | Shows commit details |

---

# 9. Explain Atomic Commits.

One commit should contain one logical change only.

---

# 10. How does git blame help debugging?

Shows:

- Who changed line
- Which commit changed it
- When change happened

Useful for production debugging.

---

# 🚀 Senior DevOps Perspective

In production environments Git repositories store:

✅ Kubernetes manifests  
✅ Terraform infrastructure  
✅ Jenkins pipelines  
✅ Docker configurations  
✅ Helm charts  
✅ ArgoCD applications  

Git becomes:

> Infrastructure Source of Truth

Every change becomes:

✅ Auditable  
✅ Traceable  
✅ Recoverable  
✅ Version controlled  

---

# 🎯 Summary

After completing this lab, you should understand:

✅ Repository initialization  
✅ Git lifecycle  
✅ Staging and commits  
✅ File operations  
✅ Commit history  
✅ .gitignore usage  
✅ Professional commit practices  
✅ Debugging using Git history  


---
