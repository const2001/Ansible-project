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

## Deploy your project without docker & kubernates
```bash
ansible-galaxy install geerlingguy.postgresql
ansible-galaxy install jebovic.mailhog
```

## Open ports on your vm
```bash
8000, 9000, 8025, 5432, 1025, 80, 100
```

## Urls for access project's componets
```bash
http://your_vm_ip:8000/    #adminSystem
http://your_vm_ip:9000/    #userSystem
http://your_vm_ip:8025/    #mailhog
```

## Deploy your project with docker
```bash
ansible-playbook playbooks/docker-install.yml
ansible-playbook playbooks/django-app-docker.yml
ansible-playbook playbooks/django2-app-docker.yml
```

## Open ports on your vm
```bash
8001, 9001, 81, 8026, 5433, 101
```

## Urls for access project's componets
```bash
http://your_vm_ip:8001    #adminSystem
http://your_vm_ip:9001/    #userSystem
http://your_vm_ip:8026/    #mailhog)
```

## Deploy your project with kubernates
```bash
ansible-playbook playbooks/django-install-microk8s.yml
ansible-playbook playbooks/django2-install-microk8s.yml
```

## Install kubernates on your vm
```bash
sudo snap install microk8s --classic
sudo ufw allow in on eth0 && sudo ufw allow out on eth0
sudo ufw default allow routed
```
## Enable kubernates
```bash
microk8s start
microk8s enable dns ingress storage
microk8s enable dashboard
```

## Access with sudo
```bash
sudo usermod -a -G microk8s $USER
sudo chown -f -R $USER ~/.kube
su - $USER
```

## Open ports on your vm
```bash
8000, 9000, 80, 8025, 100, 16443, 30191
```

## Urls for access project's componets
```bash
http://your_ip_address:8000 #adminSystem
http://your_ip_address:9000 #userSystem
your_vm_ip:8025 #mailhog
```
