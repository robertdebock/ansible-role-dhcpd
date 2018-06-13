
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-dhcpd.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-dhcpd)

Provides a DHCP server for your system.

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

|distribution|ansible 2.3|ansible 2.4|ansible 2.5|
|------------|-----------|-----------|-----------|
|alpine-3.6|yes|yes|yes|
|alpine-3.7|yes|yes|yes|
|archlinux|yes|yes|yes|
|centos-6|yes|yes|yes|
|centos-7|yes|yes|yes|
|debian-buster|yes|yes|yes|
|debian-stretch|yes|yes|yes|
|debian-wheezy|yes|yes|yes|
|fedora-27|yes|yes|yes|
|fedora-28|yes|yes|yes|
|opensuse-42.2|yes|yes|yes|
|opensuse-42.3|yes|yes|yes|
|ubuntu-artful|yes|yes|yes|
|ubuntu-bionic|yes|yes|yes|

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

Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
