exporter setup
=========

install [node_exporter](https://github.com/prometheus/node_exporter)


Usage
------------
you can clone this rules [collection](https://github.com/dgithuba/stacks) and run predefined playbooks:
```bash
ansible-playbook playbooks/node_exporter_setup.yml
```
Requirements
------------

This role optionally uses the community.docker collection, only if you are installing Node Exporter via Docker.
You can install it with:
```bash
ansible-galaxy collection install community.docker
```

Role Variables
--------------

# Where to place node_exporter Docker Compose stack (used with Docker install)
node_exporter_stacks_path: "{{ docker_stacks_path }}/node_exporter"

# Version of node_exporter to install. Leave empty to auto-detect latest version.
# Note: Do not include the "v" prefix. Example: "1.9.1"
node_exporter_version: ""

# The Linux user (and group) that will run node_exporter
node_exporter_user: "node_exporter"

# Path to place the node_exporter binary (used for binary install)
node_exporter_executable_path: "/usr/local/bin/node_exporter"

# Listening address for node_exporter metrics endpoint
# For example, using the Docker bridge IP (172.17.0.1) makes it accessible from other containers.
node_exporter_listen_address: "127.0.0.1:9100"

# Custom flags to pass to node_exporter
# You can add more flags as needed based on your monitoring setup.
node_exporter_flags:
  - "--web.listen-address={{ node_exporter_listen_address }}"


Dependencies
------------

This role does not include Docker installation by default.
If you plan to use the Docker-based setup for Node Exporter, it is recommended to use a separate role to install Docker first (for example, a docker role), before running this one.
You can use [dgithuba.stacks.docker](/roles/docker/) to install docker.

Example Playbook
----------------
```yaml
- name: Install node exporter
  hosts: all
  become: true
  gather_facts: true
  roles:
    - node_exporter
```
