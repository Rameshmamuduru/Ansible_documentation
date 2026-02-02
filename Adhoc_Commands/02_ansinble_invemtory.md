# What is Ansible Inventory?
Inventory = the list of all servers (nodes) that Ansible will manage.
## It tells Ansible:
- Where to connect (IP/hostname)
- How to connect (user, SSH key, port)
- Which group the server belongs to (web, db, etc.)
- Variables for servers (paths, configs, roles)

# Types of invetory:
```
| Type    | Definition                  | Best Use           | Pros                   | Cons                         |
| ------- | --------------------------- | ------------------ | ---------------------- | ---------------------------- |
| Static  | Manual file listing servers | Small/mid-scale    | Simple, easy           | Not scalable, manual updates |
| Dynamic | Generated automatically     | Large-scale, cloud | Scales, always updated | More setup complexity        |
| Hybrid  | Static + dynamic            | Mixed infra        | Flexible               | More complex                 |
```

# Ansible inventory:
in older version we use get the hosts incentory file under
```
/etc/ansible/host
```
but for updated versions we need to create a oath and inventory file as well
```
sudo mkdir -p /etc/ansible
sudo vim /etc/ansible/ansible.cfg
and paste these commands

[defaults]
inventory=/etc/ansible/hosts
host_key_checking=False
```
And then create a host inventory file using below commands
```
sudo vim /etc/ansible/hosts

and update the servers like below

[qa-server]
172.31.7.172
```
and done with all  use the below command and check the output

```
ansible qa-server -m ping

Output:
ansible@ip-172-31-1-57:/etc/ansible$ ansible qa-server -m ping
[WARNING]: Invalid characters were found in group names but not replaced, use -vvvv to see details
[WARNING]: Host '172.31.7.172' is using the discovered Python interpreter at '/usr/bin/python3.12', but future installation of another Python interpreter could cause a different interpreter to be discovered. See https://docs.ansible.com/ansible-core/2.20/reference_appendices/interpreter_discovery.html for more information.
172.31.7.172 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.12"
    },
    "changed": false,
    "ping": "pong"
}
ansible@ip-172-31-1-57:/etc/ansible$ 

