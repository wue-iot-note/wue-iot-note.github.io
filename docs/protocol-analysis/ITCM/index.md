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

## Basic Message Packet Structure

![](./figure-1.jpeg)

<table>
    <tbody>
        <tr>
            <th>L2/L1 Headers</th>
            <th>IP Header</th>
            <th>TCP Header</th>
            <th>Class D Header</th>
            <th>EMP Header \x02 </th>
        </tr>
        <tr>
            <th>CTC Message</th>
            <th>EMP Header</th>
            <th colspan=2></th>
        </tr>
    </tbody>
</table>

### Class D Packet Structure


<table>
    <tbody>
        <tr>
            <th>1 byte</th>
            <th>1 byte</th>
            <th>4 byte</th>
            <th>1 byte</th>
            <th>1 byte</th>
        </tr>
        <tr>
            <th>STX</th>
            <th>Protocol Version</th>
            <th>COMMID</th>
            <th>Message type</th>
            <th>Message Version</th>
        </tr>
        <tr>
            <th>4 byte</th>
            <th>variable</th>
            <th>1 byte</th>
            <th colspan=2></th>
        </tr>
        <tr>
            <th>Data Length</th>
            <th>Message Body</th>
            <th>ETX</th>
            <th colspan=2></th>
        </tr>
    </tbody>
</table>

STX: Start of message delimiter ASCII (0x02)
ETX: End of message delimiter ASCII (0x03)

