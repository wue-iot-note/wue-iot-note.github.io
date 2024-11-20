---
title: Device Broadcast Discovery
nav_order: 2
layout: default
has_toc: false
---

# Device Broadcast Discovery
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## HID Global - VertX Controller UPD Discovery
References:<br>
[https://www.zerodayinitiative.com/advisories/ZDI-16-223/](https://www.zerodayinitiative.com/advisories/ZDI-16-223/)<br>
[https://github.com/coldfusion39/VertXploit/tree/master](https://github.com/coldfusion39/VertXploit/tree/master)
```
echo -n "discover;013;" | netcat -u XXX.XXX.XXX.XXX
```
```
0000   64 69 73 63 6f 76 65 72 65 64 3b 30 39 36 3b 30   discovered;096;0  MAC       : 00:06:8E:03:0C:AE
0010   30 3a 30 36 3a 38 45 3a 30 33 3a 30 43 3a 41 45   0:06:8E:03:0C:AE  Make model: VertX_EVO_V2000
0020   3b 56 65 72 74 58 5f 45 56 4f 5f 56 32 30 30 30   ;VertX_EVO_V2000  IP        : 175.177.166.73
0030   3b 31 37 35 2e 31 37 37 2e 31 36 36 2e 37 33 3b   ;175.177.166.73;  Model     : V2-V2000
0040   31 3b 56 32 2d 56 32 30 30 30 3b 33 2e 36 2e 33   1;V2-V2000;3.6.3  Version   : 3.6.3.101
0050   2e 31 30 31 3b 30 37 2f 32 37 2f 32 30 31 37 3b   .101;07/27/2017;  FW Date   : 07/27/2017
```