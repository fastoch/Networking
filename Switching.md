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

### How do 



