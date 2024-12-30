---
title: PROFINET DCP
parent: Protocol Analysis
nav_order: 2
---

# PROFINET DCP (Discovery and Configuration Protocol)
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overview
The Discovery and Configuration Protocol (DCP) for Profinet is a link layer protocol that's part of the Profinet protocol suite. It's used to configure device settings, identify device information, and discover devices on a Profinet network

### Basic Structure
PROFINET Real-Time Ethernet frame
![](./figure-1.png)
![](./figure-2.png)

PROFINET DCP PDU
![](./figure-3.png)
![](./figure-4.png)

PDU Data Block
![](./figure-5.png)


### Reference
[https://github.com/boundary/wireshark/blob/master/plugins/profinet/packet-pn.h](https://github.com/boundary/wireshark/blob/master/plugins/profinet/packet-pn.h)<br>
[https://github.com/boundary/wireshark/blob/master/plugins/profinet/packet-pn.c](https://github.com/boundary/wireshark/blob/master/plugins/profinet/packet-pn.c)<br>
[https://github.com/boundary/wireshark/blob/master/plugins/profinet/packet-pn-dcp.c](https://github.com/boundary/wireshark/blob/master/plugins/profinet/packet-pn-dcp.c)<br>
[https://us.profinet.com/profinet-network-geeks-want/](https://us.profinet.com/profinet-network-geeks-want/)

### Sig

--ethertype profinet