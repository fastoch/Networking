# Switching

## VLANs

VLANs are a switching technology which operates at layer 2.

VLANs allow us to split our network into many subnets on one single switch.  
This is cost-efficient, good for security and it simplifies network administration.

Each VLAN has an ID. This ID is a number ranging from 0 to 4095.  
IDs 0 and 4095 are both reserved. So our usable range goes from 1 to 4094.  
Each port on a switch is assigned to a different VLAN by using this ID.  

When we add VLANs to a switch, we change the broadcast domain.  
If a broadcast frame arrives on a switch port, it will be sent out all other ports in the VLAN.  
But it will not be sent to ports in other VLANs.  

The same is true with flooding. If a frame needs to be flooded, it will only be flooded on ports within that VLAN.  
And with less flooding, we reduce our security risk.

>[!note]
>Flooding = the switch sends the data frame on all ports when it doesn't know the port number on which to forward.

**Best practice** = one subnet per VLAN  

When it comes to VLANs, **Cisco** do a couple of things a little differently to the standard.  
The VLAN is from 1 to 4094, but on many of their switches, Cisco reserves VLANs 1002 to 1005 for compatibility with their
older equipment. Also, Cisco breaks the VLAN space into 2 ranges:
- normal range: 1-1005
- extended range: 1006-4094

Their original switches only supported the normal range.  
Inside some of their switches, the normal range is handled a bit differently to the extended range.  
Also, Cisco use technologies like **VTP** which handles these ranges differently.

>[!note]
>VTP = VLAN Trunk Protocol | https://www.cisco.com/c/fr_ca/support/docs/lan-switching/vtp/10558-21.html

### How do we get devices on different VLANs to talk to each other?

In most cases, we need to allow some traffic between devices in differents VLANs.  
VLANs provide a layer 2 boundary: **frames** from one vlan will not pass through to another vlan.  
But we can use technologies in other layers to help. This is where **layer 3** comes in.  

Layer 3 is all about **IP addressing** and moving **packets** from one network to another.  
And this what **routers** are made for.  

Each vlan should be associated with only one subnet.  
The router has an interface connected to each vlan, and each interface is connected with an IP address from that subnet.  
Devices in each network will configure their **default gateway** to be the IP address of the router.  

When a device needs to send a frame outside of its vlan, it sends a frame to the router using the MAC address of the router as the destination.  
The router, as it is connected to both networks, will know where to send the frame. It will rewrite the destination address field with the
MAC address of the destination device, and then it will forward the frame on.  

### How do devices, switches and routers know which IPs match up to which MAC addresses?

They use a protocol called **ARP**, which stands for **Address Resolution Protocol**.  
Devices broadcast an ARP message asking who owns a particulat IP address.  
If the owner is in the local network, it will respond withits MAC address.  
We'll this in more detail in a later lesson.  

**Example**:
![image](https://github.com/fastoch/Networking/assets/89261095/8dbd2a53-083f-478a-9cba-a38918d71d51)

First step is to jump onto our switch and create our vlans.  

