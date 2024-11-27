---
title: BER Encoding
parent: snmp
nav_order: 1
---

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
            <th>Class (2 bit)</th>
            <th>Form (1 bit)</th>
            <th>Number (5 bit)</th>
        </tr>
    </tbody>
</table>

### Class

- [ 00 ] universal class. Most BER elements have a universal type, so any element with a universal type specifies what kind of data it holds. Examples of universal types include 0x01 (BOOLEAN), 0x02 (INTEGER), 0x04 (OCTET STRING), 0x05 (NULL), 0x0A (ENUMERATED), 0x30 (SEQUENCE), and 0x31 (SET). The binary encodings for all of those type values have the leftmost two bits set to zero.

- [ 01 ] The application-specific class. This class allows an application to define its own types that are consistent throughout that application. In this context, LDAP is considered an application. For example, when 0x42 appears in LDAP, it indicates an unbind request protocol op, because RFC 2251 section 4.3 states that the unbind request protocol op has a type of [APPLICATION 2].

- [ 10 ] The context-specific class. This class indicates that the type is specific to a particular usage within a given application. The same type can be re-used in different contexts in the same application as long as there is enough other information to determine which context is applicable in a given situation. For example, in the context of the credentials in a bind request protocol op, the context-specific type 0x80 is used to hold the bind password, but in the context of an extended operation it would be used to hold the request OID.

- [ 11 ] The private class, not typically used in LDAP.

### Form

- [ 0 ] primitive - is used with types that do not contain other types (INTEGERs and BOOLEANs). The contents octets directly represent the encoded value.
- [ 1 ] constructed - is used for types that can include values of other types (SEQUENCEs).

### Number

- For casese when identifer is 0 <=  value <= 30 </br> the Number filed will just be the value of the identifer. e.g. For Identifier 13:

| Class || Form | Number |

| Class | Form              | Number |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

<table>
    <tbody>
        <tr>
            <th colspan=2>Class</th>
            <th>Form</th>
            <th colspan=5>Number</th>
        </tr>
        <tr>
            <th>-</th>
            <th>-</th>
            <th>-</th>
            <th>0</th>
            <th>1</th>
            <th>1</th>
            <th>0</th>
            <th>1</th>
        </tr>
    </tbody>
</table>
