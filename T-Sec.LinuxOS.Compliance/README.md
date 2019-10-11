# Hardening for Linux OS Servers


## Description

This Ansible role can be used to implement hardening of the Linux OS on
servers. The hardening will be done following the security requirements
from Deutsche Telekom Security (see 'References' for used versions of document).

## Supported Platforms

Ansible version >= 2.6.x
Python version >= 3.5

The role is tested with the following Linux versions:

  * Ubuntu 18.04 LTS

-------------------------------------------------------------------------------

**IMPORTANT:** This role only supports Linux versions for SERVERS! The role
is not tested with desktop systems and can cause unexpected malfunctions.

-------------------------------------------------------------------------------

## Role

The downloaded role must be stored in the directory for Ansible roles on your computer. The default path to store roles is `/etc/ansible/roles`. In the file
`/etc/ansible/ansible.cfg` with variable `roles_path` an own path can be
specified.

```
roles_path    = ~/roles
```

## Variables

The default variables are located in:
```
defaults/
└── main
    ├── main.yml
    ├── linux(01)basic-hardening.yml
    ├── linux(02)logging.yml
    ├── linux(03)pam.yml
    ├── linux(04)iptables.yml
    └── linux(05)mac.yml
```
 Before execution of the playbook please set this variables following the demands of the systems you like to harden.


| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `config_iptables_rules_tcp` | `true` | Defines if TCP iptables rules should be configured. |
| `tcp_services` | `22` | Defines needed TCP ports.|
| `config_iptables_rules_udp` | `true` | Defines if UDP iptables rules should be configured. |
| `tcp_services` | none | Defines needed UDP ports.|
| `config_partitions` | `false` | Defines if separate partitions are used. |
| `partitions` | `tmp, var` | Defines existing partitions. |
| `config_ipv6_enable` | `false` | Enables if IPv6 should be used. |
| `do_system_upgrade` | `false` | Defines if a system upgrade should be performed .|
| `config_mgmt_interface_ipv4` | `false` | Specifies if a dedicated IPv4 management interface is used. |
| `mgmt_interface_ipv4` | `0.0.0.0` | Defines IPv4 address of management interface. |
| `config_mgmt_interface_ipv6` | `false` | Enable if (true) a dedicated IPv6 management interface is used. |
| `mgmt_interface_ipv6` | `::` | Defines IPv6 address for management interface. |
| `config_ntp` | `true` | Defines if NTP should be configured. |
| `ntp_servers` | `ntp-pool-info_ntpp10.telekom.de`, `ntp-pool-info_ntpp21.telekom.de` | Defines addresses of NTP servers to use. |
| `set_timezone` | `true` | Defines if time zone should be configured. |
| `use_timezone` | `Europe/Berlin` | Defines time zone to use. |
| `config_syslog` | `false` |  Defines if Syslog should be configured. |
| `syslog_type` | `rsyslog` | Defines type of syslog to use. |
| `syslog_server` |  | Defines IP addresses of Syslog server(s) to use. |
| `config_restart_handlers` | `true` | Defines whether service restart handlers should be triggered. |

Additional variables are located in the following files in directory `/vars` and are meant to be _hardcoded_ values meant for distribution differences.

```
vars/
├── RedHat.yml
├── Ubuntu-18.yml
├── Ubuntu.yml
└── main.yml
```

-------------------------------------------------------------------------------

**NOTE:"" Changing variables in these files can affect security compliance and must be approved by your responsible Project Security Manager!

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
* SecReq 3.65: Linux OS for Servers

**Not implemented requirements**

The following security requirements of the named document are not implemented in
this version of the Ansible role:

* Req 5:	Dedicated partitions must be used for growing content that can influence the availability of the system.

Note! Req 5 should be implemented during system installation!

* Req 6:	Parameters nodev, nosuid and noexec must be set for partitions where this is applicable.
* Req 20: GPG check for repository server must be activated and corresponding keys for trustable repositories must be configured.
* Req 21:	User accounts must be used that allow unambiguous identification of
the user.
* Req 24:	User accounts with extensive rights must be protected with two authentication attributes.
* Req 25:	The system must be connected to a central system for user administration.
* Req 27: The management of the operating system must be done via a dedicated management network which is independent from the production network.
* Req 29: Encrypted protocols must be used for management access to administrate
the operating system.
* Req 42:	If Syslog-NG is used, the default permission of 640 or more restrictive for logfiles must be configured.
* Req 43:	If Syslog-NG is used, at least one central logging server must be
configured.

The following requirements are not included as they are regular compliance checks and not relevant for hardening:

* Req 61:	No legacy + entries must exist in files passwd, shadows and group.
* Req 62	A user's home directory must be owned by the user and have mode 750 or more restrictive.
* Req 63:	Default group for the root account must be GID 0.
* Req 64:	Root must be the only UID 0 account.
* Req 65:	All groups in /etc/passwd must exist in /etc/group.
* Req 66:	No duplicate UIDs and GIDs must exist.
* Req 67:	No duplicate user and group names must exist.
* Req 68: The shadow group must be empty (only Ubuntu Linux).
* Req 69: No files and directories without assigned user or group must exist.
* Req 70:	Permissions of security relevant configuration files must have the distribution default values or more restrictive.

## License

Apache License, Version 2.0

See file LICENSE
