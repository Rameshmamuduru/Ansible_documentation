Nice question 👍 This is **core Ansible skill** (and asked a LOT in interviews).
Let’s go **step-by-step**, from **zero → PROD-ready role**.

---

## 1️⃣ What is an Ansible Role? (simple words)

An **Ansible role** is a **structured, reusable way** to organize:

* tasks
* variables
* files
* templates
* handlers

Instead of writing everything in one big playbook, roles keep things **clean and reusable**.

👉 Think of a role like a **module for one purpose**
Example:

* `nginx`
* `docker`
* `java`
* `mysql`

---

## 2️⃣ Create a role (recommended way)

Always use:

```bash
ansible-galaxy init nginx
```

This creates:

```text
nginx/
├── defaults/
│   └── main.yml
├── files/
├── handlers/
│   └── main.yml
├── meta/
│   └── main.yml
├── tasks/
│   └── main.yml
├── templates/
├── tests/
│   ├── inventory
│   └── test.yml
├── vars/
│   └── main.yml
└── README.md
```

---

## 3️⃣ Role directory explained (VERY IMPORTANT)

### 🔹 tasks/ (heart of the role)

```yaml
# tasks/main.yml
- name: Install nginx
  apt:
    name: nginx
    state: present
    update_cache: yes

- name: Start nginx
  service:
    name: nginx
    state: started
    enabled: true
```

➡️ This is where **actual work happens**.

---

### 🔹 defaults/ (low priority variables)

```yaml
# defaults/main.yml
nginx_port: 80
```

Used for:

* configurable values
* safe defaults

---

### 🔹 vars/ (high priority variables)

```yaml
# vars/main.yml
nginx_user: www-data
```

⚠️ Avoid overusing `vars/` — hard to override.

---

### 🔹 handlers/ (restart/reload services)

```yaml
# handlers/main.yml
- name: restart nginx
  service:
    name: nginx
    state: restarted
```

Used with `notify`.

---

### 🔹 templates/ (Jinja2 config files)

```nginx
# templates/nginx.conf.j2
server {
    listen {{ nginx_port }};
}
```

---

### 🔹 files/ (static files)

Used for:

* scripts
* certs
* binaries

```yaml
- copy:
    src: myfile.txt
    dest: /tmp/myfile.txt
```

---

### 🔹 meta/ (role metadata & dependencies)

```yaml
# meta/main.yml
dependencies:
  - role: common
```

---

## 4️⃣ Example: Simple NGINX role (complete flow)

### tasks/main.yml

```yaml
- name: Install nginx
  apt:
    name: nginx
    state: present
    update_cache: yes

- name: Deploy nginx config
  template:
    src: nginx.conf.j2
    dest: /etc/nginx/nginx.conf
  notify: restart nginx
```

### handlers/main.yml

```yaml
- name: restart nginx
  service:
    name: nginx
    state: restarted
```

### defaults/main.yml

```yaml
nginx_port: 80
```

---

## 5️⃣ Use the role in a playbook

```yaml
# site.yml
- hosts: web
  become: yes
  roles:
    - nginx
```

Run:

```bash
ansible-playbook site.yml
```

---

## 6️⃣ Recommended PROD folder structure 🏗️

```text
project/
├── ansible.cfg
├── inventory/
│   └── prod
├── roles/
│   ├── nginx/
│   ├── docker/
│   └── common/
├── group_vars/
│   └── all.yml
├── host_vars/
├── site.yml
```

💡 **PROD rule**:

* Keep logic in roles
* Keep environment config in `group_vars`

---

## 7️⃣ Best practices (interview gold ⭐)

✅ Use `defaults/` instead of `vars/`
✅ Make roles **idempotent**
✅ One role = one responsibility
✅ Use handlers for restarts
✅ Avoid hardcoding values
✅ Use `tags` inside roles

Example:

```yaml
- name: Install nginx
  apt:
    name: nginx
  tags: install
```

---

## 8️⃣ Common interview questions

**Q: Difference between playbook and role?**
➡️ Playbook = orchestration
➡️ Role = reusable component

**Q: Where do you define variables in role?**
➡️ defaults, vars, group_vars, host_vars

**Q: Role vs Collection?**
➡️ Role = automation logic
➡️ Collection = roles + modules + plugins

---
