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

## Voice VLAN on a Cisco switch

A typical scenario is having a PC connected to an IP phone that is in turn connected to a switch.  

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

What happens is the switch is configured with what's called a **voice VLAN** and a native VLAN.  
The Voice VLAN is tagged, so tagged frames get sent to the phone, and the phone, with its built-in 3-way switch, is able to read the 802.1Q frames.  
Untagged frames are sent on what's called the "native VLAN" or "data VLAN". That information is sent to the phone, and the phone just switches that to the PC.   

So, the PC receives the untagged or native VLAN frames, and the phone receives the tagged or voice VLAN frames.  
No configuration of the phone is necessary to enable this.  
You simply type a few commands on the switch, telling the switch what the Voice VLAN is and what the Data VLAN is.

The rest happens automatically because when the phones boot up, they query the switch through CDP (Cisco Discovery Protocol) to find out which VLAN they belong to. The switch updates the phone's configuration through the use of CDP.

## How ports are assigned to VLANs

- They can be **statically assigned** by an administrator. Enable mode > config mode > config-if mode > put the interface into a VLAN
- you can also create **Dynamic VLANs** using a **VLAN Membership Policy Server** (VMPS)
- Lastly, we have **Voice VLANs**, whice are used specifically for IP phones. 

### Dynamic VLANs

**Dynamic VLANs** allow for a port's VLAN to be dynamically updated based on the MAC address of the device attached to that port.  
In a boardroom for example, when a director plugs in his laptop, based on the MAC address of that laptop, the corresponding port on the switch is automatically assigned to the director's VLAN.  
When a manager plugs his laptop into the same port, the VLAN is automatically updated to the manager's VLAN.  
Based on the source MAC address of the frames received on the port, this port is automatically assigned to the proper VLAN.  

## VTP

VLAN Trunking Protocol is a Cisco proprietary layer 2 protocol which allows for propagation of VLAN information from one switch to another.  
Rather than telneting to mutliple switches, you can create, delete or rename VLANs on one switch and have that information automatically propagated to other switches across trunk links.  

VTP can save you a lot of time. But as a lot of Cisco engineers will tell you, VTP can cause you a lot of headaches.  
Switches can have the entire VLAN configuration wiped out if a new switch is added to the network without following a proper procedure.  

A lot of network engineers will not enable VTP because of the inherent risk associated with this protocol.  

VTP messages are sent to the following MAC address: 01-00-0C-CC-CC-CC, which is a well-known multicast address for CDP and VTP flooding.  

There are 3 types of messages in VTP:
- summary advertisements
- avdertisement requests
- subset advertisements

When setting up VTP, devices will by default belong to **the null domain**.  
For VTP to work, you need to configure and put the devices into a specific VTP domain.  
Only devices within the same VTP domain will be updated with VLAN information.  
A switch can only be configured in a single VTP domain at any given time.  

By default, Cisco switches are in the null domain or "no management" domain, until they receive an advertisement for a domain over a trunk link, or until you manually configure a management domain.  

An important concept to understand in VTP is the concept of "**revision number**".  
Everytime a change is made to the VLAN database, the revision number will increment by one.  

When a change is made on one of the switches, the information is advertised to all other switches in the VTP domain, so that they can synchronize their databases to the latest revision number.  

The switch on which the change is made will send a VTP **summary advertisement** to inform all other switches that a change has been made.  
These switches will then request the latest information using an **advertisement request**, and the switch on which the change has been made will send them detailed information about the change using a **subset advertisement**.  
Finally, the **revision number** on all of these switches will increment to the same revision number as the switch where the change was made.  

The whole concept with VTP is that you can make changes on an individual device, and all other devices in the VTP domain are informed and will synchronize their databases to the latest revision number so that they end up having the same VLANs.  

>[!warning]
>VTP is just a VLAN database update mechanism. It does not put ports into VLANs. Administrators still need to put those ports into the relevant VLANs.

- Summary advertisements are sent every 5 minutes or whenever there's a change. 
- 


@15min



---
EOF
