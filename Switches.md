A switch is different to a hub in that it has a separate collision domain on every port.

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
- Bandwidth is not shared between all devices. Each device connected to a switch can leverage the full bandwidth capacity.

Some switches have **backplanes** that operate at terabits per second.  
This is very fast in comparison to interface speeds.  
It means that a switch can move traffic from one port to another port faster than it can receive traffic on an interface.  

Like we said, connecting more devices to a switch doesn't degrade the throughput that each device gets.  
In addition, you can increase the speed by changing the duplex.  

Full-duplex doubles the bandwidth allocated to each port by allowing to send and receive traffic at the same time.  
Half-duplex communication is like a walkie-talkie, where only one side can send at any given time.  

Hubs use CSMA/CD (Carrier Sense Multiple-Access Collisition Detection), which is half-duplex.  
On individual ports on a switch however, you can set those ports to use full-duplex.  

Using full-duplex implies that collision detection is turned off. This can cause issues if both sides are not set to full-duplex.  

Full-duplex is often negotiated automatically between devices.  
It does happen that one side chooses full-duplex and the other side chooses half-duplex. This will cause problems on that link.  

>[!tip]
>If a user is complaining about slow throughput, check the duplex on both sides.

The throughput of modern switches is much much greater than hubs or bridges.  

Be aware however that in **wireless networks**, access points tend to **operate like hubs**, which means they have a shared infrastructure.
Shared infrastructure means **shared bandwidth**.  
Whereas with **switches** devices have **dedicated bandwidth**.


---
EOF
