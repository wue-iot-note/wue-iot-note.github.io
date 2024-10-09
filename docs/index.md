---
title: Schneider Electric UMAS
layout: default
---

# Schneider Electric UMAS
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Structure

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

## Wireshark Dissector
[modbus-umas-schneider.lua](https://github.com/biero-el-corridor/Wireshark-UMAS-Modicon-M340-protocol/blob/main/modbus-umas-schneider.lua)

## Device scanning
[modicon-info.nse](https://github.com/digitalbond/Redpoint/blob/master/modicon-info.nse)