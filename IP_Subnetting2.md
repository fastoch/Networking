# Subnetting - Packet Tracer - Lab 2

In a previous lab, 192.168.1.0/24 was broken up to support 4 subnets.  
Now you need to subnet the network to extend and conserve IP addresses.  
1. Break up subnet 2, which is 192.168.1.64/26, to support as many subnets as possible with 8 hosts per subnet
2. Allocate the first new subnet to site 3 (new site)
3. Manually configure all devices in this new subnet as follows:
* Router with last IP address in the subnet
* Switch with the 2nd last IP address
* Hosts from 1st IP address
4. Subnet the last new subnet you got from 192.168.1.64/26 with /30 masks
5. Then allocate the /30 subnets to the serial links (the links between the 3 routers and the Internet router)
6. Configure the routers appropriately

---

## Solution

Already existing subnets are:
- 192.168.1.0/26
- 192.168.1.64/26
- 192.168.1.128/26
- 192.168.1.192/26

We must break up the second subnet.  
8 hosts per subnet means using 4 bits for the host portion.  
3 bits is not enough for our subnet to contain 8 hosts (2³ - 2 = 6 hosts).  
So we'll have a /28 subnet mask in each new subnet. 

192.168.1.64/26 will be broken up as follows:
- 192.168.1.64/28
- 192.168.1.80/28
- 192.168.1.96/28
- 192.168.1.112/28

Site 3 will be allocated subnet 192.168.1.80/28  
Router 3 IP address on int Gi0/0/0 will be 192.168.1.94/28  
Switch 3 IP address on int Gi1/0/1 will be 192.168.1.93/28  
Hosts IP adresses will go from 192.168.1.81/28 to 192.168.1.88/28  

Now we must subnet the last new subnet, which is 192.168.112/28, into /30 subnets:
- 192.168.1.112/30
- 192.168.1.116/30
- 192.168.1.120/30
- 192.168.1.124/30
  
We'll allocate the first new subnet to the interface s0/1/0 on router 1 (serial link between router 1 and the Internet router).  
The second new subnet will be allocated to s0/1/0 on router 2 (serial link between router 2 and the Internet router).  
The third new subnet will be allocated to s0/1/0 on router 3 (serial link between router 3 and the Internet router). 

---
EOF