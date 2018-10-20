
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-dhcpd.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-dhcpd)

Installs and configures a DHCP server for your system.

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-clamav) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-clamav/issues)

To test this role locally please use [Molecule](https://github.com/metacloud/molecule):
```
pip install molecule
molecule test
```
There are many scenarios available, please have a look in the `molecule/` directory.

Context
--------
This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/dhcpd.png "Dependency")

Requirements
------------

Access to a repository to install the dhcp server package from.

Role Variables
--------------

ISC DHCP has quite some parameters to set. Here is a list, but please have a look at defaults/main.yml for an applied idea.

- dhcpd_ipv4_interface - INTERFACE
- dhcpd_default_lease_time - INTEGER
- dhcpd_max_lease_time - INTEGER
- dhcpd_subnet_mask - IPADDRESS
- dhcpd_broadcast_address - IPADDRESS
- dhcpd_routers - IPADDRESS
- dhcpd_domain_name_servers - comma separated IPADDRESS
- dhcpd_domain_search - DOMAIN
- dhcpd_filename - FILENAME
- dhcpd_next_server - IPADDRESS

dhcpd_subnets:
  - network - IPADDRESS
    netmask - IPADDRESS
    range_start - IPADDRESS
    range_end - IPADDRESS

Where:
INTERFACE can be eth0 for example.
INTEGER can be 600 for example.
IPADDRESS can be 192.168.0.0 or 172.16.0.255 for example.
DOMAIN can be a string like example.com.
FILENAME can be a file like pxelinux.0.

Dependencies
------------

You can prepare you system by including this role.

- [robertdebock.bootstrap](https://travis-ci.org/robertdebock/ansible-role-bootstrap)

Download the dependencies by issuing this command:
```
ansible-galaxy install --role-file requirements.yml
```

Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.4|ansible 2.5|ansible 2.6|ansible-2.7|ansible-devel|
|------------|-----------|-----------|-----------|-----------|-------------|
|alpine-edge*|yes|yes|yes|yes|yes*|
|alpine-latest|yes|yes|yes|yes|yes*|
|archlinux|yes|yes|yes|yes|yes*|
|centos-6|yes|yes|yes|yes|yes*|
|centos-latest|yes|yes|yes|yes|yes*|
|debian-latest|yes|yes|yes|yes|yes*|
|debian-stable|yes|yes|yes|yes|yes*|
|debian-unstable*|yes|yes|yes|yes|yes*|
|fedora-latest|yes|yes|yes|yes|yes*|
|fedora-rawhide*|yes|yes|yes|yes|yes*|
|opensuse-leap|yes|yes|yes|yes|yes*|
|opensuse-tumbleweed|yes|yes|yes|yes|yes*|
|ubuntu-artful|yes|yes|yes|yes|yes*|
|ubuntu-devel*|yes|yes|yes|yes|yes*|
|ubuntu-latest|yes|yes|yes|yes|yes*|

The star means the build may fail, it's marked as an experimental build.

Example Playbook
----------------

```
- hosts: servers
  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.dhcpd
      dhcpd_ipv4_interface: eth0
      dhcpd_default_lease_time: 60
      dhcpd_max_lease_time: 120
      dhcpd_subnet_mask: 255.255.255.0
      dhcpd_broadcast_address: 192.168.1.255
      dhcpd_routers: 192.168.1.1
      dhcpd_domain_name_servers: 192.168.1.127
      dhcpd_domain_search: install
      dhcpd_filename: pxelinux.0
      dhcpd_next_server: 192.168.1.127
      dhcpd_subnets:
      - network: 192.168.1.0
        netmask: 255.255.255.0
        range_start: 192.168.1.200
        range_end: 192.168.1.210
```

Install this role using `galaxy install robertdebock.dhcpd`.

License
-------

Apache License, Version 2.0

Author Information
------------------

[Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
