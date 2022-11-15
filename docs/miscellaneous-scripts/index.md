# Miscellaneous Scripts

### Product list by vendor name from NVD feed JSON (Linux)
```bash
# Replace XXX with vendor name. Negative grep for pattern "firmware" to exlcude name with syntax firmware. Product name list save to file "product_list.txt"
cat nvdcpematch-1.0.json | grep ":XXX:" | awk -F':' '{print $6}' | sort -u | grep -v "firm" > product_list.txt
```

### Curl request ingore certificate
```bash
curlk -k http://example.com
```

### Python simple web hosting (linux)
```bash
python3 -m http.server
```

### Kill all process by name (Linux)
```bash
kill -9 `pgrep firefox`
```

### Remote tcpdump
```bash
# stop caputre after 1 gigbyte
ssh root@10.0.0.1 tcpdump -i any -U -s0 -w - 'not port 22' | wireshark -a filesize:1000000 -k -i -
```

### Python install
```bash
python -m pip install [module_name]
```

### Replace obfuscated variable name in file
```python
# examples regex: 
# $FLERQQJBMH = Number(" 1 ") -> 1 = Number(" 1 ")

import re
import sys

#input file
fin = open(sys.argv[1], "rt")
#output file to write the result to
fout = open(sys.argv[1] + ".deobfuscate", "wt")
#for each line in the input file
for line in fin:
    #read replace the string and write to output file
    for match in re.finditer(r"(\$FL[0-9A-Z]{8})\s\=\sNumber\s\(\s\"\s([0-9]+)\s\"\s\)", line):
        line = line.replace(match.groups()[0], match.groups()[1])
    fout.write(line)
#close input and output files
fin.close()
fout.close()
```
