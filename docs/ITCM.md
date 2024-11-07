---
title: ITCM (Interoperable Train Control Messaging)
layout: default
---

# ITCM (Interoperable Train Control Messaging)
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Basic Message Packet Structure

```markdown
--------------------------------------------------------------------------------------------------------
L2/L1 Headers | IP Header | TCP Header| Class D Header | EMP Header \x02 | CTC Message | EMP Header \x03
--------------------------------------------------------------------------------------------------------
```

### Class D Packet Structure

```markdown
1 byte | 1 byte           | 4 byte | 1 byte       | 1 byte          | 4 byte      | variable     | 1 byte      
---------------------------------------------------------------------------------------------------------
STX    | Protocol Version | COMMID | Message type | Message Version | Data Length | Message Body | ETX
```
STX: Start of message delimiter ASCII (0x02)
ETX: End of message delimiter ASCII (0x03)

