**Repeater** = old device that amplifies the signal from one port to another.  

**Hub** = multi-port repeater, repeating the signal from one port to all other ports.  
A hub simply amplifies the traffic received, we say it "floods" it, out of all ports.

>[!note]
>A Wi-Fi network is essentially a hub in the air.

**Switch** = unlike a hub, it has "intelligence", it can read the frames received on its ports.  
A switch uses a MAC address table to only forward the frames out of the correct ports, based on the destination  
MAC address in the frame. It's a Layer 2 device in the OSI model, whereas a hub is a Layer 1 device.  
Switches allow us to connect many devices in a local network. They were invented in the late 80s.  

Modern switches have routing functionalities, we call them **Layer 3 switches**.  
They can route traffic from one VLAN to another VLAN, meaning from one subnet to another.

**Bridge** = intermediate device between a switch and a hub. Invented in 1983.

**Router** = use IP addresses to route traffic from one network to another. It's a Layer 3 device.  

**Firewall** = allows us to stop malicious traffic from entering our network.  
We use rules to permit or deny traffic. A firewall can be placed in front of the router or behind it.  
In most cases, you will have: Internet > router > firewall > switch.  

**Next-Generation Firewall** = support features such as IPS (intrusion prevention syst) or IDS (intrusion detection).  
An IDS simply warns you when there's an attack.  
An IPS also alerts you, but it can block the attack.

**Wireless LAN controller** = used to manage numerous Wi-Fi Access Points. Abbreviated to WLC.  
They don't have many ports, so they usually connect to the Access Points through one or more switches.  


