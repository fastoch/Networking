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

**Example 1**: 10.1.1.0/24  
Split this into smaller subnets, each subnet needs to support 14 machines. 

14 hosts = we only need 4 host bits for the host portion = a subnet mask of /28
- Our first subnet will be 10.1.1.0/28
- Our second subnet will be 10.1.1.16/28
- Our third subnet will be 10.1.1.32/28
- ...
- Last subnet will be 10.1.1.240/28
  
We've created 16 subnets that can each contain 14 hosts.
The 2 remaining addresses in each subnet will be for the subnet ID and for the broadcast.

**Example 2**: 10.128.192.0/18  
Create 30 subnets with as many hosts as possible.


---
EOF
