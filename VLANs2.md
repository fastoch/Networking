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

### The Native VLAN

802.1Q trunks have a special vlan called the "native vlan".  
When a port on a switch is set up as a trunk, that port can transmit and receive tagged frames.  
However, frames that belong to the native vlan do not carry vlan tags when sent over a trunk link.  
For this reason, management traffic will go across the native vlan.  

For instance, STP BPDUs will use the native vlan, and so will DTP (dynamic trunking protocol).  
DTP is a way that switches negociate to set up a trunk between themselves automatically.

>[!note]
>STP BPDU is a spanning tree protocol (STP) message unit that describes the attributes of a switch port such as its MAC address, priority and cost to reach. BPDUs enable switches that participate in a spanning tree protocol to gather information about each other.

If you have left VLAN1 as the native vlan, traffic like CDP, VTP, PAgP and UDLD will be transmitted across the native vlan, untagged.  
If you have changed the native vlan to something other than VLAN1, these protocols will be tagged in that specific vlan.  

- CDP = Cisco Discovery Protocol
- VTP = VLAN Trunking Protocol
- PAgP = Port Aggregation Protocol
- UDLD = Uni-Directional Link Detection

>[!important]
>The important thing to take note of here is that on trunk links there's a special vlan known as the native vlan, where traffic is sent untagged if left at the default of vlan1. A lot of management traffic will be sent across that native vlan. 

It's important that the native vlan on both sides of the trunk be the same. If they're not set the same, the switches will notify you by telling you that there's a native vlan mismatch. The issue that arises if the native VLANs are not the same is that traffic from one vlan on a given switch will automatically be associated and end up in a different vlan on another switch.

### A typical scenario

A PC is connected to an IP phone that is in turn connected to a switch.  
An IP phone has a built-in 3-way switch:
- one port is connected back to the network infrastructure 
- a second port allows the PC to connect to the infrastructure through the phone
- a third port allows for voice traffic from the handset to be prioritized over data when sent to the network infrastructure

The IP phone can be configured in a separate vlan to the PC.  
This way, the PC will not be able to sniff voice traffic.  

Some very powerful hacking tools allow you to sniff the network and capture the voice traffic.  
But if the phone is in a separate vlan, **security is enhanced** because the PC is not able to see the voice traffic.  

From a QoS point of view, this is also a lot better to put the phone in a separate vlan.  
Because it makes it easier to prioritize the voice traffic over the data traffic.  

Setting up the network this way also has the advantage of easier IP address management, because you can assign a different subnet to your phones versus your PCs and thus scale your IP addressing.  

What happens is the switch is configured with what's called a voice VLAN and a native VLAN.  


@8min


---
EOF
