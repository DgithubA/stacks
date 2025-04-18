docker installer
=========

install [docker](https://docs.docker.com/engine/install/) with version selection capability.


Usage
------------
To use this role, you can simply run the playbook provided in this repository.
This role automatically detects your Linux distribution (currently supports Ubuntu and Rocky, with more to be added in the future), adds the official Docker repository to your package manager, installs Docker using the appropriate package manager, and then configures the Docker daemon according to the provided variables. The daemon is restarted to apply the new configuration.

In addition, for roles that depend on the community.docker collection, a Python virtual environment is created using python-venv, and all required Python packages are installed inside it.

Finally, a user named deployer is created and added to the docker group.

Tags
------------

- python: Only installs the Python packages required for Docker SDK (docker_required_python_packages).

- prepare: Removes conflicting packages, installs required packages defined in docker_required_packages, and adds the Docker repository.

- repo: Only adds the Docker repository to the package manager.

- config, daemon: Applies Docker daemon configurations defined in docker_daemon_options.

- interpreter: Creates a Python interpreter using `python-venv` and installs the required Python packages for the Docker SDK. This ensures compatibility and proper execution of roles that rely on the `community.docker` collection.

- deployer: Creates a deployer user and adds it to the docker group.


Role Variables
--------------

Here are the variables you can configure:

| Variable           | Default     | Description                                               |
|--------------------|-------------|-----------------------------------------------------------|
| `docker_version`   | `""`        | Specific version of Docker to install. If empty, installs the latest available. |
| `docker_daemon_options`| `{"live_restore": true, "experimental": false}` | docker daemon configuration. |

You can set `docker_version` like this:
```yaml
docker_version: "27.0.1"
```
and can set `docker_daemon_options` like this:
```yaml
docker_daemon_options: {"proxy":{"http_url": "http://127.0.0.1:10808", "https_url": "http://127.0.0.1:10808", "no_proxy_url": "127.0.0.0/8"}}
```


Example Playbook
----------------
```yaml
- name: Setup Docker
  hosts: all
  become: true
  roles:
    - role: dgithuba.stacks.docker
      vars:
        docker_version: "27.0.1"
```