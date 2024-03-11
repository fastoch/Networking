## Address Classes

Address Classes or Classful Networks were used in the Internet from **1981** until the introduction of  
Classless Inter-Domain Routing (**CIDR**) in **1993**.  

---

**IANA** = Internet Assigned Numbers Authority is a standards organization that oversees:
- global IP address allocation,
- autonomous system number allocation,
- root zone management in the Domain Name System,
- media types,
- and other Internet Protocol–related symbols and Internet numbers.

---

Class A, B and C were used for **Unicast** traffic (one-to-one communication).  
Class D was used for **Multicast** traffic (talking to a group of devices).  
Class E was reserved for future or experimental purposes.  

>[!note]
>IPv6 does not use address classes.  

Classes A, B and C were used to accomodate different sizes of networks.  
- Class A range: from 1.0.0.0 to 126.255.255.255 
- Class B range: from 128.0.0.0 to 191.255.255.255
- Class C range: from 192.0.0.0 to 223.255.255.255
- Class D range: from 224.0.0.0 to 239.255.255.255 (Multicast)
- Class E range: from 240.0.0.0 to 255.255.255.255 (reserved addresses)

An IPv4 address is made of 4 octets (or bytes), which equals 4 x 8 bits.  
- In a class A address, the first 8 bits denote the network portion, and the last 24 bits denote the host portion.
- In a class B address, the first 16 bits denote the network portion, and the last 16 bits denote the host portion.
- In a class C address, the first 24 bits denote the network portion, and the last 8 bits denote the host portion.

---

## Special Addresses

### Directed Broadcast Address 
used to send data to all devices on a specific network.  
The **host portion** of the address is populated with binary ones.  
Example: 172.31.255.255  

Routers can be configured to route directed broadcast. But this is disabled by default.  
For security reasons, it's recommended that the forwarding of directed broadcast be disabled.
Nowadays, routers and switches drop directed broadcast traffic to prevent denial of service attacks.  

### Local Broadcast Address
used to communicate with all devices on the local network.  
The entire address is populated with binary ones: 255.255.255.255  
This address is used, for example, by a host when requesting an IP address from a DHCP server.

>[!note]
>DHCP = Dynamic Host Configuration Protocol

>[!warning]
>Local Broadcast addresses are always dropped by Layer 3 devices such as routers and Layer 3 switches. You can override that functionality
>by configuring what is called "**DHCP forwarding**" or "**DHCP relay**" on the switch or router.

### Local Loopback Address
used to let a device send a message to itself for testing.  
This is very useful to make sure that the TCP/IP stack is correctly installed on a machine.  
A typical loopback address is 127.0.0.1.  

>[!note]
>Anything in the 127.x.x.x range is deemed a local loopback address.

In **IPv6**, a different address is used for the loopback, it's **::1**.  

>[!note]
>Routers and switches also have loopback addresses which are not the same as the local loopback address.

---

## Private Addresses

**RFC1918** (February 1996) discusses **private IP addresses**, which are non-routable on the Internet.  
Its purpose was to prevent the exhaustion of IPv4 addresses.  

The IANA has reserved the following 3 blocks of the IP address space for private internets:
- 10.0.0.0 to 10.255.255.255 (10/8 prefix)
- 172.16.0.0 to 172.31.255.255 (172.16/12 prefix)
- 192.168.0.0 to 192.168.255.255 (192.168/16 prefix)

In brief, **NAT** (network address translation) will translate one of these IP addresses to a publicly  
routable address when traversing a router (our local Internet gateway).

>[!note]
>RFCs or Requests For Comments are formal documents from the IETF (Internet Engineering Rask Force).
>A final version of an RFC will become an Internet standard.

---

## Link-Local Addresses 

**RFC3927** - May 2005
Automatic Private IP Address (APIPA) - only works on Microsoft Windows operating systems.  
It's used when a PC is configured for DHCP but no DHCP servers are available.  
Allows 2 computers in the same LAN to communicate when there are no DHCP servers available.
- range: 169.254.0.0/16
- no manual configuration required
- host randomly generate the host specific portion of the address
- Be aware that this address range is not routable, it's only for communication within the local link.

---

## Subnet Masks
used to determine which part of an IP address is the network portion and which part is the host portion.  

This allows a local machine to determine whether the device it wants to communicate with is:
- on a remote network and thus can be reached via a default gateway 
- on the local subnet and therefore does not require the use of a default gateway

The network portion in a subnet mask consists of contiguous ones starting from the left hand side.
The host portion in a subnet mask consists of contiguous zeros starting from the right hand side.

---

## Discontiguous Network Mask

Cisco and most network vendors do not support discontiguous subnet masks.  
"Discontiguous" means that ones and zeros are mixed, they're not grouped together.  

Subnets masks must start with contiguous binary ones and end with contiguous zeros.

---

### CIDR Notation

CIDR = Classless Inter-Domain Routing  
introduced in 1993, replaces classful IP addresses  
allows us to use **VLSM** (Variable Length Subnet Mask)  

255.255.255.0 = /24
255.255.240.0 = /20
255.255.0.0 = /16
255.240.0.0 = /12
255.0.0.0 = /8

**Before CIDR**:
- class A: 16 million hosts, subnet mask of /8
- class B: 65500 hosts, subnet mask of /16
- class C: 254 hosts (256 minus network & broadcast addresses), subnet mask of /24

---
EOF
