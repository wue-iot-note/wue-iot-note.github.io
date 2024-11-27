---
title: SNMP
parent: Protocol Analysis
nav_order: 1
has_toc: false
---

# SNMP
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overview
Simple Network Management Protocol (SNMP) is an Internet Standard protocol for collecting and organizing information about managed devices on IP networks and for modifying that information to change device behavior.<br>

SNMP exposes management data in the form of variables on the managed systems organized in a management information base <b>(MIB)</b>, which describes the system status and configuration. These variables can then be remotely queried/manipulated by managing applications.<br>

An SNMP message is a packet sent over UDP/IP to port 161. UDP/IP is the User Datagram Protocol over IP. an SNMP message must be a valid <b>ASN.1</b> data type, and encoded according to the <b>BER</b>.

### Structure
References: [https://www.ranecommercial.com/legacy/note161.html](https://www.ranecommercial.com/legacy/note161.html)
![](./figure-1.png)

![](./figure-2.jpeg)

### Common Data Types
Refer to [BER Encoding] for more details (./ber-encoding/)

| Primitive Type | Identifier | Complex Data Types | Identifier |
|:---------------|:-----------|:-------------------|:-----------|
| Integer        | 0x02       | get-request        | 0xA0       |
| Octet String   | 0x04       | get-next-request   | 0xA1       |
| Null           | 0x05       | get-response       | 0xA2       |
| OID            | 0x06       | set-request        | 0xA3       |
|                |            | trap               | 0x04       |
|                |            | getBulkRequest     | 0x05       |
|                |            | informRequest      | 0x06       |
|                |            | snmpV2-trap        | 0x07       |
|                |            | report             | 0x08       |

### Common MIB & OID for device identification

#### General

| MIB        | OID                     | Value                     | Description                       |
|:-----------|:------------------------|:--------------------------|:----------------------------------|
| MIB-II     | sysDescr                | 1.3.6.1.2.1.1.1           | textual description of the entity |
| ENTITY-MIB | entPhysicalSoftwareRev  | 1.3.6.1.2.1.47.1.1.1.1.10 | vendor specifc software revision  |
|            | entPhysicalModelName    | 1.3.6.1.2.1.47.1.1.1.1.13 | vendor specific model name        |
|            | entPhysicalDescr        | 1.3.6.1.2.1.47.1.1.1.1.2  | textual description of the entity |
|            | entPhysicalName         | 1.3.6.1.2.1.47.1.1.1.1.7  | textual name of entity            |
|            | entPhysicalHardwareRev  | 1.3.6.1.2.1.47.1.1.1.1.8  | vendor specific hardware revision |
|            | entPhysicalFirmwareRev  | 1.3.6.1.2.1.47.1.1.1.1.9  | vendor specific firmware revision |

#### Printer

| MIB                      | OID                        | Value                          | Description                       |
|:-------------------------|:---------------------------|:-------------------------------|:----------------------------------|
| PRINTER-PORT-MONITOR-MIB | ppmPrinterIEEE1284DeviceId | 1.3.6.1.4.1.2699.1.2.1.2.1.1.3 | IEEE 1284 Device id               |

#### UPS

| MIB     | OID                          | Value                | Description                   |
|:--------|:-----------------------------|:---------------------|:------------------------------|
| UPS-MIB | upsIdentManufacturer         | 1.3.6.1.2.1.33.1.1.1 | UPS manufacturer              |
|         | upsIdentModel                | 1.3.6.1.2.1.33.1.1.2 | UPS model                     |
|         | upsIdentUPSSoftwareVersion   | 1.3.6.1.2.1.33.1.1.3 | UPS firmware/software version |
|         | upsIdentAgentSoftwareVersion | 1.3.6.1.2.1.33.1.1.4 | UPS agent software version    |