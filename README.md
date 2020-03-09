Ansible Role: osm_linux_armour
=========

This Ansible roles deals with auditing of Ubuntu according to CIS benchmark.

|  **S. No.**    |**Services**           |**Checks that should be in place**|
|----------------|-----------------------|----------------------------------|
|1.  |Special Purpose Services           |Ensure Avahi, DHCP, LDAP Server is not enabled|
|2.  |Service Client                     |Ensure rsh, telnet, LDAP client is not installed|
|3.  |inetd Services                     |Ensure telnet server, discarded services,rsh server is not installed|
|4.  |Logging and Auditing               |auditd is installed and enabled, audit log storage size, system is disabled when audit logs are full, audit logs are not automatically deleted, login and logout events are collected, session initiation information is collected|
|5.  |Filesystem Configuration           |Disable unused filesystems, Ensure /tmp, /var/tmp is configured|
|6.  |System File Permissions            |Ensure passwd, passwd-, group, group-, shadow, shadow-, gshadow, gshadow- are configured|
|7.  |Filesystem Integrity Check         |Ensure filesystem integrity is regularly checked|
|8.  |Additional Process Hardening       |Ensure core dumps are restricted and prelink is disabled|
|9.  |Network Configuration Host         |Ensure IP forwarding, packet redirect sending are disabled and suspicious packets are logged|
|10. |Network Configuration Host and Router|Ensure bogus ICMP responses are ignored, Reverse Path Filtering is enabled, TCP SYN Cookies is enabled|
|11. |TCP Wrapper                        |Ensure permissions on /etc/hosts.allow and /etc/hosts.deny are configured|
|12. |Uncommon Network Protocols         |Ensure DCCP and SCTP are disabled|

Version History
---------------
|**Date**| **Version**| **Description**| **Changed By** |
|----------|---------|---------------|-----------------|
|**Feb 27** | v.1.0 | Initial Draft | Anjali Singh |

Salient Features
----------------
* This role will configure the OS on the basis of the CIS benchmark.

Supported OS
------------
  * Ubuntu:bionic

Dependencies
------------
* Python should be on present on testing server.

Role Variables
--------------
There are two types of variables i.e Mandatory and optional. Mandatory variables are those which should be configured as per CIS benchmark and Optional variables depends upon the service one is using. It can be enable or disable depending upon the requirements.

### Mandatory Variables

|**Variables**| **Default Values**| **Description**|
|-------------|-------------------|----------------|
| System_File_Permissions | host.conf, hostname, hosts, hosts.allow, hosts.deny, passwd, passwd-, shadow, shadow-, gshadow, gshadow-, group, group- | Special files whose permissions will change. |
|os_kernel_enable_core_dump| false|core dump value which is set to 0|
|os_packages_clean| true |deprecated packages are removed|
|os_packages_list|xinetd, inetd, ypserv, telnet-server, telnet-client, rsh-server, rsh-client, prelink, openldap-clients, openldap2-client, ldap-utils| Disbale these sevices if not required|
|audit_package |auditd     |This is used to keep record of every logs|

### Optional Variables

|**Variables**| **Optional Values**| **Description**|
|-------------|--------------------|---------------|
| os_services_name | avahi-daemon, dhcpd, slapd, named | Special purpose services which can be stop if not required|
|audit_max_log_file | 5 | Number of log files one needs to keep|
|os_audit_max_log_file_action| keep_logs | To save logs |

Inventory
----------
An inventory should look like this:
```ini
[osconfig]                 
192.168.1.198    ansible_user=ubuntu    
```

Example Playbook
----------------

* Here is an example playbook :-

```sh
---
- name: Ubuntu audit
  hosts: osconfig
  become: true
  roles:
    - role: ubuntu_hardening
```

Future Proposed Changes
-----------------------
Will add support for other os as well.

References
----------
- **[cis_benchmark_pdf](http://gauss.ececs.uc.edu/Courses/c6056/lectures/ubuntu-18.04-LTS.pdf)**

Author Information
------------------

- **[Anjali Singh](mailto:anjali.singh@opstree.com)*
