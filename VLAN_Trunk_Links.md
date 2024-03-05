# VLAN Trunk Links

Using VLANs is like breaking a physical switch into a few virtual ones.  
But eventually we'll need more physical ports, which means more physical switches.  

## How do get our VLANs to work across several switches?

Like the many branches on a tree trunk, we can use a **trunk link** to carry many VLANs.  

If the company we work for grows, then they're going to need more computers, printers, servers, and other devices.  
Which means we have to buy more switches.  

Normally, we would connect one switch to another to extend our number of ports.  
But we have cut our network into VLANs now. So how do we connect the two switches together?  

**Should we run a link between our switches for each VLAN?**  
We could, but what happens if we have many VLANs? We would be out of ports pretty quickly.  
And then what happens if we want to add a third switch?  
Clearly this method is not scalable.  

Instead, we can use **a single link** which is capable of carrying all of our VLANs.  
This uses a technology called **trunking** or **tagging**.  

In VLANs.md, we saw how to add devices to a VLAN. The type of port they connect to is called an **access** port.  
Typically, we would connect workstations, printers, servers and phones to an access port.  
When we connect 2 switches together, we configure these ports as **trunk** ports.  

Trunk ports are able to have many VLANs configured on them at one time.  

---

### Why do we want to use VLANs to separate traffic if a trunk link just mixes them all together again?

The traffic doesn't fully get mixed together. It goes over the same link, but it won't leave its VLAN.  
This is thanks to our good friend Ethernet.  

Think of a device on a VLAN sending a frame to a device on another VLAN.  
The switch knows which VLAN this frame belongs to.  
When the frame reaches the trunk link, the switch adds a 4 byte tag to the Ethernet header.  

This tag contains (amongst other things) the VLAN ID. When the frame arrives at the destination trunk port,  
the switch looks at the tag and knows the VLAN that this frame belongs to. It can now strip the tag from the  
frame and deliver it to the destination workstation. 

>[!note]
>VLAN names are locally significant to each switch. They don't have to match on 2 different switches.

**A trunk link extends VLANs from one switch to another.**  

As VLANs are in a broadcast domain, trunk links also extend broadcast domains across switches.  
So broadcast messages will stay within a VLAN but will pass over a trunk to other switches.  

And the same is true for flooding. Any frame that needs to be flooded will stay within the VLAN, but will   
travel over the trunk links to other switches.  

Once again, Cisco's terminology is a little bit different to everyone else's.  
To start with, a trunk port is called a **"tagged port"**, because of the tag that is added to the frame as it passes between the switches.

Also, an access port is really an **"untagged port"**.  

When it comes to tagging, there are two ways it can be done:
- **802.1q** - IEEE standard (well supported): a trunk between switches from different manufacturers is possible
- **ISL** - Cisco's original trunking standard (rare): inter-switch link

---

## Voice VLANs

These are important if you have IP telephony in your network.  
Workstations belong to a **data VLAN**, whereas IP phones belong to a **voice VLAN**.  

Usually, phones are a little bit special. They have a miniature 3 port switch built-in.  
So we can connect the phone to the switch, and the workstation to the phone.  
The third port is hidden from sight, it's inside the phone, connecting to the phone hardware.  

**Why do phones have a built-in switch?**  
For one, there's less need for ports on the main switch.  
Secondly, you don't normally connect phones and workstations directly into a switch.  
They normally go into a wall socket, with cabling through the wall which is eventually connected to the switch.  

The link from the phone to the switch is like a mini-trunk link, except it carries only 2 VLANs:
- the data VLAN
- the voice VLAN

Voice networking is a subject entirely of its own (see Voice_networking.md).






---
EOF
