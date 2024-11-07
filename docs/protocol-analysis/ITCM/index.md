---
title: ITCM
parent: Protocol Analysis
nav_order: 1
layout: default
---

# ITCM (Interoperable Train Control Messaging)
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Basic Message Packet Structure

![](./figure-1.jpeg)

### Class D Packet Structure

![](./figure-2.jpeg)

![](./figure-3.jpeg)

### EMP Packet Structure

```
tcp.payload[0:2] == 02:02 && tcp.payload[6:1] == 01 &&  tcp.payload[13:2] == 1B:D0
```