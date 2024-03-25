## Scenario
PC1 (10.1.1.1/24) sends an echo request to PC2 (10.1.3.2/24): `ping 10.1.3.2`  
Between PC1 and PC2 there is a switch (switch1), 2 routers (router1 and router2), and another switch (switch2).  

## Echo Request

### From PC1 to Router1

When traffic is sent from one network to another across a router, the source PC is going to ARP for its router's MAC address.  
Once PC1 knows its router's MAC address (Gigabit interface), it can send a frame to Router1 via switch1.  
This frame contains the MAC address of Router1 Gigabit interface as the destination. Encapsulation used is Ethernet 2.  

### From Router1 to Router2

Router1 encapsulates the frame in an IP packet and moves the packet from its Gigabit interface to its Serial interface.  
In this packet, there is no MAC address. Encapsulation used is HDLC (High-Level Data Link Control).  
Router 1 sends the packet to Router2 Serial interface. Source IP is PC1 and Destination IP is PC2.  

### From Router2 to PC2

Router2 moves the packet from its Serial interface to its Gigabit interface.  
Then it strips out the Layer 3 headers and sends the frame to PC2 via switch2.  
Destination MAC address is PC2. Encapsulation used is Ethernet 2.

---

Notice that switches don't modify the frames, only routers do.  

---

## Echo Reply

### From PC2 to Router2

Source MAC address is PC2 and Destination MAC address is Router2 Gigabit interface.

### From Router2 to Router1

No MAC address. Frame is encapsulated in an IP packet and sent from Router2 Serial interface to Router1 Serial interface.  

### From Router1 to PC1

IP packet is received by Router1 Serial interface and then moved to Router1 Gigabit interface.
IP headers are removed and frame is sent from Router1 Gigabit interface to PC1.  
Destination MAC address is PC1, source MAC address is Router1.


---
EOF
