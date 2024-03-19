A hub is a **Layer 1 device** in the OSI model (Physical layer).  
You would use a Cat5 UTP cable with an RJ45 connector to connect a device to a hub.  

>[!note]
>UTP = Unshielded Twisted Pair

Hubs have been superseded by switches.  
However, it's important you understand how a hub operates because **wireless operates in the same way**.  
When you connect to a wireless network, you'll often encounter the same issues that you would when connecting to a hub.  

Hubs have multiple ports, and thus multiple devices can be connected to a hub at the same time.  
A hub is not "intelligent" and does not understand the frames going through it.  
It's basically a multiport repeater. **It will amplify or repeat the frames that it receives on one port out of all other ports**.  

The physical topology of a hub is a **star topology**.  
In a star topology, you have a central device (a hub in this case) and devices hanging off that central device just as  
spokes in a bicycle wheel. Each spoke device is connected to the central device with its own cable, and all communications  
between devices are through the central device.  

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
EOF
