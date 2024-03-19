A hub is a **Layer 1 device** in the OSI model (Physical layer).  
You would use a Cat5 UTP cable with an RJ45 connector to connect a device to a hub.  

>[!note]
>UTP = Unshielded Twisted Pair

Hubs have been **superseded by switches**.  
However, it's important you understand how a hub operates because **wireless operates in the same way**.  
When you connect to a wireless network, you'll often encounter the same issues that you would when connecting to a hub.  

Hubs have multiple ports, and thus multiple devices can be connected to a hub at the same time.  
A hub is not "intelligent" and does not understand the frames going through it.  
It's basically a multiport repeater. **It will amplify or repeat the frames that it receives on one port out of all other ports**.  

The physical topology of a hub is a **star topology**.  
In a star topology, you have a central device (a hub in this case) and computers hanging off that central device just as  
spokes in a bicycle wheel. Each computer is connected to the central device with its own cable, and all communications  
between computers of the network are through the central device.  

---

## Why people were using hubs?

There were some major advantages to using hubs and UTP rather than 10base2 (hubs use 10base-T):
- a cable break would only affect one device (in a 10base2 bus topology, it would bring the entire network down)
- you can extend to further distances by simply adding hubs, whereas 10base2 are limited in size

Hubs were there for good reasons, to move away from 10base2 and 10base5, and implement UTP instead of coaxial cables.  
Another advantage is that UTP cabling is cheaper and easier to manage.

---

**Note about Ethernet variants:**
- 10base5 = 10Mbps baseband over thick coaxial cable (first variant of Ethernet, 1982)
- 10base2 = 10Mbps baseband over thin coaxial cable (mid to late 1980s)
- 10base-T = 10Mbps baseband over Twisted Pair cables (1990)

---

## How does it work?

Since a hub is not able to send frames to a specific destination, all devices in the network will receive them.  
Then, the NICs (Network Interface Cards) of these devices have to read the destination MAC address in the frame.  

If the destination MAC address does not match, the NIC will drop the frame.  

If the destination MAC address matches, the NIC will accept the frame, strip the layer 2 headers and pass the packet to  
the higher layer protocol (IPv4 if it's an IPv4 packet).  

---

## No MAC address table

Keep in mind that, unlike switches, hubs don't have a MAC address table.  
The MAC address table is where a switch stores information about the other Ethernet interfaces to which it is connected  
on a network. This table enables the switch to send outgoing data (Ethernet frames) on the specific port required to reach  
its destination, instead of broadcasting the data on all ports (**flooding**).

---

## Physical vs. logical topology

The physical topology of a hub is a star. But logicallly, it's a bus.  
**It's very important to realize that there's a difference between a physical and logical topology in networks.**
The way the network is physically cabled isn't necessarily the way the network is going to operate.  

When a device sends traffic in a hub environment, all devices receive the frame.  
That's exactly the way it works in 10base2 or 10base5.  

A hub operates in the same way as 10base2 because when A sends a frame onto the network, all devices receive it.  
Just like in a 10base2 environment, when there's a collision on the network, it will affect all devices.  
This is a **single collision domain**.  

A collision anywhere will cause devices to back off, send a jamming signal and then attend to transmit again.  
As you increase the number of devices in a hub environment, the number of collisions increases and your network  
throughput goes down.  

In addition, broadcasts are received by everyone, as this is a single broadcast domain.  
Broadcast traffic will flood through the entire network and interrupt the CPU of every device.  

From a bandwidth point of view, this may be 10baseT, but it's 10 Mbps shared between all devices in the network.  
So assuming there are 4 devices in the network, with a maximum utilization of 30%, each device will only get 0.75 Mbps.  




---
EOF
