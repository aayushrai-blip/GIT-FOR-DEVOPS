# 🔴 STAGE 5 — Merge Conflicts Mastery

> Beginner → Advanced → Production-Level Conflict Resolution 🚀

---

## 📖 Goal of This Stage

This stage focuses on understanding and resolving Git merge conflicts professionally in real-world scenarios.

In production DevOps and software engineering environments, merge conflicts are extremely common when:

- 👥 Multiple developers modify the same files
- 🏗️ Infrastructure code changes simultaneously
- ☸️ Kubernetes manifests overlap
- 🌍 Terraform modules are updated together
- 🔄 CI/CD pipelines evolve rapidly
- 🔀 Long-lived feature branches are merged

### This stage teaches:

- ✅ Conflict detection and identification
- ✅ Manual and automated conflict resolution
- ✅ Merge tools (GUI and terminal)
- ✅ YAML conflict handling (Kubernetes)
- ✅ Terraform/HCL conflict resolution
- ✅ Production-safe merge workflows
- ✅ Conflict prevention strategies

---

## 📚 Table of Contents

- [What is a Merge Conflict](#-what-is-a-merge-conflict)
- [Git Conflict Workflow](#-git-conflict-workflow)
- [Why Conflicts Happen](#-why-merge-conflicts-happen)
- [Conflict Types](#-conflict-types)
- [Conflict Markers](#-conflict-markers)
- [Resolution Methods](#-conflict-resolution-methods)
- [Resolution Workflow](#-conflict-resolution-workflow)
- [Best Practices](#-enterprise-conflict-strategy)
- [DevOps Scenarios](#-devops-specific-conflicts)
- [Practical Tasks](#-practical-tasks)
- [Outcome](#-outcome-of-this-stage)

---

## 📚 What is a Merge Conflict?

A **merge conflict** occurs when Git cannot automatically determine which changes should be kept during a merge operation.

### Usually happens when:

- 📝 Same file is modified in different branches
- ✏️ Same lines are changed with different content
- 🌳 Different branch histories overlap
- 🔀 Concurrent development on shared code

### Example Scenario:

```
Developer A (main):        Developer B (feature):
replicas: 2                replicas: 5
     ↓                            ↓
          git merge attempt
                  ↓
            ⚠️ CONFLICT!
```

---

## 📌 Git Conflict Workflow

```text
Developer A Changes File
            ↓
Developer B Changes Same File
            ↓
    Git Merge Attempt
            ↓
   ⚠️ Conflict Detected
            ↓
Manual Resolution Required
            ↓
     git add + commit
            ↓
    Merge Completed ✅
```

---

## 📌 Why Merge Conflicts Happen?

| Cause | Example | Frequency |
|-------|---------|-----------|
| **Same line edited** | Two developers modify the same line | Very High |
| **File renamed differently** | Different rename operations on same file | Medium |
| **File deleted & modified** | One deletes, another edits | Medium |
| **Binary files** | Images/videos cannot auto-merge | Low |
| **YAML overlap** | Kubernetes manifest changes | High (DevOps) |
| **Terraform overlap** | Same HCL resources edited | High (DevOps) |
| **Whitespace changes** | Different indentation/formatting | Medium |

---

## 📌 Conflict Types

### 🔹 Content Conflicts

**Most common conflict type.**

Occurs when:
- ✅ Same file
- ✅ Same line(s)
- ✅ Different modifications

#### Example:

**Branch A (main):**
```yaml
replicas: 2
```

**Branch B (feature-scaling):**
```yaml
replicas: 5
```

**Result:**
```yaml
<<<<<<< HEAD
replicas: 2
=======
replicas: 5
>>>>>>> feature-scaling
```

> Git cannot decide which value is correct - **manual resolution required**.

---

### 🔹 Rename Conflicts

Occurs when the same file is renamed differently in two branches.

#### Example:

| Branch A | Branch B |
|----------|----------|
| `app.yaml` → `deployment.yaml` | `app.yaml` → `k8s.yaml` |

**Git cannot determine the final filename** and requires manual intervention.

---

### 🔹 Delete Conflicts

Occurs when:
- One branch **deletes** a file
- Another branch **modifies** the same file

#### Example:

| Branch A | Branch B |
|----------|----------|
| ❌ Deleted `nginx.conf` | ✏️ Modified `nginx.conf` |

**Git asks:**
- Keep deletion?
- Keep modifications?
- Manual decision required

---

### 🔹 Binary File Conflicts

Git **cannot auto-merge binary files** like:

- 🖼️ PNG, JPG, GIF
- 📦 ZIP, TAR
- 📄 PDFs
- 🎵 MP3, WAV
- 🎬 MP4, AVI

**Resolution:** Manual selection required - choose one version or the other.

---

### 🔹 Kubernetes Manifest Conflicts

**Very common in DevOps workflows.**

Common conflict scenarios:

- 🏷️ Image tag updates
- 📊 Replica count changes
- 🌐 Ingress rule modifications
- 💾 Resource limit adjustments
- 🔧 ConfigMap/Secret updates
- 📡 Service port changes

#### Example YAML Conflict:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
spec:
<<<<<<< HEAD
  replicas: 2
  image: nginx:1.19
=======
  replicas: 5
  image: nginx:1.21
>>>>>>> feature-scaling
```

**Resolution needed for:**
- Replica count (2 vs 5)
- Image version (1.19 vs 1.21)

---

### 🔹 Terraform Conflicts

Occurs in `.tf` files during infrastructure changes.

Common scenarios:

- 🏗️ Resource name changes
- 🔢 Variable conflicts
- 📦 Module version conflicts
- 🌍 Provider version mismatches
- 🔧 Resource attribute changes

#### Example HCL Conflict:

```hcl
resource "aws_instance" "web" {
<<<<<<< HEAD
  instance_type = "t2.micro"
  ami           = "ami-12345"
=======
  instance_type = "t3.medium"
  ami           = "ami-67890"
>>>>>>> feature-update
}
```

**Resolution needed for:**
- Instance type (t2.micro vs t3.medium)
- AMI ID (different images)

---

## 📌 Conflict Markers

Git inserts special markers inside conflicted files to show the conflict boundaries.

### Structure:

```
<<<<<<< HEAD
Current branch code
=======
Incoming branch code
>>>>>>> feature-branch
```

### 📌 Meaning of Markers:

| Marker | Meaning | Description |
|--------|---------|-------------|
| `<<<<<<< HEAD` | Current branch | Code from the branch you're on |
| `=======` | Separator | Divides the two conflicting versions |
| `>>>>>>> branch-name` | Incoming changes | Code from the branch being merged |

### Real Example:

```python
def calculate_discount(price):
<<<<<<< HEAD
    # Apply 10% discount
    return price * 0.9
=======
    # Apply 15% discount
    return price * 0.85
>>>>>>> feature-pricing
```

---

## 📌 Conflict Resolution Methods

### 🔹 Manual Resolution

**Most common and flexible approach.**

#### Steps:

1. **Check status:**
   ```bash
   git status
   ```

2. **Open conflicted file:**
   ```bash
   vim deployment.yaml
   # or
   code deployment.yaml
   ```

3. **Remove conflict markers and choose correct code:**
   - Delete `<<<<<<< HEAD`
   - Delete `=======`
   - Delete `>>>>>>> branch-name`
   - Keep the correct code (or combine both)

4. **Stage the resolved file:**
   ```bash
   git add deployment.yaml
   ```

5. **Commit the merge:**
   ```bash
   git commit
   ```

#### Example Resolution:

**Before (conflicted):**
```yaml
<<<<<<< HEAD
replicas: 2
=======
replicas: 5
>>>>>>> feature-scaling
```

**After (resolved):**
```yaml
replicas: 5  # Chose the feature branch value
```

---

### 🔹 VS Code Merge Editor

**Modern GUI conflict resolver with visual interface.**

#### Benefits:

- ✅ Visual side-by-side comparison
- ✅ Accept Current / Accept Incoming buttons
- ✅ Accept Both Changes option
- ✅ Inline diff highlighting
- ✅ User-friendly interface

#### Enable VS Code as Merge Tool:

```bash
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait --merge $REMOTE $LOCAL $BASE $MERGED'
```

#### Usage:

```bash
git mergetool
```

VS Code will open with conflict resolution interface.

---

### 🔹 git mergetool

Launches your configured merge tool automatically.

```bash
git mergetool
```

#### Popular Merge Tools:

| Tool | Platform | Type |
|------|----------|------|
| **VS Code** | All | GUI |
| **vimdiff** | All | Terminal |
| **meld** | Linux/macOS | GUI |
| **kdiff3** | All | GUI |
| **p4merge** | All | GUI |
| **Beyond Compare** | All | GUI (Commercial) |

---

### 🔹 vimdiff

**Terminal-based merge resolution tool.**

#### Open vimdiff:

```bash
vimdiff file1 file2
```

Or automatically during merge:

```bash
git config --global merge.tool vimdiff
git mergetool
```

#### Benefits:

- ⚡ Fast and lightweight
- 🖥️ Works in SSH sessions
- 🛠️ Server-friendly
- 💪 Powerful for experienced users

#### Basic vimdiff Commands:

| Command | Action |
|---------|--------|
| `]c` | Jump to next conflict |
| `[c` | Jump to previous conflict |
| `:diffget LOCAL` | Get from local version |
| `:diffget REMOTE` | Get from remote version |
| `:wqa` | Save all and quit |

---

### 🔹 meld

**GUI merge resolution tool for Linux/macOS.**

#### Install:

```bash
# Ubuntu/Debian
sudo apt install meld

# macOS
brew install meld
```

#### Configure:

```bash
git config --global merge.tool meld
```

#### Benefits:

- 🎨 Visual three-way merge
- 🖱️ Click-based resolution
- 📊 Side-by-side comparison
- 🔍 Syntax highlighting

---

## 📌 Conflict Resolution Workflow

```
   Merge Attempt
        ↓
⚠️ Conflict Detected
        ↓
   git status
        ↓
  Open Conflicted File
        ↓
 Resolve Conflict Manually
        ↓
Remove Conflict Markers
        ↓
     git add <file>
        ↓
    git commit
        ↓
  ✅ Merge Complete
```

### Complete Example:

```bash
# 1. Attempt merge
git merge feature-scaling

# Output: CONFLICT (content): Merge conflict in deployment.yaml

# 2. Check status
git status

# 3. Open and resolve file
vim deployment.yaml

# 4. Stage resolved file
git add deployment.yaml

# 5. Complete merge
git commit -m "Resolved conflict: kept feature-scaling replica count"
```

---

## 📌 Aborting Conflicts

If you want to **cancel** the merge and start over:

### Abort Merge:

```bash
git merge --abort
```

Returns to the state before the merge attempt.

### Abort Rebase:

```bash
git rebase --abort
```

Returns to the state before the rebase.

---

## 📌 Enterprise Conflict Strategy

### Professional teams use these strategies to **reduce conflicts**:

#### ✅ Prevention Strategies:

- 🔄 **Rebase frequently** - Keep branches up to date
- 📥 **Pull latest changes often** - Sync with main regularly
- 📝 **Use small commits** - Easier to resolve conflicts
- 🌱 **Avoid long-lived branches** - Merge features quickly
- 👥 **Communicate with team** - Coordinate on shared files
- 🔀 **Feature flags** - Deploy incomplete features safely
- 📦 **Modular code** - Reduce file overlap

#### ✅ Resolution Best Practices:

- 🔍 **Review both changes** - Understand context
- 💬 **Discuss with author** - When unsure
- 🧪 **Test after resolution** - Ensure functionality
- 📋 **Document decisions** - In commit messages
- 🔄 **CI/CD validation** - Run tests automatically

---

## 📌 DevOps-Specific Conflicts

### 🔹 Kubernetes Conflict Best Practices

#### ❌ Avoid:

- Giant monolithic YAML files
- Manual edits directly in production
- Hardcoded values in manifests
- Shared namespace conflicts

#### ✅ Prefer:

- **Helm charts** - Templating and versioning
- **Kustomize** - Overlay-based customization
- **Modular manifests** - Separate files per resource
- **GitOps workflows** - Declarative deployments
- **Namespaced resources** - Isolation

#### Example Resolution Strategy:

```yaml
# Instead of conflicting on:
<<<<<<< HEAD
replicas: 2
=======
replicas: 5
>>>>>>> feature

# Use Helm values:
replicas: {{ .Values.replicaCount }}
```

---

### 🔹 Terraform Conflict Best Practices

#### ❌ Avoid:

- Multiple developers editing same module simultaneously
- Shared state file conflicts
- Manual state manipulation
- Monolithic terraform files

#### ✅ Prefer:

- **Modular infrastructure** - Separate modules
- **Isolated state files** - Per environment/module
- **Pull request reviews** - Before applying
- **Terraform workspaces** - Environment separation
- **State locking** - Prevent concurrent changes
- **Remote state** - S3/GCS backends

#### Example Resolution:

```bash
# Before merging Terraform changes:
terraform fmt
terraform validate
terraform plan

# Review plan output for conflicts
# Resolve in PR before merging
```

---

## 📌 Real-World Scenarios Practiced

During this stage we practiced:

- ✅ Content merge conflicts
- ✅ Rebase conflicts
- ✅ Branch divergence resolution
- ✅ Non-fast-forward push errors
- ✅ Upstream sync conflicts
- ✅ Feature branch conflicts
- ✅ Stash during conflicts
- ✅ Rebase continuation workflow
- ✅ YAML/Kubernetes conflicts
- ✅ Terraform HCL conflicts
- ✅ Binary file conflicts
- ✅ Multi-file conflict resolution

---

## 🧪 Practical Tasks

### ✅ Simulate Conflict

```bash
# Create conflict scenario
git checkout -b feature-conflict
echo "version: 2.0" > app.yaml
git add app.yaml && git commit -m "Update to v2.0"

git checkout main
echo "version: 3.0" > app.yaml
git add app.yaml && git commit -m "Update to v3.0"

# Trigger conflict
git merge feature-conflict
```

### ✅ Check Conflict Status

```bash
git status
```

**Output:**
```
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   app.yaml
```

### ✅ Open Conflict File

```bash
vim app.yaml
# or
code app.yaml
```

### ✅ Resolve Conflict Manually

```bash
# Edit file, remove markers, choose correct version
vim app.yaml

# Stage resolved file
git add app.yaml

# Commit merge
git commit -m "Resolved version conflict: chose 3.0"
```

### ✅ Launch Merge Tool

```bash
git mergetool
```

### ✅ Continue Rebase After Conflict

```bash
# After resolving conflicts during rebase
git add <resolved-files>
git rebase --continue
```

### ✅ Abort Merge

```bash
git merge --abort
```

### ✅ Abort Rebase

```bash
git rebase --abort
```

### ✅ Skip Rebase Commit

```bash
# Skip problematic commit during rebase
git rebase --skip
```

### ✅ Show Conflict in Diff Format

```bash
git diff
```

### ✅ List Conflicted Files

```bash
git diff --name-only --diff-filter=U
```

### ✅ Configure Merge Tool

```bash
# VS Code
git config --global merge.tool vscode

# vimdiff
git config --global merge.tool vimdiff

# meld
git config --global merge.tool meld
```

---

## 📌 Important Concepts Learned

| Concept | Status |
|---------|--------|
| Content Conflicts | ✅ |
| Rename Conflicts | ✅ |
| Delete Conflicts | ✅ |
| Binary Conflicts | ✅ |
| Kubernetes YAML Conflicts | ✅ |
| Terraform HCL Conflicts | ✅ |
| Manual Resolution | ✅ |
| VS Code Merge Editor | ✅ |
| git mergetool | ✅ |
| vimdiff | ✅ |
| meld | ✅ |
| Rebase Conflict Handling | ✅ |
| Conflict Prevention Strategies | ✅ |
| Enterprise Workflows | ✅ |

---

## 🎯 Outcome of This Stage

### After completing this stage, you can now:

- ✅ Identify and understand different conflict types
- ✅ Resolve merge conflicts professionally
- ✅ Handle Kubernetes YAML conflicts
- ✅ Resolve Terraform/HCL conflicts
- ✅ Work with rebase conflicts safely
- ✅ Use GUI merge tools (VS Code, meld)
- ✅ Use terminal merge tools (vimdiff)
- ✅ Perform production-safe merges
- ✅ Understand enterprise conflict workflows
- ✅ Apply conflict prevention strategies
- ✅ Make informed resolution decisions
- ✅ Communicate effectively during conflicts

---

## 🔗 Next Steps

Continue to **Stage 6** for advanced Git topics:

- 🪝 Git hooks and automation
- 🔄 CI/CD integration patterns
- 🔍 Git internals and plumbing commands
- 🎯 Advanced rebase techniques
- 📊 Repository analysis and optimization

---

## 📝 Resources

- [Git Conflict Resolution Docs](https://git-scm.com/docs/git-merge#_how_conflicts_are_presented)
- [VS Code Merge Conflict Guide](https://code.visualstudio.com/docs/sourcecontrol/overview#_merge-conflicts)
- [Kubernetes GitOps Best Practices](https://www.gitops.tech/)
- [Terraform Team Workflows](https://www.terraform.io/docs/cloud/guides/recommended-practices/index.html)

---

**🚀 STAGE 5 COMPLETED SUCCESSFULLY!**

**You're now a merge conflict resolution expert! 💪**
