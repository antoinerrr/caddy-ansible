[![Build Status](https://travis-ci.org/antoiner77/caddy-ansible.svg?branch=master)](https://travis-ci.org/antoiner77/caddy-ansible)
[![Galaxy Role](https://img.shields.io/badge/ansible--galaxy-caddy-blue.svg)](https://galaxy.ansible.com/antoiner77/caddy/)

Caddy Ansible Role
=========

This role installs and configures the caddy web server. The user can specify any http configuration parameters they wish to apply their site. Any number of sites can be added with configurations of your choice.

Dependencies
------------
None

Role Variables
--------------

**The [Caddyfile](https://caddyserver.com/docs/caddyfile)** expressed as path to a [template](https://docs.ansible.com/ansible/template_module.html)<br>
example:
```
Caddyfile.jinja2
```
example of content as Jinja2 template:
```
localhost:{{ myport }}
gzip
# tls email@example.com
root {{ myroot }}
git github.com/antoiner77/caddy-ansible
```
example of content as plan Caddyfile:
```
localhost:2020
gzip
# tls email@example.com
root /var/www
git github.com/antoiner77/caddy-ansible
```
**Auto update Caddy?**<br>
default:
```
caddy_update: yes
```
**Features that can be added to core:** DNS, awslambda, cors, expires, filemanager, filter, git, hugo, ipfilter, jsonp, jwt, locale, mailout, minify, multipass, prometheus, ratelimit, realip, search, upload<br>
Changing this variable will reinstall Caddy with the new features if `caddy_update` is enabled<br>
default:
```
caddy_features: git
```
**Use `setcap` for allowing Caddy to open a low port (e.g. 80, 443)?**
default:
```
caddy_setcap: yes
```

Example Playbook
----------------
```
---
- hosts: all
  roles:
    - role: caddy-ansible
      caddy_config: |
        localhost:2020
        gzip

        tls email@example.com

        root /var/www
        git github.com/antoiner77/caddy-ansible
```

Debugging
---------
If the service fails to start you can figure out why by looking at the output of Caddy.<br>
**Upstart (ubuntu, debian wheezy, centos/rhel 6)**<br>
`tail /var/log/upstart/caddy.log`<br>
**Systemd (debian jessie, centos/rhel 7)**<br>
`systemctl status caddy -l`

If something doesn't seem right, open an issue!

Contributing
------------
Pull requests are welcome. Please test your changes beforehand with vagrant:
```
vagrant up
vagrant provision (since it already provisioned there should be no changes here)
vagrant destroy
```
