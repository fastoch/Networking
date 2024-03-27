# Duplex and speed mismatch

With Full Duplex, a device can transmit and receive at the same time.  
With Half Duplex, devices of the network are either sending data or receiving it, they can't do both.

Originally, Ethernet was half-duplex because devices were connected to hubs.  
Devices connected to a hub are in the same collision domain, therefore they can't communicate simultaneously.  

These days, thanks to Ethernet switches, we generally use Full Duplex.  

---

Duplex and speed mismatches occur when autonegotiation fails, or when manual configurations are mismatched.  
Autonegotiation fails because of physical problems such as cabling problems or a hub somewhere in the network.

Duplex mismatches do cause performance issues. Pings may succeed, but the movement of large files can be seriously affected.  
UDP in particular may have problems with recovering from duplex mismatch issues.  

When there is a mismatch, the side that is set for half duplex will see late collisions on the connection.  
Keep in mind that this only occurs when you're sending enough traffic. A standard ping doesn't show that problem.  
But when a large amount of traffic is sent on the half duplex connection, we're getting late collisions. 

---
EOF
