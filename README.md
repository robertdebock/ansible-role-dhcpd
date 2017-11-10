Role Name
=========

Provides a DHCP server

Requirements
------------

Access to a repository to install the dhcp server package from.

Role Variables
--------------

ISC DHCP has quite some parameters to set. Here is a list, but please have a look at defaults/main.yml for an applied idea.

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
