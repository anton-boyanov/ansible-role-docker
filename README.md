# Ansible Role: Docker

An Ansible role to install Docker (CE or EE) on various Linux distributions.

## Requirements

#### Supported distributions

| Distribution | Version            |
| ------------ | ------------------ |
| CentOS       | 7                  |
| Debian       | Buster 10          |
|              | Stretch 9 (stable) |
| Fedora       | 29                 |
|              | 28                 |
| Ubuntu       | Cosmic 18.10       |
|              | Bionic 18.04 (LTS) |
|              | Xenial 16.04 (LTS) |


## Role Variables

```yaml
# Flag to uninstall old versions of Docker
docker_uninstall_old_versions: false

# Edition can be one of: 'ce' (Community Edition) or 'ee' (Enterprise Edition)
docker_edition: ce
# Docker and containerd packages
docker_packages:
  - "docker-{{ docker_edition }}"
  - "docker-{{ docker_edition }}-cli"
  - containerd.io
# State can be one of: 'present' or 'latest'
docker_state: present

# List of users to be added to the docker group
docker_users:
  - "{{ lookup('env', 'USER') }}"

# Flag to configure Docker to start on boot
docker_start_on_boot: true
```

#### Debian / Ubuntu

```yaml
# Architecture can be one of: 'amd64', 'armhf', 'arm64', 'ppc64el' or 's390x'
docker_arch: amd64
# APT release channel can be one or many of: 'stable', 'nightly' or 'test'
docker_channels:
  - stable
```

## Dependencies

None.

## Example Playbook

```yaml
- name: Install Docker
  hosts: localhost
  become: yes

  roles:
    - ansible-role-docker
```
