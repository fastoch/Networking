Source = David Bombal - Cisco CCNA 200-301 - Udemy

---

## What is a VLAN?

A virtual LAN is a single broadcast domain. It's also a virtual subnet or logical network.  
You could say it's a group of hosts with a common set of requirements attached to the same broadcast domain, regardless 
of where they are physically located. You are able to group multiple devices together logically rather than physically.  

It is possible to span a subnet (or VLAN) across multiple switches, even though that's not recommended today.  

Some of the advantages of VLANs include:
- segmentation: separate users based on function (sales, accountancy, ...)
- flexibility: without changing physical cabling, you can move a user from one vlan to another
- security: users are in separate vlans, and therefore have to traverse a layer 3 device to get from one vlan to another

>[!note]
>On the router, you could implement ACLs to control which users have access to various vlans

These days, VLANs also have other advantages, specifically when implementing VoIP.  
You can put your IP phones into a separate VLAN to your workstations', and therefore provide a better QoS to the IP phones.  



---
EOF
