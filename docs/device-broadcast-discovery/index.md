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

## HID Global - VertX Controller UDP Discovery
References:<br>
[https://www.zerodayinitiative.com/advisories/ZDI-16-223/](https://www.zerodayinitiative.com/advisories/ZDI-16-223/)<br>
[https://github.com/coldfusion39/VertXploit/tree/master](https://github.com/coldfusion39/VertXploit/tree/master)
```
echo -n "discover;013;" | netcat -u XXX.XXX.XXX.XXX 4070
```
```
0000   64 69 73 63 6f 76 65 72 65 64 3b 30 39 36 3b XX   discovered;096;X
0010   XX 3a XX XX 3a XX XX 3a XX XX 3a XX XX 3a XX XX   X:XX:XX:XX:XX:XX
0020   3b 56 65 72 74 58 5f 45 56 4f 5f 56 32 30 30 30   ;VertX_EVO_V2000
0030   3b XX XX XX 2e XX XX XX 2e XX XX XX 2e XX XX 3b   ;XXX.XXX.XXX.XX;
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
0030   00 0a 00 1c 19 41 58 49 53 20 XX XX XX XX XX 20   .....AXIS XXXXX 
0040   2d 20 30 30 XX XX XX XX XX XX XX XX XX XX c0 0c   - 00XXXXXXXXXX..
0050   c0 34 00 21 00 01 00 00 00 0a 00 1a 00 00 00 00   .4.!............
0060   00 50 11 61 78 69 73 2d 30 30 34 30 38 63 37 33   .P.axis-00408c73
0070   66 65 36 65 c0 1d c0 34 00 10 00 01 00 00 00 0a   fe6e...4........
0080   00 18 17 6d 61 63 61 64 64 72 65 73 73 3d XX XX   ...macaddress=XX
0090   XX XX XX XX XX XX XX XX XX XX c0 62 00 01 00 01   XXXXXXXXXX.b....
00a0   00 00 00 0a 00 04 80 df 0a 0e c0 62 00 01 00 01   ...........b....
00b0   00 00 00 0a 00 04 a9 fe 6b a5                     ........k.
```

## Vivotek - UDP port 10000
References:<br>
[https://www.vivotek.com/products/software/shepherd](https://www.vivotek.com/products/software/shepherd)<br>
[https://github.com/julienblitte/UniversalScanner/blob/master/UniversalScanner/Vivotek.cs](https://github.com/julienblitte/UniversalScanner/blob/master/UniversalScanner/Vivotek.cs)<br>
*The hex value "ABCDEF" seems to be session identifier, thus value can vary
```
echo -n "01ABCDEF03" | xxd -r -p | netcat -u -p 5678 XXX.XXX.XXX.XXX 10000
```
```
0000   02 f5 dd 76 03 01 11 49 42 39 33 36 30 2d 56 56   ...v...IB9360-VV
0010   54 4b 2d 30 32 32 33 62 02 06 00 02 d1 97 64 70   TK-0223b......dp
0020   03 04 a9 fe 08 2a 04 24 06 02 3d 22 16 02 bb 01   .....*.$..="....
0030   08 02 65 6e 09 08 49 42 39 33 36 30 2d 48 10 04   ..en..IB9360-H..
0040   03 00 82 00 0a 01 00 17 03 01 01 81 05 04 00 00   ................
0050   00 00                                             ..
```

## Vstarcam - UDP port 8600
References:<br>
[https://github.com/julienblitte/UniversalScanner/blob/master/UniversalScanner/Vstarcam.cs](https://github.com/julienblitte/UniversalScanner/blob/master/UniversalScanner/Vstarcam.cs)<br>
[Eye4 for Windows](https://www.vstarcam.com/software-download)<br>
```
echo -n "44480101" | xxd -r -p | netcat -u -p 8601 XXX.XXX.XXX.XXX 8600
```
```
0000   44 48 01 08 31 39 32 2e 31 36 38 2e 31 2e 35 31   DH..192.168.1.51
0010   00 00 00 00 32 35 35 2e 32 35 35 2e 32 35 35 2e   ....255.255.255.
0020   30 00 00 00 31 39 32 2e 31 36 38 2e 31 2e 31 00   0...192.168.1.1.
0030   00 00 00 00 38 2e 38 2e 38 2e 38 00 00 00 00 00   ....8.8.8.8.....
0040   00 00 00 00 31 39 32 2e 31 36 38 2e 31 2e 31 00   ....192.168.1.1.
0050   00 00 00 00 48 02 2d 01 5c e9 55 00 56 53 54 41   ....H.-.\.U.VSTA
0060   XX XX XX XX XX XX XX XX XX 58 58 00 00 00 00 00   XXXXXXXXXXX.....
0070   00 00 00 00 00 00 00 00 00 00 00 00 49 50 43 41   ............IPCA
0080   4d 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   M...............
0090   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
00a0   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
00b0   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
00c0   00 00 00 00 00 00 00 00 00 00 00 00 XX XX 2e XX   ............XX.X
00d0   XX 2e XX XX 2e XX XX 00 00 00 00 00 00 00 00 00   X.XX.XX.........
00e0   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
00f0   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
0100   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
0110   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
0120   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
0130   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
0140   00 00 00 00 75 73 65 72 32 2e 67 6f 63 61 6d 2e   ....user2.gocam.
0150   73 6f 00 00 00 00 00 00 00 00 00 00 00 00 00 00   so..............
0160   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
0170   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
0180   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
0190   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
01a0   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
01b0   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
01c0   00 00 00 00 66 6a 65 64 72 00 00 00 00 00 00 00   ....fjedr.......
01d0   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
01e0   00 00 00 00 38 31 39 38 33 39 00 00 00 00 00 00   ....819839......
01f0   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
0200   00 00 00 00 44 48 01 08 31 39 32 2e               ....DH..192.
```

## Dahua - UDP DHCPDiscover port 37810
References:<br>
[https://www.shadowserver.org/what-we-do/network-reporting/open-dvr-dhcpdiscover-report/](https://www.shadowserver.org/what-we-do/network-reporting/open-dvr-dhcpdiscover-report/)<br>
```
echo -ne '\xff'|nc -u 218.5.136.140 37810
```
```
0000   20 00 00 00 44 48 49 50 00 00 00 00 00 00 00 00    ...DHIP........
0010   b4 02 00 00 00 00 00 00 b4 02 00 00 00 00 00 00   ................
0020   7b 22 6d 61 63 22 3a 22 XX XX 3a XX XX 3a XX XX   {"mac":"XX:XX:XX
0030   3a XX XX 3a XX XX 3a XX XX 22 2c 22 6d 65 74 68   :XX:XX:XX","meth
0040   6f 64 22 3a 22 63 6c 69 65 6e 74 2e 6e 6f 74 69   od":"client.noti
0050   66 79 44 65 76 49 6e 66 6f 22 2c 22 70 61 72 61   fyDevInfo","para
0060   6d 73 22 3a 7b 22 64 65 76 69 63 65 49 6e 66 6f   ms":{"deviceInfo
0070   22 3a 7b 22 41 6c 61 72 6d 49 6e 70 75 74 43 68   ":{"AlarmInputCh
0080   61 6e 6e 65 6c 73 22 3a 38 2c 22 41 6c 61 72 6d   annels":8,"Alarm
0090   4f 75 74 70 75 74 43 68 61 6e 6e 65 6c 73 22 3a   OutputChannels":
00a0   30 2c 22 44 65 76 69 63 65 43 6c 61 73 73 22 3a   0,"DeviceClass":
00b0   22 56 54 4f 22 2c 22 44 65 76 69 63 65 54 79 70   "VTO","DeviceTyp
00c0   65 22 3a 22 56 54 4f 32 30 30 30 41 2d 32 22 2c   e":"VTO2000A-2",
00d0   22 46 69 6e 64 22 3a 22 42 43 22 2c 22 48 74 74   "Find":"BC","Htt
00e0   70 50 6f 72 74 22 3a 38 30 2c 22 49 50 76 34 41   pPort":80,"IPv4A
00f0   64 64 72 65 73 73 22 3a 7b 22 44 65 66 61 75 6c   ddress":{"Defaul
0100   74 47 61 74 65 77 61 79 22 3a 22 31 39 32 2e 31   tGateway":"192.1
0110   36 38 2e 31 2e 31 22 2c 22 44 68 63 70 45 6e 61   68.1.1","DhcpEna
0120   62 6c 65 22 3a 66 61 6c 73 65 2c 22 49 50 41 64   ble":false,"IPAd
0130   64 72 65 73 73 22 3a 22 31 39 32 2e 31 36 38 2e   dress":"192.168.
0140   31 2e 32 30 32 22 2c 22 53 75 62 6e 65 74 4d 61   1.202","SubnetMa
0150   73 6b 22 3a 22 32 35 35 2e 32 35 35 2e 32 35 35   sk":"255.255.255
0160   2e 30 22 7d 2c 22 49 50 76 36 41 64 64 72 65 73   .0"},"IPv6Addres
0170   73 22 3a 7b 22 44 65 66 61 75 6c 74 47 61 74 65   s":{"DefaultGate
0180   77 61 79 22 3a 6e 75 6c 6c 2c 22 44 68 63 70 45   way":null,"DhcpE
0190   6e 61 62 6c 65 22 3a 66 61 6c 73 65 2c 22 49 50   nable":false,"IP
01a0   41 64 64 72 65 73 73 22 3a 22 5c 2f 30 22 2c 22   Address":"\/0","
01b0   4c 69 6e 6b 4c 6f 63 61 6c 41 64 64 72 65 73 73   LinkLocalAddress
01c0   22 3a 22 XX XX XX XX 3a 3a XX XX XX XX 3a XX XX   ":"XXXX::XXXX:XX
01d0   XX XX 3a XX XX XX XX 3a 34 66 65 35 5c 2f 36 34   XX:XXXX:4fe5\/64
01e0   22 7d 2c 22 49 6e 69 74 22 3a 33 32 32 32 2c 22   "},"Init":3222,"
01f0   4d 61 63 68 69 6e 65 4e 61 6d 65 22 3a 22 35 46   MachineName":"5F
0200   30 34 36 39 30 50 41 5a 46 30 39 33 34 22 2c 22   04690PAZF0934","
0210   4d 61 6e 75 66 61 63 74 75 72 65 72 22 3a 22 47   Manufacturer":"G
0220   65 6e 65 72 61 6c 22 2c 22 50 6f 72 74 22 3a 33   eneral","Port":3
0230   37 37 37 37 2c 22 52 65 6d 6f 74 65 56 69 64 65   7777,"RemoteVide
0240   6f 49 6e 70 75 74 43 68 61 6e 6e 65 6c 73 22 3a   oInputChannels":
0250   30 2c 22 53 65 72 69 61 6c 4e 6f 22 3a 22 XX XX   0,"SerialNo":"5F
0260   XX XX XX XX XX XX XX XX XX XX XX XX XX 22 2c 22   XXXXXXXXXXXXX","
0270   56 65 6e 64 6f 72 22 3a 22 47 65 6e 65 72 61 6c   Vendor":"General
0280   22 2c 22 56 65 72 73 69 6f 6e 22 3a 22 34 2e 33   ","Version":"4.3
0290   30 30 2e 30 30 30 30 30 30 30 2e 31 2e 52 22 2c   00.0000000.1.R",
02a0   22 56 69 64 65 6f 49 6e 70 75 74 43 68 61 6e 6e   "VideoInputChann
02b0   65 6c 73 22 3a 31 2c 22 56 69 64 65 6f 4f 75 74   els":1,"VideoOut
02c0   70 75 74 43 68 61 6e 6e 65 6c 73 22 3a 31 36 7d   putChannels":16}
02d0   7d 7d 0a 00                                       }}..
```

## Advantech - UDP discovery port 5048
```
echo -n "4D41444100000083010050(print "%0*d 84)20000000000000" | xxd -r -p | netcat -u XXX.XXX.XXX.XXX 5048
```
```
0000   4d 41 44 41 00 00 00 83 01 00 60 60 00 00 d0 c9   MADA......``....
0010   00 f8 81 13 0f 0f 0f 0f 0f 0f 0f 0f 00 00 00 00   ................
0020   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
0030   00 00 00 00 80 20 00 48 00 00 00 00 00 07 00 1e   ..... .H........
0040   00 1f 00 07 00 01 00 e8 00 08 00 00 00 00 00 00   ................
0050   00 01 0d 53 00 03 84 00 00 00 00 32 00 01 c2 00   ...S.......2....
0060   31 30 32 30 00 00 00 18 41 44 41 4d 36 30 36 30   1020....ADAM6060
0070   20 44 69 67 69 74 61 6c 20 49 2f 4f 20 4d 6f 64    Digital I/O Mod
0080   75 6c 65 00 00                                    ule..
```