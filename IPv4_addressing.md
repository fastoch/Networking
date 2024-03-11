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
- Class D range: from 224.0.0.0 to 239.255.255.255
- Class E range: from 240.0.0.0 to 255.255.255.255

An IPv4 address is made of 4 octets (or bytes), which equals 4 x 8 bits.  
- In a class A address, the first 8 bits denote the network portion, and the last 24 bits denote the host portion.
- In a class B address, the first 16 bits denote the network portion, and the last 16 bits denote the host portion.
- In a class C address, the first 24 bits denote the network portion, and the last 8 bits denote the host portion.

