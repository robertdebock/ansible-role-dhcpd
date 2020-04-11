# dhcpd

Install and configure dhcpd on your system.

|Travis|GitHub|Quality|Downloads|
|------|------|-------|---------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-dhcpd.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-dhcpd)|[![github](https://github.com/robertdebock/ansible-role-dhcpd/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-dhcpd/actions)|[![quality](https://img.shields.io/ansible/quality/21853)](https://galaxy.ansible.com/robertdebock/dhcpd)|[![downloads](https://img.shields.io/ansible/role/d/21853)](https://galaxy.ansible.com/robertdebock/dhcpd)|

## Example Playbook

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  vars:
    dhcpd_subnets:
      - subnet: "{{ ansible_default_ipv4.network }}/{{ansible_default_ipv4.netmask }}"
        paramaters:
          interface: "{{ ansible_default_ipv4.interface }}"

  roles:
    - role: robertdebock.dhcpd
```

The machine may need to be prepared using `molecule/resources/prepare.yml`:
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.apt_autostart
    - role: robertdebock.core_dependencies
```

For verification `molecule/resources/verify.yml` run after the role has been applied.
```yaml
---
- name: Verify
  hosts: all
  become: yes
  gather_facts: yes

  tasks:
    - name: check if connection still works
      ping:
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## Role Variables

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for dhcpd

# Configuration settings for the daemon.
dhcpd_ipv4_interface: "{{ ansible_default_ipv4.interface | default(eth0) }}"

# Setting applicable for the global scope.
dhcpd_default_lease_time: 600
dhcpd_max_lease_time: 7200
dhcpd_subnet_mask: 255.255.255.0
dhcpd_broadcast_address: 10.0.2.255
dhcpd_routers: 10.0.2.254
dhcpd_domain_name_servers: 192.168.1.1, 192.168.1.2
dhcpd_domain_search: example.com

# The image to serve for PXE booting.
dhcpd_filename: pxelinux.0
# Where the image can be downloaded from.
dhcpd_next_server: 10.0.2.254

# DHCP works with subnets, a list containing predefined format of dicts with properties and options per subnet.
dhcpd_subnets:
  - subnet: "10.0.2.0/24"
    parameters:
        range: "10.0.2.30  10.0.0.200"
        next-server: "10.0.0.0"
    options:
        domain-name-servers: "10.0.2.1"
```

## Requirements

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)
- python netaddr lib

```

## Context

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/dhcpd.png "Dependency")

## Compatibility

This role has been tested on these [container images](https://hub.docker.com/):

|container|tags|
|---------|----|
|amazon|all|
|alpine|all|
|debian|all|
|el|7, 8|
|fedora|all|
|ubuntu|bionic|

The minimum version of Ansible required is 2.8 but tests have been done to:

- The previous version, on version lower.
- The current version.
- The development version.

## Exceptions

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| Suse | Starting ISC DHCPv4 Server chown: invalid user: 'dhcpd:root
shadow
... |


## Testing

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-dhcpd) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-dhcpd/issues)

Testing is done using [Tox](https://tox.readthedocs.io/en/latest/) and [Molecule](https://github.com/ansible/molecule):

[Tox](https://tox.readthedocs.io/en/latest/) tests multiple ansible versions.
[Molecule](https://github.com/ansible/molecule) tests multiple distributions.

To test using the defaults (any installed ansible version, namespace: `robertdebock`, image: `fedora`, tag: `latest`):

```
molecule test

# Or select a specific image:
image=ubuntu molecule test
# Or select a specific image and a specific tag:
image="debian" tag="stable" tox
```

Or you can test multiple versions of Ansible, and select images:
Tox allows multiple versions of Ansible to be tested. To run the default (namespace: `robertdebock`, image: `fedora`, tag: `latest`) tests:

```
tox

# To run CentOS (namespace: `robertdebock`, tag: `latest`)
image="centos" tox
# Or customize more:
image="debian" tag="stable" tox
```

## License

Apache-2.0


## Author Information

[Robert de Bock](https://robertdebock.nl/)
