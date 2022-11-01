# TCP Stream Reconstruct
* [tcp_stream_create.py](#tcp_rewrite_pcappy)
* [tcp_rewrite_pcap.py](#tcp_rewrite_pcappy)
* [config.py](#configpy)

## tcp_stream_create.py
```python
import logging
import time
import threading
from threading import Thread
import socket
from config import conversation, pcap_config

class TrafficStreamSim:
    def __init__(self):
        self.value = 0
        self._lock = threading.Lock()
        self.client_socket = 0
        self.server_socket = 0
        self.connections = [0] * 1

    def socket_setup(self):
        #create a socket object for clinet
        self.client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self.client_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)

        self.server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self.server_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        server_ip = "127.0.0.1"
        server_port = pcap_config["server"]["port"]
        #Bind socket to port
        self.server_socket.bind((server_ip, server_port))

    def handler(self): 
        self.connections[0] = self.server_socket.accept()[0]

    def begin_conversation(self):
        self.server_socket.listen(5)
        server_thread = threading.Thread(target=self.handler)
        server_thread.start()
        self.client_socket.connect(("127.0.0.1", pcap_config["server"]["port"]))
        while(self.connections[0] == 0): time.sleep(1)
        for i in conversation:
            payload = bytes.fromhex(i["payload"])
            if i["src"] == "client":
                self.client_socket.send(payload)
            if i["src"] == "server":
                self.connections[0].send(payload)

if __name__ == "__main__":
    simulator = TrafficStreamSim()
    simulator.socket_setup()
    simulator.begin_conversation()

```
## tcp_rewrite_pcap.py
```python
from scapy.all import *
import logging
import sys
logging.getLogger("scapy.runtime").setLevel(logging.ERROR)

# Add some colouring for printing packets later
YELLOW = '\033[93m'
GREEN = '\033[92m'
END = '\033[0m'
RED = '\033[91m'

if len(sys.argv) != 6:
    print('Usage is ./tcp_stream_rewrite.py <input pcap file> <client ip> <server ip> <server port> <output pcap file>')
    print('Example - ./tcp_stream_rewrite.py 10.0.0.1 10.0.0.2 sample.pcap 8000 /tmp/out.pcap')
    sys.exit(1)

pcap = sys.argv[1]
client_ip = sys.argv[2]
server_ip = sys.argv[3]
server_port = int(sys.argv[4])
outfile = sys.argv[5]

pkts = rdpcap(pcap)

print(GREEN + '[+] Rewrite begin...' + END)

# Delete the IP and TCP checksums so that they are recreated when we change the IP addresses
print(YELLOW + '[-] Deleting old checksums so that scapy will regenerate them correctly' + END)
for p in pkts:
    del p[IP].chksum
    del p[TCP].chksum

# Rewrite the packets with the new addresses
print(YELLOW + '[-] Rewriting source and destination IP addresses' + END)
for p in pkts:
    if p.haslayer(TCP):
        if p[TCP].dport == server_port:
            p[IP].src = client_ip
            p[IP].dst = server_ip
        if p[TCP].sport == server_port:
            p[IP].src = server_ip
            p[IP].dst = client_ip
# Write the packets out to a new file
print(GREEN + '[!] Writing out pkts to new file ' + outfile + END)
wrpcap(outfile, pkts)

print(GREEN + '[!] All done!!!' + END)
```
## config.py
```python
# payload is hex byte. 00AABBCC...
conversation = [
    {"src": "client", "payload": ""},
    {"src": "server", "payload": ""},
    {"src": "server", "payload": ""},
    {"src": "client", "payload": ""},
    {"src": "server", "payload": ""}
]

pcap_config = {
    "server": {
        "port": 23,
        "mac": 0
    },
    "client" : {
        "port": 0,
        "mac": 0
    }
}

```