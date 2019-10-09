<img align="left" src="images/telekom.png" alt="Deutsche Telekom Pan-Net" height="80" width="80">

# DT Pan-Net, s.r.o - Security Compliance

-------------------------------------------------------------------------------

## Description

_This is a fork from the original work started at [Telekom Security](https://github.com/telekomsecurity/TelekomSecurity.Compliance.Automation)._

The goal of the project is to provide a quick and reliable way to reach compliance against Deutsche Telekom group-wide security Requirements.

NOTE: changing default values is HIGHLY **not** recommended.

## Features

- Can be run in live systems
- Can be run at image-creation time

## Available Scripts

**Ansible:**

  1. [SSH](/T-Sec.SSH.Compliance)
  2. [Linux OS for Servers](/T-Sec.LinuxOS.Compliance)

## Usage

You can't use ansible-galaxy since the roles are packed in one repository, but here is a way to deal with that:

```
TEMP_DIR=$(mktemp -d)
git clone --depth 1 -b v0.1 https://github.com/pan-net-security/compliance-automation.git $TEMP_DIR
mv $TEMP_DIR/T-Sec.* /etc/ansible/roles
rm -fr $TEMP_DIR
```

## References

Telekom Security - Security Requirements:
  1. SecReq 3.04: Secure Shell
  2. SecReq 3.65: Linux OS for Servers

-------------------------------------------------------------------------------

Authors:
- [Telekom Security](https://security.telekom.com/) (original work)
- Deutsche Telekom Pan-Net
