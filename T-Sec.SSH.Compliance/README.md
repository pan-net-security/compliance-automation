# Hardening for SSH

## Description

This Ansible role can be used to implement hardening of OpenSSH on
servers. The hardening will be done following the security requirements
from Telekom Security (see 'References' for used versions of document).

## Supported Platforms

Ansible version >= 2.6.x
Python version >= 3.5.x

The role is tested with the following SSH versions:

  * OpenSSH > Version 7.x

## Variables

The default variables are located in:

```
defaults/
└── main
    ├── main.yml
    └── ssh(01)ssh-requirements.yml
```

Before execution of the playbook please change this variables following the
demands of the systems you like to harden.

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `config_ipv6_enable` | `false` | Enables if IPv6 should be used. |
| `config_mgmt_interface_ipv4` | `false` | Specifies if a dedicated IPv4 management interface is used. |
| `mgmt_interface_ipv4` | `0.0.0.0` | Defines IPv4 address of management interface. |
| `config_mgmt_interface_ipv6` | `false` | Enable if (true) a dedicated IPv6 management interface is used. |
| `mgmt_interface_ipv6` | `::` | Defines IPv6 address for management interface. |
| `config_new_user` | `false` | Defines if a new user should be configured. |
| `user_name` | `none` | Defines name for new user. |
| `password` | `none` | Defines password for new user. |
| `public_key_file` | `{{ role_path }}/files/id_rsa.pub` |  Defines path to public-key file (e.g. id_rsa.pub). |
| `group_sudo` | `sudo` | Defines group used for sudo. |
| `config_restart_handlers` | true | Defines whether service restart handlers should be triggered. |

Be advised that changing any values in `defaults/main/ssh*` are not advised.

Additional variables are located in the following files in directory '/vars':

* /vars
  * /main.yml
  * /RedHat.yml
  * /Ubuntu.yml
  * /vars_ssh(01)ssh-requirements.yml

-------------------------------------------------------------------------------

**NOTE:** Changing variables in these files can affect security compliance and must be approved by your responsible Project Security Manager!

-------------------------------------------------------------------------------

## Execution of Playbook

Example of playbook:
```
---

- hosts: test-system
  become: true    # Become root (sudo)
  roles:
    - T-Sec.LinuxOS.Compliance
```

Start playbook with:

```
$ ansible-playbook <playbook>.yml
```

## References

Telekom Security - Security Requirements:
* SecReq 3.04: Secure Shell (SSH)

## Development

Pre-requisite:
- Vagrant
```
$ which -s vagrant && echo 'Vagrant found' || echo 'Vagrant not found'
Vagrant found
$ which -s VirtualBox && echo 'VirtualBox found' || echo 'VirtualBox not found'
Vagrant found
```

Virtual environment & tests:

```
virtualenv -p python3 .venv
. .venv/bin/activate
pip install molecule[vagrant] python-vagrant
molecule test
````

## License

Apache License, Version 2.0

See file LICENSE
