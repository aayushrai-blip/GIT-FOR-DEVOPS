# GitHub Multi-Account SSH Setup Guide 🚀

---

# 📚 Table of Contents

1. Objective
2. Why Multiple GitHub Accounts?
3. Final Architecture
4. Generate SSH Keys
5. Start SSH Agent
6. Add SSH Keys
7. Configure SSH Config File
8. Add Public Keys to GitHub
9. Verify Authentication
10. Clone Repositories
11. Configure Git Identity
12. Check Which Account is Being Used
13. Change Account if Wrong Account is Used
14. Security Best Practices
15. Important Interview Questions
16. Summary

---

# 🎯 Objective

Configure multiple GitHub accounts on the same machine using SSH authentication.

This setup allows:

✅ Personal repositories using personal account  
✅ Company repositories using company account  
✅ Separate SSH identities  
✅ Correct commit author visibility  
✅ Secure authentication without passwords  

---

# 🧠 Real-World Scenario

Suppose you have:

| Account Type | GitHub Username |
|---|---|
| Personal | `aayushrai23` |
| Company | `aayushrai-blip` |

You want:

✅ Push personal code using personal account  
✅ Push company code using company account  
✅ Avoid authentication conflicts  
✅ Keep workflow secure and professional  

---

# 🏗️ Final Architecture

```text
~/.ssh/
│
├── id_ed25519_personal
├── id_ed25519_personal.pub
│
├── id_ed25519_company
├── id_ed25519_company.pub
│
└── config
```

---

# 1️⃣ Generate SSH Key for Personal Account

---

# 📌 Command

```bash
ssh-keygen -t ed25519 -C "personal-email@gmail.com"
```

---

# 📌 Save As

```bash
~/.ssh/id_ed25519_personal
```

---

# 📌 Files Created

```text
id_ed25519_personal
id_ed25519_personal.pub
```

---

# 🚨 Important

Never share:

```bash
id_ed25519_personal
```

This is PRIVATE key.

---

# 2️⃣ Generate SSH Key for Company Account

---

# 📌 Command

```bash
ssh-keygen -t ed25519 -C "company-email@gmail.com"
```

---

# 📌 Save As

```bash
~/.ssh/id_ed25519_company
```

---

# 📌 Files Created

```text
id_ed25519_company
id_ed25519_company.pub
```

---

# 3️⃣ Start SSH Agent

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

# 4️⃣ Add SSH Keys to SSH Agent

---

# 📌 Add Personal Key

```bash
ssh-add ~/.ssh/id_ed25519_personal
```

---

# 📌 Add Company Key

```bash
ssh-add ~/.ssh/id_ed25519_company
```

---

# 📌 Verify Loaded Keys

```bash
ssh-add -l
```

---

# 5️⃣ Configure SSH Config File

---

# 📌 Open Config File

```bash
vim ~/.ssh/config
```

---

# 📌 Add Configuration

```bash
# Personal GitHub Account
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_personal

# Company GitHub Account
Host github-company
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_company
```

---

# 📌 Save File

```text
ESC → :wq
```

---

# 📌 Learning

SSH aliases decide which SSH key gets used.

---

# 6️⃣ Add Public Keys to GitHub

---

# 📌 Personal Account

Copy key:

```bash
cat ~/.ssh/id_ed25519_personal.pub
```

Add into:

:contentReference[oaicite:0]{index=0}

while logged into personal account.

---

# 📌 Company Account

Copy key:

```bash
cat ~/.ssh/id_ed25519_company.pub
```

Add into company GitHub account.

---

# 7️⃣ Verify Authentication

---

# 📌 Test Personal Account

```bash
ssh -T git@github-personal
```

---

# 📌 Expected Output

```text
Hi aayushrai23! You've successfully authenticated...
```

---

# 📌 Test Company Account

```bash
ssh -T git@github-company
```

---

# 📌 Expected Output

```text
Hi aayushrai-blip! You've successfully authenticated...
```

---

# 8️⃣ Clone Repositories Using Correct Account

---

# 📌 Personal Repository

```bash
git clone git@github-personal:aayushrai23/project.git
```

---

# 📌 Company Repository

```bash
git clone git@github-company:aayushrai-blip/project.git
```

---

# 📌 Important Understanding

| Clone URL Used | Account Used |
|---|---|
| github-personal | Personal account |
| github-company | Company account |

---

# 9️⃣ Configure Git Identity Per Repository

This controls:

✅ Commit author name  
✅ Commit email shown on GitHub  

---

# 📌 Personal Repository

Inside repository:

```bash
git config user.name "Aayush Rai"
git config user.email "personal@gmail.com"
```

---

# 📌 Company Repository

```bash
git config user.name "Aayush Rai VA2PT"
git config user.email "company@gmail.com"
```

---

# 🚨 IMPORTANT

Do NOT use:

```bash
--global
```

Otherwise all repositories use same identity.

---

# 🔟 How to Check Which Account is Currently Being Used

---

# 📌 Check Remote URL

Run:

```bash
git remote -v
```

---

# 📌 Example Output

```text
origin git@github-company:aayushrai-blip/project.git
```

---

# 📌 Meaning

This repository is currently using:

✅ Company GitHub account

---

# 📌 If Output Contains

```text
github-personal
```

Then:

✅ Personal account is being used.

---

# 📌 Authentication Check

Run:

```bash
ssh -T git@github-company
```

OR

```bash
ssh -T git@github-personal
```

---

# 1️⃣1️⃣ How to Change Account if Wrong Account is Being Used

---

# 📌 Current Wrong Remote

Example:

```text
git@github-company:aayushrai-blip/project.git
```

---

# 📌 Change to Personal Account

```bash
git remote set-url origin git@github-personal:aayushrai23/project.git
```

---

# 📌 Change to Company Account

```bash
git remote set-url origin git@github-company:aayushrai-blip/project.git
```

---

# 📌 Verify After Change

```bash
git remote -v
```

---

# 📌 Result

Git will now use new SSH key/account automatically.

---

# 1️⃣2️⃣ Security Best Practices

---

# 🚨 NEVER SHARE

```bash
~/.ssh/id_ed25519_personal
~/.ssh/id_ed25519_company
```

These are PRIVATE keys.

---

# ✅ SAFE TO SHARE

```bash
*.pub
```

Public keys only.

---

# 📌 Secure Permissions

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519_personal
chmod 600 ~/.ssh/id_ed25519_company
chmod 644 ~/.ssh/*.pub
```

---

# 📌 Add Sensitive Files to .gitignore

```bash
.env
*.pem
*.key
id_ed25519*
```

---

# 🎯 Important Interview Questions

---

# 1. Why use multiple SSH keys?

To securely manage multiple GitHub accounts on same machine.

---

# 2. What is SSH config file?

SSH config file maps SSH aliases to specific SSH keys.

---

# 3. How does Git decide which GitHub account to use?

Using:

- Remote repository URL
- SSH alias
- SSH key mapping

---

# 4. Difference between global and local git config?

| Global | Local |
|---|---|
| Applies everywhere | Applies only to repository |

---

# 5. Why is SSH preferred over HTTPS?

| SSH | HTTPS |
|---|---|
| More secure | Token/password based |
| Better automation | Credential conflicts |
| Better CI/CD support | Less efficient |

---

# 🚀 Senior DevOps Perspective

This setup is heavily used in:

✅ Enterprise DevOps  
✅ Client infrastructure management  
✅ Open-source contributions  
✅ Multi-tenant workstations  
✅ Kubernetes GitOps workflows  
✅ CI/CD automation  

Professional engineers prefer:

✅ SSH authentication  
✅ Multiple SSH identities  
✅ Per-repository Git configuration  
✅ SSH alias-based workflows  

---

# 🎯 Summary

After completing this setup, you should understand:

✅ Multi-account GitHub authentication  
✅ SSH key generation  
✅ SSH agent usage  
✅ SSH config management  
✅ Per-repository Git identities  
✅ Switching between GitHub accounts  
✅ Checking active GitHub account  
✅ Correcting wrong account usage  
✅ Secure Git workflows  

---

# 🚀 Recommended Workflow

| Repository Type | Recommended Alias |
|---|---|
| Personal Projects | github-personal |
| Company Projects | github-company |

This creates clean, scalable, enterprise-grade Git workflows 🔥
