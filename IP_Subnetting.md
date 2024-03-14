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

# Subnetting Lab 1

You've been allocated subnet 192.168.1.0/24.  
Subnet this into 4 subnets as follows:
- Subnet 1 for site 1
- Subnet 2 for the link between R1 and the Internet Router
- Subnet 3 for site 2
- Subnet 4 for the link between R2 and the Internet Router

**Solution**:  
4 subnets means borrowing 2 bits to the network portion.  
Our mask will be 24 + 2 = /26
- subnet 1 = 192.168.1.0/26 (site 1)
- subnet 2 = 192.168.1.64/26
- subnet 3 = 192.168.1.128/26 (site 2)
- subnet 4 = 192.168.1.192/26

## Configuring the routers

IP address for Router1, int Gi 0/0/0 = 192.168.1.62/26 (link between router1 and switch1).
```
en
sh ip int brief
conf t
int g0/0/0
no shut
ip address 192.168.1.62 255.255.255.192
end
sh ip int brief
wr
```

IP address for Router1, int Serial 0/1/0 = 192.168.1.126/26  
Serial port is used to connect Router1 to the Internet router.
```
en
conf t

```

IP address for R2 = 192.168.1.190/26  
```
en
sh ip int brief
conf t
int g0/0/0
no shut
ip address 192.168.1.190 255.255.255.192
end
sh ip int brief
wr
```

## Configuring the switches 

IP address for switch 1 = 192.168.1.61/26  
```
en
sh ip int brief
conf t
host S1
ip default-gateway 192.168.1.62
int vlan1
no shut
ip address 192.168.1.61 255.255.255.192
end
sh ip int brief
ping 192.168.1.62
wr
```

IP address for switch 2 = 192.168.1.189/26  
```
en
sh ip int brief
conf t
host S1
ip default-gateway 192.168.1.190
int vlan1
no shut
ip address 192.168.1.189 255.255.255.192
end
sh ip int brief
ping 192.168.1.190
wr
```
## Configuring the DHCP servers

IP address for DHCP server 1 = 192.168.1.60/26 with gateway 192.168.1.62  
On the DHCP server, we need to configure a **DHCP pool**.  
- start IP address = 192.168.1.1/26
- maximum number of users = 50
- Default gateway is router 1, so 192.168.1.62

IP address for DHCP server 2 = 192.168.1.188/26 with gateway 192.168.1.190



---
EOF
