# Ansible Galaxy role for install and configure Bareos Storage Daemon.

![Build Status](https://github.com/leadlineit/ansible-role-bareos_sd/actions/workflows/ansible-galaxy-ci.yml/badge.svg)
[![Galaxy Role](https://img.shields.io/badge/Ansible--Galaxy-leadlineit.bareos_sd-blue.svg?logo=ansible&logoColor=white)](https://galaxy.ansible.com/leadlineit/bareos_sd/)

This role helps to install and configure Bareos Storage Daemon to Debian (buster/bullseye).

Requirements
------------

This role requires Ansible 2.9 or higher.

Role Variables
--------------

The variables that can be passed to this role and a brief description about them are as follows:

```yaml
---
bareos_keyserver: keyserver.ubuntu.com
bareos_apt_key: E01957D6C9FED482
bareos_release: 21
bareos_tls_path: /etc/bareos/tls
bareos_tls_certs: your.bareos.dir.com

bareos_sd:
  location: /data/bareos
  director:
    - name: your-dir
      description: Director description (who is permitted to contact this storage daemon)
      password: DIRAver@gEStr0ngPaSSw0rd
      tls_enable: "yes"
    - name: your-mon
      description: Restricted Director monitor description
      password: MONAver@gEStr0ngPaSSw0rd
      monitor: "yes"
      tls_enable: "yes"
  storage:
    - name: your.storage
      description: Storage description
      max_jobs: 20
      tls_enable: "yes"
  device:
    - name: your-data
      description: Device description
      max_jobs: 20
      path: /data/bareos
  messages:
    - name: your-messages
      description: Messages description
      server: your-dir
```

The variables above are optional. They don't have a default value, so if you don't define them - tasks using them will be skipped. 
You can set only some of them, or not set at all (in this case, you will simply install Bareos Storage with default configuration). 

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: servers
  roles:
    - { role: leadlineit.bareos_sd, tags: bareos_sd }
```

License
-------

MIT

Author Information
------------------

This role was created by Artem Kasianchuk.
