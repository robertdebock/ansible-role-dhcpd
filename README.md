dhcpd
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-dhcpd.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-dhcpd)

Install and configure dhcpd on your system.

Example Playbook
----------------

This example is taken from `molecule/default/playbook.yml`:
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - robertdebock.dhcpd
```

The machine you are running this on, may need to be prepared. Tests have been done on machines prepared by this playbook:
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no

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
- A recent version of Ansible. (Tests run on the last 3 release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.apt_autostart

```

Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/dhcpd.png "Dependency")


Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.6|ansible 2.7|ansible devel|
|------------|-----------|-----------|-------------|
|alpine-edge*|yes|yes|yes*|
|alpine-latest|yes|yes|yes*|
|archlinux|yes|yes|yes*|
|centos-6|yes|yes|yes*|
|centos-latest|yes|yes|yes*|
|debian-latest|yes|yes|yes*|
|debian-stable|yes|yes|yes*|
|debian-unstable*|yes|yes|yes*|
|fedora-latest|yes|yes|yes*|
|fedora-rawhide*|yes|yes|yes*|
|opensuse-leap|yes|yes|yes*|
|ubuntu-devel*|yes|yes|yes*|
|ubuntu-latest|yes|yes|yes*|
|ubuntu-rolling|yes|yes|yes*|

A single star means the build may fail, it's marked as an experimental build.

Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-dhcpd) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-dhcpd/issues)

To test this role locally please use [Molecule](https://github.com/metacloud/molecule):
```
pip install molecule
molecule test
```

To test on Amazon EC2, configure [~/.aws/credentials](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html) and `export AWS_REGION=eu-central-1` before running `molecule test --scenario-name ec2`.

There are many specific scenarios available, please have a look in the `molecule/` directory.

Run the [ansible-galaxy](https://github.com/ansible/galaxy-lint-rules) and [my](https://github.com/robertdebock/ansible-lint-rules) lint rules if you want your change to be merges:

```shell
git clone https://github.com/ansible/ansible-lint.git /tmp/ansible-lint
ansible-lint -r /tmp/ansible-lint/lib/ansiblelint/rules .

git clone https://github.com/robertdebock/ansible-lint /tmp/my-ansible-lint
ansible-lint -r /tmp/my-ansible-lint/rules .
```

License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
