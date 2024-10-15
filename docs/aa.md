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
            <th>Class (2 bit)</th>
            <th>Form (1 bit)</th>
            <th>Number (5 bit)</th>
        </tr>
        <tr>
            <th>00 universal</th>
            <th>0 primitive</th>
            <th></th>
        </tr>
        <tr>
            <th>01 application</th>
            <th>1 constructed</th>
            <th></th>
        </tr>
        <tr>
            <th>10 context-specific</th>
            <th></th>
            <th></th>
        </tr>
        <tr>
            <th>11 private</th>
            <th></th>
            <th></th>
        </tr>
    </tbody>
</table>