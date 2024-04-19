source = https://www.youtube.com/watch?v=qiQR5rTSshw&t=20s  

This college-level course will prepare you to configure, manage, and troubleshoot computer networks.  
It will also help you prepare for CompTIA's Network+ exam.  

---

# Introduction to Network Devices

The OSI reference model was developed to help disaparate devices communicate on networks.  
**OSI** stands for Open Systems Interconnection.  
Devices may be classified by the level of the OSI model at which they operate. 

## Layer 1 devices

The analog **modem** modulates a digital signal into an analog signal and demodulates the return signal to allow  
for network communication.  

The **hub** receives a network signal on a port and replicates that signal out of all the remaining ports.  

## Layer 2 devices 

The **switch** utilizes an ASIC chip to learn which devices are connected to which ports via the device's MAC address.  
When the switch receives network traffic, it will only forward that traffic to the specified MAC address.  
**ASIC** stands for Application-Specific Integrated Circuit.  

The **WAP** (Wireless Access Point) is used to bridge wireless network segments with wired network segments. 

## Layer 3 devices

The **Multi-Layer Switch** (MLS) operates at more than just the layer 2 of the OSI model.  
The most common MLS is the Layer 3 switch. The ASIC chip is programmed to handle more than just MAC addresses.  

The **router** is the most common device used to connect different networks together.  
It utilizes software programming to learn about routes between networks. 

---

## Security Devices

### Firewall

A firewall can be placed on routers or hosts (software-based) or can be its own device (appliance).  
It functions at multiple layers of the OSI model: layers 2, 3, 4, and 7.  

Firewalls are the first line of defense in protecting the internal network from outside threats.  

A firewall blocks packets from entering or leaving the network via:
- stateless inspection
- stateful inspection

**Stateless inspection:**  
The firewall will examine every packet against a set of rules.  
When a packet matches a rule, the rule is enforced, and the specified action is taken.  

**Stateful inspection**:  
The firewall will only examine the state of the connection between networks.  
Specifically, when a connection is made from an internal network to an external network, the firewall will not examine any packets  
returning from the external connection.  
As a general rule, external connections are not allowed to be initiated with the internal network.  

### Intrusion Detection System (IDS)

An IDS is a passive system designed to identify when a network breach or attack against the network is occurring.  
It's usually designed to inform a network administrator when a breach or attack has occurred through log files, SMS, or  
email notifications.

An IDS cannot prevent or stop a breach or attack on its own.  
It receives a copy of all traffic and evaluates it against a set of standards.  

Those standards can be:
- signature-based: evaluates network traffic for known malwares or attack signatures
- anomaly-based: evaluates network traffic for suspicious changes
- policy-based: evaluates network traffic against a specific declared security policy

An IDS can be deployed at the host level. We talk about an "Host-based IDS" or "**HIDS**".  

### Intrusion Prevention System (IPS)

An IPS is an active system designed to stop a breach or attack from succeeding in damaging the network.  
- It's usually designed to perform an action or set of actions to stop the malicious activity.
- Will inform a network administrator through the use of log files, SMS, or email notifications.

For an IPS to work, all traffic on the network segment needs to flow through the IPS as it enters or leaves the network segment.  
Like the IDS, all traffic is evaluated against a set of standards.  

The **best placement** on the network is between a router (with a firewall) and the destination network segment.  

An IPS is programmed to make an active response to the situation:
- block the offending IP address
- close down the vulnerable interface
- terminate the network session
- redirect the attack
- plus more

### VPN Concentrator

A virtual private network concentrator will allow for many more secure VPN connections to a network.  

The concentrator will provide proper tunneling and encryption, depending on the type of VPN connection that is allowed.  
Most concentrators can function at multiple layers of the OSI model (layers 2, 3, and 7).  

Outside of Internet transactions (which use SSL VPN connections at Layer 7), most concentrators will function at the  
network layer (Layer 3), providing IPsec encryption through a secure tunnel.  

---

## Optimization and performance devices

### Load Balancer

A load balancer may also be called a "content switch" or "content filter".  
It's a network appliance that is used to load balance between multiple hosts that contain the same data, spreading out  
the workload for greater efficiency.  

It's commonly used to distribute the requests (workload) to a server farm among the various servers, helping to ensure  
that no single server gets overloaded.  

### Proxy server

A proxy server is an appliance that requests resources on behalf of client machines.  
It's often used to retrieve resources from outside untrusted networks on behalf of the requesting client.  

- It hides and protects the requesting client from untrusted networks.
- It can also be utilized to filter allowed content.
- It can increase network performance by caching commonly requested Web pages.

---

# Networking Services and Applications

## VPN Basics

A virtual private network (VPN) is used by remote hosts to access a private network through an encrypted tunnel through a public network.  

Once the VPN connection is made, the remote host is no longer considered remote.  
It is actually seen by the private network as a local host.  

Even though the network traffic may pass through many different routers or systems, it is seen by both ends as a direct connection.  

The use of a VPN can help to reduce networking costs for organizations and businesses.  
The cost reduction is partially achieved because the VPN doesn't require the use of a dedicated leased line to create the connection.

## VPN Types

- The **site-to-site VPN** allows a remote site's network to connect to the main site's network and be seen as a local network segment.
  VPN concentrators on both ends of the VPN will manage the connection.
- The **remote-access VPN (host-to-site VPN)** allows select remote users to connect to the local network. A VPN concentrator on the
  local network will manage the connections coming in from the remote users. The remote system requesting the connection uses special
  software called a VPN client. Users need to have a preconfigured VPN client installed on their machine.
- The **host-to-host VPN (SSL VPN)** allows a secure connection between two systems without the use of VPN client software. A VPN
  concentrator on the local network manages the connections. The host seeking to connect uses a Web browser that supports the correct
  encryption technology (either SSL or more likely TLS) to make the connection to the VPN concentrator.

## VPN Protocols 

### Internet Protocol security (IPsec)

- works at layer 3 of the OSI model or above
- the most common suite of protocols used to secure a VPN connection
- can be used with the **Authentication Header (AH)** protocol. AH only offers authentication services, no encryption
- can be used with **Encapsulating Security Payload (ESP)**. ESP both authenticates and encrypts packets (the most popular method)

Both AH and ESP will operate in one of two modes:
- **Transport Mode**: between two devices (host-to-host VPN)
- **Tunnel Mode**: between two endpoints (site-to-site VPN)

IPsec implements **Internet Security Association and Key Management (ISAKMP)** by default.  
ISAKMP provides a method for transferring security key and authentication data between systems, outside of the security key  
generating process.

### Generic Routing Encapsulation (GRE)

- a tunneling protocol that is capable of encapsulating a wide variety of network layer protocols
- often used to create a sub-tunnel within an IPsec connection

IPsec will only transmit unicast packets (one-to-one communication).  
In many cases, there's a need to transmit multicast (one-to-some communication) or broadcast (one-to-many communication) packets  
across an IPsec connection. By using GRE, this can be accomplished. 

### Point-to-Point Tunneling Protocol (PPTP)

An older VPN technology that supports dial-up VPN connections. On its own, it lacked native security features.  
Microsoft's implementation included additional security by adding GRE.  

### Transport Layer Security (TLS)

- a cryptographic protocol used to create a secure encrypted connection between two end devices or applications.
- it uses asymmetrical cryptography to authenticate endpoints, and then negotiate a symmetrical security key, which is used to
  encrypt the session.
- **TLS has largely replaced the Secure Socket Layer (SSL) protocol**
- it works at layer 5 and above of the OSI model
- its most common use is in creating a secure encrypted Internet session (SSL VPN). All modern Web browsers support TLS.

### Secure Socket Layer (SSL)

SSL is an older cryptographic protocol that is very similar to TLS.  
Its most common use is in Internet transactions. All modern Web browsers support SSL.  

Due to issues with earlier versions of the protocol, it has largely been replaced by TLS.  
SSL v.3.3 has been developed to address the weaknesses of the earlier versions.  

---

## Network Access Services

### Network Interface Controller (NIC)

- can also be called a network interface card
- the NIC is how a device connects to a network
- it works at two layers of the OSI model: layer 2 (data link) and layer 1 (physical).

At layer 2, it provides the functional means of network communication by determining which networking protocols will be used.  
For instance, Ethernet (LAN technology) or Point-to-Point Protocol (WAN technology).  
It also provides the local network node address through its burned-in physical MAC (media access control) address.  

At layer 1, it determines how the network data traffic will be converted a bit at a time into an electrical signal that can  
traverse the network media being used.  

- Most modern computers come with at least one built-in Ethernet NIC.  
- Routers and other network devices may use separate modules that can be inserted into the device to provide the proper NIC  
for the type of media they are connecting to and the networking protocol that is being used.

### RADIUS (Remote Authentication Dial-In User Service)

- A remote access service that is used to authenticate remote **users** and grant them access to authorized network resources.
- It's a popular **AAA (Authentication, Authorization and Accounting) protocol** used to help ensure that only authenticated
  **end users** are using the network resources they are authorized to use.
- The accounting features are very robust.
- only the requestor's (the end user's) password is encrypted. Everything else get sent in the clear.

### TACACS+ (Terminal Access Controller Access-Control System Plus)

- A remote access service that is used to authenticate remote **devices** and grant them access to authorized network resources.
- It's also a popular AAA protocol used to help ensure that only authenticated remote **network devices** are using the network
  resources they are authorized to use.
- The accounting features are not as robust as those of RADIUS.
- All transmissions between devices are encrypted.

---

## Other Services and Applications

### RAS (Remote Access Services)

Not a protocol, but a roadmap.  
It's a description of the combination of software and hardware required for a remote access connection.
A client requests access from a RAS server, which either grants or rejects access.

### Web services

Creating a means of cross communication.  
Provides the means for communication between software packages or disparate platforms.  
It's usually achieved by translating the communication into an **XML** (Extensible Markup Language) file.  

### Unified voice services 

Creating better voice communication systems.  
A description of the combination of software and hardware required to integrate voice communication channels into a network.  
Example: Voice over IP (VoIP)

---

# DHCP

## Static vs. Dynamic IP addressing

How does a computer know what its IP configuration is?  
Most likely, a computer received its IP configuration from a DHCP server.  

Not only did the server give the PC an IP address, but it also told the PC: 
- where the default gateway was,
- and more than likely, how to find a DNS server.

DHCP stands for **Dynamic Host Configuration Protocol**.  

A computer will receive its IP configuration in one of two ways:
- statically (manually set)
- dynamically (through a service like DHCP)

Static address assignment works fine for very small and stable networks.  
But it quickly becomes unwieldy and error prone as the network grows and more nodes come on to the network. 

## Static IP addressing

- The administrator assigns an IP number and subnet mask to each host in the network.
  Each network interface that is going to be available to connect to the network requires this information
- The administrator also assigns a default gateway lcoation and DNS server location to each host.
  These are required if access outside of the network is going to be allowed (default gateway) and human-friendly
  naming conventions are allowed to find network resources (DNS server).
- Each time a change is made, IP configuration on each host must be updated.

## Dynamic IP addressing

The administrator configures a DHCP server to handle the assigning process, which automates the process.  
The DHCP server listens on a specific port for IP information requests.  
Once it receives a request, the DHCP server responds with the required information.

## How DHCP works

- Upon boot up, a PC that is configured to request an IP configuration sends a **DHCP discovery packet**
- The discovery packet is sent to the broadcast address 255.255.255.255:67 (UDP port 67)
- The DHCP server receives the discovery packet and responds with an **offer packet**
- The offer packet is sent to the MAC address of the computer using UDP port 68
- The computer receives the offer packet from the DHCP server and returns a **request packet**, requesting the proper
  IP configuration to the DHCP server.
- Once the DHCP server receives the request packet, it sends back an **acknowledgement packet** which contains the required
  IP configuration information.
- Upon receipt of the acknowledgement packet, the PC changes its IP configuration to reflect the information received.

## Components and Processes of DHCP

### Ports used

- The computer sends a discovery packet to 255.255.255.255:67
- The DHCP server sends an offer packet to the PC's MAC address on port 68

### Address scope

On the DHCP server, the administrator configures the IP address range with one that is available to be handed out.

### Address reservations

- The administrator reserves specific IP addresses to be handed out to specific MAC addresses.
  These are used for devices that should always have the same IP address (servers, routers, firewalls).
- This allows for these addresses to be changed from a central location instead of having to log in to each device separately.

### Leases

Configuration parameters are only good for a specified amount of time.  
Leases are configured by the administrator.

### Options

- default gateway location
- DNS server addresses
- Time server addresses
- Many additional options

### Preferred IP configuration 

A PC can have a preferred IP address.  
The administrator can configure the DHCP server to either honor this preference or ignore it.

## DHCP Relay

Under the right circumstances, a DHCP server isn't required to reside on the local network segment.  

As a general rule, broadcast transmissions cannot pass through a router.  
But if there's no DHCP server on the local network segment, the router can be configured to be a **DHCP relay**.  

When a DHCP relay (which can also be called an **IP helper**) receives a discovery packet from a node, it will forward  
that packet to the network segment on which the DHCP server resides.  

This allows to reduce the number of configured DHCP servers in a big network (WAN), reducing the amount of maintenance.

---

# Introduction to the DNS service

## DNS servers

**Domain Name System** (DNS) is the process that maps human-friendly names to IP addresses.  
Without it, we would have to memorize numerous IP addresses.  

DNS is hierarchical (very structured) in nature.  
If the local DNS server doesn't contain the needed record, it sends a request up the chain until a positive responses  
is received (which gets passed back down to the original requestor).  
DNS does require a **Full Qualified Domain Name** (FQDN) in order to function.  

**Example**:  
In www.google.com: 
- .com is the top level domain
- .google is the local domain
- and www is the specific service

### Different levels of DNS servers

- **Local DNS server**: the server on the local network that contains the HOSTS file that maps all of the FQDNs to
  their corresponding IP addresses in the local subdomain.
- **Top Level Domain (TLD) server**: the server that the records for a top level domain. Examples include
  .com, .org, .net, .edu, .gov, .mit, .int, etc. Each of these servers contain all of the information for their
  respective domains (kind of). TLD servers do delegate down to second level servers to ease the load. However,
  the TLD server is the server that is responsible for maintaining the records.
- **Root server**: the server that contains the records for the TLD servers.

### Authoritative servers

An authoritative DNS server is the final holder of the IP of the domain you are looking for.  
An authoritative response comes from the DNS server that actually holds the original record.

### Non-authoritative servers

A non-authoritative DNS server is one that responds to a request with DNS information that it received from another DNS server.  
A non-authoritative response is not a response from the official name server for the domain.  
Instead, it's a second or third-hand response (or even further removed).  

In **most cases**, when we send a DNS request, we get a **non-authoritative response**.

---

## DNS records

### A record

Maps a hostname (or FQDN) to its IPv4 address.

### AAAA record

Maps a hostnames (or FQDN) to its IPv6 address.

### CNAME record

Maps a canonical name (alias) to a hostname.  
That means you can have two URLs for a single website.  
This works in part because of the pointer record.

### PTR record

Pointer record that points to a canonical name.  
Its function is to indicate that there is an existing canonical name (alias).

### MX record

Maps to the email server that is specified for a specific domain.  
It's the record that determines how an email travels from sender to recipient.

---

## Dynamic DNS

Dynamic DNS (DDNS) permits lightweight and immediate updates to a local DNS database.  
This is very useful when the FQDN (or hostname) remains the same, but the IP address is able to change on a regular basis.  
It's implemented as an additional service to DNS.

### DDNS updating

DDNS is implemented through DDNS updating.  
DDNS updating is a method of updating traditional name servers without the intervention of an administrator.  
No manual editing or inputting of the configuration files is required.  

A DDNS provider supplies software that will monitor the IP address of the referenced system.  
Once the IP address changes, the software sends an update to the proper DNS server.  

DDNS is useful when access is needed to a domain whose IP address is being supplied dynamically by an Internet Service Provider.  
That way the IP address can change but people can still get to the service that they are looking for. 

---

# Introducting Network Address Translation (NAT)

## The purpose of NAT

**NAT solves the problem of how to route non-routable IP addresses.**  
As a partial effort to conserve the IPv4 address space, the private IPv4 addressing spaces were developed.  
These address spaces were removed from the public IPv4 address space and made non-routable across public IPv4 networks.  

Being non-routable prevents the private IPv4 addresses from communicating with remote public networks.  
NAT very simply solves this problem.  

A router with NAT enabled will translate a private IP address into a routable public IP address.  
When the response reaches the router, it passes the response back to the device that requested it. 

## How NAT works

### The 2 categories of NAT

- **Static NAT (SNAT)**: each private IP address is assigned to a specific routable public IP address.
  This relationship is kept and maintained by the NAT-enabled router.
  
  When a device needs access outside of the local network, the router translates the local IP address to the assigned
  public IP address. When the response comes back, the router will translate the public IP address back into the local one.

  SNAT is not flexible and leads to scalability issues. An individual routable IP address must be kept for every device
  that requires access outside of the local network. As the network grows, you need to increase the amount of public IP
  addresses that are under your control. That can quickly become expensive and complicated.
  
- **Dynamic NAT (DNAT)**: the NAT-enabled router dynamically assigns a routable IP address to devices from a pool of
  available public IP addresses.

  When a device needs access outside of the local network, the router performs the NAT function, only the public address
  comes from a re-usable pool of public IP addresses. Once outside access is stopped, the routable IP address goes back
  into the pool to be reused.

  As initially designed, DNAT was more flexible than SNAT, but still led to some scalability issues.
  As more network traffic requires access to remote networks, the pool of available public IP addresses needs to increase.
   
The solution to these scalability issues is called Port Address Tranlsation (PAT).  
In Cisco terms, that would be "**NAT with PAT**".

### Port Address Translation (PAT)

PAT is a type of DNAT that was developed to increase the scalability of NAT.  

When a local network device requires access to a public network, the NAT-enabled router assigns the public IP address to  
the device with the addition of dynamically assigning a port number to the end of the public IP address.  

The router tracks the IP addresses and port numbers to ensure that network traffic is routed to and from the proper devices.  

PAT still requires a pool of public IP addresses, but the pool may only contain one public address, or it may contain several  
for a large private network.  

This is the preferred method of implementing NAT for two reasons:
- less public IP addresses are required 
- it's easier for admins to maintain

### The NAT terminology

- **inside local address**: a private IP address on the local network, assigned to a specific device.
  | **Example**: 192.168.0.2
- **inside global address**: a public IP address referencing an inside device, assigned to a inside device by the
  NAT-enabled router to allow access from outside of the network.
  | **Example**: 24.113.185.118:1001
- **outside global address**: a public IP address referencing an outside device, assigned to a device that is outside
  of our local network.
  | **Example**: 74.125.28.147
- **outside local address**: a private IP address assigned by our NAT-enabled router to an outside device, on the interior
  of our local network. 
  | **Example**: 192.168.0.1:2002

---

# WAN technologies

## What makes a WAN a WAN, as opposed to a LAN?

As a general rule, if you own and control the line that the data is using to get from one place to another, you are not  
using a wide area network (**WAN**) technology. On the other hand, if you are using a form of transmission that you don't  
own, then you are likely using WAN technology.  

One of the most common physical infrastructures used in WAN technology is the public switched telephone network (**PSTN**),  
due to its widespread availability.

## Public switched telephone network

### Dial-up 

- Utilizes the PSTN to transmit network traffic as an analog signal.
- Requires an analog modem to format the network traffic.
- Maximum theoretical speed is 56 Kbps (not very fast).

### ISDN (Integrated Services Digital Network)

- Digital point-to-point WAN technology using the PSTN
- Completely digital service
- requires the use of a terminal adapter (TA) for the connection to the end node 
- can be implemented as a Primary Rate Interface (PRI) uses twenty-three 64 Kbps B channels and one 64 Kbps D channel
- The D channel is used for call setup and link management
- a PRI achieves 1.544 Mbps speed (T1 leased line)
- most commonly implemented as a Basic Rate Interface (**BRI**) using two B channels and one D channel
- a BRI aciheves 128 Kbps speed
- ISDN is **not as capable as a DSL** (digital subscriber line), but it can often be implemented where DSL cannot be installed

### xDSL

- a digital WAN technology using the PSTN
- requires the use of a digital modem
- dedicated digital line between the end point and a class-5 central office (CO)
- it's only possible within 18,000 feet of the CO (within 5.4 kilometers of a Central Office)
- carries voice and data (filters are put in place so the voice signal can come through without any interference)

### SDSL (Symmetric DSL)

- Synchronous in nature (upload and download speed is the same)
- does not carry voice communications
- if voice service is required, an additional line is needed
- used by businesses that don't need the performance of a T1 leased line, but that do require the symmetrical upload and download speeds

### ADSL (Asymmetric DSL)

- Asynchronous in nature (upload speed is slower than download speed)
- it can carry data and voice
- common upload speed of 768 Kbps with download speed of up to 9 Mbps
- most common implementation of DSL in SOHO environments (Small Office or Home Office)

### VDSL (Very high-bit-rate DSL)

- asynchronous in nature
- used when high quality video and VoIP is necessary
- commonly limited to a download speed of 52 Mbps and an upload speed of 12 Mbps
- only possible when located within 4,000 feet of a CO (within 1.2 kilometers of a Central Office)
- current standard allows for up to 100 Mbps over PSTN. To achieve that, the end point must be within 300 meters of a CO 

## Broadband cable

Broadband cable is **coaxial cable networking**.
- broadband connection to a location delivered by the cable company
- it can deliver voice, data and television, all through the same connection
- **Headend**: all cable signals are received at this point.
- signals are processed and formatted then transmitted to the distribution network.
- **Distribution network**: smaller service areas served by the cable company.
  The distribution network architecture can be composed of fiber optic cabling, coaxial cabling or hybrid fiber-coaxial cabling.
- unlike DSL, the bandwidth of the distribution network is shared by all of those who connect to it, which can lead to increase
  latency and congestion during busy times.
- final distribution to the premise is usually through a coaxial cable
- Data over cable service interface specification (**DOCSIS**): the specifications for how the signal will be received.
  All cable modems and similar devices must measure up to the ISP's required DOCSIS standard. 

## Fiber

- using light to transmit data and voice
- allows for more bandwidth over greater distances
- more expensive to install, but also less susceptible to line noise
- The fiber synchronous data transmission standard in the U.S. is Synchronous Optical Network (**SONET**)
- The international standard is Synchronous Digital Hierarchy (**SDH**)
- SONET and SDH define the base rates of transmission over fiber, which are known as Optical Carrier (**OC**) levels
- Dense Wavelength-Division Multiplexing (**DWDM**) is a method of multiplexing several OC levels (up to 32 channels)
  into a single optical fiber, effectively increasing the bandwidth of a single optical fiber.
- Coarse Wavelength-division multiplexing (**CWDM**) is similar to DWDM but only allows for up to 8 channels on a single fiber
- When fiber optic is delivered to the premise, it's usually done over a Passive Optical Network (**PON**)
- PON is a point-to-multipoint technology thats uses a single optical fiber to connect multiple locations to the Internet
- PON uses unpowered optical splitters

---

## GSM/CDMA WAN connections

All cellular carriers use one of two methods for connecting devices to their networks, and they are not compatible.  

Currently in the United States, AT&T and T-Mobile use **Global System for Mobile** (GSM) to connect their devices to their networks.  
Whereas Sprint and Verizon use **Code Division Multiple Access** (CDMA) as their method of connecting to networks.  

The majority of the rest of the World utilizes GSM as the method of accessing cellular networks.  

### Cellular Networking

Cellular networking involves using a cellular phone system for more than just phone calls.  
- 1G cellular was only capable of voice transmissions
- **2G** cellular added simple data transmission capability (**text messaging**)
- 2G EDGE offered some basic cellular networking connectivity and was a stopgap between 2G and 3G
- **3G** cellular is the beginning of cellular WAN networking
- HSPA+ (Evolved High Speed Packet Access) was a stopgap between 3G and 4G (maximum data rate of 84 Mbps)
- **LTE** (Long Term Evolution) uses an all-IP based core with high data rates. It's compatible with 3G and WiMAX
- **4G** consists of LTE and WiMAX (Worlwide Interoperability for Microwave Access)
- **5G** is the fifth generation of wireless cellular technology, offering higher upload and download speeds, more consistent connections,
  and improved capacity than previous networks.

## WiMAX WAN connections

WiMAX stands for **Worldwide Interoperability for Microwave Access**.  
- WiMAX was originally developed as a last mile alternative for use when DSL or cable was not available.
- It provides an alternative broadband connection to a fixed location
- it uses microwave transmissions as an over-the-air method to transmit voice and data
- it requires a line of sight between relay stations
- it can be used to cover significant distances
- many municipalities are exploring the use of WiMAX as a means of providing reasonably priced broadband to their citizens
- it's often considered to be a type of 4G technology because it is compatible with LTE networks
- but it's not compatible with 3G networks

## Satellite WAN conections

Satellite WAN connections are a type of **microwave satellite networking**.  
- it uses microwave transmisions as an over-the-air method to transmit voice and data
- can be an effective means of extending networks into places that are hard to reach
- **Microwave radio relay** is the method of transmitting data through the atmosphere
- requires a line of sight between relay stations, but can cover vast distances
- the distances covered by the satellite network may lead to latency problems
- a **communication satellite** (comsat) forms part of the microwave relay network
- comsats may use a variety of orbits: Molniya, geostationary, low-polar, or polar orbits are all used for microwave
  radio relay networks
- **Low-polar and polar orbits** are used to boost the microwave signal before sending the signal back to Earth

---

## Metro Ethernet WAN connections

A metro Ethernet connection is when the service provider connects to the customer's site through an RJ45 connector.  
The customers view that WAN connection as an Ethernet connection, while, in reality, the type of connection will be  
dependent on the level of service that has been purchased.  

The service provider may use a variety of WAN technologies behind the scenes, but the customer will only view it as being  
an Ethernet connection.  

Metro Ethernet is commonly deployed as a WAN technology by municipalities at the metropolitan area network (MAN) level.

## Leased line WAN connections

- A leased line is a dedicated circuit (connection) between two end points used for communication.  
- It's usually a digital point-to-point connection.
- a leased line can utilize either a plain old telephone service (POTS) line on the public switched telephone network (PSTN),
  or it can be a fiber optic circuit provided by a telecommunications company.
- leased lines tend to be more expensive for the customer, as the circuit cannot be utilized by any other entity
- most often, the speed is limited by what the customer is willing to pay
- multiplexing technology can be used to increase the amout of channels that are provided on the connection

### PPP

Point-to-Point Protocol (PPP) is a common data link layer (OSI Layer 2) protocol used with leased line networks.  
- PPP can simultaneously transmit multiple layer 3 protocols (for instance, IP and IPX) through the use of control
  protocols (which are specific to the layer 3 protocol being transmitted).
- PPP includes a feature called **Multilink PPP**, which allows for multiple physical interfaces to be bonded together
  and act as a single logical interface, effectively increasing the available bandwidth.

### Types of leased line connections

- **T-carrier**:
- **E-carrier**:
- **Optical carrier (OC) lines**:

## Common standards




---
EOF
