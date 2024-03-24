## Scenario
PC1 (10.1.1.1/24) sends an echo request to PC2 (10.1.3.2/24): `ping 10.1.3.2`  
Between PC1 and PC2 there is a switch (switch1), 2 routers (router1 and router2), and another switch (switch2).  

## Traffic flow
When traffic is sent from one network to another across a router, the source PC is going to ARP for its router's MAC address.  
Once PC1 knows its router's MAC address, it can send a frame to Router1 via switch1.  
This frame contains the MAC address of Router1 inbound interface as the destination.  

Router1 encapsulates the frame in an IP packet and moves the packet from its inbound interface to its outbound interface.  
In this packet, there is no MAC address. Source IP is PC1 and Destination IP is PC2.  
Router1 will relay the packet to Router 2 (From Router1 outbound interface to Router2 outbound interface).  

Router2 moves the packet from its outbound interface to its inbound interface.  
Then it strips out the Layer 3 headers and sends the frame to PC2 via switch2.  

Notice that switches don't modify the frames, only routers do.  






---
EOF
