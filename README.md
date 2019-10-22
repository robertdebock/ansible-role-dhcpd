dhcpd
=========

<img src="https://docs.ansible.com/ansible-tower/3.2.4/html_ja/installandreference/_static/images/logo_invert.png" width="10%" height="10%" alt="Ansible logo" align="right"/>
<a href="https://travis-ci.org/robertdebock/ansible-role-dhcpd"><img src="https://travis-ci.org/robertdebock/ansible-role-dhcpd.svg?branch=master" alt="Build status" align="left"/></a>

Install and configure dhcpd on your system.

<img src="https://img.shields.io/ansible/role/d/21853"/>
<img src="https://img.shields.io/ansible/quality/21853"/>

Example Playbook
----------------

This example is taken from `molecule/resources/playbook.yml`:
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  vars:
    dhcpd_ipv4_interface: eth0
    dhcpd_default_lease_time: 60
    dhcpd_max_lease_time: 120
    dhcpd_subnet_mask: 255.255.255.0
    dhcpd_broadcast_address: 10.0.2.255
    dhcpd_routers: 10.0.2.1
    dhcpd_domain_name_servers: 10.0.2.1
    dhcpd_domain_search: install
    dhcpd_filename: pxelinux.0
    dhcpd_next_server: 10.0.2.1
    dhcpd_subnets:
      - network: 10.0.2.0
        netmask: 255.255.255.0
        range_start: 10.0.2.127
        range_end: 10.0.2.254

  roles:
    - robertdebock.dhcpd
```

The machine you are running this on, may need to be prepared.
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - robertdebock.bootstrap
    - robertdebock.apt_autostart
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

Role Variables
--------------

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

# DHCP works with subnets, a list containing properties per subnet.
dhcpd_subnets:
  - network: 10.0.2.0
    netmask: 255.255.255.0
    range_start: 10.0.2.200
    range_end: 10.0.2.210
```

Requirements
------------

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.apt_autostart

```

This role uses the following modules:
```yaml
---
- package
- service
- template
```

Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/dhcpd.png "Dependency")


Compatibility
-------------

This role has been tested on these [container images](https://hub.docker.com/):

|container|tag|allow_failures|
|---------|---|--------------|
|docker-alpine-openrc|latest|no|
|docker-alpine-openrc|edge|yes|
|docker-debian-systemd|stable|yes|
|docker-debian-systemd|unstable|yes|
|docker-debian-systemd|latest|no|
|docker-centos-systemd|7|no|
|docker-redhat-systemd|7|no|
|docker-centos-systemd|latest|no|
|docker-redhat-systemd|latest|no|
|docker-fedora-systemd|latest|no|
|docker-fedora-systemd|rawhide|yes|
|docker-opensuse-systemd|latest|no|
|docker-ubuntu-systemd|rolling|yes|
|docker-ubuntu-systemd|devel|yes|
|docker-ubuntu-systemd|latest|no|

This role has been tested on these Ansible versions:

- ansible~=2.7
- ansible~=2.8
- git+https://github.com/ansible/ansible.git@devel

The indicator '\~=' means [compatible with](https://www.python.org/dev/peps/pep-0440/#compatible-release). For example 'ansible\~=2.8' would pick the latest ansible-2.8, for example ansible-2.8.6.




Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-dhcpd) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-dhcpd/issues)

To test this role locally please use [Molecule](https://github.com/ansible/molecule):
```
pip install molecule
molecule test
```

To test on Amazon EC2, configure [~/.aws/credentials](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html) and set a region using `export AWS_REGION=eu-central-1` before running `molecule test --scenario-name ec2`.

There are many specific scenarios available, please have a look in the `molecule/` directory.

License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/)
