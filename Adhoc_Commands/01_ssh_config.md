# SSH Configaration:
it was mandatory create a SSH configaration with all of the servers so that mastaer node can able to take ssh into the managed nodes and then excuete the commadns. usually we can make ssh wasys in two ways
## 1.Passwordless authentication:
Perfect 👍 — let’s do this **REAL-TIME PROD-GRADE**, the way it’s actually done in companies.
No shortcuts, no “lab-only” stuff.

I’ll give you a **production standard design + exact commands + hardening**.

---

# 🔐 PROD-GRADE Password-less Ansible Setup (Private IP)

## 🎯 Goals (Production)

✔ No passwords
✔ Private IP only
✔ Dedicated Ansible user
✔ Least privilege
✔ Auditable & secure
✔ Works for Ubuntu + CentOS
✔ Ready for scale

---

## 1️⃣ Create a Dedicated **ansible** User (ALL Linux Nodes)

> ❌ Never use `root`
> ❌ Never use personal users (`ubuntu`, `ec2-user`)

### On **Ubuntu & CentOS nodes**

```bash
sudo useradd -m -s /bin/bash ansible
sudo passwd -l ansible
```

---

## 2️⃣ Password-less SUDO (Controlled)

### Edit sudoers

```bash
sudo visudo -f /etc/sudoers.d/ansible
```

Add:

```text
ansible ALL=(ALL) NOPASSWD: /usr/bin/apt, /usr/bin/yum, /usr/bin/systemctl, /bin/mkdir, /bin/cp, /bin/chown
```

📌 **Least privilege** (not ALL commands)

---

## 3️⃣ Generate SSH Key (Control Node ONLY)

```bash
su - ansible
ssh-keygen -t ed25519 -f ~/.ssh/ansible_key
```

Files:

```
~/.ssh/ansible_key
~/.ssh/ansible_key.pub
```

---

## 4️⃣ Distribute Public Key (One-time only)

### From control node

```bash
ssh-copy-id -i ~/.ssh/ansible_key.pub ansible@10.0.0.10
ssh-copy-id -i ~/.ssh/ansible_key.pub ansible@10.0.0.11
```

---

## 5️⃣ Harden SSH (PROD MANDATORY)

### On ALL Linux nodes

```bash
sudo nano /etc/ssh/sshd_config
```

Set:

```text
PasswordAuthentication no
PermitRootLogin no
PubkeyAuthentication yes
AllowUsers ansible
```

Restart SSH:

```bash
sudo systemctl restart sshd
```

⚠️ **DO THIS ONLY AFTER SSH KEY TEST PASSES**

---

## 6️⃣ Ansible Inventory (PROD Style)

```ini
[prod_linux]
web01 ansible_host=10.0.0.10
app01 ansible_host=10.0.0.11

[prod_linux:vars]
ansible_user=ansible
ansible_ssh_private_key_file=~/.ssh/ansible_key
ansible_become=true
ansible_become_method=sudo
```

---

## 7️⃣ Validate Connectivity (PROD TESTS)

```bash
ansible prod_linux -m ping
ansible prod_linux -m command -a "whoami" -b
```

Expected:

```
pong
root
```

---

## 8️⃣ Firewall / Security Group Rules

✔ Allow SSH **only** from Ansible subnet
✔ Deny public SSH
✔ Use private routing (VPC / VNET)

---

## 9️⃣ Ansible Config (Optional but Recommended)

`/etc/ansible/ansible.cfg`

```ini
[defaults]
inventory = /etc/ansible/hosts
host_key_checking = True
forks = 20
timeout = 30
```

---

## 🔐 Windows (PROD-Level Summary)

* Use **WinRM over HTTPS (5986)**
* Use **domain service account**
* Disable basic auth
* Use certificates

👉 Say the word and I’ll give **full Windows PROD setup** too.

---

## 🧠 REAL-WORLD BEST PRACTICES

| Practice               | Reason                |
| ---------------------- | --------------------- |
| Dedicated ansible user | Audit + revoke access |
| SSH keys only          | No brute force        |
| Private IP             | Zero exposure         |
| Limited sudo           | Least privilege       |
| Disable passwords      | Hard security         |

---

## 🎯 Interview-Ready Answer

> **In production, Ansible uses a dedicated service account with SSH key-based authentication over private IPs, password login disabled, limited sudo privileges, and hardened SSH configuration.**

---

## ✅ Final Checklist

* [x] Dedicated ansible user
* [x] SSH key-based auth
* [x] Password login disabled
* [x] Limited sudo
* [x] Private IP only
* [x] Inventory hardened

---

If you want next:

* 🔥 **PROD Windows WinRM setup**
* 🔥 **Ansible Vault for secrets**
* 🔥 **Jump host / Bastion design**
* 🔥 **Multi-environment (dev/qa/prod)**

Just tell me 🚀
