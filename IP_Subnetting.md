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

14 hosts means that we only need 4 bits for the host portion, since 2 to the power of 4 = 16  
The 2 remaining addresses in each subnet will be for the subnet id and for the broadcast.

Our subnet mask will be: 32 - 4 = /28  
- Our first subnet will be 10.1.1.0/28
- Our second subnet will be 10.1.1.16/28
- Our third subnet will be 10.1.1.32/28
- ...
- Last subnet will be 10.1.1.240/28
  
We've created 16 subnets that can each contain 14 hosts.  

**Example 2**: 10.128.192.0/18  
Create 30 subnets with as many hosts as possible.  

30 subnets means that we need 5 bits for the network portion, since 2 to the power of 5 = 32  

Our subnet mask will be: 18 + 5 = /23
- first subnet will be 10.128.192.0/23
- second subnet will be 10.128.194.0/23
- third subnet will be 10.128.196.0/23
- ...
- last subnet will be 10.128.254.0/23

We've created 32 subnets that can each contain 510 hosts.

---
EOF
