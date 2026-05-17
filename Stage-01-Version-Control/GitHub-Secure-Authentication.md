# GitHub SSH Configuration Task — Secure Git Authentication 🔐

---

# 📚 Table of Contents

1. Objective
2. Generate SSH Key
3. Start SSH Agent
4. Add SSH Key to Agent
5. Copy Public Key
6. Add SSH Key to GitHub
7. Verify Authentication
8. Configure Git Identity
9. Use SSH Instead of HTTPS
10. Security Best Practices
11. Prevent Credential Leakage
12. Folder Permissions
13. Personal Access Tokens
14. Final Verification
15. Important Interview Questions
16. Summary

---

# 🎯 Objective

Configure secure Git authentication using SSH keys while keeping credentials and private keys protected from public exposure.

This setup is heavily used in:

✅ DevOps  
✅ CI/CD pipelines  
✅ GitHub Actions  
✅ Kubernetes automation  
✅ Jenkins pipelines  
✅ Infrastructure repositories  

---

# 1️⃣ Generate SSH Key

---

# 📌 Command

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

---

# 📌 What This Does

Creates:

| File | Purpose |
|---|---|
| id_ed25519 | Private key |
| id_ed25519.pub | Public key |

---

# 📌 Save Location

Press Enter to save at default path:

```bash
/home/username/.ssh/id_ed25519
```

---

# 📌 Passphrase

Add passphrase for additional security.

Benefits:

✅ Extra encryption  
✅ Protects private key if system compromised  

---

# 📌 Important

Never share:

```bash
~/.ssh/id_ed25519
```

This is PRIVATE key 🚨

---

# 2️⃣ Start SSH Agent

SSH Agent manages SSH keys securely in memory.

---

# 📌 Command

```bash
eval "$(ssh-agent -s)"
```

---

# 📌 Expected Output

```text
Agent pid 12345
```

---

# 📌 Why Important?

Avoids repeatedly entering passphrase during Git operations.

---

# 3️⃣ Add SSH Key to Agent

---

# 📌 Command

```bash
ssh-add ~/.ssh/id_ed25519
```

---

# 📌 Purpose

Loads private key into SSH agent for authentication.

---

# 📌 Verify Loaded Keys

```bash
ssh-add -l
```

---

# 4️⃣ Copy Public Key

---

# 📌 Command

```bash
cat ~/.ssh/id_ed25519.pub
```

---

# 📌 Example Public Key

```text
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIExampleKey user@example.com
```

---

# 📌 Safe to Share?

✅ YES — Public key is safe.

---

# 📌 Never Share

❌ id_ed25519  
❌ id_rsa  

These are private keys.

---

# 5️⃣ Add SSH Key to GitHub

Open:

:contentReference[oaicite:0]{index=0}

---

# 📌 Steps

1. Click **New SSH key**
2. Add title
3. Paste public key
4. Click **Add SSH key**

---

# 📌 Result

GitHub now trusts your machine securely.

---

# 6️⃣ Verify Authentication

---

# 📌 Command

```bash
ssh -T git@github.com
```

---

# 📌 Expected Output

```text
Hi username! You've successfully authenticated...
```

---

# 📌 What This Means

✅ SSH authentication works  
✅ GitHub trusts your key  
✅ Secure communication established  

---

# 7️⃣ Configure Git Identity

---

# 📌 Configure Username

```bash
git config --global user.name "Your Name"
```

---

# 📌 Configure Email

```bash
git config --global user.email "your_email@example.com"
```

---

# 📌 Verify Configuration

```bash
git config --list
```

---

# 📌 Why Important?

Every commit stores:

- Author name
- Email
- Timestamp

Used for:

✅ Collaboration  
✅ Audit tracking  
✅ Commit ownership  

---

# 8️⃣ Use SSH Instead of HTTPS

---

# 📌 Check Current Remote

```bash
git remote -v
```

---

# 📌 Change HTTPS to SSH

```bash
git remote set-url origin git@github.com:USERNAME/REPOSITORY.git
```

---

# 📌 Example

```bash
git remote set-url origin git@github.com:aayushrai23/devops-project.git
```

---

# 📌 Benefits of SSH

| SSH | HTTPS |
|---|---|
| More secure | Token/password based |
| No repeated login | Frequent authentication |
| Better automation | Less automation friendly |
| Preferred in DevOps | Mostly manual |

---

# 9️⃣ Security Best Practices

---

# 🚨 NEVER Share These Files

Do NOT expose:

```bash
~/.ssh/id_ed25519
~/.ssh/id_rsa
```

These are PRIVATE keys.

---

# ✅ Safe File to Share

Only share:

```bash
~/.ssh/id_ed25519.pub
```

---

# 🔐 Hide Credentials & Tokens

---

# ❌ Bad Practice

```bash
TOKEN=ghp_123456789abcdef
```

---

# ✅ Good Practice

```bash
export GITHUB_TOKEN="your_token"
```

---

# 📌 Temporary Environment Variable

```bash
export GITHUB_TOKEN="your_token"
```

---

# 📌 Permanent Configuration

Add to:

```bash
~/.bashrc
```

OR

```bash
~/.zshrc
```

---

# 📌 Example

```bash
export GITHUB_TOKEN="your_token"
```

Reload shell:

```bash
source ~/.bashrc
```

---

# 🔟 Prevent Credential Leakage

---

# 📌 Add Sensitive Files to .gitignore

```bash
.env
*.pem
*.key
id_ed25519
```

---

# 📌 Check Before Push

See staged files:

```bash
git status
```

See commit contents:

```bash
git diff --cached
```

---

# 📌 Why Important?

Prevents:

❌ Secret leakage  
❌ AWS credential exposure  
❌ GitHub token leaks  
❌ SSH private key exposure  

---

# 1️⃣1️⃣ Recommended Folder Permissions

---

# 📌 Secure .ssh Directory

```bash
chmod 700 ~/.ssh
```

---

# 📌 Secure Private Key

```bash
chmod 600 ~/.ssh/id_ed25519
```

---

# 📌 Public Key Permissions

```bash
chmod 644 ~/.ssh/id_ed25519.pub
```

---

# 📌 Why Important?

SSH rejects insecure key permissions.

---

# 1️⃣2️⃣ Optional — GitHub Personal Access Token (PAT)

If HTTPS authentication is required:

Open:

:contentReference[oaicite:1]{index=1}

---

# 📌 Best Practices

✅ Use fine-grained tokens  
✅ Set expiration dates  
✅ Minimum required permissions  

---

# 🚨 Never Commit Tokens

Never push:

```bash
ghp_xxxxxxxxxxxxx
```

inside Git repositories.

---

# 1️⃣3️⃣ Final Verification

---

# 📌 Test SSH Authentication

```bash
ssh -T git@github.com
```

---

# 📌 Test Git Push

```bash
git push origin main
```

---

# 📌 Successful Result

If both commands work:

✅ GitHub SSH setup complete  
✅ Secure authentication working  
✅ Ready for DevOps workflows  

---

# 🎯 Important Interview Questions

---

# 🟢 Beginner Level

---

# 1. What is SSH in GitHub?

SSH provides secure authentication between local machine and GitHub without using passwords repeatedly.

---

# 2. Difference between SSH and HTTPS in Git?

| SSH | HTTPS |
|---|---|
| Key-based authentication | Token/password authentication |
| More secure | Less convenient |
| Better automation | More manual |

---

# 3. What is Public Key and Private Key?

| Key | Purpose |
|---|---|
| Public Key | Shared with GitHub |
| Private Key | Kept secret locally |

---

# 4. Why should private keys never be shared?

Private keys provide access to repositories and servers.

If leaked:

❌ Unauthorized access possible  
❌ Repository compromise  
❌ Infrastructure breach  

---

# 🟡 Intermediate Level

---

# 5. What is SSH Agent?

SSH Agent securely stores SSH keys in memory to avoid repeatedly entering passphrases.

---

# 6. Why use .gitignore for secrets?

Prevents accidental exposure of:

- API keys
- Tokens
- SSH keys
- Environment files

---

# 7. What are recommended SSH permissions?

| Path | Permission |
|---|---|
| ~/.ssh | 700 |
| Private Key | 600 |
| Public Key | 644 |

---

# 8. How does SSH improve CI/CD workflows?

SSH enables:

✅ Secure automation  
✅ Non-interactive Git operations  
✅ Safer deployments  
✅ Pipeline authentication  

---

# 🚀 Senior DevOps Perspective

In production environments:

SSH authentication is heavily used for:

✅ CI/CD pipelines  
✅ Kubernetes GitOps  
✅ Terraform automation  
✅ Jenkins deployments  
✅ GitHub Actions  
✅ Infrastructure repositories  

SSH-based authentication provides:

✅ Better security  
✅ Easier automation  
✅ Reduced credential exposure  
✅ Enterprise-grade access management  

---

