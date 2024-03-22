Routers do not make routing decisions based on full IP addresses, they make it based on **network addresses**.  
A **routing table** is not populated with IP addresses, it's populated with network addresses.  

Routers are Layer 3 devices (some switches also are), meaning they operate at the Network layer of the OSI model.  
Routers still use MAC addresses on Ethernet interfaces, but the decision making process of **which interface traffic should  
be transmitted out of** is made based on IP addresses (actually the network portion of these addresses).  

A router may have **Serial interfaces** as well as **Ethernet interfaces**.  
An Ethernet interface uses MAC addresses for forwarding of traffic (frames) at layer 2.  
A Serial interface uses PPP or **Point-to-Point Protocol**.  

---

For a device to know the MAC address associated with the IP address of another device, it uses a protocol called **ARP**.  
ARP stands for **Address Resolution Protocol**.  

If the local ARP cache doesn't contain the targeted IP address, the device will send out a broadcast to try and find out  
which device has this IP address.  





---
EOF
