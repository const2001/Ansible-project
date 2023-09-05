# Ansible-project

# Project set up 
* change the inventory file (hosts.yaml) that holds the remote hosts that ansible will handle.
* Example entry is
```yaml
webserver: # <-- group
  hosts: # <-- List of hosts in group
    gcloud_host: # <-- host number 1 in group
      ansible_host: 35.189.109.16
      ansible_port: 22
      ansible_ssh_user: rg
    app01:  # <-- host number 2 in group
      ansible_host: app01
    app02:  # <-- host number 3 in group
      ansible_host: app02
  vars:  # <-- common variables in this group
    ansible_python_interpreter: /usr/bin/python3
```
* to test if all hosts are accesible, run
```bash
ansible -m ping all
```
* to test if a group of hosts are accesible, run
```bash
ansible -m ping all <group-name>
```
# Install ansible & roles
```bash
sudo apt update
sudo apt install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible

sudo apt update
sudo apt install ansible

ansible-galaxy install geerlingguy.docker
ansible-galaxy install geerlingguy.pip
```


## Open ports on your vm
```bash
8000, 8001, 8025, 5432
```
## Deploy your project with docker
```bash
ansible-playbook ansible_playbook_flask_db_setup.yml
ansible-playbook ansible_playbook_flask_admin_setup.yml
ansible-playbook ansible_playbook_mailhog_setup.yml
```

## Urls for access project's componets
```bash
http://your_vm_ip:8001/    #adminSystem
http://your_vm_ip:8000/    #userSystem
http://your_vm_ip:8025/    #mailhog
```




