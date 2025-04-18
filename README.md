# Ansible Collection - dgithuba.stacks

A collection of useful, production-ready Ansible roles and playbooks for setting up common infrastructure services

## 🚀 What’s Inside?

This collection currently includes:

- [common](roles/common/) — common configurations like ssh dns users and install packages
- [node_exporter](roles/node_exporter/) — Install Prometheus Node Exporter (binary or Docker-based)
- [docker](roles/docker/) — Install Docker & Docker Compose (you can specifiy docker version)
- More roles coming soon: VPN, DNS setup, monitoring stack, etc.

## 📦 Installation

You can install this collection using Ansible Galaxy:

```bash
ansible-galaxy collection install dgithuba.stacks
```

Or clone it manually:
```bash
git clone https://github.com/dgithuba/ansible-collection-stacks.git
```

## 🛠️ Usage
Example playbook:
```yaml
- name: Setup node_exporter
  hosts: all
  collections:
    - dgithuba.stacks
  roles:
    - role: node_exporter
```
### playbooks
- [base_configuration](/playbooks/base_configuration.yml): run common roles for install common packages and common configuration like ssh,dns,user.
- [docker_setup](/playbooks/docker_setup.yml): run docker role to install docker.
- [node_exporter_setup](/playbooks/node_exporter_setup.yml): to install node_exporter.
- [os_hardening](/playbooks/os_hardening.yml): hardening os and ssh base [devsec.hardening.os_hardening](https://github.com/dev-sec/ansible-collection-hardening/tree/master/roles/os_hardening) and [devsec.hardening.ssh_hardening](https://github.com/dev-sec/ansible-collection-hardening/tree/master/roles/ssh_hardening)
- [setup_interpreter](/playbooks/setup_interpreter.yml): Creates a Python interpreter using `python-venv` and installs the required Python packages for the Docker SDK. This ensures compatibility and proper execution of roles that rely on the `community.docker` collection.

```bash
ansible-playbook playbooks/node_exporter_setup.yml
```
## todo
- [ ] setup prometheus-grafana on one-node with docker
- [ ] setup nginx with docker
- [ ] setup vpn on node with configuration
