Got it 👍 — you want **ONE CLEAN TABLE** that shows
**Ansible `state` values + which modules use them**.
Below is a **real-world, interview + production ready** reference.

---

## ✅ Ansible States vs Modules (Master Table)

> ⚠️ Note: Not every module supports every state.
> This table covers **99% of commonly used PROD modules**.

---

### 🔹 Package Management

| State     | Meaning        | Modules                               |
| --------- | -------------- | ------------------------------------- |
| `present` | Installed      | `package`, `apt`, `yum`, `dnf`, `pip` |
| `absent`  | Removed        | `package`, `apt`, `yum`, `dnf`, `pip` |
| `latest`  | Latest version | `package`, `apt`, `yum`, `dnf`        |

---

### 🔹 Services (Linux)

| State       | Meaning             | Modules              |
| ----------- | ------------------- | -------------------- |
| `started`   | Service running     | `service`, `systemd` |
| `stopped`   | Service stopped     | `service`, `systemd` |
| `restarted` | Restart service     | `service`, `systemd` |
| `reloaded`  | Reload config       | `service`, `systemd` |
| `enabled`   | Start on boot       | `service`, `systemd` |
| `disabled`  | Don’t start on boot | `service`, `systemd` |

---

### 🔹 Files & Directories

| State       | Meaning      | Modules |
| ----------- | ------------ | ------- |
| `file`      | Regular file | `file`  |
| `directory` | Directory    | `file`  |
| `link`      | Symlink      | `file`  |
| `hard`      | Hard link    | `file`  |
| `touch`     | Empty file   | `file`  |
| `absent`    | Remove       | `file`  |

---

### 🔹 Users & Groups

| State     | Meaning | Modules         |
| --------- | ------- | --------------- |
| `present` | Exists  | `user`, `group` |
| `absent`  | Removed | `user`, `group` |

---

### 🔹 Mounts & Filesystems

| State       | Meaning            | Modules |
| ----------- | ------------------ | ------- |
| `mounted`   | Mounted + fstab    | `mount` |
| `unmounted` | Unmounted          | `mount` |
| `present`   | Entry in fstab     | `mount` |
| `absent`    | Remove fstab entry | `mount` |

---

### 🔹 Archives

| State       | Meaning         | Modules     |
| ----------- | --------------- | ----------- |
| `present`   | Archive exists  | `archive`   |
| `absent`    | Archive removed | `archive`   |
| `extracted` | Extracted       | `unarchive` |

---

### 🔹 Docker / Containers

| State       | Meaning           | Modules            |
| ----------- | ----------------- | ------------------ |
| `started`   | Container running | `docker_container` |
| `stopped`   | Container stopped | `docker_container` |
| `restarted` | Restart container | `docker_container` |
| `absent`    | Container removed | `docker_container` |

---

### 🔹 Kubernetes (Ansible k8s modules)

| State     | Meaning          | Modules |
| --------- | ---------------- | ------- |
| `present` | Resource exists  | `k8s`   |
| `absent`  | Resource deleted | `k8s`   |

---

### 🔹 Windows Modules

| State       | Meaning   | Modules                      |
| ----------- | --------- | ---------------------------- |
| `present`   | Installed | `win_feature`, `win_package` |
| `absent`    | Removed   | `win_feature`, `win_package` |
| `started`   | Running   | `win_service`                |
| `stopped`   | Stopped   | `win_service`                |
| `restarted` | Restarted | `win_service`                |

---

### 🔹 Cloud / VM States

| State     | Meaning          | Modules                              |
| --------- | ---------------- | ------------------------------------ |
| `present` | Resource exists  | `ec2`, `azure_rm_*`, `gcp_compute_*` |
| `absent`  | Resource deleted | Same                                 |
| `running` | VM running       | Cloud VM modules                     |
| `stopped` | VM stopped       | Cloud VM modules                     |

---

## 🧠 Universal Rule (IMPORTANT)

✔ `present` / `absent` → **resource existence**
✔ `started` / `stopped` → **runtime state**
✔ `enabled` / `disabled` → **boot-time behavior**

---

## ⭐Interview One-Liner

> **Ansible states define the desired condition of resources, and supported states vary by module such as present/absent for packages, started/stopped for services, and directory/file for filesystem objects.**

---

If you want next:

* 📄 **Printable PDF cheat sheet**
* 🧪 **State-based interview questions**
* 🛠 **Real PROD playbook using multiple states**
* 🎯 **Tricky edge cases (enabled vs started)**

Just tell me 👍
