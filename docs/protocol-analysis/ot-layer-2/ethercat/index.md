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

EtherCAT ethernet frame header<br>
![](./figure-1.png)

EtherCAT telegram
![](./figure-2.png)

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