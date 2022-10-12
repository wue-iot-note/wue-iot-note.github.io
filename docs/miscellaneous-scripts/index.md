# Miscellaneous Scripts

* [product list by vendor name from NVD feed JSON (Linux)](#product-list-by-vendor-name-from-nvd-feed-json-linux)
* [curl request ignore certificate](#curl-request-ingore-certificate)
* [python simple web hosting (Linux)](#python-simple-web-hosting-linux)
* [kill all process by name](#kill-all-process-by-name-linux)

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
