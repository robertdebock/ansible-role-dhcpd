# [dhcpd](#dhcpd)

Install and configure dhcpd on your system.

|Travis|GitHub|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-dhcpd.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-dhcpd)|[![github](https://github.com/robertdebock/ansible-role-dhcpd/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-dhcpd/actions)|[![quality](https://img.shields.io/ansible/quality/21853)](https://galaxy.ansible.com/robertdebock/dhcpd)|[![downloads](https://img.shields.io/ansible/role/d/21853)](https://galaxy.ansible.com/robertdebock/dhcpd)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-dhcpd.svg)](https://github.com/robertdebock/ansible-role-dhcpd/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  vars:
    dhcpd_subnets:
      - network: "{{ ansible_default_ipv4.network }}"
        netmask: 255.255.255.0

  roles:
    - role: robertdebock.dhcpd
```

The machine needs to be prepared in CI this is done using `molecule/resources/prepare.yml`:
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

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for dhcpd

# Configuration settings for the daemon.
dhcpd_ipv4_interface: "{{ ansible_default_ipv4.interface | default('eth0') }}"

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

# DHCP works with subnets, a list containing properties per subnet.
dhcpd_subnets:
  - network: 10.0.2.0
    netmask: 255.255.255.0
    range_start: 10.0.2.200
    range_end: 10.0.2.210
```

## [Requirements](#requirements)

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

## [Status of requirements](#status-of-requirements)

| Requirement | Travis | GitHub |
|-------------|--------|--------|
| [robertdebock.apt_autostart](https://galaxy.ansible.com/robertdebock/apt_autostart) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-apt_autostart.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-apt_autostart) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-apt_autostart/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-apt_autostart/actions) |
| [robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-bootstrap.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-bootstrap) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions) |
| [robertdebock.core_dependencies](https://galaxy.ansible.com/robertdebock/core_dependencies) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-core_dependencies.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-core_dependencies) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-core_dependencies/actions) |

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/dhcpd.png "Dependency")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|alpine|all|
|amazon|all|
|el|7, 8|
|debian|buster, bullseye|
|fedora|all|
|ubuntu|focal, bionic, xenial|

The minimum version of Ansible required is 2.9, tests have been done to:

- The previous version.
- The current version.
- The development version.

## [Exceptions](#exceptions)

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| Suse | Starting ISC DHCPv4 Server chown: invalid user: 'dhcpd:root
shadow
... |


## [Testing](#testing)

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

## [License](#license)

Apache-2.0


## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
