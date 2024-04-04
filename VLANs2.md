Source = David Bombal - Cisco CCNA 200-301 - Udemy

---

## What is a VLAN?

A virtual LAN is a single broadcast domain. It's also a virtual subnet or **logical** network.  
You could say it's a group of hosts with a common set of requirements attached to the same broadcast domain, regardless 
of where they are physically located. You are able to group multiple devices together **logically** rather than physically.  

It is possible to span a subnet (or VLAN) across multiple switches, even though that's not recommended today.  

---

## Why using VLANs?

Some of the **advantages** of VLANs include:
- **segmentation**: separate users based on function (sales, accountancy, ...)
- **flexibility**: without changing physical cabling, you can move a user from one vlan to another
- **security**: users are in separate vlans, and therefore have to traverse a layer 3 device to get from one vlan to another

>[!note]
>On the router, you could implement **ACLs** to control which users have access to various vlans

These days, VLANs also have other advantages, specifically when implementing **VoIP**.  
You can put your IP phones into a separate VLAN to your workstations', and therefore provide a better **QoS** to the IP phones.  

Implementing VLANs has many advantages in modern networks.

---

## Logical vs. Physical Topology

Something that often confuses people is the difference between a physical topology and a logical topology.  
When using VLANs, you need to change your paradigm and no longer think about the physical topology of the network,  
but rather envision what the logical topology looks like.  

We can put interfaces of a single switch into different VLANs.  
By default, all ports belong to VLAN1 on Cisco switches. But, by using a single command, you can move a port to another vlan.  

---

## Trunking

Trunking allows multiple VLANs to traverse a single physical link between 2 switches.  
When machines are in the same VLAN but are not connected to the same switch, trunking allows them to communicate.  

The 2 trunking protocols are:
- 802.1Q: the industry standard, most used
- ISL: inter-switch link, Cisco proprietary, rarely used

A 802.1Q frame is different to a standard Ethernet frame. It has a TAG field that contains the **VLAN id**.  
In theory, 4096 VLANs can be configured on a 802.1Q switch, since the VLAN id size is 12 bits.  



---

## 



---
EOF
