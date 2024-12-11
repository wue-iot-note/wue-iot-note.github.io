---
title: DNS SD
parent: Protocol Analysis
nav_order: 2
---

# DNS-Based Service Discovery
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Overview
DNS Service Discovery aka DNS-SD requests can also be sent using mDNS to yield zero-configuration DNS-SD. This uses DNS PTR, SRV, TXT records to advertise instances of service types, domain names for those instances, and optional configuration parameters for connecting to those instances. But SRV records can now resolve to .local domain names, which mDNS can resolve to local IP addresses.<br>

Service instance can be described using a <b>DNS</b> SRV [RFC 2782] and <b>DNS TXT</b> [RFC 1035] record. The SRV record has a name of the form "<Instance>.<Service>.<Domain>" and gives the target host and port where the service instance can be reached. The DNS TXT record of the same name gives additional information about this instance, in a structured form using key/value pairs.<br>

## SRV Record
A SRV record has the form
```
_service._proto.name. ttl IN SRV priority weight port target.
```
- service: the symbolic name of the desired service.
- proto: the transport protocol of the desired service; this is usually either TCP or UDP.
- name: the domain name for which this record is valid, ending in a dot.
- ttl: standard DNS time to live field.
- IN: standard DNS class field (this is always IN).
- SRV: Type of Record (this is always SRV).
- priority: the priority of the target host, lower value means more preferred.
- weight: A relative weight for records with the same priority, higher value means higher chance of getting picked.
- port: the TCP or UDP port on which the service is to be found.
- target: the canonical hostname of the machine providing the service, ending in a dot.
- An example SRV record in textual form that might be found in a zone file might be the following:

```
_sip._tcp.example.com. 86400 IN SRV 0 5 5060 sipserver.example.com.
```

This points to a server named sipserver.example.com listening on TCP port 5060 for Session Initiation Protocol (SIP) protocol services. The priority given here is 0, and the weight is 5.<br>

A client can discover list of available instances of a given service type using a query for a DNS PTR [RFC 1035] record with a name of the form "<Service>.<Domain>", which returns a set of zero or more names. The example below uses linux "dig" command to do so.<br>
References: [https://www.rfc-editor.org/rfc/rfc6763.html#section-7.2](https://www.rfc-editor.org/rfc/rfc6763.html#section-7.2)

```
dig _axis-video._tcp.local PTR @10.0.0.1 -p 5353 # SRV Record
dig _axis-video._tcp.local TXT @10.0.0.1 -p 5353 # TXT Record
```

```
dig _services._dns-sd._udp.local PTR @10.0.0.1 -p 5353 
```

```
──(root㉿kali)-[/home/kali/Desktop]
└─# dig _services._dns-sd._udp.local PTR @123.114.33.36 -p 5353 

; <<>> DiG 9.18.0-2-Debian <<>> _services._dns-sd._udp.local PTR @123.114.33.36 -p 5353
;; global options: +cmd
;; Got answer:
;; WARNING: .local is reserved for Multicast DNS
;; You are currently testing what happens when an mDNS query is leaked to DNS
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 37526
;; flags: qr aa; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;_services._dns-sd._udp.local.  IN      PTR

;; ANSWER SECTION:
_services._dns-sd._udp.local. 10 IN     PTR     _workstation._tcp.local.
_services._dns-sd._udp.local. 10 IN     PTR     _http._tcp.local.
_services._dns-sd._udp.local. 10 IN     PTR     _device-info._tcp.local.
_services._dns-sd._udp.local. 10 IN     PTR     _ASUSTOR_ADM._tcp.local.

;; Query time: 243 msec
;; SERVER: 123.114.33.36#5353(123.114.33.36) (UDP)
;; WHEN: Wed Dec 11 18:38:32 EST 2024
;; MSG SIZE  rcvd: 152



──(root㉿kali)-[/home/kali/Desktop]
└─# dig _ASUSTOR_ADM._tcp.local PTR @123.114.33.36 -p 5353

; <<>> DiG 9.18.0-2-Debian <<>> _ASUSTOR_ADM._tcp.local PTR @123.114.33.36 -p 5353
;; global options: +cmd
;; Got answer:
;; WARNING: .local is reserved for Multicast DNS
;; You are currently testing what happens when an mDNS query is leaked to DNS
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 47741
;; flags: qr aa; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;_ASUSTOR_ADM._tcp.local.       IN      PTR

;; ANSWER SECTION:
_ASUSTOR_ADM._tcp.local. 10     IN      PTR     Fileservers._ASUSTOR_ADM._tcp.local.
Fileservers._ASUSTOR_ADM._tcp.local. 10 IN TXT  "httpport=3000" "httpenabled=No" "httpsport=3001" "httpsenabled=Yes" "model=AS6404T" "version=3.2.1.RKU4" "hostid=10-BF-48-8C-69-E6" "serialnumber=AL18036404TM0052" "wol=Yes" "canSuspend=Yes" "netif=[\010  {\010    \"name\":\"LAN1\",\010    \"mac\":\"10:bf:48:8c:69:e6\"\010  },\010  {\010    \"name\":\"LAN2\",\010    \"mac\":\"10:bf:48:8c:69:e7\"\010  }\010]"
Fileservers._ASUSTOR_ADM._tcp.local. 10 IN SRV  0 0 3001 Fileservers.local.
Fileservers.local.      10      IN      A       192.168.1.243

;; Query time: 211 msec
;; SERVER: 123.114.33.36#5353(123.114.33.36) (UDP)
;; WHEN: Wed Dec 11 18:44:35 EST 2024
;; MSG SIZE  rcvd: 424

```

## IoT device SRV record ptr
```
_device-info._tcp.local  # General device info
_axis-video._tcp.local   # Axis Camera
_qdiscover._tcp.local    # QNAP Camera
_qsan-storage._tcp.local # QSAN NAS
```

## References
[https://www.rfc-editor.org/rfc/rfc6763.html](https://www.rfc-editor.org/rfc/rfc6763.html)