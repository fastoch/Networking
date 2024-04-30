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

---

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

- **T-carrier** (US, Japan and South Korea): each T line circuit level is composed of 24 digital signal channels.
  These are often called Digital Signal 0 (DS0) channels. Each channel is capable of carrying 64 Kbps.
  The 24 DS0s make what is called a digital signal 1 (DS1) channel.
  
- **E-carrier** (Europe): each E line circuit level is composed of 30 digital signal channels.
  These are also called DS0 channels. The 30 DS0 also make up a DS1.
  
- **Optical carrier (OC) lines**: the OC data rates per channel are established by both the SONET (US) and SDH (international)
  networking standards. These rates are the same across the two standards.
  Using dense wavelength-division multiplexing (DWDM) allows for up to 32 separate channels on a single fiber cable.
  Using coarse wavelength-division multiplexing (CWDM) allows for up to 8 separate channels on a single fiber cable.

---

## Common standards (speeds)

**T-carrier lines**: 
- T1 composed of 24 DS0 channels = 1.544 Mbps
- T3 composed of 28 T1 lines = 44.736 Mbps

**E-carrier lines**: 
- E1 composed of 30 DS0 channels = 2.048 Mbps
- E3 composed of 16 E1 lines = 34.368 Mbps
  
**Optical Carrier lines**: 
- OC-1 = 51.84 Mbps
- OC-3 = 155.52 Mbps
- OC-12 = 622.08 Mbps
- OC-48 = 2.488 Gbps
- OC-192 = 9.953 Gbps 

---

## Circuit-switched vs. Packet-switched networks

### Circuit switched networks

- Circuit-switched networks have a dedicated circuit (connection) between two endpoints used for communication.
- While set up, the circuit can only be used for communication between those endpoints.
- An example of this is a phone call using a land line
- Circuit-switched networks are most common in networks with leased line communication
- Best use is when there needs to be a fair amount of continuous data traffic between two endpoints
- There is only one path for the data to take

### Packet switched networks

- in packet switched networks, data is broken up into smaller chunks and moved through the network, only to be
  reassembled at the other end
- data traffic is routed using the destination address
- data may take different paths through the network
- packet switched networks are less expensive since you don't have to maintain a dedicated circuit 24/7

## Frame relay vs. Asynchronous Transfer Mode

### Frame relay

- Frame relay is a WAN technology in which variable length packets are switched across a network
- frame relay is less expensive than leased lines
- can be made to look like a leased line through the use of a virtual circuit (VC)
- frame relay will track a VC using a data link connection identifier (DLCI)
- **access rate**: the max speed of the frame relay interface
- **Committed Information Rate** (CIR): guaranteed bandwidth (may go faster but never slower)

### Asynchronous Transfer mode (ATM)

- ATM is a WAN technology in which fixed length cells (each cell is 53 bytes long) are switched across a network
- ATM can handle real time voice and video
- very fast technology but poor bandwidth utilization (the small cell size reduces the efficiency of the technology)
- common ATM speeds are 51.84 Mbps and 155.52 Mbps 

## Multiprotocol Label Switching (MPLS)

- MPLS is a routing technique that directs data from one node to the next based on labels rather than network addresses
- Whereas network addresses identify endpoints, the labels identify established paths between endpoints.
- MPLS is a scalable and protocol independent
- MPLS can be used to replace both frame relay switching and ATM switching
- it can also be used to packet switch both frame relay and ATM network traffic
- this allows MPLS to be used in conjunction with both frame relay and ATM technologies
- MPLS is used to improve the Quality of Service (QoS) and flow of network traffic
- **Label Edge Router (LER)**: adds MPLS labels to incoming packets if they don't have them
- **Label Switching Router (LSR)**: forwards packets based on their MPLS labels

---

# Network Cabling

## Twisted pair network cabling

Most people are familiar with twistes pair cables, as they are the standard in the modern LAN.  
Twisted pair cables are composed of 4 pairs of wires contained within an insulating sheath.  
Each pair of wires is twisted together to reduce electromagnetic interference (EMI).  
The twist rates differ between the pairs of wires to reduce crosstalk between the pairs (a type of EMI).  
The colors of the pairs are: 
- white orange / orange
- white blue / blue
- white green / green
- white brown / brown

Twisted pair is usually either a straight-through cable, but it can also be used to create a rollover (console) cable.  
- a **straight-through cable** is used to connect **different** types of **devices** together (PC to switch, or switch to router)
- a **crossover cable** is used to connect **similar devices** together (PC to PC, or switch to switch)

A **rollover or console cable** is often required to connect to the console port on a switch or router.  
It's quite common for one end of the rollover cable to use an RJ45 connector, while the other end utilizes an RS232 (DB9) connector.

### Unshielded vs. shielded twisted pair (UTP vs. STP) 

- STP has an additional shield that is either wrapped around each pair of wires or around all four pairs.
- STP reduces the opportunity for EMi or crosstalk, but is more expensive and a little harder to work with
- UTP is much more common than STP

### Plenum vs. non-plenum twisted pair

- most twisted pair is non-plenum grade
- building codes often call for plenum grade cable to be run in plenum spaces*
- plenum cable is jacketed in either a fire-retardant cover or in a low-smoke PVC jacket
- plenum cable often has a polymer or nylon strand woven into it to help take the weight of hanging cables.
  This reduces the chance for the cable to stretch, which can cause the pair inside to break.

*plenum spaces are areas designed to assist in the air flow of a building for HVAC purposes  
*HVAC = Heating, Ventilation, and Air Conditioning

---

## Twisted pair network connectors

### RJ11

- uses a six-position four-contact (6P4C) modular connector
- can carry data or voice; common usage is voice communication (telephony)

### RJ45

- uses an eight-position eight-contact (8P8C) modular connector
- can carry data or voice; common usage is data networking (Ethernet)

### RJ48C

- uses an eight-position eight-contact (8P8C) modular connector
- used as the terminating connector at the demarc for T1 lines
- often confused with an RJ45, but the active pins are different

### UTP coupler

- used to connect UTP cables back to back and still maintain adherence to industry standards

### 66 block

- a punchdown block initially developed to terminate and distribute telephone lines in an enterprise environment
- it was also used in slower speed networks, as it can handle data traffic rated for Cat 3 cabling.

### 110 block

- a punchdown block developed to terminate and distribute twisted pair network cabling
- it's capable of handling the signaling requirements of the modern network

### DB9 (RS-232)

- a 9 pin D-subminiature (D-sub) connector developed for asynchronous serial communication between nodes
- it was a common type of connection between a computer and an external analog modem
- it often makes up one end of the rollover cable (console cable)

### DB25 (EIA-232/RS-232 serial)

- a 25 pin D-subminiature (D-sub) connector developed for asynchronous serial communication between nodes
- it was a type of connection between a computer and an external analog modem

---

## Categories of twisted pair

### Cat 3

- rated for up to 10 Mbps speed, 10BaseT networking.
- max distance of 100 meters

### Cat 5

- rated for up to 100 Mbps speed, 100BaseT networking

### Cat 5e

- rated for up to 1 Gbps, 1000BaseT networking

### Cat 6

- rated for up to 10 Gbps, 10 Gigabit Ethernet (GbE)
- max distance of 55 meters when used for 10 GbE

### Cat 6a

- rated for up to 10 Gbps, 10 GbE
- max distance of 100 meters when used for 10 GbE

---

## Coaxial cabling

- Coaxial cabling is one of the oldest Ethernet cabling standards (1973).
- It's been used for baseband (carries single digital signal)
- it's been use for broadband (carries multiple digital signals)
- it's composed of a central conductor that is covered by an insulating layer, which is covered by an outer metal mesh
  or foil layer that is finished with an outer insulating layer
- the inner metal mesh or foil layer helps to protect against EMI (electro-magnetic interference)

### Coaxial cable types

- **RG58**: 10Base2, max distance of 185 m, 50 ohms impedance, no longer commonly found in modern networks
- **RG59**: commonly used to provide a broadband connection between 2 devices over a short distance
- **RG6**: cable TV or broadband, commonly used to make the connection to cable modems by cable companies

### Coaxial cable connectors

- **BNC** (Bayonet Neill-Concelman): now considered obsolete. Also known as a bayonet connector.
  The connection from the cable to the device was achieved through a twist-lock type connection.
  
- **F connector**: a threaded bayonet connector, 

---

## Fiber optic cabling

- it's relatively expensive and harder to work with
- it resists all form of EMI and cannot be easily tapped
- it can cover long distances at high speed
- most applications require that fiber cables be run in pairs (send cable + receive cable)

The type of connector used on fiber optic cabling can impact the performance of the transmissions:
- The **UPC** (Ultra Physical Contact) connector has a back reflection rating of around -55 dB
- The **APC** (Angled Physical Contact) connector has a back reflection rating of around -70 dB, making it the
  better performing connector.

### Fiber types

**Multimode fiber (MMF)**  
- it uses an infrared LED system to transmit the light
- it uses multiple rays of light going down the cable
- it's used for shorter fiber runs, under 2 km
- less expensive to implement than SMF
- the most common application in networking is MMF 62.5/125µ, which is good for up to 275 m

**Single-mode fiber (SMF)**
- it uses a laser-diode arrangement to transmit the light
- it uses a single ray of light transmitted down the cable
- it's used for longer runs that require high speed
- it can traverse more than 40 km

### Fiber optic cabling connectors

**SC**:
- Subscriber Connector, or Square Connector, or Standard Connector (Stick and Click)
- a push-pull type of connector

**ST**:
- Straight Tip (Stick and Twist)
- a twist lock type of connector

**LC**:
- Local Connector, or Lucent Connector, or Little Connector
- uses a locking tab to secure the connection

**MTRJ**:
- Mechanical Transfer Registered Jack
- a small form factor connector that contains 2 fibers and that utilizes a locking tab to secure the connection

**Fiber optic coupler**: used to connect 2 fiber optic cables back to back.

---

## Media converters 

It's not uncommon to be in a situation where a network contains more than onoe type of cabling.  
This can lead to situations where there's a desire to connect different types of media together in order to  
make a cohesive (or single) network.  

Thankfully, media converters are readily available. The issue mostly comes into play when joining  
fiber optic transmissions to a copper wire infrastructure.  

Some common media converters will connect:
- SMF to Ethernet
- MMF to Ethernet
- SMF to MMF
- fiber to coaxial cabling

## Cabling tools

Every technician should put some thought into the tools that are in his/her toolbox.  
It's often said that you get what you pay for, and that is very true with tools.  
While a good technician can get away with buying the cheapest tools, speding a little more money for a  
better tool can often make a task easier and, ultimately, make the technician more efficient.  

### Crimpers (sertisseuses)

- used to place cable ends on cables
- they can be designed to work with a single type of cable or with multiple types

### Wire strippers (pinces à dénuder)

- used to remove the insulating cover on wires and cables
- many are designed to just cut through the insulation without damaging the cable contained in it
- some are also designed to cut all the way through the cable, so that excess cabling can be trimmed

### The punchdown tool

- used to secure cable wires into **punchdown blocks**
- good ones will trim the ends at the same time
- in many cases, punchdown blocks are used to terminate cable runs in a central location
- often, these blocks are on the backside of **patch panels**

### The cable tester

This tool is used to test cables for common problems:
- misconfiguration of the ends (incorrect pinouts)
- check the cable standard used (T568A or T568B)
- breaks in the cable
- some testers can also test for the cable length and quality, these are called **cable certifiers**

### TDR (time-domain reflectometer)

- a cable tester for copper cabling that can also determine the length of a segment and the electrical
  characteristics of the cable
- they can also tell where a break is in a segment
- more expensive than a standard cable tester

### OTDR (optical TDR)

- performs the same functions as a TDR, but used for fiber optic cabling

---

# Network Topologies

## What is a topology?

It's basically a map that can describe how a network is laid out or how it functions.  
A network topology can be described as either **logical** or **physical**.  
- A logical topology describes the theoretical signal path
- A physical topology describes the physical layout of the network

## Peer-to-peer vs. client/server

### Peer-to-peer model

- nodes control & grant access to resources on the network
- each node is responsible for the resources it is willing to share

### Client/Server model

- network resources access is controlled by a central server or a group of servers
- servers determine what resources get shared, who is allowed to access them, and even when the resources can be used

### Hybrid model

A combination of peer-to-peer & client/server networking.

---

## Network topology models 

The original Ethernet standards established a "**bus**" topology for the network, both logically & physically.  
As time went on, the "bus" developed some mechanical problems. That led to the development of different physical  
topologies, but the logical topology remained the same in order to maintain backward compatibility.  

So when discussing Ethernet networks, **the logical topology is always a "bus"** topology, while the physical topology  
can be different.  

### Bus

- the signal traverses from one end of the network to the other
- a break in the line breaks the network
- the ends of the line needed to be terminated in order to prevent signal bounce
- the network cable is the central point

### Ring

- a bus line with the end points connected together
- a node failure or cable break affects the whole network
- often implemented with 2 rings that counter rotate
- not very common in the LAN anymore, but still used in the WAN (fiber networks especially)

### Star

- nodes radiate out from a central point
- when implemented with a **hub**, a break in a segment brings down the whole bus 
- when implemented with a **switch**, a break in a segment only brings down the segment
- star + switch = **most common implementation of the modern LAN**

### Mesh

- mutliple connections between nodes on the network
- full mesh means that every node has a physical connection to every other node
- partial mesh means that there are multiple paths between nodes
- a **full mesh** topology is **expensive** to install because of the wiring constraints

### Point-to-point

- 2 nodes or systems connected directly together
- 2 computers connected with a crossover cable create a point-to-point topology
- no central device is required to manage the connection
- a common topology when implementing a **WAN** connection 

### Point-to-multipoint

- a central device that controls the paths to all other devices
- differs from a star in that the central device is intelligent
- wireless network often implement point-to-multipoint topologies
- when the WAP (wireless access point) sends data, all devices on the network receive it
- when a device sends data, it is only passed along to the destination
- also a common topology when implementing a **WAN** connection  

### MPLS

- Multiprotocol Label Switching is a topology used to replace both Frame Relay switching and ATM switching
- it's a topology because it specifies both signal path and layout
- it's used to improve the QoS and flow of network traffic
- Label edge router (**LER**) adds MPLS labels to incoming packets if they don't have them
- Label switching router (**LSR**) forwards packets based on their MPLS labels

---

# Network Infrastructure implementations

## Design vs. function

When describing a network, you have a couple of different options.  
Are you going to describe its design or its function?  

If you're going to describe the network's design, then the first place to start is to describe its topology.  
If you're going to describe the network's function, then the first thing to do is to describe its category or infrastructure implementation.  

## Categories of networks

### LAN

- most LANs are encompassed by a single network address range.
- this address range may be broken into subgroups
- each subgroup is called a virtual local area network (**VLAN**)
- LANs can span from a small area (a single room) to a building or a small group of buildings
- LANs tend to be high-speed (1 Gbps or 10 Gbps networking)
- **802.3** (Ethernet) and **802.11** (WLAN, wireless LAN) are **the most common types** of network found in the LAN

### MAN

- larger than a LAN
- most often, it contains multiple LANs
- they are often owned by municipalities
- when a MAN is owned by a private entity, it is sometimes called a campus area network (CAM)

### WAN

- a wide area network spans significant geographic distances
- they can be described as a network of networks
- the best example is the Internet (**inter**connected **net**works)
- as a general rule, if all of the infrastructure implementation has a single owner, then it is not a WAN

### PAN

- extremely distance and size limited
- most often, it's a connection between 2 devices
- common examples include: bluetooth connection, infrared (IR) connection, near field communication (NFC)
- they tend to provide low throughput of data and have a low power output
- as the distance between devices increases, throughput decreases

### Supervisory control and data acquisition (SCADA)

- a type of industrial control system (**ICS**) that is designed to control large scale deployments of equipment.
- The controlled equipment is usually at more than one site
- SCADA is often deployed in energy distribution systems by utility companies
- uses a distributed control system (**DCS**) to communicate with programmable logic controllers (**PLCs**) and/or
  remote terminals to control equipment and processes from a central location
- Theses systems are often proprietary and often require additional training to understand and operate them 

### Medianet

- networks designed and implemented specifically to handle voice and video
- designed and implemented to remove QoS issues (like latency or jitter) that can occur in other infrastructures
- a video teleconference (**VTC**) network is an example of a medianet
- it may be implemented as its own infrastructure or as a sub-infrastructure of a larger network

---

# Introduction to IPv4

## Purpose of IP addressing

When Bob on network A wants to view a Web page hosted on a server on network B, how does his computer know where to send Bob?  
Well somehow Bob has gotten the server's IP address, either in IPv4 or IPv6 format.  
IP addresses are the location of a PC or server, identified as both network location and host location within that network.  

IP addressing provides a logical addressing scheme for our computers so that they can communicate on networks.  
Being logical means that an IP address can be changed with minimal fuss at any time, unlike a MAC address, which is physically  
embedded into the device.  

## IPv4 address properties

As IPv4 is made up of a 32-bit binary number, there are 2³² possible address combinations.  
With all of these possibilities, a process needed to be developed to keep everything neat and tidy.  
The implementation of the **subnet mask** was the answer.  

- 32-bit binary number
- divided into 4 sets of eight bits (called octets or bytes) that are separated by periods
- represented in human friendly format by a dotted decimal format
- requires the use of a mask to determine which portion defines the network and which defines the node
- the subnet mask has the same format as the IP address (32 bits represented in dotted decimal format)

## interaction of IP address and subnet mask

- example: 192.168.1.9 255.255.255.0
- the IP address of the host = 192.168.1.9
- the subnet mask = 255.255.255.0 = /24 in CIDR notation (Classless Inter-Domain Routing)
- in the subnet mask binary notation, all the bits before the first zero define the network portion
- in our example, the network address is 192.168.1.0
- the last octet is reserved to the host portion: from 192.168.1.1 to 192.168.1.254
- in our example, 192.168.1.255 is the broadcast address

---

## Classes of IPv4 addresses

**Internet Protocol version 4** is a binary addressing scheme that is used for networking.  
It was finalized as a standard in **1981**.  

There is an issue though. Because of its structure and the growth in popularity of the Internet, most  
of the world has run out of assignable IPv4 addresses.  

Thanks to some forethought though, it is still a valid scheme today.  

### Class A network address

- address range: 0.0.0.0 to 127.255.255.255
- subnet mask = 255.0.0.0 = /8
- number of addresses available for hosts = 16,777,214 (2²⁴ - 2)

### Class B network address

- address range: 128.0.0.0 to 191.255.255.255
- subnet mask = 255.255.0.0 = /16
- number of addresses available for hosts = 65,534 (2¹⁶ - 2)

### Class C network address

- address range: 192.0.0.0 to 223.255.255.255
- subnet mask = 255.255.255.0 = /24
- number of addresses available for hosts = 254 (2⁸ - 2)

To calculate the number of IP addresses available for hosts, we subtract 2 addresses: 
- one address for the network
- another address for the broadcast

### Class D network address

- address range: 224.0.0.0 to 239.255.255.255
- subnet mask = not defined
- used for multicast communication

### Automatic Private IP Addressing (APIPA)

In some cases, the DHCP process may fail. In these cases, a node will self configure an APIPA address (Windows only).
- APIPA range: between 169.254.0.1 and 169.254.255.254 (/16)

## Public vs. Private IP addresses

### Public IP addresses

- routable
- each must be unique

### Private IP addresses

- non-routable
- 10.0.0.0 to 10.255.255.255 (1 class A license)
- 172.16.0.0 to 172.31.255.255 (16 class B licenses)
- 192.168.0.0 to 192.168.255.255 (256 class C licenses)

## Classless IPv4 addressing

First routing protocols required the class structure, but classes of addresses limited the flexibility of IPv4.  
Classless addressing does not affect the private address space ranges.  

Combining classless addressing and private IP addresses, we were able to slow the exhaustion of IPv4 addresses.  
We have more flexibility because the subnet mask becomes fluid. Therefore, subnetting is now possible and desirable.

### CIDR Notation Example

- 192.168.128.0/23 = subnet mask of 255.255.254.0
- The /23 represents all of the ones in the subnet mask
- network = 192.168.128.0
- host range = 192.168.128.1 to 192.168.129.254 (510 hosts)
- broadcast address = 192.168.129.255

---

## Subnetting IPv4 addresses

### Subnetting cuts the address space into smaller pieces

- provides flexibility in network design
- provides efficiency in address space utilization

### Small office network example

223.15.1.0/24 network = 254 addresses available for hosts (can't use 223.15.1.0 and 223.15.1.255)  
All hosts can get to all other hosts. For security reasons, you want two separate networks.  

You could use 223.15.1.0/25 and 223.15.1.128/25 by subnetting the original address space as follows:
- network 1 host address range: 223.15.1.1 to 223.15.1.126 (broadcast address is 223.15.1.127)
- network 2 host address range: 223.15.1.129 to 223.15.1.254 (broadcast address is 223.15.1.255)

---

# Introduction to IPv6

## IPv6 address structure

IPv6 is the answer to the question: "What do we do about running out of IPv4 addresses?"  

Unlike IPv4, IPv6 will provide enough IP addresses for the foreseeable future.  
Shortly after IPv4's creation and implementation, the Internet Assigned Numbers Authority (IANA)  
realized that the available IPv4 address space would not be enough.  

The IANA then set about creating the replacement and started working on IPv5.  
Soon after that, the IANA determined that it was not going to be sufficient.  
They scrapped IPv5 and began working on IPv6.  

The IANA is confident that IPv6 will function as the replacement for IPv4 for many decades to come.  

### IPv6 is a 128-bit binary addressing scheme

- The 128 bits are grouped together in sets. These sets are separated by a colon.
- each set is 2 bytes long (16 bits)
- for human readability, the binary IPv6 number is converted to hexadecimal
- each hexadecimal number is equal to 4 bits (1 nibble)
- An IPv6 address is 8 sets of 4 hexadecimal numbers

### IPv6 address scopes

The IPv6 addresses fall under three scopes: global, link-local, and unique local.
- Global: An address that has an unlimited scope.
- Link-local: An address with a link-only scope that can be used to reach neighboring nodes attached to the same link.
  This address is automatically assigned to a network interface.
- Unique local: The address scope is limited to a local site or local set of sites. These addresses cannot be routed on the Internet.

### IPv6 local address structure (private)

- the first 64 bits represent the local network
- the last 64 bits represent the host
- the local address structure follows the Extended Unique Identifier format (EUI-64)
- the local address is called the **link-local address** and it always begins with **fe80**

>[!note]
>The 64-bit Extended Unique Identifier (EUI-64) is a special address format that maps device hardware network addresses into IPv6 addresses.
>EUI-64 works by splitting a 48-bit hardware address (MAC address) into two 24-bit parts, inserting a special 16-bit code between them, and
>changing one bit, resulting in a 64-bit interface identifier.
>https://www.catchpoint.com/benefits-of-ipv6/eui-64 

### IPv6 global address structure (public)

- 3 basic parts that make up the address are the routing prefix, the subnet ID and the interface ID.
- the host address is still the last 64 bits (the interface ID)
- the network portion is actually composed of the routing prefix and the subnet
- the number that follows the slash is the routing prefix
- the subnet is composed of the bits between the prefix and the EUI-64 host address
- global IPv6 addresses always begin in the range of **2000 to 3999**

---

In most cases, the need for DHCP has been eliminated.  
When implemented, IPv6 will auto-configure both the local and global addresses.  
These addresses are required to be unique on the networks.  

When a device first comes online, it will use Neighbor Discover Protocol (**NDP**) to discover what the  
required network addresses are, both the local and the global.  
This allows the device to configure its own IPv6 addresses without an administrator's intervention.

---

### IPv6 notation

The 128-bit nature of IPv6 makes it cumbersome to write out and can take up unnecessary space.  
Because of this, some rules were developed to ease the burden and to save space.  
- Leading 0s in a set can be dropped
- any single set of consecutive 0s may be replaced by a double colon

### IPv6 notation example

- original address = 2001:0db8:0000:0000:0000:ff00:0042:8329
- drop the leading 0s = 2001:db8:0:0:0:ff00:42:8329
- remove sets of consecutive 0s = 2001:db8::ff00:42:8329

>[!warning]
>Remember that only one set of consecutive 0s can be replaced with the double colon.
>If you could do it more than once, how would routers and other devices know how many zeros to pad in there?

---

## IPv6 network transmissions

### Unicast

- one-to-one communication: a specific device sends network traffic to another specific device
- unicast can occur on the local network (fe80) or it can occur on the global network (2000 to 3999)

### Multicast

- one-to-a-few communication: a specific device sends network traffic to a specific group of devices that
  have registered to receive that traffic
- routers register to receive multicast transmissions that involve the routing protocols they are programmed to use
- multicast addresses always begin with an **ff**

### Anycast (does not exist in IPv4)

- one-to-the-closest communication: a specific device sends traffic to a specific IPv6 address that has been assigned
  to multiple devices
- the router only sends the data to the closest one
- involves implementing DHCPv6

### DHCPv6

IPv6 is capable of auto-configuring its own local and global addresses. In certain situations, that is not always desirable.  
- DHCPv6 can be configured to hand out specific IPv6 addresses (or duplicate IPv6 addresses) when necessary
- useful for when load balancing a network, or for when network redundancy has been created, or for when you have a user that
  has multiple devices and you want to deliver the transmission to the clsoest device (one that he's currently using)

### IPv6 and IPv4

IPv6 and IPv4 are not compatible, but we can do what's called a **dual stack configuration**.  
In a dual stack config, devices on the network receive both an IPv6 configuration and an IPv4 configuration.  

Or we can use **Tunneling**.  
6to4 tunneling is used to encapsulate IPv6 data packets in an IPv4 datagram, allowing IPv6 packets to travel across  
or through all IPv4 networks.  
6to4 tunneling is can also be called **Teredo tunneling**.

---

# Special IP networking concepts

## The media access control (MAC) address

All networking interfaces come with a special address already configured: the MAC address.  
The MAC address is often referred to as the **physical address** or the **burnt-in address**of the interface.  
While the MAC address may be changed (or **spoofed**), most often it is set by the manufacturer and never changes.  

Switches and other Layer 2 devices rely upon the MAC address in order to get network frames to the correct destinations.

### MAC address format

MAC addresses come in two basic formats that are either 48 or 64 bits in length, and are represented by hexadecimal numbers.  

Both formats can be broken down into two parts:
- the Organizationally Unique Identifier (OUI)
- the Extended Unique Identifier (EUI)

The Institute of Electrical and Electronic Engineers (IEEE) assignes all electronic manufacturers their own 24-bit OUI, which  
makes up the first portion of the map.  

Each manufacturer assigns either a 24-bit or 40-bit EUI to each device that is produced.  

Theoretically, no two interfaces will have the same MAC address.

### EUI-64

IPv6 requires that the node address be in an EUI-64 format.  
If the EUI of the interface is only 24 bits, it is split into two parts, and 16 bits of padding (**fffe**) are added  
to create the EUI-64 format address.

---

## Collision domains vs. broadcast domains

Ethernet networks use a technology called Carrier Sense Multiple Access with Collision Detection (**CSMA/CD**).  

All Ethernet devices have equal access to the network media and are capbable of transmitting data at any time.  
This can lead to data collisions.  

With CSMA/CD, a device listens to the carrier signal on the network media.
- if no other device is transmitting, the device is free to send data
- if another device sends data at the same time, a collision is possible, which can corrupt the data

The devices also listen for collisions.  
If a collision occurs, devices will stop transmitting and wait a random period of time before attempting to transmit again.  
To do this, they use what is called a **back-off algorithm**.

### Collision domains

- A collision domain is an area of the network where network packets can collide.
- a collision can occur when two devices send packets at the same time
- Collision domains are broken up by switches, bridges and routers
- Collision domains are not broken up by hubs

### Broadcast domains

- A broadcast domain = all the nodes that can be reached by a broadcast transmission
- all nodes that can be reached reside in the same network
- broadcast domains cannot pass routers

### Special note

Technically, IPv6 does not use broadcast transmissions.  
IPv6 utilizes multicast instead of broadcast transmissions.

---

## Types of network transmissions

### IPv4 network transmissions

- **Unicast**: a specific source address transmission going to a specific destination address. 
- **Multicast**: a specific source address transmission going to a set of registered destination addresses. 
- **Broadcast**: a specific source address transmission going to all addresses on the local network.

### IPv6 network transmissions

- **Unicast**: the same as IPv4
- **Multicast**: the same as IPv4
- **Anycast**: a specific source address transmission going to a specific IPv6 address that has been assigned to multiple devices.
  The router uses an algorithm to determine which MAC address is the closest and only that device receives the anycast transmission.

---

# Introduction to routing concepts

## The purpose of routing

In a nutshell, the purpose of routing is to interconnect different networks to allow them to communicate and exchange data.  
Most often, routing protocols are how networks determine where to send data traffic (the routes that will be taken).  
They build maps (routing tables) that they use for directing network traffic.  

Routing is what makes this interconnected world function as well as it does. Networking would be pure chaos without it.

## Basic routing concepts

### Static routing

- uses administrator-defined routes
- in a static routing configuration, each router must contain the route
- a static route from A to B requires that B has a static route to A
- easy to set up in a small network, not so easy to maintain
- routes only change when the admin changes them

### Dynamic routing

- routers use protocols in order to determine the best route between two networks
- The admin determines which protocols will be in use
- The routers must all use the same protocols. An exception is when route redistribution has been implemented.
- Dynamic routing protocols can be stacked within a router
- Dynamic routing is very fluid and is what makes possible today's interconnected world

>[!information]
>Route redistribution is when an admin configures a router to take one dynamic protocol and transform it into a different
>routing protocol to be used from that point on.

### The default route

This is the direction that a router will send network traffic when there is no known route in the routing table.  
- It is assigned by an admin
- It's usually a designated interface on the router, or it's the designated next hop interface

### The routing table

It's a list of the known routes to all known networks from the router's perspective.
- It's established by an admin when static routing is used
- It's dynamically built by routing protocols when dynamic routing is employed

Each routing protocol maintains a routing table.  
Different routing protocols may have different routes to the same network.

### The loopback interface 

It's an administratively configured logical number assigned to a router to ease administrative functions or routing processes.  
- Often, the loopback interface is assigned in an IPv4 address format
- many routing protocols have been designed to take the loopback interface into account when performing administrative functions.

The interface may be completely logical, or a physical interface may be configured to be the loopback interface.

### Routing loops

A possible problem that can be created if interconnected routers have a breakdown in their routing algorithms.
- When a routing loop occurs, the network keeps looping through the routers until some system or mechanism breaks the cycle.
- Routing loops can create network congestion or even bring down a network

Routing protocols use multiple methods to prevent loops from occuring.  
The time to live (TTL) is also utilized to stop routing loops after they have occurred.

---

## Routing metrics

There may be more than one route available to a remote network. Routing protocols use metrics to determine the best route.  
Each routing protocol will use its own set of metrics in determining which routes to which networks are placed in its routing table.  

The same basic metric may be used by different routing protocols. When this occurs, the metric is usually implemented in  
a different manner through the use of different algorithms.  

### Hop count

The number of routers between two endpoints, determined from the sending router's perspective.  

### Maximum transmission unit (MTU)

The maximum allowed size of a packet, measured in bytes.  
The standard MTU for Ethernet is 1500 bytes.  

Packets that exceed the MTU must be fragmented, leading to more packets, leading to slower connection.

### Bandwidth

A measure of the speed of the network connection. Can be measured in Kbps, Mbps, or Gbps.

### Latency

A measure of time that a packet takes to traverse a link.  
When implemented by routing protocols, the total amount of latency (or delay) to go end to end between two points is used.

### Administrative Distance (AD)

- Probably the most important metric that's used on routers.
- AD is the believability of a routing protocol's advertised routes.
- Some routing protocols are considered to be more believable (trustworthy) than others.
- Routers use the AD to determine which routing protocol to use when more than one is installed on the router.
- The lowest AD of an advertised route will determine the protocol used

**Common standard ADs**:
- directly connected route = 0 (no protocol required)
- statically configured route = 1 (no protocol required)
- **EBGP** = 20 (exterior border gateway protocol)
- **internal EIGRP** = 90 (enhanced interior gateway routing protocol)
- **OSPF** = 110 (Open shortest path first)
- **IS-IS** = 115 (intermediate system to intermediate system)
- **RIP** = 120 (routing information protocol)
- **external EIGRP** = 170
- **IBGP** = 200 (interior border gateway protocol)
- unknown = 255 (not believable)

The AD can be set by an administrator, so that a specific protocol is preferred to another. 

---

## Route aggregation

Without some mechanisme put in place, routing tables soon become very large and highly inefficient.  
Through careful planning, network administrators use a process called **route aggregation** to condense the  
size of routing tables. They do so through the use of Classless Inter-Domain Routing (**CIDR**) to summarize  
routes to different networks. Route aggregation is common in networking.  

### Example of route aggregation

Suppose we have a router that has the following networks connected to its serial 0/1 interface (S/0/1):
- 10.1.1.0/24
- 10.1.17.0/24
- 10.1.32.0/24
- 10.1.128.0/24

These routes could be summarized (aggregated) by a common CIDR entry in a routing table:
- 10.1.0.0/16

### Warning on route aggregation

Route aggregation takes careful planning during the network design phase.  
The above example would not work if interface s/1/1 on the same router was connected to network 10.1.2.0/24, because  
that new network makes those networks on the 0/1 interface **non-contiguous** networks.

---

## High availability

Part of a network administrator's job is to ensure that networks remain up and active at all time.  
In an effort to ensure that networks don't go down, admins often remove single points of failure (SPoFs).  
A single point of failure in a network is the point where a single failure will cause the network to cease functioning.  

Network admins often use high availability techniques in order to remove thos single points of failure.  
An example of such a technique is the use of redundant links to outside networks.

### Hot Standby Router Protocol (HSRP)

- a proprietary Cisco method of creating a fault tolerant link using two or more routers.
- The involved routers are connected together as well as having connections outside of the local network.
- a **virtual IP address** is created and shared between the routers
- devices on the network are configured to use the virtual IP address as the default gateway for packets leaving the network
- if a router goes down, the link outside of the network is still available

### Virtual Router Redundancy Protocol (VRRP)

It's an IETF (Internet Engineering Task Force) standard that is similar in operation to HSRP.  

---

# Introduction to routing protocols

## Interior vs. exterior gateway routing protocols

### Interior Gateway Protocol (IGP)

- IGPs are a category of protocols used within autonomous networks.
- Autonomous networks are networks that are under the control of a single organization.
- The most popular IGPs are **OSPF** and **RIPv2**
- **IS-IS** is popular with extremely large autonomous networks like an ISP's network (Internet Service Provider)

### Exterior Gateway Protocol (EGP)

- A category of protocols used between non-autonomous networks
- The type of routing protocol used between networks that are controlled by different entities
- The most popular EGP is **BGP** (Border Gateway Protocol)

### Autonomous Networks

It's not uncommon for organizations to have several networks between which they are routing traffic.  
These are called autonomous networks.  

Some IGPs use an administrator-defined autonomous system (**AS**) number as one means of identifying which  
networks can directly communicate with each other.  

The AS is not a metric, but a means of identifying a network that might possibly accept another network's traffic.  
Remember, the AS is only significant withing autonomous networks and has no relevance outside of them.

---

## More routing concepts

### Classification of routing protocols

- IGP and EGP routing protocols can be broken out into three other categories of protocols, which is designated
  by their main method of determining routes between networks.
- **Distance-vector** routing protocols: routes are determined by how many routers exist between the source and
  the destination. The efficiency of the links in the selected route is not taken into consideration.
  Periodically, the whole routing table is broadcasted.
- **Link state** routing protocols: metrics are used to determine the best possible route between destinations.
  The protocol then only monitors the state of directly connected links and only makes changes when changes to
  links occur. Only changes in link status are broadcasted.
- **Hybrid** routing protocols: use aspects of both the distance vector and link state routing protocols.

### Next hop

The next router in the path between two points.  
It's often designated by an interface address of the device that is receiving the data, or by the router's name,  
or by the router's location.

### Routing table

The database table that is used by a router to determine the best possible route between two points.  
Different routing protocols use different algorithms to place routes in the table.

### Convergence (steady state)

The amount of time that it takes all of the routers in an autonomous system (AS) to learn all of the possible  
routes within that system.

---

## Routing protocols

### Routing Information protocol v2 (RIPv2)

- An IGP (autonomous) distance-vector protocol.
- A hop count of 16 is considered unreachable
- RIPv2 uses various methods, including hop count to reduce the chances of a routing loop
- uses multicast to advertise routing tables (224.0.0.9)

### Open Shortest Path First (OSPF)

---
EOF
