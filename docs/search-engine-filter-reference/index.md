# Search Engine Filter Reference (Censys/Shodan)

## Filter List:
* [positive/negative match](#positive-and-negative-match)
* [SNMP](#snmp)
* [CPE based search](#cpe-based-search)
* [HTTPS/TLS](#httpstls)
* [port/service based filter](#portservice-based-filter)

***
### positive and negative match
```python
# Shodan - positive match for "Cisco", negative match for "Dell"
"Cisco" -"Dell"

# Censys - positive match for "Dell", negative match for "Cisco"
"Dell" and not "Cisco"
```

***
### CPE based search
```python
# cpe verison can be either 2.3 or 2.2. Although 2.3 is more common.
# The third field value "a", "h" and "o" stand for "application", 
# "hardware" and "os" respectively 

# Censys - exact/partial CPE match
services.software.uniform_resource_identifier="cpe:2.3:o:digi:connect_me4_9210:82001607_m:\*:\*:\*:\*:\*:\*:\*"
services.software.uniform_resource_identifier:"cpe:2.3:o:digi"
``` 

***
### SNMP
```python
# Shodan - SNMP OID, example shows results with SNMP OID "Objectid: 
# 1.3.6.1.4.1.674.10892.5". In this case, simply use MIB brower to 
# walk the subtree "1.3.6.1.4.1.674.10892". The information is more 
# usefull along with MIB file used by the server device.

"Objectid: 1.3.6.1.4.1.674.10892.5"

# Censys SNMP sysDescr -Search patterns within "sysDescr" node. The 
# relavent MIB file is SNMPv2-MIB. This is the default MIB file for 
# browsing.
# exact/partial match
services.snmp.oid_system.desc="Digi Connect ME4 9210 Version 82001607_M 08/30/2013"
services.snmp.oid_system.desc:"Digi Connect"
```

***
### HTTPS/TLS
```python
# Censys - match patterns within organization name or common name of TLS 
# certificate. Unless the pattern is fairly unique, it is recommended to 
# match both to avoid FP.
# issuer.organization, subject.organization and issuer.common_name
services.tls.certificates.leaf_data.issuer.organization="Cisco"
services.tls.certificates.leaf_data.subject.organization:"Cisco"
services.tls.certificates.leaf_data.issuer.common_name:"USG"
```

***
### port/service based filter
```python
# Censys
services.port=`80`
services.service_name=`HTTP`

# Shodan
http port:80,8080
```
