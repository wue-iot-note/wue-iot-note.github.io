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
            <th >Form</th>
            <th colspan=5>Number</th>
        </tr>
        <tr>
            <th colspan=2>2 bit</th>
            <th >1 bit</th>
            <th colspan=5>5 bit</th>
        </tr>
        <tr>
            <th ></th>
            <th ></th>
            <th ></th>
            <th ></th>
            <th ></th>
            <th ></th>
            <th ></th>
            <th ></th>
        </tr>
    </tbody>
</table>