---
title: ITCM
parent: Protocol Analysis
nav_order: 1
layout: default
has_toc: false
---

# ITCM (Interoperable Train Control Messaging)
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overview
Interoperable Train Control Messaging (ITCM) is a messaging system used by the railroad industry. The Centralized train control (CTC)
messages are transported over ITCM. A railroad edge messaging protocol (EMP) header and a railroad Class D messaging transport header are appended to the message to generate a packet. The packet is transmitted to a receiving one of the railroad dispatch system and the railroad wayside system across the railroad communications system.

### Basic Message Packet Structure

![](./figure-1.jpeg)

### Class D Packet Structure

![](./figure-2.jpeg)

![](./figure-3.jpeg)

### EMP General Packet Structure

![](./figure-4.jpeg)

### Sample Hex Dump
```
0000   02 02 00 00 1d 01 01 02 00 00 00 50 04 13 ec 00   ...........P....
0010   09 00 00 10 00 00 00 00 66 a3 b9 ee 2b 00 10 06   ........f...+...
0020   38 63 73 78 74 2e 77 2e 37 33 39 31 30 30 3a 31   8csxt.w.739100:1
0030   31 2e 77 69 75 00 78 78 2e 6c 2e 78 2e 30 30 30   1.wiu.xx.l.x.000
0040   30 30 30 3a 74 6d 63 00 a5 e8 b6 fb fb 82 0e 8a   000:tmc.........
0050   f7 bd ef 2a 0f 2d f0 3d 82 d6 df 53 03            ...*.-.=...S.

ITCM
    STX: (\x02)
    Protocol Version: (\x02)
    COMMID: (\x00001D01) 7425
    Message Type: Data Message (\x01)
    Message Version: (\x02) 2
    Data Length: (\x00000050) 80
EMP
    Protocol Version: (\x04) 4
    Message Type: (\x13EC) 5100
    Message Version: (\x00) 0
    Flags: (\x09)
    Data Length: (\x000010) 16
    Message Number: (\x00000000)
    Message Time: (\x66A3B9EE)
    Remaining Header Size: (\x2B) 43
    Time to Live: (\x0010) 16 sec
    Source: ..csxt.w.739100:11.wiu
    Destination: xx.l.x.000000:tmc
    Data Integrity: (\xA5E8B6FBFB820E8AF7BDEF2A0F2DF03D82D6DF53)
ITCM
    ETX: (\x03)
```

wireshark filter for EMP message type (sub XX to message id in hex)
```
tcp.payload[0:2] == 02:02 && tcp.payload[6:1] == 01 &&  tcp.payload[13:2] == XX:XX
```

### EMP Message Body - Application

### Reference
- AAR Manual of Standards and Recommended Practices Railway Electronics - CLASS D MESSAGING SPECIFICATION
Standard S-9356
- Federal Railroad Administration - Railroad Wireless Communications Roadmap