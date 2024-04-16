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
  software called VPN client software.
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




---

@22min

---
EOF

