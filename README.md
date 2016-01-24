Caddy Ansible Role
=========

This role installs and configures the caddy web server. The user can specify any http configuration parameters they wish to apply their site. Any number of sites can be added with configurations of your choice.

Dependencies
------------
None

Role Variables
--------------

Email is used for the lets encrypt integration:<br>
example:
```
caddy_email: foo@foo.bar
```
Features that can be added to core: cors,git,hugo,ipfilter,jsonp,search<br>
default:
```
caddy_features: git
```
List of sites and their options<br>
example:
```
caddy_sites:
  foo.bar:
    - root /var/www
    - gzip
```
Directives like git are also possible (notice the semicolons)<br>
example:
```
caddy_sites:
  foo.bar:
    - root /var/www
    - git github.com/user/site {
        branch development;
      }
```
Site indepentent config options<br>
default:
```
caddy_config:
  - gzip
```

Example Playbook
----------------
```
---
- hosts: all
  roles:
    - role: caddy-ansible
      caddy_email: foo@foo.bar
      caddy_sites:
        foo.bar:
          - root /var/www
```

Contributing
------------
Pull requests are welcome. Please test your changes beforehand with vagrant:
```
vagrant up
vagrant provision (since it already provisioned there should be no changes here)
vagrant destroy
```
