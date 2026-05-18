# 🟡 STAGE 3 — Branching & Merging

> Beginner → Advanced → Production-Level Git Branching & Collaboration Workflow 🚀

---

## 📖 Goal of This Stage

This stage focuses on understanding how professional teams work collaboratively using Git branches, merges, rebasing, pull requests, release workflows, and conflict resolution.

### By the end of this stage, you will understand:

- ✅ Real-world branching strategies
- ✅ Feature development workflows
- ✅ Merge conflict handling
- ✅ Rebase workflows
- ✅ Pull Request lifecycle
- ✅ Fork & upstream workflows
- ✅ Safe collaboration practices
- ✅ Production-level Git operations

---

## 📚 Table of Contents

- [Branching Basics](#-branching-basics)
- [Branch Commands](#-branch-commands)
- [Branching Strategies](#-branching-strategies)
- [Merge Types](#-merge-types)
- [Merge Conflicts](#-merge-conflicts)
- [Rebasing](#-rebasing)
- [Stashing](#-stashing)
- [Cherry Pick](#-cherry-pick)
- [Tags & Releases](#-tags--releases)
- [Practical Tasks](#-practical-tasks)
- [Real-World Workflow](#-real-world-workflow-practiced)
- [Outcome](#-outcome-of-this-stage)

---

## 📌 Branching Basics

### 🔹 What is Branching

A branch is an independent line of development in Git.

**Branches allow developers to:**
- Work safely without affecting production code
- Develop features independently
- Test changes before merging
- Collaborate with teams efficiently

---

### 🔹 Why Branching Matters

Branching helps in:

- **Isolated development** - Work on features without breaking main code
- **Safe experimentation** - Test ideas without risk
- **Parallel team collaboration** - Multiple developers working simultaneously
- **Clean production workflows** - Organized release management
- **Controlled releases** - Deploy when ready

---

### 🔹 HEAD Pointer

`HEAD` is a pointer to the currently active branch/commit.

**Example:**

```bash
git branch
```

**Output:**

```
* main
  feature-login
```

> `*` indicates current HEAD location.

---

### 🔹 Branch Naming Conventions

Professional naming standards:

| Branch Type | Example |
|------------|---------|
| Feature | `feature/login-api` |
| Bugfix | `bugfix/navbar-fix` |
| Hotfix | `hotfix/payment-failure` |
| Release | `release/v1.0.0` |

---

## 📌 Branch Commands

### 🔹 Create Branch

```bash
git branch feature-login
```

### 🔹 Switch Branch

**Modern Method:**
```bash
git switch feature-login
```

**Older Method:**
```bash
git checkout feature-login
```

### 🔹 Create + Switch Together

```bash
git switch -c feature-login
```

### 🔹 Merge Branch

```bash
git switch main
git merge feature-login
```

### 🔹 Delete Branch (Safe)

Deletes only merged branches.

```bash
git branch -d feature-login
```

### 🔹 Force Delete Branch

Deletes branch forcefully.

```bash
git branch -D feature-login
```

---

## 📌 Branching Strategies

### 🔹 Feature Branching

Each feature is developed in a separate branch.

**Example:**

```
main
 └── feature/login
 └── feature/payment
```

**Benefits:**
- Safe development
- Easier reviews
- Better collaboration

---

### 🔹 Git Flow

Production-oriented workflow.

**Branches used:**
- `main`
- `develop`
- `feature/*`
- `release/*`
- `hotfix/*`

**Best for:**
- Large enterprise applications
- Structured release cycles

---

### 🔹 GitHub Flow

Simple workflow:

```
main
  └── feature branch
        └── Pull Request
```

**Best for:**
- CI/CD pipelines
- SaaS applications
- Agile teams

---

### 🔹 GitLab Flow

Environment-based branching strategy.

**Example:**

```
feature → dev → staging → production
```

---

### 🔹 Trunk-Based Development

All developers integrate frequently into a shared branch.

**Focus:**
- Small commits
- Continuous integration
- Fast deployments

---

### 🔹 Release Branches

Used for:
- Version stabilization
- QA testing
- Release preparation

**Example:**
```bash
release/v1.0.0
```

---

### 🔹 Hotfix Branches

Used for urgent production fixes.

**Example:**
```bash
hotfix/payment-bug
```

---

## 📌 Merge Types

### 🔹 Fast Forward Merge

Linear history.

**Before:**
```
A---B---C
         \
          D
```

**After merge:**
```
A---B---C---D
```

> No merge commit created.

---

### 🔹 Three-Way Merge

Creates merge commit.

**Before:**
```
      D---E
     /
A---B---C
```

**After merge:**
```
      D---E
     /     \
A---B---C---M
```

---

### 🔹 Squash Merge

Combines all commits into one.

**Useful for:**
- Clean history
- Feature cleanup

---

### 🔹 Rebase Merge

Reapplies commits linearly.

> Cleaner history without merge commits.

---

## 📌 Merge Conflicts

### 🔹 Conflict Detection

Occurs when:
- Same file
- Same lines
- Different changes

---

### 🔹 Conflict Markers

**Example:**

```
<<<<<<< HEAD
Main branch code
=======
Feature branch code
>>>>>>> feature-login
```

---

### 🔹 Manual Conflict Fixing

**Steps:**

```bash
git status
vim conflicted-file.txt
git add .
git commit
```

---

## 📌 Rebasing

### 🔹 git rebase

Moves commits onto another base branch.

```bash
git rebase main
```

---

### 🔹 Interactive Rebase

Used for:
- Squashing commits
- Reordering commits
- Cleaning history

```bash
git rebase -i HEAD~3
```

---

### 🔹 Rebase vs Merge

| Rebase | Merge |
|--------|-------|
| Cleaner history | Preserves exact history |
| Linear commits | Merge commits created |
| Better for local cleanup | Better for collaboration |

---

## 📌 Stashing

### 🔹 Save Temporary Work

```bash
git stash
```

### 🔹 Apply + Remove Stash

```bash
git stash pop
```

### 🔹 Apply Without Removing

```bash
git stash apply
```

### 🔹 View Stashes

```bash
git stash list
```

---

## 📌 Cherry Pick

### 🔹 Copy Specific Commit

```bash
git cherry-pick <commit-id>
```

**Useful for:**
- Hotfix workflows
- Moving commits selectively

---

## 📌 Tags & Releases

### 🔹 Create Tag

```bash
git tag v1.0
```

### 🔹 Semantic Versioning

**Format:**
```
vMAJOR.MINOR.PATCH
```

**Example:**
```
v1.0.0
```

### 🔹 Release Tags

Used for:
- Production releases
- Deployment versions
- CI/CD tagging

---

## 🧪 Practical Tasks

### ✅ Create Branch

```bash
git branch feature-login
git switch feature-login
```

### ✅ Merge Branch

```bash
git switch main
git merge feature-login
```

### ✅ Delete Branch

```bash
git branch -d feature-login
```

### ✅ Force Delete Branch

```bash
git branch -D feature-login
```

### ✅ Create Merge Conflict

Modify same line in two branches.

```bash
git merge feature-branch
```

### ✅ Resolve Conflict

```bash
git status
vim conflicted-file.txt
git add .
git commit
```

### ✅ Rebase Branch

```bash
git rebase main
```

### ✅ Interactive Rebase

```bash
git rebase -i HEAD~3
```

### ✅ Stash Changes

```bash
git stash
git stash pop
```

### ✅ Apply Stash Without Deleting

```bash
git stash apply
```

### ✅ View Stashes

```bash
git stash list
```

### ✅ Cherry Pick Commit

```bash
git cherry-pick <commit-id>
```

### ✅ Create Tag

```bash
git tag v1.0
```

---

## 🚀 Real-World Workflow Practiced

This stage also covered:

- ✅ Fork workflows
- ✅ Upstream & origin remotes
- ✅ Feature branch development
- ✅ Pull Request lifecycle
- ✅ Safe merge workflows
- ✅ Production-safe Git operations
- ✅ Rebase conflict handling
- ✅ Non-fast-forward push issues
- ✅ Branch cleanup workflows

---

## 📌 Important Concepts Learned

| Concept | Status |
|---------|--------|
| Feature Branch Workflow | ✅ |
| Fork-Based Workflow | ✅ |
| Pull Requests | ✅ |
| Upstream vs Origin | ✅ |
| Merge Conflicts | ✅ |
| Rebasing | ✅ |
| Stashing | ✅ |
| Cherry Picking | ✅ |
| Tags & Releases | ✅ |
| Production Git Workflow | ✅ |

---

## 🎯 Outcome of This Stage

### After completing this stage, you can now:

- ✅ Work with professional Git workflows
- ✅ Handle team collaboration safely
- ✅ Create & manage Pull Requests
- ✅ Resolve merge conflicts confidently
- ✅ Use rebase workflows properly
- ✅ Work with fork-based repositories
- ✅ Manage releases & tags
- ✅ Follow enterprise Git standards

---

## 🔗 Next Steps

Ready to level up? Continue to **Stage 4** for advanced Git topics including:
- Git hooks
- CI/CD integration
- Advanced collaboration
- Git internals

---

## 📝 License

This educational material is open for learning purposes.

---

**Happy Git-ing! 🚀**
