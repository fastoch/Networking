Switches are very similar to bridges, as they both reside at layer 2 (data link) of the OSI model.  

The big advantage of switching when compared to bridging is that **processing can be done in hardware**, using what are  
called **ASICs** or Application Specific Integrated Circuits.  
The number of ports supported by switches is also a lot higher.  

Switches can move traffic from one port to another at the same speed as if they weren't there.  
They can process and switch frames from one port to another without slowing the frame down.  

For a switch, the network topology is also a star topology where devices are cabled directly to ports on the switch.  
Switches are essentially very efficient bridges.  

Switches work just like bridges. At first their MAC address table is empty and they have to flood the frames out of all ports.  
When receiving frames, they learn MAC addresses and become able to target the specific ports to which they must forward the traffic.  

Just like a bridge, each port on a switch is a separate collision domain.  
However, a switch will flood broadcast and multicast traffic by default. This is a single broadcast domain.   

There are some major advantages to using switches over hubs and bridges:
- switches can support many ports (some switches have hundreds of ports)
- switches can operate at wire speed (they don't slow frames down)

Some switches have **backplanes** that operate at terabits per second.  
This is very fast in comparison to interface speeds.  
It means that a switch can move traffic from one port to another port faster than it can receive traffic on an interface.  


---
EOF
