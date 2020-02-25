# Ansible Role: Singularity

[![Actions Status](https://github.com/pddg/ansible-singularity/workflows/Test%20and%20lint/badge.svg)](https://github.com/pddg/ansible-singularity/actions)

An Ansible Role that installs [Singularity](https://www.sylabs.io/singularity/) on Linux. This role supports Singularity >= 3.0.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# Singularity target version
singularity_version: "3.5.3"
```

From the role gantsign.golang

```yaml
# Required
# Location for GOPATH environment variable
golang_gopath: /opt/go/packages

# Base installation directory the Go language SDK distribution
golang_install_dir: '/opt/go/{{ golang_version }}'
```

Please refer the compatibility table of Singularity and Golang version.

| Singularity/Go | 1.11.x | 1.12.x | 1.13.x |
| -------------- | :----: | :----: | :----: |
| 3.0.x          | o      | o      | x      |
| 3.1.x          | o      | o      | x      |
| 3.2.x          | o      | o      | x      |
| 3.3.x          | o      | o      | x      |
| 3.4.x          | o      | o      | x      |
| 3.5.x          | x      | x      | o      |

## Dependencies

Roles:
 - [gantsign.golang](https://galaxy.ansible.com/gantsign/golang)

## Example Playbook

```yaml
- hosts: hpc-nodes
  pre_tasks:
    - name: create a folder for go
      file:
        path: "{{ golang_install_dir }}"
        recurse: yes
    - name: apt update
      apt:
        cache_valid_time: 3600
        update_cache: yes
      when: ansible_os_family == "Debian"
  roles:
    - singularity
```

## License

GNU General Public License v3.0

## Author Information

This role is modified by [Shoma Kokuryo](https://github.com/pddg).
The original is created by [Gildas Le Corguillé](https://github.com/lecorguille).

