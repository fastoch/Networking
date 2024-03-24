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

**Wireshark** is a sniffing tool that allows you to capture localhost traffic. It's an **invaluable tool** for network engineers.  

---

In summary, when a device wants to communicate with another device **within the same subnet**, it will send a broadcast onto the 
local segment to find the MAC address of the targeted device, asking "Who has the following IP address?".

---

## Routing between subnets

The first thing a computer will do is to check whether the IP address it's trying to communicate with is in a separate subnet  
or in the same subnet as itself. It does this by applying a logical AND between the IP address and the subnet mask.  

By doing so, the computer compares the network portion with the device that it's trying to communicate with to check if  
this device is local or remote.  

If the network portion of the address is different, the local PC knows that the targeted device is in a different subnet to itself.  
And it will therefore send the traffic to its default gateway.  

The PC will firstly check if it has the router's MAC address in its local ARP cache.  
It does this because we're on an Ethernet segment, so it has to know the MAC address associated with the gateway's IP address.

If the PC doesn't know the router's MAC address, it will send an arp request to ask the router to provide its MAC address.  
The router responds to the arp request and the PC now knows which MAC address is associated with the IP address of the router.  

Then, the PC can send traffic to the remote machine via its default gateway (the router), using the destination MAC address  
of the router and the destination IP address of the remote host.  

---

So, when sending traffic from one subnet to another subnet, the Layer 3 headers contain the source host IP address and the  
destination host IP address. But at Layer 2, the source MAC address is the local host and the destination MAC address is  
the local router on the local Ethernet segment.  

When the frame gets to the router, the router will strip the Layer 2 headers and then read the Layer 3 headers to determine  
what to do with the traffic. The router will then check if the destination IP address is a local address.  
If it's not a local address, it checks its routing table to determine where to send the traffic for this IP address.  

Before sending the traffic, the router has to check its arp cache to see if it has an entry for the destination IP address.  
If there is no arp entry for this IP address, the router sends a broadcast in order to get the associated MAC address.  
This broadcast is once again an arp request that will be replied by the device having the requested MAC address.  
The arp reply will contain the requested MAC address and the router will then update its arp cache.  

Once the router has the MAC address corresponding to the destination IP, it can relay the traffic sent by the source host.  
When it sends the traffic, the router **rewrites** the source MAC address entry so that the MAC address of the source host is   
replaced by the MAC address of the interface through which the traffic exits the router.  

---

It's important to remember that when traversing a router or a Layer 3 switch, **the Layer 2 information is rewritten**.  
The Layer 3 information is left the same, but every time traffic hops across a router or is sent from one vlan to another,  
the Layer 2 information is rewritten in the frame.





---
EOF
