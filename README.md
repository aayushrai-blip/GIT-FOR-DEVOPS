# Git for DevOps — ULTIMATE Mastery Roadmap 🚀

> Beginner → Advanced → Production-Level Git for DevOps Engineers

---

# Goal of This Roadmap

This roadmap is designed specifically for:

* DevOps Engineers
* Cloud Engineers
* Platform Engineers
* SREs
* Kubernetes Administrators
* CI/CD Engineers

By the end of this roadmap, you will be able to:

* Handle production Git workflows
* Manage infrastructure repositories
* Work with Kubernetes + GitOps
* Handle merge conflicts confidently
* Perform production rollbacks safely
* Build CI/CD workflows
* Manage Terraform and Helm repositories
* Work with enterprise branching strategies
* Handle Git debugging and recovery
* Understand Git internals
* **Avoid dangerous commands in production**
* **Master merge conflict resolution**
* **Work with upstream/fork workflows**

---

# ROADMAP STRUCTURE (Part 1: Stages 1-10)

| Stage | Topic                          | Level                   |
| ----- | ------------------------------ | ----------------------- |
| 1     | Git Fundamentals               | Beginner                |
| 2     | Local Repository Management    | Beginner                |
| 3     | Branching & Merging            | Beginner → Intermediate |
| 4     | Remote Repositories            | Intermediate            |
| 5     | **Merge Conflicts Mastery**    | **Intermediate**        |
| 6     | **Fork & Upstream Workflows**  | **Intermediate**        |
| 7     | Production Git Operations      | Intermediate            |
| 8     | **Production Safety & Rules**  | **Intermediate**        |
| 9     | Advanced Git                   | Advanced                |
| 10    | Git Internals                  | Advanced                |

---

# STAGE 1 — GIT FUNDAMENTALS

## Topics to Learn

### 1. What is Version Control

* Centralized Version Control
* Distributed Version Control
* Why Version Control Exists
* Problems Solved by Git

### 2. What is Git

* Distributed Architecture
* Local Repository
* Remote Repository
* Commit History
* Snapshot-Based Tracking

### 3. Git Architecture

* Working Directory
* Staging Area (Index)
* Repository (.git)
* HEAD
* Index

### 4. Difference Between

* Git vs GitHub
* Git vs GitLab
* GitHub vs GitLab
* Git vs SVN

### 5. Installing Git

* Linux (Ubuntu/CentOS/Fedora)
* Windows
* MacOS

### 6. Git Configuration

* Username
* Email
* Default Branch
* Credential Helpers
* **Git Aliases (Productivity)**

---

## Practical Tasks

### Task 1 — Install Git and Verify

```bash
# Ubuntu/Debian
sudo apt update
sudo apt install git

# CentOS/RHEL
sudo yum install git

# Fedora
sudo dnf install git

# MacOS
brew install git

# Windows - Download from https://git-scm.com/download/win

# Verify installation
git --version
```

---

### Task 2 — Configure Git

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
git config --global init.defaultBranch main
```

---

### Task 3 — Check Configuration

```bash
# View all configuration
git config --list

# View global configuration only
git config --global --list

# View specific configuration
git config user.name
git config user.email
```

---

### Task 4 — Setup Git Aliases (Productivity Boost)

```bash
# Shorthand for common commands
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm 'commit -m'
git config --global alias.st status
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual 'log --oneline --graph --all'
git config --global alias.amend 'commit --amend --no-edit'

# Now you can use:
# git co main          (instead of git checkout main)
# git st               (instead of git status)
# git cm "message"     (instead of git commit -m "message")
# git visual           (beautiful commit graph)
```

---

### Task 5 — Configure Default Editor

```bash
# Set VS Code as default editor
git config --global core.editor "code --wait"

# OR Vim
git config --global core.editor "vim"

# OR Nano
git config --global core.editor "nano"
```

---

### Task 6 — Setup Credential Helper

```bash
# For Linux
git config --global credential.helper cache
git config --global credential.helper 'cache --timeout=3600'

# For macOS
git config --global credential.helper osxkeychain

# For Windows
git config --global credential.helper wincred
```

---

# STAGE 2 — LOCAL REPOSITORY MANAGEMENT

## Topics to Learn

### 1. Creating Repository

* `git init`
* Repository Structure
* `.git` Folder

### 2. Git Lifecycle

* Untracked
* Modified
* Staged
* Committed

### 3. Basic Commands

* `git status`
* `git add`
* `git commit`
* `git log`
* `git diff`
* `git show`

### 4. Understanding Commits

* Commit Hash
* SHA-1
* Commit Messages
* Atomic Commits
* **Writing Good Commit Messages**

### 5. File Operations

* `git rm`
* `git mv`
* `git restore`

### 6. Viewing History

* `git log`
* `git log --oneline`
* `git log --graph`
* `git log --all --oneline --graph`
* `git blame`

### 7. .gitignore

* Ignoring Files
* Ignoring Secrets
* Ignoring Build Artifacts
* **Patterns and Wildcards**

---

## Practical Tasks

### Task 1 — Create Repository

```bash
mkdir devops-git-lab
cd devops-git-lab
git init

# Verify .git directory created
ls -la
```

---

### Task 2 — Create Kubernetes Manifests

```bash
touch deployment.yaml
touch service.yaml
touch ingress.yaml
```

---

### Task 3 — Check Status and Stage Files

```bash
# Check status (files are untracked)
git status

# Stage all files
git add .

# OR stage specific files
git add deployment.yaml service.yaml

# Check status again (files are staged)
git status
```

---

### Task 4 — Commit Changes

```bash
git commit -m "Initial Kubernetes manifests"

# View commit history
git log
```

---

### Task 5 — Modify Files and Check Diff

Add content to deployment.yaml:

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

Check changes:

```bash
# See unstaged changes
git diff

# Stage changes
git add deployment.yaml

# See staged changes
git diff --staged

# Commit
git commit -m "Add nginx deployment configuration"
```

---

### Task 6 — Use .gitignore

Create `.gitignore`:

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

Test .gitignore:

```bash
# Create ignored file
echo "SECRET_KEY=abc123" > .env

# Check status (should not show .env)
git status

# Add and commit .gitignore
git add .gitignore
git commit -m "Add .gitignore for sensitive files"
```

---

### Task 7 — File Operations

```bash
# Rename file
git mv service.yaml svc.yaml
git commit -m "Rename service.yaml to svc.yaml"

# Delete file
git rm svc.yaml
git commit -m "Remove svc.yaml"

# Restore deleted file (if not committed yet)
git restore svc.yaml

# Unstage file
git add deployment.yaml
git restore --staged deployment.yaml
```

---

### Task 8 — Practice Good Commit Messages

```bash
# ❌ BAD COMMIT MESSAGES
git commit -m "fixed stuff"
git commit -m "update"
git commit -m "changes"
git commit -m "asdf"

# ✅ GOOD COMMIT MESSAGES
git commit -m "fix: resolve nginx ingress path routing issue"
git commit -m "feat: add prometheus monitoring to deployment"
git commit -m "docs: update README with deployment instructions"
git commit -m "refactor: simplify service selector logic"

# ✅ BEST - With detailed description
git commit -m "fix: resolve nginx ingress path routing issue

- Updated path from /* to /api/*
- Added rewrite-target annotation
- Tested in staging environment
- Resolves issue #123"
```

**Commit Message Convention:**

* `feat:` - New feature
* `fix:` - Bug fix
* `docs:` - Documentation changes
* `style:` - Code style changes (formatting)
* `refactor:` - Code refactoring
* `test:` - Adding tests
* `chore:` - Maintenance tasks

---

### Task 9 — View History

```bash
# Basic log
git log

# Compact one-line format
git log --oneline

# With graph visualization
git log --oneline --graph --all

# Last 5 commits
git log -5

# Show specific commit
git show <commit-hash>

# Show who changed each line
git blame deployment.yaml
```

---

# STAGE 3 — BRANCHING & MERGING

## Topics to Learn

### 1. Branching Basics

* What is a Branch
* Why Branching Matters
* HEAD Pointer
* **Branch Naming Conventions**

### 2. Branch Commands

* `git branch`
* `git checkout`
* `git switch` (modern)
* `git merge`
* `git branch -d` (safe delete)
* `git branch -D` (force delete)

### 3. Branching Strategies

* **Feature Branching**
* **Git Flow**
* **GitHub Flow**
* **GitLab Flow**
* **Trunk-Based Development**
* **Release Branches**
* **Hotfix Branches**

### 4. Merge Types

* Fast Forward Merge
* Three-Way Merge
* Squash Merge
* **When to Use Each**

### 5. Best Practices

* Small, Focused Commits
* Frequent Pulls
* Clean Commit History
* **Branch Naming: feature/**, **bugfix/**, **hotfix/**

---

## Practical Tasks

### Task 1 — Create and Switch Branches

```bash
# Create new branch
git branch feature/nginx-ingress

# Switch to branch (old way)
git checkout feature/nginx-ingress

# OR modern way (create and switch)
git switch -c feature/nginx-ingress

# List all branches
git branch

# List all branches with last commit
git branch -v
```

---

### Task 2 — Work on Feature Branch

```bash
# Ensure you're on feature branch
git branch --show-current

# Create ingress.yaml
cat > ingress.yaml << 'EOF'
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: nginx-service
            port:
              number: 80
EOF

# Stage and commit
git add ingress.yaml
git commit -m "feat: add nginx ingress configuration"
```

---

### Task 3 — Merge Feature Branch

```bash
# Switch to main branch
git checkout main

# Merge feature branch
git merge feature/nginx-ingress

# View log with graph
git log --oneline --graph
```

---

### Task 4 — Practice Different Merge Types

```bash
# Fast-forward merge (default if possible)
git checkout main
git merge feature/simple-change

# No fast-forward (always create merge commit)
git merge --no-ff feature/important-feature

# Squash merge (combine all commits into one)
git checkout main
git merge --squash feature/multiple-commits
git commit -m "feat: add complete authentication module"
```

---

### Task 5 — Branch Naming Conventions

```bash
# Feature branches
git checkout -b feature/user-authentication
git checkout -b feature/payment-integration
git checkout -b feature/email-notifications

# Bug fix branches
git checkout -b bugfix/login-error
git checkout -b bugfix/memory-leak

# Hotfix branches (urgent production fixes)
git checkout -b hotfix/security-patch
git checkout -b hotfix/critical-crash

# Release branches
git checkout -b release/v1.0.0
git checkout -b release/v2.1.0

# Experiment branches
git checkout -b experiment/new-architecture
```

---

### Task 6 — Delete Branches Safely

```bash
# Safe delete (only if merged)
git branch -d feature/nginx-ingress

# If branch is not merged, you get error
# Force delete (even if not merged)
git branch -D feature/abandoned-work

# Delete remote branch
git push origin --delete feature/old-branch
```

---

### Task 7 — View Branch Information

```bash
# List local branches
git branch

# List remote branches
git branch -r

# List all branches (local + remote)
git branch -a

# Show merged branches
git branch --merged

# Show unmerged branches
git branch --no-merged

# Show branch with commit info
git branch -v
```

---

# STAGE 4 — REMOTE REPOSITORIES

## Topics to Learn

### 1. Remote Repository Concepts

* `origin`
* `upstream`
* `fork`
* `clone`

### 2. GitHub

* Repository Creation
* Pull Requests
* Forking
* Code Review
* **Protected Branches**

### 3. GitLab

* Merge Requests
* Pipelines
* Protected Branches

### 4. Authentication

* HTTPS
* SSH Keys
* Personal Access Tokens
* **SSH Key Security**

### 5. Remote Commands

* `git remote`
* `git push`
* `git pull`
* `git fetch`
* `git clone`
* **`git remote -v`** (verify remotes)

---

## Practical Tasks

### Task 1 — Create GitHub Repository

1. Go to GitHub.com
2. Click "New Repository"
3. Name: `devops-git-lab`
4. Keep it private
5. Don't initialize with README
6. Click "Create repository"

---

### Task 2 — Connect Local Repo to GitHub

```bash
# Add remote
git remote add origin git@github.com:username/devops-git-lab.git

# Verify remote
git remote -v

# Push to GitHub
git push -u origin main
```

---

### Task 3 — Setup SSH Keys for GitHub

```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your-email@example.com"

# When prompted, press Enter for default location
# Set a strong passphrase

# Start ssh-agent
eval "$(ssh-agent -s)"

# Add key to ssh-agent
ssh-add ~/.ssh/id_ed25519

# Copy public key
cat ~/.ssh/id_ed25519.pub
# Copy the output
```

**Add to GitHub:**

1. Go to GitHub Settings
2. SSH and GPG keys
3. Click "New SSH key"
4. Paste your public key
5. Click "Add SSH key"

---

### Task 4 — Verify SSH Connection

```bash
ssh -T git@github.com

# You should see:
# Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

### Task 5 — Clone Repository

```bash
# Clone via SSH
git clone git@github.com:username/repo-name.git

# Clone via HTTPS
git clone https://github.com/username/repo-name.git

# Clone specific branch
git clone -b develop git@github.com:username/repo-name.git

# Shallow clone (only latest commit)
git clone --depth 1 git@github.com:username/repo-name.git
```

---

### Task 6 — Push and Pull

```bash
# Make changes
echo "# DevOps Git Lab" > README.md
git add README.md
git commit -m "docs: add README"

# Push to remote
git push origin main

# Pull from remote
git pull origin main

# Pull with rebase (cleaner history)
git pull --rebase origin main
```

---

### Task 7 — Fetch vs Pull

```bash
# Fetch (download changes, don't merge)
git fetch origin

# See what changed
git log origin/main

# Manually merge if needed
git merge origin/main

# Pull (fetch + merge)
git pull origin main
```

---

### Task 8 — Create Pull Request (GitHub)

```bash
# Create feature branch
git checkout -b feature/add-ci-pipeline

# Make changes
cat > .github/workflows/ci.yml << 'EOF'
name: CI
on: [push]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Run tests
      run: echo "Running tests..."
EOF

# Commit and push
git add .github/workflows/ci.yml
git commit -m "ci: add GitHub Actions workflow"
git push origin feature/add-ci-pipeline
```

**On GitHub:**

1. Click "Compare & pull request"
2. Add title and description
3. Click "Create pull request"
4. Request reviewers
5. After approval, merge PR

---

### Task 9 — Remote Management

```bash
# List remotes
git remote -v

# Add remote
git remote add upstream git@github.com:original/repo.git

# Remove remote
git remote remove upstream

# Rename remote
git remote rename origin old-origin

# Change remote URL
git remote set-url origin git@github.com:new-username/repo.git

# Show remote details
git remote show origin
```

---

# STAGE 5 — MERGE CONFLICTS MASTERY ⚠️

## Topics to Learn

### 1. Understanding Conflicts

* What Causes Conflicts
* Conflict Markers (`<<<<<<<`, `=======`, `>>>>>>>`)
* **Types of Conflicts**

### 2. Conflict Types

* **Content Conflicts** (same line changed)
* **Rename Conflicts** (file renamed in both branches)
* **Delete Conflicts** (one deleted, one modified)
* **Binary File Conflicts** (images, PDFs)
* **Directory Conflicts**

### 3. Conflict Resolution Tools

* Manual Resolution
* `git mergetool`
* VS Code Merge Editor
* IntelliJ IDEA
* **vimdiff, meld, kdiff3**

### 4. Advanced Conflict Scenarios

* Multiple File Conflicts
* **Terraform State Conflicts**
* **Kubernetes Manifest Conflicts**
* **package.json/requirements.txt Conflicts**
* **Helm Chart Conflicts**

### 5. Conflict Resolution Strategies

* Accept Current Change
* Accept Incoming Change
* Accept Both Changes
* **Manual Edit (Best for Production)**

---

## Practical Tasks

### Task 1 — Create Simple Conflict

```bash
# On main branch
git checkout main
echo "replicas: 3" > deployment.yaml
git add deployment.yaml
git commit -m "Set replicas to 3"

# Create feature branch 1
git checkout -b feature/scale-up
echo "replicas: 5" > deployment.yaml
git commit -am "Scale up to 5 replicas"

# Go back to main
git checkout main

# Create feature branch 2
git checkout -b feature/scale-down
echo "replicas: 2" > deployment.yaml
git commit -am "Scale down to 2 replicas"

# Merge first feature (OK)
git checkout main
git merge feature/scale-up

# Merge second feature (CONFLICT!)
git merge feature/scale-down
```

---

### Task 2 — Understand Conflict Markers

```bash
# Check status
git status

# View conflict
cat deployment.yaml

# You'll see:
<<<<<<< HEAD
replicas: 5
=======
replicas: 2
>>>>>>> feature/scale-down

# Explanation:
# <<<<<<< HEAD          : Start of your current changes (main branch)
# replicas: 5           : Your version
# =======               : Separator
# replicas: 2           : Their version (incoming branch)
# >>>>>>> feature/...   : End of their changes
```

---

### Task 3 — Resolve Conflict Manually

```bash
# Option 1: Keep current change (5)
echo "replicas: 5" > deployment.yaml

# Option 2: Keep incoming change (2)
echo "replicas: 2" > deployment.yaml

# Option 3: Use different value (compromise)
echo "replicas: 3" > deployment.yaml

# Mark as resolved
git add deployment.yaml
git commit -m "Resolved replica conflict - using 5 replicas"
```

---

### Task 4 — Use VS Code for Conflict Resolution

```bash
# When conflict occurs, open in VS Code
code deployment.yaml

# VS Code shows:
# - Accept Current Change (button)
# - Accept Incoming Change (button)
# - Accept Both Changes (button)
# - Compare Changes (button)

# Click appropriate button or manually edit

# Save file
# Stage and commit
git add deployment.yaml
git commit -m "Resolved conflict using VS Code"
```

---

### Task 5 — Configure and Use Git Mergetool

```bash
# Configure mergetool
git config --global merge.tool vimdiff

# OR use VS Code
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'

# When conflict occurs
git mergetool

# This opens configured tool
# Resolve conflict in tool
# Save and exit

# Clean up backup files
git clean -f

# Commit
git commit -m "Resolved conflict using mergetool"
```

---

### Task 6 — Terraform Conflict Resolution

```bash
# Simulate Terraform conflict
# Create main.tf on main branch
cat > main.tf << 'EOF'
resource "aws_instance" "web" {
  ami           = "ami-12345678"
  instance_type = "t3.large"
  
  tags = {
    Name = "WebServer"
  }
}
EOF

git add main.tf
git commit -m "Add EC2 instance"

# Create branch and change instance type
git checkout -b feature/cost-optimization
sed -i 's/t3.large/t3.medium/' main.tf
git commit -am "Optimize instance type for cost"

# Create another branch with different change
git checkout main
git checkout -b feature/increase-capacity
sed -i 's/t3.large/t3.xlarge/' main.tf
git commit -am "Increase instance capacity"

# Merge first (OK)
git checkout main
git merge feature/cost-optimization

# Merge second (CONFLICT!)
git merge feature/increase-capacity

# Resolve - choose cost-effective option
cat > main.tf << 'EOF'
resource "aws_instance" "web" {
  ami           = "ami-12345678"
  instance_type = "t3.medium"
  
  tags = {
    Name = "WebServer"
  }
}
EOF

# Validate before committing
terraform fmt main.tf
terraform validate

# Commit resolution
git add main.tf
git commit -m "Resolved instance type conflict - using t3.medium for cost"
```

---

### Task 7 — Kubernetes Manifest Conflict

```bash
# Create deployment.yaml
cat > deployment.yaml << 'EOF'
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
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
        resources:
          limits:
            memory: "128Mi"
            cpu: "500m"
EOF

git add deployment.yaml
git commit -m "Add nginx deployment"

# Branch 1: Update image
git checkout -b feature/update-nginx
sed -i 's/nginx:1.21/nginx:1.22/' deployment.yaml
git commit -am "Update nginx to 1.22"

# Branch 2: Update resources
git checkout main
git checkout -b feature/increase-resources
sed -i 's/memory: "128Mi"/memory: "256Mi"/' deployment.yaml
git commit -am "Increase memory limit"

# Merge both (CONFLICT!)
git checkout main
git merge feature/update-nginx
git merge feature/increase-resources

# Resolve - keep both changes
cat > deployment.yaml << 'EOF'
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
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
        image: nginx:1.22
        resources:
          limits:
            memory: "256Mi"
            cpu: "500m"
EOF

# Validate
kubectl apply -f deployment.yaml --dry-run=client

# Commit
git add deployment.yaml
git commit -m "Resolved deployment conflict - updated nginx and increased memory"
```

---

### Task 8 — Package Dependency Conflict (package.json)

```bash
# Create package.json
cat > package.json << 'EOF'
{
  "name": "my-app",
  "version": "1.0.0",
  "dependencies": {
    "express": "^4.17.1",
    "axios": "^0.21.1"
  }
}
EOF

git add package.json
git commit -m "Add package.json"

# Branch 1: Update express
git checkout -b feature/update-express
sed -i 's/"express": "^4.17.1"/"express": "^4.18.0"/' package.json
git commit -am "Update express version"

# Branch 2: Update axios
git checkout main
git checkout -b feature/update-axios
sed -i 's/"axios": "^0.21.1"/"axios": "^0.27.0"/' package.json
git commit -am "Update axios version"

# Merge both (CONFLICT!)
git checkout main
git merge feature/update-express
git merge feature/update-axios

# Resolve - keep both updates
cat > package.json << 'EOF'
{
  "name": "my-app",
  "version": "1.0.0",
  "dependencies": {
    "express": "^4.18.0",
    "axios": "^0.27.0"
  }
}
EOF

# Test dependencies
npm install
npm test

# Commit
git add package.json
git commit -m "Resolved dependency conflict - updated both express and axios"
```

---

### Task 9 — Abort Merge if Too Complex

```bash
# If conflict is too complex or you need to restart
git merge --abort

# This returns repository to pre-merge state
# You can now:
# - Review changes more carefully
# - Coordinate with team
# - Try different merge strategy
```

---

### Task 10 — Check Conflict Status

```bash
# See which files have conflicts
git status

# See conflicted changes
git diff

# See only conflicted files
git diff --name-only --diff-filter=U

# See number of conflicts
git diff --check
```

---

### Task 11 — Binary File Conflicts

```bash
# Binary files (images, PDFs) cannot be merged automatically
# Git will ask you to choose one version

# Example conflict:
# warning: Cannot merge binary files: logo.png (HEAD vs feature/new-logo)

# Choose your version
git checkout --ours logo.png

# OR choose their version
git checkout --theirs logo.png

# Mark as resolved
git add logo.png
git commit -m "Resolved logo conflict - using new logo"
```

---

# STAGE 6 — FORK & UPSTREAM WORKFLOWS 🔄

## Topics to Learn

### 1. Fork Concepts

* What is a Fork
* Fork vs Clone
* **Origin vs Upstream**

### 2. Upstream Repository

* Adding Upstream
* Fetching from Upstream
* Keeping Fork Updated
* **Sync Strategies**

### 3. Contributing to Open Source

* Fork Workflow
* Pull Request Process
* Code Review
* **Contribution Guidelines**

### 4. Multi-Remote Workflows

* Multiple Remotes
* Remote Naming Conventions
* **Pushing to Different Remotes**

---

## Practical Tasks

### Task 1 — Fork a Repository (GitHub)

**Steps:**

1. Go to https://github.com/kubernetes/examples
2. Click "Fork" button (top right)
3. Select your account
4. Wait for fork to complete

---

### Task 2 — Clone Your Fork

```bash
# Clone YOUR fork (not original)
git clone git@github.com:YOUR_USERNAME/examples.git
cd examples

# Verify remote
git remote -v
# Output:
# origin  git@github.com:YOUR_USERNAME/examples.git (fetch)
# origin  git@github.com:YOUR_USERNAME/examples.git (push)
```

---

### Task 3 — Add Upstream Remote

```bash
# Add the original repository as "upstream"
git remote add upstream git@github.com:kubernetes/examples.git

# Verify both remotes
git remote -v

# Output:
# origin    git@github.com:YOUR_USERNAME/examples.git (fetch)
# origin    git@github.com:YOUR_USERNAME/examples.git (push)
# upstream  git@github.com:kubernetes/examples.git (fetch)
# upstream  git@github.com:kubernetes/examples.git (push)
```

**Understanding:**

* **origin** = Your fork (you can push here)
* **upstream** = Original repo (you can only fetch, not push)

---

### Task 4 — Keep Fork Updated (Sync with Upstream)

```bash
# Fetch latest changes from upstream
git fetch upstream

# View upstream branches
git branch -r

# Switch to your main branch
git checkout main

# Merge upstream changes
git merge upstream/main

# Push updates to YOUR fork
git push origin main
```

**One-liner sync:**

```bash
git fetch upstream && git checkout main && git merge upstream/main && git push origin main
```

---

### Task 5 — Create Feature Branch from Latest Upstream

```bash
# Always sync with upstream first
git fetch upstream

# Create feature branch from upstream/main
git checkout -b feature/my-contribution upstream/main

# Make changes
echo "# My contribution" > new-example.md
git add new-example.md
git commit -m "docs: add new Kubernetes example"

# Push to YOUR fork (origin)
git push origin feature/my-contribution
```

---

### Task 6 — Open Pull Request to Upstream

**On GitHub:**

1. Go to YOUR fork
2. Click "Compare & pull request"
3. Ensure:
   * **Base repository:** `kubernetes/examples` (upstream)
   * **Base branch:** `main`
   * **Head repository:** `YOUR_USERNAME/examples` (your fork)
   * **Compare branch:** `feature/my-contribution`
4. Add descriptive title and description
5. Click "Create pull request"

---

### Task 7 — Sync After Upstream Merge

```bash
# After your PR is merged into upstream
git fetch upstream
git checkout main
git merge upstream/main
git push origin main

# Delete feature branch locally
git branch -d feature/my-contribution

# Delete feature branch on your fork
git push origin --delete feature/my-contribution
```

---

### Task 8 — Rebase Feature Branch on Latest Upstream

```bash
# If upstream changed while you were working
git fetch upstream

# Switch to your feature branch
git checkout feature/my-contribution

# Rebase on latest upstream
git rebase upstream/main

# If conflicts occur, resolve them:
# 1. Fix conflicts in files
# 2. git add <resolved-files>
# 3. git rebase --continue

# Force push to YOUR fork (safe because it's your branch)
git push --force-with-lease origin feature/my-contribution
```

---

### Task 9 — Handle Merge Conflicts During Rebase

```bash
# During rebase, conflict occurs
git rebase upstream/main

# Output:
# CONFLICT (content): Merge conflict in file.txt
# error: could not apply abc1234... your commit message

# Resolve conflict
vim file.txt
# Fix conflicts

# Stage resolved file
git add file.txt

# Continue rebase
git rebase --continue

# If too complex, abort
git rebase --abort
```

---

### Task 10 — Multiple Remotes Workflow

```bash
# Scenario: Contributing to multiple forks

# Add multiple remotes
git remote add upstream git@github.com:original/repo.git
git remote add colleague git@github.com:colleague/repo.git

# Fetch from all remotes
git fetch --all

# View all remote branches
git branch -r

# Create branch from colleague's work
git checkout -b feature/based-on-colleague colleague/feature-branch

# Make changes and push to your fork
git push origin feature/based-on-colleague
```

---

### Task 11 — Fork Workflow Summary

```bash
# Complete workflow:

# 1. Fork on GitHub (one time)
# 2. Clone your fork
git clone git@github.com:YOUR_USERNAME/repo.git

# 3. Add upstream (one time)
git remote add upstream git@github.com:original/repo.git

# 4. Before starting work, sync with upstream
git fetch upstream
git checkout main
git merge upstream/main
git push origin main

# 5. Create feature branch
git checkout -b feature/my-feature

# 6. Make changes and commit
git add .
git commit -m "feat: add new feature"

# 7. Push to your fork
git push origin feature/my-feature

# 8. Open Pull Request on GitHub

# 9. If upstream changes, rebase
git fetch upstream
git rebase upstream/main
git push --force-with-lease origin feature/my-feature

# 10. After merge, sync and cleanup
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
git branch -d feature/my-feature
git push origin --delete feature/my-feature
```

---

# STAGE 7 — PRODUCTION GIT OPERATIONS

## Topics to Learn

### 1. Stashing

* `git stash`
* `git stash pop`
* `git stash apply`
* **`git stash list`**
* **Named Stashes**

### 2. Reset

* **Soft Reset** (`--soft`)
* **Mixed Reset** (`--mixed`, default)
* **Hard Reset** (`--hard`)
* **When to Use Each**

### 3. Revert

* Safe Reverts
* Production Reverts
* **Revert vs Reset**

### 4. Reflog

* Recover Deleted Commits
* Recover Lost Branches
* **Time-Based Recovery**

### 5. Cherry Pick

* Porting Hotfixes
* Emergency Fixes
* **Cherry-Pick Conflicts**

### 6. Tags

* Lightweight Tags
* Annotated Tags
* Release Management
* **Semantic Versioning**

### 7. Detached HEAD

* Causes
* Recovery
* **When It's Useful**

---

## Practical Tasks

### Task 1 — Basic Stashing

```bash
# Working on feature but need to switch branches urgently
echo "work in progress" >> feature.txt
git add feature.txt

# Stash changes
git stash

# OR with message
git stash save "WIP: implementing user authentication"

# Check stash list
git stash list
# Output: stash@{0}: WIP: implementing user authentication

# Switch to another branch
git checkout main
# Make urgent fix
git checkout feature/authentication

# Restore stash
git stash pop

# OR apply without removing from stash
git stash apply
```

---

### Task 2 — Advanced Stashing

```bash
# Stash only staged changes
git stash --keep-index

# Stash including untracked files
git stash -u

# Stash everything (including ignored files)
git stash -a

# List all stashes
git stash list
# stash@{0}: WIP on feature: abc1234 Latest commit
# stash@{1}: WIP on main: def5678 Another commit

# Apply specific stash
git stash apply stash@{1}

# Show stash contents
git stash show -p stash@{0}

# Drop specific stash
git stash drop stash@{0}

# Clear all stashes
git stash clear
```

---

### Task 3 — Create Branch from Stash

```bash
# Stash changes
git stash

# Later, create branch from stash
git stash branch feature/new-work stash@{0}

# This:
# 1. Creates new branch
# 2. Applies stash
# 3. Drops stash
```

---

### Task 4 — Understanding Reset Types

```bash
# Create some commits
echo "v1" > test.txt
git add test.txt
git commit -m "Version 1"

echo "v2" >> test.txt
git commit -am "Version 2"

echo "v3" >> test.txt
git commit -am "Version 3"

# Current state:
# HEAD -> Version 3
# test.txt contains: v1 v2 v3

# SOFT RESET (move HEAD, keep changes staged)
git reset --soft HEAD~1
git status
# Changes to be committed:
#   modified: test.txt (v3 changes are staged)

# Commit again if needed
git commit -m "Version 3 revised"

# MIXED RESET (move HEAD, keep changes unstaged) - DEFAULT
git reset HEAD~1
# OR
git reset --mixed HEAD~1
git status
# Changes not staged for commit:
#   modified: test.txt (v3 changes are unstaged)

# HARD RESET (move HEAD, discard changes) - DANGEROUS!
git reset --hard HEAD~1
git status
# Working tree clean (v3 changes are GONE)
```

**When to Use:**

* **--soft**: Undo commits but keep all changes staged (good for combining commits)
* **--mixed**: Undo commits and unstage changes (good for reorganizing)
* **--hard**: Undo commits and discard changes (DANGEROUS - use carefully!)

---

### Task 5 — Reset to Specific Commit

```bash
# View history
git log --oneline
# abc1234 (HEAD) Latest commit
# def5678 Middle commit
# ghi9012 Old commit

# Reset to specific commit
git reset --soft def5678
git reset --mixed ghi9012
git reset --hard abc1234
```

---

### Task 6 — Safe Production Revert

```bash
# BAD commit was pushed to production
git log --oneline
# abc1234 (HEAD) BAD: broke production
# def5678 Good deployment
# ghi9012 Feature A

# DON'T use reset (rewrites history)
# git reset --hard def5678  ❌

# DO use revert (creates new commit)
git revert abc1234  ✅

# This creates new commit that undoes abc1234
git log --oneline
# jkl3456 (HEAD) Revert "BAD: broke production"
# abc1234 BAD: broke production
# def5678 Good deployment

# Push safely
git push origin main
```

---

### Task 7 — Revert Multiple Commits

```bash
# Revert last 3 commits
git revert HEAD~2..HEAD

# OR revert range
git revert abc1234..def5678

# Revert without auto-commit
git revert -n HEAD
git revert -n HEAD~1
git commit -m "Revert last two commits"
```

---

### Task 8 — Using Reflog (Recovery)

```bash
# Accidentally deleted branch or reset too far
git reflog

# Output:
# abc1234 HEAD@{0}: reset: moving to HEAD~5
# def5678 HEAD@{1}: commit: Important feature
# ghi9012 HEAD@{2}: commit: Another commit

# Recover lost commit
git checkout def5678
git checkout -b recovered-feature

# OR cherry-pick the commit
git cherry-pick def5678

# OR reset to that point
git reset --hard def5678
```

---

### Task 9 — Reflog Time-Based Recovery

```bash
# Show reflog with timestamps
git reflog show --date=relative

# Go back to state from 2 hours ago
git reset --hard HEAD@{2.hours.ago}

# Go back to state from yesterday
git reset --hard HEAD@{yesterday}

# Go back to specific date
git reset --hard master@{2024-01-15}
```

---

### Task 10 — Cherry Pick

```bash
# Hotfix was made on release branch, need it in main
git checkout release/1.0
git log --oneline
# abc1234 Fix critical security bug
# def5678 Previous commit

# Switch to main
git checkout main

# Cherry-pick the fix
git cherry-pick abc1234

# Commit is now in main
```

---

### Task 11 — Cherry Pick with Conflicts

```bash
# Cherry-pick a commit
git cherry-pick abc1234

# If conflict occurs:
# CONFLICT (content): Merge conflict in file.txt
# error: could not apply abc1234...

# Resolve conflict
vim file.txt
# Fix conflicts

# Stage resolved file
git add file.txt

# Continue cherry-pick
git cherry-pick --continue

# OR abort if too complex
git cherry-pick --abort
```

---

### Task 12 — Cherry Pick Multiple Commits

```bash
# Cherry-pick range of commits
git cherry-pick abc1234..def5678

# Cherry-pick multiple specific commits
git cherry-pick abc1234 def5678 ghi9012
```

---

### Task 13 — Create Tags (Semantic Versioning)

```bash
# Lightweight tag (simple pointer)
git tag v1.0.0

# Annotated tag (recommended - has metadata)
git tag -a v1.0.0 -m "Release version 1.0.0 - Initial production release"

# Tag specific commit
git tag -a v0.9.0 abc1234 -m "Beta release"

# List all tags
git tag
git tag -l

# Show tag details
git show v1.0.0

# Push single tag
git push origin v1.0.0

# Push all tags
git push origin --tags
```

**Semantic Versioning:**

* `v1.0.0` - Major.Minor.Patch
* `v1.0.1` - Patch (bug fixes)
* `v1.1.0` - Minor (new features, backward compatible)
* `v2.0.0` - Major (breaking changes)

---

### Task 14 — Work with Tags

```bash
# Checkout tag
git checkout v1.0.0

# This puts you in "detached HEAD" state

# Create branch from tag
git checkout -b hotfix/v1.0.1 v1.0.0

# Delete local tag
git tag -d v1.0.0

# Delete remote tag
git push origin --delete v1.0.0

# Search tags
git tag -l "v1.*"
```

---

### Task 15 — Detached HEAD State

```bash
# Detached HEAD occurs when you checkout:
# - A commit hash
git checkout abc1234

# - A tag
git checkout v1.0.0

# - A remote branch
git checkout origin/main

# Current state:
# You are in 'detached HEAD' state

# To recover:

# Option 1: Create branch from this point
git checkout -b new-feature

# Option 2: Go back to branch
git checkout main

# Option 3: If you made commits in detached state
git checkout -b save-my-work
# Or note the commit hash and cherry-pick it
git log  # Note the hash
git checkout main
git cherry-pick <hash>
```

---

### Task 16 — Production Rollback Workflow

```bash
# Production is broken due to recent deploy
git log --oneline
# abc1234 (HEAD, main) Deploy v2.1.0 - BROKEN
# def5678 Deploy v2.0.0 - LAST GOOD
# ghi9012 Deploy v1.9.0

# Step 1: Revert to last good state
git revert abc1234

# Step 2: Or create hotfix
git checkout -b hotfix/emergency-fix def5678
# Apply minimal fix
git commit -am "hotfix: fix critical production issue"

# Step 3: Tag the fix
git tag -a v2.0.1 -m "Emergency hotfix"

# Step 4: Deploy
git checkout main
git merge hotfix/emergency-fix
git push origin main
git push origin v2.0.1
```

---

# STAGE 8 — PRODUCTION SAFETY & RULES 🚨

## Topics to Learn

### 1. Dangerous Commands

* **Commands to NEVER Use in Production**
* **When Force Push is Acceptable**
* **Safe Alternatives**

### 2. Force Push Rules

* `--force` vs `--force-with-lease`
* **When It's OK**
* **When It's FORBIDDEN**

### 3. Branch Protection

* Protected Branches
* Approval Rules
* **Status Checks**

### 4. Production Checklist

* Pre-Push Checks
* **Team Communication**
* **Rollback Plans**

### 5. Git Hooks for Safety

* Pre-commit
* Pre-push
* **Automated Validations**

---

## ❌ DANGEROUS COMMANDS - NEVER IN PRODUCTION

### 1. Force Push (Wrong Way)

```bash
# ❌ NEVER DO THIS
git push --force
git push -f

# Why dangerous:
# - Overwrites remote history
# - Deletes other people's commits
# - Breaks team's work
# - No safety check

# ✅ SAFE ALTERNATIVE
git push --force-with-lease origin feature/my-branch

# Why safer:
# - Checks if remote has commits you don't have
# - Prevents overwriting others' work
# - Still force pushes, but with safety check
```

---

### 2. Hard Reset on Shared Branches

```bash
# ❌ NEVER DO THIS on main/master/develop
git checkout main
git reset --hard HEAD~5
git push --force  # Disaster!

# Why dangerous:
# - Deletes commits permanently
# - Rewrites shared history
# - Breaks everyone's local repos

# ✅ SAFE ALTERNATIVE
git revert HEAD~4..HEAD
git push origin main

# Why safer:
# - Creates new commits
# - Doesn't rewrite history
# - Everyone can pull safely
```

---

### 3. Rebase on Public Branches

```bash
# ❌ NEVER DO THIS
git checkout main
git rebase feature/something
git push --force

# Why dangerous:
# - Rewrites shared history
# - Changes commit hashes
# - Breaks everyone's branches

# ✅ SAFE ALTERNATIVE
git checkout main
git merge feature/something
git push origin main

# Why safer:
# - Preserves history
# - No force push needed
# - Safe for everyone
```

---

### 4. Amend Pushed Commits

```bash
# ❌ DANGEROUS if already pushed to shared branch
git commit --amend -m "New message"
git push --force

# Why dangerous:
# - Changes commit hash
# - Rewrites history
# - Breaks branches based on original commit

# ✅ SAFE - only on local unpushed commits
git commit --amend -m "New message"  # Before first push is OK

# ✅ SAFE - only on personal feature branches
git commit --amend
git push --force-with-lease origin feature/my-personal-branch
```

---

### 5. Delete Branch Without Checking

```bash
# ❌ Force delete without verification
git branch -D important-feature

# Why dangerous:
# - Might contain unmerged work
# - No warning given
# - Hard to recover

# ✅ SAFE - checks if merged first
git branch -d important-feature

# If unmerged:
# error: The branch 'important-feature' is not fully merged.
# If you are sure you want to delete it, run 'git branch -D important-feature'.
```

---

### 6. Checkout with Force

```bash
# ❌ Loses all uncommitted changes
git checkout -f main

# Why dangerous:
# - Discards all local changes
# - No warning
# - Unrecoverable

# ✅ SAFE - stash first
git stash
git checkout main
git stash pop
```

---

### 7. Clean Without Dry Run

```bash
# ❌ Deletes untracked files immediately
git clean -fd

# Why dangerous:
# - Permanent deletion
# - No undo

# ✅ SAFE - check first
git clean -n  # Dry run
git clean -fd # Only after reviewing
```

---

## ✅ WHEN FORCE PUSH IS ACCEPTABLE

```bash
# 1. Personal feature branch (only you working on it)
git push --force-with-lease origin feature/my-personal-feature

# 2. After interactive rebase on YOUR branch
git checkout feature/cleanup
git rebase -i HEAD~5
git push --force-with-lease origin feature/cleanup

# 3. Fixing commit message BEFORE PR merge
git commit --amend -m "fix: correct commit message"
git push --force-with-lease origin feature/my-branch

# 4. Emergency hotfix with TEAM APPROVAL
# Document in team chat first!
git push --force-with-lease origin hotfix/critical-fix
```

---

## ❌ WHEN FORCE PUSH IS FORBIDDEN

```bash
# NEVER force push to these branches:

# 1. main / master
git push --force origin main  ❌

# 2. develop
git push --force origin develop  ❌

# 3. Shared feature branches
git push --force origin feature/team-working  ❌

# 4. Release branches
git push --force origin release/v1.0.0  ❌

# 5. After PR is merged
git push --force origin feature/merged-pr  ❌

# 6. Production branches
git push --force origin production  ❌
```

---

## Practical Tasks

### Task 1 — Setup Branch Protection on GitHub

**Steps:**

1. Go to repository Settings
2. Click "Branches" in sidebar
3. Click "Add rule"
4. Branch name pattern: `main`
5. Enable:
   * ✅ Require a pull request before merging
   * ✅ Require approvals: 2
   * ✅ Require status checks to pass before merging
   * ✅ Require branches to be up to date before merging
   * ✅ Do not allow bypassing the above settings
   * ✅ Restrict who can push to matching branches
   * ✅ Do not allow force pushes
   * ✅ Do not allow deletions
6. Click "Create"

---

### Task 2 — Safe Force Push Practice

```bash
# Create personal feature branch
git checkout -b feature/safe-force-push-demo

# Make some commits
echo "v1" > test.txt
git add test.txt
git commit -m "Add test file v1"

echo "v2" >> test.txt
git commit -am "Add test file v2"

echo "v3" >> test.txt
git commit -am "Add test file v3"

# Push to remote
git push origin feature/safe-force-push-demo

# Squash commits locally (clean history)
git rebase -i HEAD~3
# In editor, mark 2nd and 3rd commits as 'squash'

# Try normal push (will be rejected)
git push origin feature/safe-force-push-demo
# Error: Updates were rejected

# ❌ DON'T DO THIS
# git push --force origin feature/safe-force-push-demo

# ✅ DO THIS
git push --force-with-lease origin feature/safe-force-push-demo
# Success - checks that no one else pushed
```

---

### Task 3 — Pre-Push Safety Check Script

Create `.git/hooks/pre-push`:

```bash
#!/bin/bash

current_branch=$(git rev-parse --abbrev-ref HEAD)
protected_branches=("main" "master" "develop" "production")

# Check if pushing to protected branch
for branch in "${protected_branches[@]}"; do
    if [ "$current_branch" = "$branch" ]; then
        echo "⚠️  WARNING: You're pushing to $current_branch!"
        read -p "Are you absolutely sure? (type 'yes' to confirm): " confirm
        if [ "$confirm" != "yes" ]; then
            echo "❌ Push cancelled."
            exit 1
        fi
    fi
done

# Check for large files
large_files=$(git diff --cached --name-only | xargs ls -lh 2>/dev/null | awk '$5 ~ /M$/ && $5+0 > 10 {print $9}')
if [ -n "$large_files" ]; then
    echo "⚠️  Large files detected:"
    echo "$large_files"
    read -p "Continue pushing? (yes/no): " confirm
    if [ "$confirm" != "yes" ]; then
        echo "❌ Push cancelled."
        exit 1
    fi
fi

# Check for potential secrets
if git diff --cached | grep -iE "password|secret|api_key|private_key|token"; then
    echo "⚠️  Potential secrets detected!"
    echo "Please review your changes for sensitive data."
    read -p "Continue anyway? (yes/no): " confirm
    if [ "$confirm" != "yes" ]; then
        echo "❌ Push cancelled."
        exit 1
    fi
fi

echo "✅ Pre-push checks passed"
exit 0
```

Make executable:

```bash
chmod +x .git/hooks/pre-push
```

---

### Task 4 — Production Push Checklist

```bash
#!/bin/bash
# save as: git-production-push.sh

echo "🔍 PRODUCTION PUSH CHECKLIST"
echo "================================"

# 1. Check current branch
current_branch=$(git branch --show-current)
echo "✓ Current branch: $current_branch"

if [ "$current_branch" = "main" ] || [ "$current_branch" = "master" ]; then
    echo "⚠️  WARNING: You're on $current_branch!"
    read -p "Continue? (yes/no): " confirm
    [ "$confirm" != "yes" ] && exit 1
fi

# 2. Pull latest changes
echo "✓ Pulling latest changes..."
git fetch origin
git pull --rebase origin main

# 3. Check what you're pushing
echo "✓ Commits to be pushed:"
git log origin/main..HEAD --oneline

read -p "Do these commits look correct? (yes/no): " confirm
[ "$confirm" != "yes" ] && exit 1

# 4. Run tests (if available)
if [ -f "package.json" ]; then
    echo "✓ Running tests..."
    npm test || exit 1
fi

# 5. Dry run
echo "✓ Performing dry run..."
git push --dry-run origin $current_branch

# 6. Confirm push
read -p "Ready to push to production? (yes/no): " confirm
if [ "$confirm" = "yes" ]; then
    git push origin $current_branch
    echo "✅ Push successful!"
else
    echo "❌ Push cancelled."
    exit 1
fi
```

Make executable and use:

```bash
chmod +x git-production-push.sh
./git-production-push.sh
```

---

### Task 5 — Recovery from Accidental Force Push

```bash
# Someone force-pushed and deleted your commits
# DON'T PANIC!

# Step 1: Find your lost commits
git reflog

# Output:
# abc1234 HEAD@{0}: reset: moving to HEAD~1
# def5678 HEAD@{1}: commit: My important commit
# ghi9012 HEAD@{2}: commit: Another important commit

# Step 2: Recover lost commits
# Option A: Cherry-pick them
git cherry-pick def5678
git cherry-pick ghi9012

# Option B: Create new branch from lost commit
git branch recovery-branch def5678
git checkout recovery-branch

# Option C: Reset to that point (if you want all history)
git reset --hard def5678

# Step 3: Push recovery
git push origin recovery-branch
```

---

### Task 6 — Pre-Commit Hook (Prevent Secrets)

Create `.git/hooks/pre-commit`:

```bash
#!/bin/bash

echo "🔍 Running pre-commit checks..."

# Check for secrets in staged files
secrets_patterns=(
    "password"
    "secret"
    "api_key"
    "private_key"
    "token"
    "AWS_ACCESS_KEY"
    "AWS_SECRET_KEY"
)

for pattern in "${secrets_patterns[@]}"; do
    if git diff --cached | grep -i "$pattern"; then
        echo "❌ ERROR: Potential secret detected: $pattern"
        echo "Please remove sensitive data before committing."
        exit 1
    fi
done

# Check for .env files
if git diff --cached --name-only | grep -q ".env"; then
    echo "❌ ERROR: .env file detected in commit"
    echo "Add .env to .gitignore instead."
    exit 1
fi

# Lint YAML files
yaml_files=$(git diff --cached --name-only --diff-filter=ACM | grep '\.ya*ml$')
if [ -n "$yaml_files" ]; then
    echo "✓ Linting YAML files..."
    for file in $yaml_files; do
        if command -v yamllint &> /dev/null; then
            yamllint "$file"
            if [ $? -ne 0 ]; then
                echo "❌ YAML lint failed for $file"
                exit 1
            fi
        fi
    done
fi

# Check for debug statements
if git diff --cached | grep -E "console\.log|debugger|print\("; then
    echo "⚠️  WARNING: Debug statements detected"
    read -p "Continue anyway? (yes/no): " confirm
    if [ "$confirm" != "yes" ]; then
        exit 1
    fi
fi

echo "✅ Pre-commit checks passed"
exit 0
```

Make executable:

```bash
chmod +x .git/hooks/pre-commit
```

---

### Task 7 — Setup Git Aliases for Safety

```bash
# Safe force push
git config --global alias.force-push 'push --force-with-lease'

# Safe delete branch
git config --global alias.delete-branch 'branch -d'

# Show what would be pushed
git config --global alias.ready 'log origin/main..HEAD --oneline'

# Undo last commit (keep changes)
git config --global alias.undo 'reset HEAD~1'

# Usage:
git force-push origin feature/my-branch
git delete-branch feature/old-branch
git ready
git undo
```

---

# STAGE 9 — ADVANCED GIT

## Topics to Learn

### 1. Rebase

* Interactive Rebase
* Rebase vs Merge
* Squashing Commits
* Rewriting History
* **When NOT to Rebase**

### 2. Advanced Log Filtering

* Search Commits by Message
* Search by Author
* Search by File Changes
* **Search by Date/Time**
* **Search by Code Content**

### 3. Bisect

* Binary Search for Bugs
* **Automated Bisect with Scripts**

### 4. Submodules

* Managing Dependencies
* **Submodule vs Subtree**

### 5. Worktrees

* Multiple Working Trees
* **Parallel Development**

### 6. Hooks

* Client-Side Hooks
* Server-Side Hooks
* **Custom Validation**

### 7. Advanced Conflict Resolution

* Merge Strategies
* **Recursive Strategy**
* **Ours/Theirs Strategy**

---

## Practical Tasks

### Task 1 — Interactive Rebase (Clean History)

```bash
# Create messy commit history
git checkout -b feature/messy-commits

echo "v1" > file.txt
git add file.txt
git commit -m "wip"

echo "v2" >> file.txt
git commit -am "temp commit"

echo "v3" >> file.txt
git commit -am "fix typo"

echo "v4" >> file.txt
git commit -am "actually add feature"

echo "v5" >> file.txt
git commit -am "final version"

# View history (messy)
git log --oneline
# Output:
# e5e5e5e final version
# d4d4d4d actually add feature
# c3c3c3c fix typo
# b2b2b2b temp commit
# a1a1a1a wip

# Clean up with interactive rebase
git rebase -i HEAD~5

# Editor opens with:
# pick a1a1a1a wip
# pick b2b2b2b temp commit
# pick c3c3c3c fix typo
# pick d4d4d4d actually add feature
# pick e5e5e5e final version

# Change to:
# pick a1a1a1a wip
# squash b2b2b2b temp commit
# squash c3c3c3c fix typo
# reword d4d4d4d actually add feature
# squash e5e5e5e final version

# Save and close editor

# New editor opens for commit message
# Write clean message:
# feat: add new feature with complete implementation

# Result: 5 messy commits → 1 clean commit
git log --oneline
# Output:
# f6f6f6f feat: add new feature with complete implementation
```

**Interactive Rebase Commands:**

* `pick` - Use commit as-is
* `reword` - Use commit, but edit message
* `edit` - Use commit, but stop to amend
* `squash` - Combine with previous commit
* `fixup` - Like squash, but discard commit message
* `drop` - Remove commit
* `exec` - Run shell command

---

### Task 2 — Rebase vs Merge (When to Use)

```bash
# Scenario: Feature branch diverged from main

# MERGE (preserves history)
git checkout main
git merge feature/my-feature
# Creates merge commit
# History: Linear with merge point visible

# REBASE (rewrites history)
git checkout feature/my-feature
git rebase main
# Moves commits on top of main
# History: Linear, no merge commit

# When to MERGE:
# - Public/shared branches
# - Want to preserve history
# - Multiple developers on branch

# When to REBASE:
# - Personal feature branches
# - Want clean linear history
# - Before merging to main
```

---

### Task 3 — Advanced Log Filtering

```bash
# Search commits by author
git log --author="John Doe"
git log --author="john@example.com"

# Search commits by message
git log --grep="fix:"
git log --grep="bug" --grep="error" --all-match

# Search commits that changed specific file
git log -- deployment.yaml
git log --follow -- old-name.yaml  # Follows renames

# Search by date range
git log --since="2 weeks ago"
git log --after="2024-01-01" --before="2024-01-31"
git log --since="2024-01-01" --until="2024-12-31"

# Search commits that added/removed specific code
git log -S "replicas: 3"  # Pickaxe search
git log -G "regex-pattern"  # Regex search

# Combine filters
git log --author="John" --since="1 month ago" --grep="fix"

# Pretty format
git log --pretty=format:"%h - %an, %ar : %s"
# Output: abc1234 - John Doe, 2 days ago : fix: resolve issue

# Custom format with colors
git log --pretty=format:"%C(yellow)%h%C(reset) - %C(green)%an%C(reset), %C(blue)%ar%C(reset) : %s"

# Show stats
git log --stat
git log --shortstat
git log --name-only
git log --name-status

# One-line with graph
git log --oneline --graph --all --decorate
```

---

### Task 4 — Git Bisect (Find Bug)

```bash
# Bug was introduced somewhere in last 20 commits
# Manual bisect:

git bisect start

# Current version has bug
git bisect bad

# 20 commits ago was working
git bisect good HEAD~20

# Git checks out middle commit
# Test if bug exists
# Run your app and check

# If bug exists:
git bisect bad

# If no bug:
git bisect good

# Repeat until Git finds the bad commit
# Git will show:
# "abc1234 is the first bad commit"

# End bisect
git bisect reset
```

---

### Task 5 — Automated Bisect

```bash
# Create test script
cat > test-bug.sh << 'EOF'
#!/bin/bash
# Test if bug exists (exit 0 = good, exit 1 = bad)

if grep -q "bug-pattern" app.js; then
    exit 1  # Bug exists
else
    exit 0  # No bug
fi
EOF

chmod +x test-bug.sh

# Run automated bisect
git bisect start HEAD HEAD~20
git bisect run ./test-bug.sh

# Git automatically finds the bad commit
# Output: abc1234 is the first bad commit

git bisect reset
```

---

### Task 6 — Working with Submodules

```bash
# Add submodule to your repo
git submodule add https://github.com/user/library.git libs/library

# This creates:
# - .gitmodules file
# - libs/library directory

# Commit the submodule
git commit -m "Add library submodule"

# Clone repo with submodules
git clone --recursive https://github.com/user/main-repo.git

# OR clone then init submodules
git clone https://github.com/user/main-repo.git
cd main-repo
git submodule init
git submodule update

# Update submodule to latest
cd libs/library
git pull origin main
cd ../..
git add libs/library
git commit -m "Update library submodule"

# Update all submodules
git submodule update --remote --merge

# Remove submodule
git submodule deinit libs/library
git rm libs/library
rm -rf .git/modules/libs/library
```

---

### Task 7 — Git Worktrees (Work on Multiple Branches)

```bash
# Main worktree
cd my-project

# Create additional worktree for hotfix
git worktree add ../my-project-hotfix hotfix/critical-bug

# Now you have two directories:
# my-project/           (main branch)
# my-project-hotfix/    (hotfix/critical-bug branch)

# Work in hotfix worktree
cd ../my-project-hotfix
# Make changes
git commit -am "Fix critical bug"

# Back to main worktree
cd ../my-project

# List worktrees
git worktree list
# Output:
# /path/to/my-project           abc1234 [main]
# /path/to/my-project-hotfix    def5678 [hotfix/critical-bug]

# Remove worktree
git worktree remove ../my-project-hotfix

# Or manually:
cd ../my-project
rm -rf ../my-project-hotfix
git worktree prune
```

---

### Task 8 — Git Hooks (Pre-Commit Example)

```bash
# Create pre-commit hook
cat > .git/hooks/pre-commit << 'EOF'
#!/bin/bash

echo "🔍 Running pre-commit checks..."

# 1. Check for secrets
if git diff --cached | grep -iE "password|secret|api_key"; then
    echo "❌ Potential secret detected!"
    exit 1
fi

# 2. Lint JavaScript files
js_files=$(git diff --cached --name-only --diff-filter=ACM | grep '\.js$')
if [ -n "$js_files" ]; then
    echo "✓ Linting JavaScript..."
    npx eslint $js_files
    if [ $? -ne 0 ]; then
        echo "❌ ESLint failed"
        exit 1
    fi
fi

# 3. Run tests
echo "✓ Running tests..."
npm test
if [ $? -ne 0 ]; then
    echo "❌ Tests failed"
    exit 1
fi

echo "✅ All checks passed"
exit 0
EOF

chmod +x .git/hooks/pre-commit
```

**Available Hooks:**

* `pre-commit` - Before commit
* `prepare-commit-msg` - Before commit message editor
* `commit-msg` - After commit message
* `post-commit` - After commit
* `pre-push` - Before push
* `pre-rebase` - Before rebase

---

### Task 9 — Advanced Merge Strategies

```bash
# Default recursive strategy
git merge feature/branch

# Ours strategy (keep our version in conflicts)
git merge -X ours feature/branch
# In conflicts, automatically choose "our" version

# Theirs strategy (prefer their version)
git merge -X theirs feature/branch
# In conflicts, automatically choose "their" version

# Patience strategy (better for large refactors)
git merge -s recursive -X patience feature/large-refactor

# Ignore whitespace changes
git merge -X ignore-space-change feature/formatting

# Octopus strategy (merge multiple branches)
git merge branch1 branch2 branch3
```

---

### Task 10 — Find When Code Was Changed

```bash
# Find when a specific line was changed
git log -L 15,20:file.txt
# Shows history of lines 15-20 in file.txt

# Find when a function was changed
git log -L :functionName:file.js

# Show who changed each line and when
git blame file.txt

# Ignore formatting commits in blame
git blame -w file.txt  # Ignore whitespace

# Show full commit in blame
git blame -L 10,20 file.txt
git show <commit-hash>
```

---

# STAGE 10 — GIT INTERNALS

## Topics to Learn

### 1. Git Objects

* **Blob** (file content)
* **Tree** (directory structure)
* **Commit** (snapshot)
* **Tag** (reference)

### 2. SHA Hashing

* Object IDs
* How Git Generates Hashes
* **Hash Collisions** (extremely rare)

### 3. Git Database

* Object Storage
* **Pack Files** (compression)
* **Garbage Collection**

### 4. References

* HEAD
* Branches (refs/heads/)
* Tags (refs/tags/)
* **Remote Refs** (refs/remotes/)

### 5. Plumbing Commands

* `git cat-file`
* `git hash-object`
* `git ls-tree`
* `git rev-parse`
* `git fsck`
* **`git count-objects`**

---

## Practical Tasks

### Task 1 — Explore .git Directory

```bash
# View .git structure
ls -la .git

# Structure:
.git/
├── config          # Repository configuration
├── description     # Repository description
├── HEAD            # Points to current branch
├── hooks/          # Git hooks scripts
├── index           # Staging area (binary)
├── info/           # Global exclude patterns
│   └── exclude
├── objects/        # All Git objects (commits, trees, blobs)
│   ├── pack/       # Packed objects (compressed)
│   └── info/
├── refs/           # References (branches, tags)
│   ├── heads/      # Local branches
│   ├── remotes/    # Remote branches
│   └── tags/       # Tags
└── logs/           # Reflogs

# View specific files
cat .git/HEAD
# Output: ref: refs/heads/main

cat .git/refs/heads/main
# Output: abc123def456... (commit hash)

cat .git/config
# Repository configuration
```

---

### Task 2 — Understand Git Objects

```bash
# Get latest commit hash
git log --oneline -1
# Output: abc1234 Latest commit

# Inspect commit object
git cat-file -t abc1234
# Output: commit

git cat-file -p abc1234
# Output:
# tree def5678
# parent ghi9012
# author John Doe <john@example.com> 1234567890 +0000
# committer John Doe <john@example.com> 1234567890 +0000
#
# Latest commit

# Inspect tree object
git cat-file -p def5678
# Output:
# 100644 blob aaa1111 README.md
# 100644 blob bbb2222 app.js
# 040000 tree ccc3333 src

# Inspect blob (file content)
git cat-file -p aaa1111
# Output: (contents of README.md)
```

---

### Task 3 — Create Git Objects Manually

```bash
# Create file
echo "Hello Git Internals" > test.txt

# Generate hash (doesn't store in Git)
git hash-object test.txt
# Output: e69de29bb2d1d6434b8b29ae775ad8c2e48c5391

# Store in Git database
git hash-object -w test.txt
# Output: e69de29bb2d1d6434b8b29ae775ad8c2e48c5391

# Verify object exists
ls .git/objects/e6/9de29bb2d1d6434b8b29ae775ad8c2e48c5391

# Retrieve content
git cat-file -p e69de29bb2d1d6434b8b29ae775ad8c2e48c5391
# Output: Hello Git Internals
```

---

### Task 4 — Understand References

```bash
# See what HEAD points to
cat .git/HEAD
# Output: ref: refs/heads/main

# See what main branch points to
cat .git/refs/heads/main
# Output: abc123def456... (commit hash)

# List all references
git show-ref
# Output:
# abc1234 refs/heads/main
# def5678 refs/heads/feature/test
# ghi9012 refs/remotes/origin/main
# jkl3456 refs/tags/v1.0.0

# Resolve reference to hash
git rev-parse main
# Output: abc123def456...

git rev-parse HEAD
# Output: abc123def456...

git rev-parse HEAD~2
# Output: (hash of 2 commits before HEAD)
```

---

### Task 5 — Examine Index (Staging Area)

```bash
# View staging area contents
git ls-files --stage
# Output:
# 100644 abc1234... 0  README.md
# 100644 def5678... 0  app.js

# View detailed index
git ls-files -s -v
```

---

### Task 6 — Garbage Collection

```bash
# See object count
git count-objects -v
# Output:
# count: 150
# size: 2048
# in-pack: 0
# packs: 0
# size-pack: 0
# prune-packable: 0
# garbage: 0
# size-garbage: 0

# Run garbage collection
git gc

# After GC:
git count-objects -v
# Objects are packed for efficiency

# Aggressive garbage collection
git gc --aggressive --prune=now

# This:
# - Packs loose objects
# - Removes unreachable objects
# - Compresses repository
```

---

### Task 7 — Examine Pack Files

```bash
# List pack files
ls -lh .git/objects/pack/

# View pack index
git verify-pack -v .git/objects/pack/pack-*.idx

# Unpack objects (for inspection)
git unpack-objects < .git/objects/pack/pack-*.pack
```

---

### Task 8 — Check Repository Integrity

```bash
# Check for corrupted objects
git fsck

# Output (if healthy):
# Checking object directories: 100% done.
# Checking objects: 100% done.

# Full check
git fsck --full

# Find dangling commits
git fsck --lost-found

# Dangling commits are orphaned (not referenced)
# You can recover them if needed
```

---

### Task 9 — Understand Commit Ancestry

```bash
# Parent of HEAD
git rev-parse HEAD^
git rev-parse HEAD~1

# Grandparent of HEAD
git rev-parse HEAD^^
git rev-parse HEAD~2

# First parent of merge commit
git rev-parse HEAD^1

# Second parent of merge commit
git rev-parse HEAD^2

# View commit tree
git log --oneline --graph --all

# Show commit parents
git log --pretty=format:"%h %p - %s"
# Output: abc1234 def5678 - Commit message
```

---

### Task 10 — Low-Level Commands (Plumbing)

```bash
# Update reference
git update-ref refs/heads/test abc1234

# Create symbolic reference
git symbolic-ref HEAD refs/heads/main

# Read tree into index
git read-tree <tree-hash>

# Write tree from index
git write-tree

# Create commit object manually
echo "Commit message" | git commit-tree <tree-hash> -p <parent-hash>

# These are low-level commands
# Normally you use porcelain commands (add, commit, push)
```

---

# 🎯 COMPLETION OF STAGES 1-10

Congratulations! You've completed the first 10 stages of the Git for DevOps Mastery Roadmap.

## What You've Learned:

✅ **Stage 1:** Git fundamentals and configuration  
✅ **Stage 2:** Local repository management  
✅ **Stage 3:** Branching and merging  
✅ **Stage 4:** Remote repositories  
✅ **Stage 5:** Merge conflict resolution (master level)  
✅ **Stage 6:** Fork and upstream workflows  
✅ **Stage 7:** Production Git operations (stash, reset, revert, tags)  
✅ **Stage 8:** Production safety rules and dangerous commands  
✅ **Stage 9:** Advanced Git (rebase, bisect, submodules, worktrees, hooks)  
✅ **Stage 10:** Git internals (objects, references, plumbing commands)

---

## 📝 Daily Practice Commands

```bash
# Morning routine
git fetch --all
git pull --rebase origin main

# Before any change
git checkout -b feature/descriptive-name
git status

# After changes
git add .
git commit -m "Clear message"
git push origin feature/descriptive-name

# Emergency stash
git stash
git stash pop

# NEVER in production
# git push --force  ❌
# git reset --hard  ❌
# git rebase (on shared branches)  ❌
```

---

## 🚨 CRITICAL RULES TO REMEMBER

### ❌ NEVER DO:
```bash
git push --force origin main
git reset --hard HEAD~5  # on shared branches
git rebase main  # when on main branch
git branch -D  # without checking first
git clean -fd  # without dry run first
```

### ✅ ALWAYS DO:
```bash
git push --force-with-lease  # instead of --force
git revert  # instead of reset on shared branches
git branch -d  # safe delete with merge check
git clean -n  # dry run before actual clean
git stash  # before switching branches with changes
```

---

## 📚 Next Steps

Part 2 of this roadmap will cover:

* **Stage 11:** Git + CI/CD
* **Stage 12:** GitOps with ArgoCD and FluxCD
* **Stage 13:** Enterprise Branching Strategies
* **Stage 14:** Terraform + Git
* **Stage 15:** Git + Docker + Kubernetes
* **Stage 16:** Production Incident Recovery
* **Stage 17:** Git Security
* **Stage 18:** Performance & Optimization
* **Stage 19:** Enterprise DevOps Workflow
* **Stage 20:** Master Level Practice Projects

---

## 🏆 You Are Now Ready For:

* Working in DevOps teams
* Managing production repositories
* Handling complex merge conflicts
* Contributing to open source projects
* Collaborating with fork/upstream workflows
* Recovering from Git disasters
* Understanding Git at a deep level

---

**Keep practicing, keep learning, and remember: Git is a tool that gets better with experience!** 🚀
