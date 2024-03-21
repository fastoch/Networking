Over time, hubs were replaced by bridges, then bridges were replaced by switches.  

A bridge is a **Layer 2 device** (Data Link layer of the OSI model).  
Bridges use a **MAC address table**, also called a **CAM table** (Content Addressible Memory).  
This table allows bridges to learn where devices are in the topology.  

Bridges are very slow in comparison to switches.  
Switches and bridges operate in a very similar way, but bridges do the processing in software  
whereas switches do the processing in hardware.  

Switches use something called an **ASIC** = application specific integrated circuit, which allows for:
- high throughput
- very quick table lookups
- forwarding of traffic often at line rate 
In other words, switches don't slow the traffic down.

Bridges were the predecessors to switches and did things in software.  
They were a lot slower, but from a forwarding point of view, bridges and switches forward traffic on a  
layer 2 segment in the same way, except switches do it in hardware.  

The number of ports on a bridge is also limited when compared to switches.

## What does a bridge do when it receives a frame?

When a bridge boots up, its MAC address table is empty.  

When a frame sent by host A arrives on port X, the bridge now knows that host A is connected to port X.  
It then creates a mapping between the MAC address of host A and port X.  

When host B replies to host A, the bridge reads the MAC address of host B and knows which port B is connected to.  
All subsequent frames destined to A or B will only be sent to the matching port, and not flooded out of all ports.  

## Advantages of bridges over hubs

Thanks to bridges, devices are not unnecessarily processing traffic not destined to them, and bandwith is being conserved.  
Overtime, a bridge will learn where all MAC addresses are, increasing the number of possible simultaneous conversations.  

Unlike with a hub, where any collision would affect all devices connected to the hub, a collision between a device and a bridge  
would only affect this device, all other devices wouldn't even realize that there was a collision in the network.  

**Each device connected to a bridge is in its own collision domain (multiple CD).   
Whereas all devices connected to a hub are in the same Collision Domain (single CD).**  

However, a bridge is still a **single broadcast domain**, just like a hub.  
Which implies that broadcasts have the same negative effects on networks using a bridge than on those using a hub.  
A broadcast storm may bring your network down, whether you're using a hub or a bridge.  
Only switches can implement the Spanning Tree Protocol (STP).


---
EOF
