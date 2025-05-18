exporter setup
=========

install [node_exporter](https://github.com/prometheus/node_exporter)


Usage
------------
you can clone this rules [collection](https://github.com/dgithuba/stacks) and run predefined playbooks:
```bash
ansible-playbook playbooks/node_exporter_setup.yml
```

If you want to force installation via Docker, use the `docker` tag. To force binary installation, use the `bin` tag.  
If no tag is specified, the role will try to detect Docker; if available, it will prefer Docker installation by default.


Requirements
------------

This role optionally uses the community.docker collection, only if you are installing Node Exporter via Docker.
You can install it with:
```bash
ansible-galaxy collection install community.docker
```

If you want to install Node Exporter using Docker, make sure the target interpreter has the following Python packages installed:  

- `docker`  
- `jsondiff`  
- `pyyaml`  

These are required for Ansible Docker modules to work properly.  

Role Variables
--------------
`node_exporter_docker_image_name`: Docker image used for running Node Exporter.  
default: `quay.io/prometheus/node-exporter`


`node_exporter_download_base_url`: Base URL for downloading Node Exporter binaries.  
default: `https://github.com/prometheus/node_exporter/releases/download`  


`node_exporter_repo_api_url`: GitHub API URL to fetch the latest Node Exporter version.  
default: `https://api.github.com/repos/prometheus/node_exporter/releases/latest`  


`node_exporter_stacks_path`: Path to the Docker stack configuration for Node Exporter.(used with Docker install)
default: `{{ docker_stacks_path }}/node_exporter`  


`node_exporter_version`: Version to install; if empty, latest version is fetched (without `v`).  


`node_exporter_user`: User used to run Node Exporter; group with the same name is also created.  default: `node_exporter`  


`node_exporter_executable_path`: Path to install Node Exporter binary when using binary installation.  
default: `/usr/local/bin/node_exporter`  


`node_exporter_listen_address`: Listen address for Node Exporter; useful for container access.  
default: `127.0.0.1:9100`


`node_exporter_flags`: Extra flags passed to Node Exporter command. you can see all options with `node_exporter --help`


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
