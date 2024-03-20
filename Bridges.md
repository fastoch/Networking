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

## What does a bridge do when it receives a frame?

When a bridge boots up, its MAC address table is empty.  

When a frame sent by host A arrives on port X, the bridge now knows that host A is connected to port X.  
It then creates a mapping between the MAC address of host A and port X.  

When host B replies to host A, the bridge reads the MAC address of host B and knows which port B is connected to.  
All subsequent frames destined to A or B will only be sent to the matching port, and not flooded out of all ports.  




---
EOF
