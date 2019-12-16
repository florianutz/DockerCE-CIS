Docker CE CIS Hardening
=========

[![Build Status](https://travis-ci.org/florianutz/DockerCE-CIS.svg?branch=master)](https://travis-ci.org/florianutz/DockerCE-CIS)
[![Ansible Role](https://img.shields.io/badge/role-florianutz.DockerCE--CIS-blue.svg)](https://galaxy.ansible.com/florianutz/DockerCE-CIS/)


Configure Docker CE engine to be CIS compliant. Level 1 and 2 findings will be corrected by default.

This role **will make changes to the system** that could break things. This is not an auditing tool but rather a remediation tool to be used after an audit has been conducted.

## IMPORTANT INSTALL STEP

If you want to install this via the `ansible-galaxy` command you'll need to run it like this:

`ansible-galaxy install -p roles -r requirements.yml`

With this in the file requirements.yml:

```
- src: https://github.com/florianutz/DockerCE-CIS.git
```

Requirements
------------

You should carefully read through the tasks to make sure these changes will not break your systems before running this playbook.

Role Variables
--------------

There are many role variables defined in defaults/main.yml. This list shows the most important.
##### 1.1 | Ensure a separate partition for containers has been created
`cis_rule_1_1: false`

##### 2.1 | Ensure network traffic is restricted between containers on the default bridge
`cis_rule_2_1: "false"`

##### 2.2 | Ensure the logging level is set to 'info'
`cis_rule_2_2: "info"`

##### 2.3 | Ensure Docker is allowed to make changes to iptables
`cis_rule_2_3: "true"`

##### 2.8 | Enable user namespace support
`cis_rule_2_8: "default"`

##### 2.13 | Ensure operations on legacy registry (v1) are Disabled (no longer supported by Docker CE)


##### 2.14 | Ensure live restore is Enabled
`cis_rule_2_14: "true"`

##### 2.15 | Ensure Userland Proxy is Disabled
`cis_rule_2_15: "false"`

##### 2.17 | Ensure experimental features are avoided in production
`cis_rule_2_17: !unsafe docker version --format '{{ .Server.Experimental }}'`

##### 2.18 | Ensure containers are restricted from acquiring new privileges
`cis_rule_2_18: "true"`

Dependencies
------------

Ansible > 2.2

Example Playbook
----------------

```
- name: Harden DOcker CE engine
  hosts: servers
  become: yes

  roles:
     - DockerCE-CIS
```
License
-------

MIT
