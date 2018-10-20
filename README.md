firewall
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-firewall.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-firewall)

Configures the firewall for your system.
Different distributions use different firewall implementations. This Ansible role aims to be very simply to use. It's been designed to work with:

|distribution|firewall       |
|------------|---------------|
|Alpine      |iptables       |
|Archlinux   |not implemented|
|CentOS 6    |iptables       |
|CentOS 7    |firewalld      |
|Debian      |uwf            |
|Fedora      |frewalld       |
|OpenSUSE    |firealld       |
|Ubuntu      |uwf            |

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-firewall) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-firewall/issues)

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
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/firewall.png "Dependency")

Requirements
------------

- A system installed with required packages to run Ansible. Hint: [bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap).
- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the last 3 release of Ansible.)
- For CentOS-7, set the variable `ansible_python_interpreter` to `/usr/bin/python3`. For example: `ansible-playbook --extra-vars "ansible_python_interpreter=usr/bin/python3" playbook.yml`

Role Variables
--------------

- firewall_services: a list of services. [default: "ssh"]

Dependencies
------------

- None known.

Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.4|ansible 2.5|ansible 2.6|
|------------|-----------|-----------|-----------|
|alpine-edge|no|no|no|
|alpine-latest|no|no|no|
|archlinux|yes|yes|yes|
|centos-6|yes|yes|yes|
|centos-latest|yes|yes|yes|
|debian-latest|yes|yes|yes|
|debian-stable|yes|yes|yes|
|fedora-latest|yes|yes|yes|
|fedora-rawhide|yes|yes|yes|
|opensuse-leap|yes|yes|yes|
|opensuse-tumbleweed|yes|yes|yes|
|ubuntu-artful|yes|yes|yes|
|ubuntu-latest|yes|yes|yes|

Example Playbook
----------------

```
---
- name: firewall
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.firewall
      firewall_services:
        - name: ssh
        - name: http
        - name: https
        - name: 4992
          protocol: tcp
```

To install this role:
- Install this role individually using `ansible-galaxy install robertdebock.firewall`

Sample roles/requirements.yml: (install with `ansible-galaxy install -r roles/requirements.yml
```
---
- name: robertdebock.bootstrap
- name: robertdebock.firewall
```

License
-------

Apache License, Version 2.0

Author Information
------------------

[Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
