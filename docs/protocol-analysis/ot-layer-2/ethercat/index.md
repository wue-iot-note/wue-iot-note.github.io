---
title: EtherCAT
parent: OT Layer 2
nav_order: 2
---

# EtherCAT
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overview
EtherCAT (Ethernet for Control Automation Technology) is an Ethernet-based fieldbus system developed by Beckhoff Automation.

### Basic Structure

The EtherCAT telegram starts with an Ethernet header, followed by the EtherCAT data. The telegram is terminated by a frame check sequence (FCS). The EtherCAT data start with an EtherCAT header, followed by EtherCAT datagrams. If the entire Ethernet frame is smaller than 64 bytes, between 1 and 32 padding bytes are inserted at the end of the EtherCAT data. The EtherCAT data can contain up to 15 datagrams. A datagram consists of a header, the data to be read or written and a working counter.

EtherCAT ethernet frame header<br>
![](./figure-1.png)

EtherCAT telegram
![](./figure-2.png)

- Cmd - EtherCAT command type
- Index - The index is a numerical identifier used by the master to identify duplicates or lost datagrams
- Address - Address: auto-increment, configured station address or logical address
- C - 0: Frame does not circulate, 1: Frame has circulated once
- M - 0: Last EtherCAT datagram, 1: At least one further EtherCAT datagram follows
- Res - reserved (0)


Both EtherCAT frame header and datagram length are in little-endian. eg.
```
EtherCAT frame header
    .... .000 0111 0110 = Length: 0x076
    .... 0... .... .... = Reserved: Valid (0x0)
    0001 .... .... .... = Type: EtherCAT command (0x1)

Hex: dump
0000   76 10 
```
```
Length     : 8 (0x8) - No Roundtrip - More Follows...
    .... .000 0000 1000 = Length: 8
    ..00 0... .... .... = Reserved: Valid (0)
    .0.. .... .... .... = Round trip: Frame is not circulating
    1... .... .... .... = Last indicator: More EtherCAT datagrams will follow

Hex dump:
0000   08 80 
```

### Reference
[https://infosys.beckhoff.com/english.php?content=../content/1033/tc3_io_intro/1257993099.html&id=](https://infosys.beckhoff.com/english.php?content=../content/1033/tc3_io_intro/1257993099.html&id=)<br>
