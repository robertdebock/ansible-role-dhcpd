Role Name
=========

Provides a DHCP server

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

Dependencies
------------

- robertdebock.bootstrap

Example Playbook
----------------

```
- hosts: servers
  roles:
    - robertdebock.dhcpd
```

License
-------

Apache License, Version 2.0

Author Information
------------------

Robert de Bock <robert@meinit.nl>
