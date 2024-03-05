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

Trunk ports are able to have many VLANs 








---
EOF
