192.168.1.18/24
- subnet = 192.168.1.0
- first host = 192.168.1.1
- last host = 192.168.1.254
- broadcast = 192.168.1.255

---

172.16.35.123/20
- subnet = 172.16.32.0
- first host = 172.16.32.1
- last host = 172.16.47.254
- broadcast = 172.16.47.255

---

172.16.129.1/17
- subnet = 172.16.128.0
- first host = 172.16.128.1
- last host = 172.16.255.254
- broadcast = 172.16.255.255

---

**How to divide a network when given:**
- a specific number of hosts
- a specific number of subnets

Number of hosts = 2 to the power of n minus 2, where n is the number of host bits (zeros) in the subnet mask  
Number of subnets = 2 to the power of n, where n is the number of network bits (ones) in the subnet mask  

We subtract 2 to calculate the number of hosts because we must allocate 1 address for the subnet and 1 for the broadcast.  

**Example**: 10.1.1.0/24
Split this into smaller subnets, each subnet needs to support 14 machines.  
14 hosts = 2 to the power of 4 minus 2, so we only need 4 host bits 
- Our first subnet will be 10.1.1.0/28
- Our second subnet will be 10.1.1.16/28
- Our third subnet will be 10.1.1.32/28
- ...
- Last subnet will be 10.1.1.240/28



---
EOF
