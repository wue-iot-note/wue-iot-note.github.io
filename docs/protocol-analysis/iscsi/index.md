---
title: iSCSI
parent: Protocol Analysis
nav_order: 2
---

# Internet Small Computer Systems Interface (iSCSI)
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overview
<b>ISCSI</b> (Internet Small Computer System Interface) is a transport layer protocol that describes how Small Computer System Interface (SCSI) packets should be transported over a TCP/IP network. The iSCSI protocol encapsulates SCSI commands and assembles the data in packets for the TCP/IP layer. The protocol typically runs on port <b>3260</b>. 

### iscsiadm
The iscsiadm utility is a command-line tool allowing discovery and login to iSCSI targets. Some iSCSI commands related to device info and login are listed below.

1. Discover available targets from a discovery portal
```
### Example CLI output
┌──(root㉿kali)-[/home/kali]
└─# iscsiadm -m discovery -t sendtargets -p 10.0.0.1                                   
10.0.0.1:3260,1 iqn.2004-04.com.qnap:ts-431u:iscsi.vmware.fa8a99
10.0.0.1:3260,1 iqn.2004-04.com.qnap:ts-431u:iscsi.vmware.fa8a99
```

2. Login to all targets/specific target
```
iscsiadm -m node -l
iscsiadm -m node -T targetname -p ipaddress -l
```

3. Log out of all targets/specific target
```
iscsiadm -m node -u
iscsiadm -m node -T targetname -p ipaddress -u
```

4. Display information about a target
```
iscsiadm -m node -T targetname -p ipaddress
```

5. Display statistics of a target:
```
iscsiadm -m node -s -T targetname -p ipaddress
```

## Reference
[Internet Small Computer Systems Interface (iSCSI) Naming and Discovery](https://datatracker.ietf.org/doc/html/rfc3721#page-5)
[iscsiadm(8) - Linux man page](https://linux.die.net/man/8/iscsiadm)