---
title: Roku 
layout: default
---

</br>
To query for a Roku device IP address, send the following HTTP request to 239.255.255.250 port 1900:

M-SEARCH * HTTP/1.1
Host: 239.255.255.250:1900
Man: "ssdp:discover"
ST: roku:ecp

$ ncat -u 239.255.255.250 1900 < roku_ecp_req.txt