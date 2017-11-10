Role Name
=========

Provides a DHCP server

Requirements
------------

Access to a repository to install the dhcp server package from.

Role Variables
--------------

None known.

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
