dhcpd
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-dhcpd.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-dhcpd)

Provides a DHCP server for your system.

Requirements
------------

Access to a repository to install the dhcp server package from.

Role Variables
--------------

ISC DHCP has quite some parameters to set. Here is a list, but please have a look at defaults/main.yml for an applied idea.

- ipv4_interface - INTERFACE
- default_lease_time - INTEGER
- max_lease_time - INTEGER
- subnet_mask - IPADDRESS
- broadcast_address - IPADDRESS
- routers - IPADDRESS
- domain_name_servers - comma separated IPADDRESS
- domain_search - DOMAIN
- filename - FILENAME
- next_server - IPADDRESS

subnets:
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

- robertdebock.bootstrap

Download the dependencies by issuing this command:
```
ansible-galaxy install --role-file requirements.yml
```

Example Playbook
----------------

```
- hosts: servers
  roles:
    - role: robertdebock.dhcpd
      ipv4_interface: eth0
      default_lease_time: 60
      max_lease_time: 120
      subnet_mask: 255.255.255.0
      broadcast_address: 192.168.1.255
      routers: 192.168.1.1
      domain_name_servers: 192.168.1.127
      domain_search: install
      filename: pxelinux.0
      next_server: 192.168.1.127
      subnets:
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

Robert de Bock <robert@meinit.nl>
