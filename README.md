# Ansible Role: linux_armour

Ansible role to **harden Linux systems based on CIS (Center for Internet Security) Benchmarks**, implemented in **staged levels** to allow progressive enforcement.

This role **actively enforces security controls** across core OS components such as filesystem, kernel, authentication, logging, networking, SSH, PAM, firewall, and user account management.

## Requirements

- Ansible 2.18+
- Privilege escalation (become)

## Hardening Approach

The role is structured around **CIS stages** using the variable `cis_Stage`.

| Stage | Description |
|------|------------|
| 1 | Essential / baseline hardening |
| 2+ | Advanced and stricter hardening controls |

Many tasks are executed **only when `cis_Stage > 1`** to avoid breaking workloads unintentionally.

## Salient Features

The role enforces security controls across the following areas:

- Filesystem hardening and kernel module restrictions
- Process and privilege hardening
- Secure boot and mandatory access control (SELinux)
- Login banners and access warnings
- Removal of unnecessary services and desktop components
- Time synchronization enforcement
- Network hardening (kernel parameters and protocols)
- SSH server hardening
- Privilege escalation controls
- PAM authentication policies
- User account and environment hardening
- System logging and accounting
- Patch management (RedHat-based systems)
- Firewall configuration
- Filesystem integrity checks
- Secure permissions for critical system files

## Supported OS
  * Ubuntu
  * Amazon Linux

## Required Variables
cis_Stage (mandatory)

Controls the level of hardening applied.
```plain
cis_Stage: 1
```

## Inventory
An inventory should look like this:
```ini
[osconfig]                 
192.168.1.198    ansible_user=ubuntu    
```

## Example Playbook
* Here is an example playbook :-

```sh
---
- name: OS audit
  hosts: osconfig
  become: true
  roles:
    - role: ot-osm.linux_armour
```

## References
- **[cis_benchmark](https://www.cisecurity.org/cis-benchmarks)**

## Contact Information

This project is managed by [OpsTree Solutions](http://opstree.com). If you have any queries or suggestions, mail us at [opensource@opstree.com](mailto:opensource@opstree.com).
