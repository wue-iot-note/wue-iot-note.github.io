---
title: Device Broadcast Discovery
nav_order: 2
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
echo -n "discover;013;" | netcat -u XXX.XXX.XXX.XXX 4070
```
```
0000   64 69 73 63 6f 76 65 72 65 64 3b 30 39 36 3b 30   discovered;096;0
0010   30 3a 30 36 3a 38 45 3a 30 33 3a 30 43 3a 41 45   0:06:8E:03:0C:AE
0020   3b 56 65 72 74 58 5f 45 56 4f 5f 56 32 30 30 30   ;VertX_EVO_V2000
0030   3b 31 37 35 2e 31 37 37 2e 31 36 36 2e 37 33 3b   ;175.177.166.73;
0040   31 3b 56 32 2d 56 32 30 30 30 3b 33 2e 36 2e 33   1;V2-V2000;3.6.3
0050   2e 31 30 31 3b 30 37 2f 32 37 2f 32 30 31 37 3b   .101;07/27/2017;
```

## Roku - External Control Protocol (ECP)
References:<br>
[https://developer.roku.com/en-ca/docs/developer-program/dev-tools/external-control-api.md](https://developer.roku.com/en-ca/docs/developer-program/dev-tools/external-control-api.md)<br>
```
echo "M-SEARCH * HTTP/1.1\nHost:239.255.255.250:1900\nMan: \"ssdp:discover\"\nST: roku:ecp" | netcat -u XXX.XXX.XXX.XXX 1900
```
```
0000   48 54 54 50 2f 31 2e 31 20 32 30 30 20 4f 4b 0d   HTTP/1.1 200 OK.
0010   0a 43 61 63 68 65 2d 43 6f 6e 74 72 6f 6c 3a 20   .Cache-Control: 
0020   6d 61 78 2d 61 67 65 3d 33 36 30 30 0d 0a 53 54   max-age=3600..ST
0030   3a 20 72 6f 6b 75 3a 65 63 70 0d 0a 55 53 4e 3a   : roku:ecp..USN:
0040   20 75 75 69 64 3a 72 6f 6b 75 3a 65 63 70 3a 58    uuid:roku:ecp:X
0050   30 31 36 30 30 43 48 56 47 44 33 0d 0a 45 78 74   01600CHVGD3..Ext
0060   3a 20 0d 0a 53 65 72 76 65 72 3a 20 52 6f 6b 75   : ..Server: Roku
0070   2f 31 34 2e 30 2e 34 20 55 50 6e 50 2f 31 2e 30   /14.0.4 UPnP/1.0
0080   20 52 6f 6b 75 2f 31 34 2e 30 2e 34 0d 0a 4c 4f    Roku/14.0.4..LO
0090   43 41 54 49 4f 4e 3a 20 68 74 74 70 3a 2f 2f 31   CATION: http://1
00a0   39 32 2e 31 36 38 2e 30 2e 34 3a 38 30 36 30 2f   92.168.0.4:8060/
00b0   0d 0a 64 65 76 69 63 65 2d 67 72 6f 75 70 2e 72   ..device-group.r
00c0   6f 6b 75 2e 63 6f 6d 3a 20 37 45 37 38 39 30 35   oku.com: 7E78905
00d0   38 30 35 31 39 31 32 44 32 42 34 44 31 0d 0a 0d   8051912D2B4D1...
00e0   0a                                                .
```

## Axis - VAPIX mDNS
References:<br>
[https://developer.axis.com/vapix/network-video/mdns-sd-api#discover](https://developer.axis.com/vapix/network-video/mdns-sd-api#discover)<br>
```
dig _axis-video._tcp.local ptr @XXX.XXX.XXX.XXX -p 5353
dig _axis-nvr._tcp.local ptr @XXX.XXX.XXX.XXX -p 5353
```
```
0000   84 d1 84 00 00 01 00 01 00 00 00 04 0b 5f 61 78   ............._ax
0010   69 73 2d 76 69 64 65 6f 04 5f 74 63 70 05 6c 6f   is-video._tcp.lo
0020   63 61 6c 00 00 0c 00 01 c0 0c 00 0c 00 01 00 00   cal.............
0030   00 0a 00 1c 19 41 58 49 53 20 32 34 31 51 41 20   .....AXIS 241QA 
0040   2d 20 30 30 34 30 38 43 37 33 46 45 36 45 c0 0c   - 00408C73FE6E..
0050   c0 34 00 21 00 01 00 00 00 0a 00 1a 00 00 00 00   .4.!............
0060   00 50 11 61 78 69 73 2d 30 30 34 30 38 63 37 33   .P.axis-00408c73
0070   66 65 36 65 c0 1d c0 34 00 10 00 01 00 00 00 0a   fe6e...4........
0080   00 18 17 6d 61 63 61 64 64 72 65 73 73 3d 30 30   ...macaddress=00
0090   34 30 38 43 37 33 46 45 36 45 c0 62 00 01 00 01   408C73FE6E.b....
00a0   00 00 00 0a 00 04 80 df 0a 0e c0 62 00 01 00 01   ...........b....
00b0   00 00 00 0a 00 04 a9 fe 6b a5                     ........k.
```