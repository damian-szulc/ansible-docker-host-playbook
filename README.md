# Ansible docker host playbook

> Minimal Ansible playbook for managing docker, firewall, and system users

## About

This playbook contains configuration for:
- docker installation
- firewall setup (using `DOCKER_USER` chain. Docker remains running with enabled `iptables`)
- zsh and oh-my-zsh configuration
- adding specified users
- disabling logging in using `root` user

## Usage

1. Clone this repository:

```
git clone git@github.com:damian-szulc/ansible-docker-host-playbook.git
```

2. Fill in hosts file. For example:

```
[hosts_group]
host1 ansible_host=<host IP here>
```

3. Modify group_vars, e.g.:

```
firewall_allow:
  - proto: tcp
    port: 22
  - proto: tcp
    port: 80
  - proto: tcp
    port: 443

users:
  - ted
  - mark
```

4. Copy ssh keys into following location `files/keys/{{ username }}/id_rsa.pub` (for example `files/keys/ted/id_rsa.pub`).

5. Run ansible. The first time you should most likely use `root` user. Later, logging in using `root` will be disabled and you should use your own user.
```
ansible-playbook -i hosts playbook.yml -u root
```