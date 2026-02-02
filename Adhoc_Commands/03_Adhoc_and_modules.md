# how to work with ansible?
in general we have a 3 ways to work with ansible
- Adhoc commands
- Modules
- Playbooks

## Adhoc commands
Ad-hoc commands = quick one-line commands you run with Ansible to perform a task immediately on one or more servers.
- No need to write a playbook
- Used for simple tasks or testing
- Ideal for real-time troubleshooting or quick updates


Adhoc- Commands:
```
ansible all -a "apt install nginx"
```

Modules:
```
ansible all -m apt -a "name=unzip state=present"
ansible all -m apt -a "name=unzip state=absent"
```
############################################################################################################################
Perfect 👍
Here is a **clean, REAL-TIME Ansible ad-hoc command table** that infra & DevOps teams actually use in production.
You can **save this as a cheat-sheet**.

---

## Ansible Ad-Hoc Commands – FULL TABLE

### 1. Connectivity & System Info

| Purpose        | Command                                           |
| -------------- | ------------------------------------------------- |
| Ping all nodes | `ansible all -m ping`                             |
| Check uptime   | `ansible all -m command -a "uptime"`              |
| OS details     | `ansible all -m command -a "cat /etc/os-release"` |
| Memory usage   | `ansible all -m command -a "free -h"`             |
| Disk usage     | `ansible all -m command -a "df -h"`               |
| CPU info       | `ansible all -m command -a "lscpu"`               |
| Hostname       | `ansible all -m command -a "hostname"`            |

---

### 2. Package Management (Ubuntu / Debian)

| Purpose                   | Command                                                             |
| ------------------------- | ------------------------------------------------------------------- |
| Install package           | `ansible all -m apt -a "name=nginx state=present update_cache=yes"` |
| Remove package            | `ansible all -m apt -a "name=nginx state=absent"`                   |
| Install multiple packages | `ansible all -m apt -a "name=git,unzip,curl state=present"`         |
| Update packages           | `ansible all -m apt -a "upgrade=dist"`                              |
| Clean cache               | `ansible all -m apt -a "autoremove=yes autoclean=yes"`              |

---

### 3. Package Management (RHEL / CentOS)

| Purpose             | Command                                            |
| ------------------- | -------------------------------------------------- |
| Install package     | `ansible all -m yum -a "name=httpd state=present"` |
| Remove package      | `ansible all -m yum -a "name=httpd state=absent"`  |
| Update all packages | `ansible all -m yum -a "name=* state=latest"`      |

---

### 4. Service Management

| Purpose         | Command                                                  |
| --------------- | -------------------------------------------------------- |
| Start service   | `ansible all -m service -a "name=nginx state=started"`   |
| Stop service    | `ansible all -m service -a "name=nginx state=stopped"`   |
| Restart service | `ansible all -m service -a "name=nginx state=restarted"` |
| Enable at boot  | `ansible all -m service -a "name=nginx enabled=yes"`     |
| Check status    | `ansible all -m command -a "systemctl status nginx"`     |

---

### 5. File & Directory Operations

| Purpose            | Command                                                              |
| ------------------ | -------------------------------------------------------------------- |
| Create directory   | `ansible all -m file -a "path=/opt/app state=directory mode=0755"`   |
| Create file        | `ansible all -m file -a "path=/tmp/test.txt state=touch"`            |
| Delete file        | `ansible all -m file -a "path=/tmp/test.txt state=absent"`           |
| Change permissions | `ansible all -m file -a "path=/opt/app mode=0777"`                   |
| Change owner       | `ansible all -m file -a "path=/opt/app owner=ansible group=ansible"` |

---

### 6. Copy & Fetch Files

| Purpose               | Command                                                         |
| --------------------- | --------------------------------------------------------------- |
| Copy file to nodes    | `ansible all -m copy -a "src=/tmp/app.conf dest=/etc/app.conf"` |
| Copy inline content   | `ansible all -m copy -a "content='hello' dest=/tmp/hello.txt"`  |
| Fetch file from nodes | `ansible all -m fetch -a "src=/etc/hosts dest=/tmp/ flat=yes"`  |

---

### 7. User & Group Management

| Purpose               | Command                                                                |
| --------------------- | ---------------------------------------------------------------------- |
| Create user           | `ansible all -m user -a "name=devops state=present"`                   |
| Create user with home | `ansible all -m user -a "name=devops shell=/bin/bash create_home=yes"` |
| Delete user           | `ansible all -m user -a "name=devops state=absent remove=yes"`         |
| Create group          | `ansible all -m group -a "name=developers"`                            |
| Add user to group     | `ansible all -m user -a "name=devops groups=developers append=yes"`    |

---

### 8. SSH & Security

| Purpose               | Command                                                                                                                      |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Add SSH public key    | `ansible all -m authorized_key -a "user=ansible key='{{ lookup(\"file\", \"~/.ssh/ansible_key.pub\") }}'"`                   |
| Disable password auth | `ansible all -m lineinfile -a "path=/etc/ssh/sshd_config regexp='^PasswordAuthentication' line='PasswordAuthentication no'"` |
| Restart SSH           | `ansible all -m service -a "name=sshd state=restarted"`                                                                      |

---

### 9. Reboot & Shutdown

| Purpose          | Command                                       |
| ---------------- | --------------------------------------------- |
| Reboot servers   | `ansible all -m reboot`                       |
| Shutdown servers | `ansible all -m command -a "shutdown -h now"` |

---

### 10. Cron Jobs

| Purpose         | Command                                                                           |
| --------------- | --------------------------------------------------------------------------------- |
| Add cron job    | `ansible all -m cron -a "name='cleanup' minute='0' hour='2' job='rm -rf /tmp/*'"` |
| Remove cron job | `ansible all -m cron -a "name='cleanup' state=absent"`                            |

---

### 11. Facts & Debugging

| Purpose          | Command                                                 |
| ---------------- | ------------------------------------------------------- |
| Gather all facts | `ansible all -m setup`                                  |
| Hostname fact    | `ansible all -m setup -a "filter=ansible_hostname"`     |
| IP address       | `ansible all -m setup -a "filter=ansible_default_ipv4"` |

---

## REAL-TIME GOLDEN RULE

> **Ad-hoc commands are for quick ops & troubleshooting.
> Playbooks are for repeatable, audited production changes.**

---


