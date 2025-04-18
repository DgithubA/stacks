common configurations
=========

Installing essential packages and configuring SSH, DNS, and more

Usage
------------
use [base_configuration.yml](/playbooks/base_configuration.yml) or use below playbook:
```yaml
- name: Apply base configurations
  hosts: all
  become: true
  roles:
    - role: common
      tags:
        - common
```

Role Variables
--------------
```yaml
common_dns_servers:
  - 8.8.8.8
  - 1.1.1.1
  - 10.202.10.202
  - 10.202.10.102
  - 178.22.122.100
  - 185.51.200.2
```
List of DNS servers to be used for name resolution. These will be added to the system's resolver configuration.

```yaml
common_ssh_permit_root_login: "no"
```
Controls whether the root user is allowed to login via SSH. Use "no" to disable root SSH login.

```yaml
common_ssh_enable_password_authentication: "no"
```
Enables or disables SSH password authentication. Use "no" to enforce key-based authentication only.

```yaml
common_ssh_permit_empty_passwords: "no"
```
Disallow login to SSH with accounts that have empty passwords.

```yaml
common_ssh_public_key_authentication: "yes"
```
Enable or disable public key authentication for SSH.

```yaml
common_ssh_authentication_methods: "publickey"
```
Specifies the allowed authentication methods. Default is "publickey".

```yaml
common_ssh_port: 22
```
The port on which the SSH server should listen.

```yaml
common_ssh_max_auth_tries: 3
```
Maximum number of authentication attempts permitted per connection.

```yaml
common_ssh_login_grace_time: 1m
```
Time allowed for successful authentication before the server disconnects.

```yaml
common_ssh_x11_forwarding: "no"
```
Enable or disable X11 forwarding over SSH.

```yaml
common_ssh_allow_tcp_forwarding: "no"
```
Control whether TCP forwarding is permitted.

```yaml
common_ssh_allow_agent_forwarding: "no"
```
Controls whether SSH agent forwarding is allowed.

```yaml
common_ssh_use_pam: "yes"
```
Enables or disables the Pluggable Authentication Module (PAM) integration.

```yaml
common_ssh_use_dns: "no"
```
Disable DNS resolution of client IPs for performance and security.

```yaml
common_ssh_banner: none
```
Path to the SSH login banner file. Use "none" to disable.

```yaml
common_ssh_max_sessions: 5
```
Maximum number of open SSH sessions permitted per network connection.

```yaml
common_ssh_users:
  - dana_ahmadi
```
List of system users whose public keys will be installed to their `~/.ssh/authorized_keys`.  
The public keys should exist in the `files/` directory with the filename format `<username>.pub`.  
For example, for `dana_ahmadi`, place the public key file as:  
`roles/common/files/dana_ahmadi.pub`

role tags
----------------
- common: Installing essential packages was stored in vars folder
- ssh: ssh configuration.
- publickey: just copy public_keys under `files/` to `~/.ssh/authorized_keys` on target hosts.
- dns: configure dns Based on variables.
- user: create user `admin_user` vars and make it sudoers.
