## What's a network?
A system that allows multiple devices to communicate with one another.

---

## Vocabulary

**Port mural** = wall socket  

**Baie de brassage** = patch panel  

Each wall socket that we plug a computer into connects back to one of the ports available on the patch panel.  
We can then connect each of these ports directly into the switch.  

---

## Protocols

802 = LAN technologies  
>802.3 = Ethernet

---

## The OSI model

The OSI model is not about specific technologies, but rather how they fit into the network stack.

- Application
- Presentation
- Session
- Transport
- Network
- Data Link
- Physical

>[!tip]
>Please Do Not Throw Sausage Pizza Away

Imagine that we have an application on one host that needs to send data to an application on another host.  
Let's now see how this data moves through the OSI model.  

The data starts at the **Application** layer. This is where network APIs and apps that access the network live.  
For example, this includes FTP and web browsing.  

The data needs to be in a format that can be easily undesrtood. That's what the **Presentation** layer is for.  
Anything related to data formats lives here. This layer is responsible for data conversion and formatting.  

The **Session** layer tracks application processes. This includes remote procedure calls and service requests.  
Think of this layer as building a session between a local application and a remote one.  

**What if the data you're transferring is very large?**  
What happens if you get right to the end of the transfer and the connection is interrupted?  
You would have to start the whole transfer again.  
Also, any application that wants to use the network would to wait until this transfer is complete.  

Fortunately, when the data reaches the **Transport** layer, it is broken into manageable chunks.  
Now, if there's a problem, only one chunk of data needs to be re-sent, not the entire file.  
Also, apps can take turns at sending chunks of data, rather than one app hogging the hosts ressources. This is called **multiplexing**.  
If we're using TCP, each block of data is called a "**segment**". If it's UDP, each block is called a "**datagram**".  

We have many blocks of data probably going to different hosts for different applications.
**So how can we track what goes where?**  
The answer is: through **port numbers**.  

Each flow of data has a port number associated with the source and destination host.  
These values are added as part of a **header** to each block of data.

In order to successfully transfer our data, we need to add more information, we call this **"metadata"**.  
Metadata is **"data that provides information about other data"**.
Adding the source and destination address is an example of this.  
Any information we add to the front of our data is called a **header**.  
Any information we add to the back of our data is called a **trailer**.  

To send information from one host to another, we need some form of addressing.  
The **Network** layer adds IP addresses to **packets** of data.  
This is required to properly **route** the data and deliver it to the remote hosts.  
IP stands for **Internet Protocol**.  
This layer adds another **header** that includes source and destination IP addresses.

Now, we need to think about getting the data from one device to another. This is where the **Data Link** layer comes in.  
This layer does not try to get data to the end device, that's the responsibility of layer 3 & 4.  
The Data Link layer creates a logical link between devices on the same network segment.  
We need to have a **logical link** as devices probably aren't directly connected.  
They're usually connected with a shared medium like a **switch** or over Wi-Fi.

Eventually, the data reaches the **Physical** layer, where it is transmitted over cable or wireless to the remote host.  
The remote host receives the data at the physical layer. The process is then **reversed**. The data flows back up through the layers.  
Each layer does its job, removing headers and trailers, and converting the data until it is in a form that the application can understand.  

Each layer will only communicate with the layer above and the layer below.  
Each layer has its own purpose and doesn't get involved with other layers, other than to pass and receive data.

---

### Let's take a closer look at what each layer does

#### Application
Developers spend a lot of time in the upper layers (application, presentation and session).  
This starts with the **application** layer. This is not strictly the application itself, but rather how the app accesses the network.  
Some examples of this include web browsing, accessing emails and transferring files. It also includes management sessions like SSH and RDP.  

#### Presentation
The app may contain a lot of data. This data does not always make sense to the rest of the network.  
The **presentation** layer helps by converting the data if needed. This conversion also includes services like encryption and compression.  
File formats also live here, including images and video files.  

#### Session
An app needs to talk to several endpoints. So it's important to track where these conversations are occurring.  
Each of these conversations is called a **session**.

#### Transport
The transport layer is used to transport traffic between processes on to endpoints.  
You've probably heard of TCP and UDP, these are the most common protocols used at this layer.  
Earlier, we were talking about how data needs to be broken into manageable blocks (segments or datagrams).  

#### Recap
- The upper layers (application, presentation, session) deal with raw data.
- The Transport layer breaks the data into smaller blocks of data and adds a first header that contains source and destination ports.  
- The Network layer adds a second header which contains source and destination IP addresses. Each block of data is now a **packet** .
- The Data Link layer adds another header that includes source and dest MAC addresses.
- A trailer may also be added with error correction information.
- Once the header and trailer are added, this block of data is now called a **frame**.
- As data moves across the network, it will pass through one or more routers.
- As each of these routers are a separate device, the destination layer 2 addresses (MAC) will change with each hop.
- But the destination layer 3 address (IP) will remain the same.
- And finally the **physical** layer which manages physical network components (radio frequencies, pulsing light, electrical signals)
- The physical layer is responsible for encoding data into physical signals. 

The **Data Link** layer is special, as it contains **2 sublayers** = LLC and MAC.  
The **Logical Link Control** sublayer is responsible for translating between the network layer and the data link layer.  
The **Media Access Control** sublayer is responsible for adding headers and trailers to packets, creating **frames**.  
The MAC is also responsible for error correction.

---

## CIDR

**Classless Inter-Domain Routing**. This method was invented in **1993**, it is pronunced "CIDER".  

CIDR introduced a new concept: the **subnet mask**. The subnet mask, just like the IP address, is made up of 4 octets.  
In the subnet mask, the bits set to 1 tell us which part of the IP address is for the network.  
Therefore, the bits set to 0 tell us which part of the IP address is for the hosts.
All the 1 bits go on the left, and all the 0 bits go on the right.  

The real power of CIDR is the ability to break a large network into small ones. We call this **subnetting**.  

### CIDR notation

a subnet mask of /24 = 255.255.255.0 = 11111111.11111111.11111111.00000000  
a subnet mask of /28 = 255.255.255.240 = 11111111.11111111.11111111.11110000

### VLSM

Variable Length Subnet Mask

initial network = 172.16.0.0 /16
we break it up into 256 networks with a /24 mask

let's say we have 3 offices:
- 172.16.1.0 /24
- 172.16.2.0 /24
- 172.16.3.0 /24

Those offices are interconnected (WAN links) via their router, these 3 routers also form a small network
we could put each pair of routers into a subnet: 
- 172.16.200.0 /30
- 172.16.200.4 /30
- 172.16.200.8 /30

A /30 network uses 30 bits for the network and 2 bits for the hosts, which leaves us exactly 2 IP addresses.
Remember that 2 IP addresses are always reserved and cannot be allocated to any device:
- the network address (.0)
- the broadcast address (.255)

---

## IP adresses 

- IP addresses are managed by an organization called "The Internet Assigned Numbers Authority" (IANA).  
- IANA assigns large blocks of addresses to sub-organizations called "Regional Internet registries" (RIRs).
- RIRs assign blocks of IP space to ISPs (Internet Service Providers) and large customers.
- ISPs give adresses to smaller customers.  

In 1996, to prevent the shortage of IP adresses, the **RFC 1918** was released.  
This RFC says that some **IP spaces are now reserved for private use**.
- 10.0.0.0 /8
- 172.16.0.0 /12
- 192.168.0.0 /16

All other IPs are **public**.  
RFC = Request For Comments = standards that describe how certain Internet technologies work.

---

## Switching

---

## Routing



