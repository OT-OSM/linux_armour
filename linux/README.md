Ansible Role: osm_linux_armour
=========

This Ansible roles deals with auditing of Ubuntu according to CIS benchmark.

Version History
--------------
|**Date**| **Version**| **Description**| **Changed By** |
|----------|---------|---------------|-----------------|
|**Feb 27** | v.1.0 | Initial Draft | Sudipt Sharma |

Salient Features
----------------
* This role will configure the OS on the basis of the CIS benchmark.

Supported OS
------------
  * Ubuntu:bionic

Dependencies
------------
* None

Role Variables
--------------
There are two types of variables i.e Mandatory and optional.

### Mandatory Variables

|**Variables**| **Default Values**| **Description**|
|----------|---------|---------------|
| System_File_Permissions | host.conf, hostname, hosts, hosts.allow, hosts.deny, passwd, passwd-, shadow, shadow-, gshadow, gshadow-, group, group- | Special files whose permissions will change. |

Inventory
----------
An inventory should look like this:-
```ini
[osconfig]                 
192.168.1.198    ansible_user=ubuntu    
```

Example Playbook
----------------

* Here is an example playbook:-

```sh
---
- name: Ubuntu audit
  hosts: osconfig
  become: true
  roles:
    - role: linux


```

Future Proposed Changes
-----------------------
Can be applied on centos.

References
----------
- **[cis_benchmark_pdf](http://gauss.ececs.uc.edu/Courses/c6056/lectures/ubuntu-18.04-LTS.pdf)**

Author Information
------------------

- **[Anjali Singh](mailto:anjali.singh@opstree.com)*
