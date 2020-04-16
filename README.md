# firewall

Manage firewall ports on all (known) Linux operating systems.

|Travis|GitHub|Quality|Downloads|
|------|------|-------|---------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-firewall.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-firewall)|[![github](https://github.com/robertdebock/ansible-role-firewall/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-firewall/actions)|[![quality](https://img.shields.io/ansible/quality/29220)](https://galaxy.ansible.com/robertdebock/firewall)|[![downloads](https://img.shields.io/ansible/role/d/29220)](https://galaxy.ansible.com/robertdebock/firewall)|

## Example Playbook

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.firewall
```

The machine may need to be prepared using `molecule/resources/prepare.yml`:
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - role: robertdebock.bootstrap
```

For verification `molecule/resources/verify.yml` run after the role has been applied.
```yaml
---
- name: Verify
  hosts: all
  become: yes
  gather_facts: yes

  tasks:
    - name: check if connection still works
      ping:
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## Role Variables

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for firewall

# A list of service to allow traffic to.
firewall_services:
  - name: ssh

# A bit more difficult example:
# firewall_services:
#   - name: ssh
#   - name: https
#   - name: 5353
#     protocol: udp
```

## Requirements

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap

```

## Context

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/firewall.png "Dependency")

## Compatibility

This role has been tested on these [container images](https://hub.docker.com/):

|container|tags|
|---------|----|
|debian|all|
|el|7, 8|
|fedora|all|
|opensuse|all|
|ubuntu|bionic|

The minimum version of Ansible required is 2.8 but tests have been done to:

- The previous version, on version lower.
- The current version.
- The development version.

## Exceptions

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| redhat | Can't test on RHEL: No package matching 'firewalld' found available, installed or updated |


## Testing

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-firewall) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-firewall/issues)

Testing is done using [Tox](https://tox.readthedocs.io/en/latest/) and [Molecule](https://github.com/ansible/molecule):

[Tox](https://tox.readthedocs.io/en/latest/) tests multiple ansible versions.
[Molecule](https://github.com/ansible/molecule) tests multiple distributions.

To test using the defaults (any installed ansible version, namespace: `robertdebock`, image: `fedora`, tag: `latest`):

```
molecule test

# Or select a specific image:
image=ubuntu molecule test
# Or select a specific image and a specific tag:
image="debian" tag="stable" tox
```

Or you can test multiple versions of Ansible, and select images:
Tox allows multiple versions of Ansible to be tested. To run the default (namespace: `robertdebock`, image: `fedora`, tag: `latest`) tests:

```
tox

# To run CentOS (namespace: `robertdebock`, tag: `latest`)
image="centos" tox
# Or customize more:
image="debian" tag="stable" tox
```

## License

Apache-2.0


## Author Information

[Robert de Bock](https://robertdebock.nl/)
