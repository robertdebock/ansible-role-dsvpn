dsvpn
=========

<img src="https://docs.ansible.com/ansible-tower/3.2.4/html_ja/installandreference/_static/images/logo_invert.png" width="10%" height="10%" alt="Ansible logo" align="right"/><img src="https://raw.githubusercontent.com/robertdebock/ansible-role-dsvpn/master/meta/logo.png" alt="Project logo" width="40" height="40" align="left"/>
<a href="https://travis-ci.org/robertdebock/ansible-role-dsvpn"> <img src="https://travis-ci.org/robertdebock/ansible-role-dsvpn.svg?branch=master" alt="Build status"/></a> <img src="https://img.shields.io/ansible/role/d/42441"/> <img src="https://img.shields.io/ansible/quality/42441"/>

Install and configure dsvpn on your system.

Example Playbook
----------------

This example is taken from `molecule/resources/playbook.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.dsvpn
```

The machine you are running this on, may need to be prepared, I use this playbook to ensure everything is in place to let the role work.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.ca_certificates
    - role: robertdebock.core_dependencies
    - role: robertdebock.buildtools
```


Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

Role Variables
--------------

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for dsvpn

# The released version to download. See https://github.com/jedisct1/dsvpn/releases.
dsvpn_version: 0.1.3

# Where to download dsvpn to.
dsvpn_temporary_directory: /tmp

# Where to install dsvpn.
dsvpn_install_directory: /usr/local/bin

# Where to generate the keys. This is a sensitive file.
dsvpn_key_directory: /tmp

# The role to let dsvpn take, can be `client` or `server`.
dsvpn_role: client

# When the role `client` is selected, this is the address of the server
# to connect to. Can be an address or a (resolvable) name.
dsvpn_server: 127.0.0.1
```

Requirements
------------

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.ca_certificates
- robertdebock.core_dependencies
- robertdebock.buildtools
- robertdebock.service

```

Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/dsvpn.png "Dependency")


Compatibility
-------------

This role has been tested on these [container images](https://hub.docker.com/):

|container|tags|
|---------|----|
|archlinux|all|
|debian|all|
|el|7, 8|
|fedora|all|
|ubuntu|artful, bionic|

The minimum version of Ansible required is 2.8 but tests have been done to:

- The previous version, on version lower.
- The current version.
- The development version.



Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-dsvpn) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-dsvpn/issues)

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

License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/)
