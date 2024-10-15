---
title: BER Encoding
layout: default
---

# BER Encoding
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Basic Encoding Rules Overview

BER uses a Tag-Length-Value (TLV) format for encoding information. The type or tag indicates what kind of data follows, the length indicates the length of the data that follows, and the value represents the actual data. Each value may consist of one or more TLV-encoded values, each with its own identifier, length, and contents.

<table>
    <tbody>
        <tr>
            <th>T (Tag)</th>
            <th>L (Len)</th>
            <th>V (Value)</th>
        </tr>
    </tbody>
</table>

## Encoding Identifiers (Tags)

The identifier consists of three parts:

<table>
    <tbody>
        <tr>
            <th colspan=2>Class</th>
            <th colspan=1>Form</th>
            <th colspan=5>Number</th>
        </tr>
        <tr>
            <th colspan=2>2 bit</th>
            <th colspan=1>1 bit</th>
            <th colspan=5>5 bit</th>
            <th></th>
            <th></th>
            <th></th>
            <th></th>
            <th></th>
        </tr>
    </tbody>
</table>

Class
00 universal
01 application
10 context-specific
11 private


<table>
    <tbody>
        <tr>
            <th>Modbus/TCP</th>
            <th colspan=5>UMAS</th>
        </tr>
        <tr>
            <th>Modbus Header</th>
            <th>Func Code (\x5A)</th>
            <th>Session Key</th>
            <th>UMAS Func</th>
            <th>Data</th>
        </tr>
        <tr>
            <th></th>
            <th>1 Byte</th>
            <th>1 Byte</th>
            <th>1 Byte</th>
            <th>1 Byte</th>
        </tr>
    </tbody>
</table>

## UMAS Function Code

request information about a device

| Code | Function | Description |
|:-----|:---------|:------------|
| 0x02 | pu_GetPlcInfo | requests information about the device |
| 0x04 | pu_GetPlcStatus | queries the PLC status |
| 0x06 | pu_GetMemoryCardInfo | requests information about the device’s SD card |

## Reference
[modbus-umas-schneider.lua](https://github.com/biero-el-corridor/Wireshark-UMAS-Modicon-M340-protocol/blob/main/modbus-umas-schneider.lua) \
[modicon-info.nse](https://github.com/digitalbond/Redpoint/blob/master/modicon-info.nse) \
[Kaspersky ICS-Cert- The secrets of Schneider Electric’s UMAS protocol](https://ics-cert.kaspersky.com/publications/reports/2022/09/29/the-secrets-of-schneider-electrics-umas-protocol/#umas-protocol)