Routers do not make routing decisions based on full IP addresses, they make it based on **network addresses**.  
A **routing table** is not populated with IP addresses, it's populated with network addresses.  

Routers are Layer 3 devices (some switches also are), meaning they operate at the Network layer of the OSI model.  
Routers still use MAC addresses on Ethernet interfaces, but the decision making process of **which interface traffic should  
be transmitted out of** is made based on IP addresses (actually the network portion of these addresses).  

A router may have **Serial interfaces** as well as **Ethernet interfaces**.  
An Ethernet interface uses MAC addresses for forwarding of traffic (frames) at layer 2.  
A Serial interface uses PPP or **Point-to-Point Protocol**.  

---

## ARP

For a device to know the MAC address associated with the IP address of another device, it uses a protocol called **ARP**.  
ARP stands for **Address Resolution Protocol**.  

If the local ARP cache doesn't already contain the targeted IP address, the device will send out a broadcast to try and find out  
who has this IP address. That message is called an **ARP request**.  

Before traffic can be sent to an IP address on the local segment, ARP is required to create a mapping between the layer 3 IP address  
and the layer 2 MAC address.  

`arp -a` to show the current arp cache  
`arp -d` to delete all entries in the arp cache

---

**Wireshark** is a sniffing tool that allows you to capture localhost traffic.  
It's an **invaluable tool** for network engineers.  

---

In summary, when a device wants to communicate with another device **within the same subnet**, it will send a broadcast onto the 
local segment to find the MAC address of the device using the target IP address.

---

## Routing between subnets

The first thing a computer will do is to check whether the IP address it's trying to communicate with is in a separate subnet  
or in the same subnet as itself. It does this by applying a logical AND between the IP address and the subnet mask.  

By doing so, the computer compares the network portion with the device that it's trying to communicate with to check if  
this device is local or remote.  

If the network portion of the address is different, the local PC knows that the targeted device is in a different subnet to itself.  
And it will therefore send the traffic to its default gateway.  

The PC will firstly check if it has the router's MAC address in its local ARP cache.  
@2min



---
EOF
