**Reminder:**
- Layer 1 = Physical (Ethernet/RJ45, bits)
- Layer 2 = Data Link (MAC address, frames)
- Layer 3 = Network (IP address, packets)
- Layer 4 = Transport (TCP/UDP)

>[!note]
>At layer 2, on WAN interfaces we would use another type of encapsulation such as Frame Relay or PPP.

---

# IP is connectionless 

Every IP packet is treated individually and separately by the countless machines that make up the Internet.  
Traffic from one host to another can take different paths, even though that traffic is part of the same conversation or same session.  
This means that the order in which packets arrive at their destination may be very different from the order in which they were sent.  

Therefore, the destination machine requires **a mechanism to reorder the packets** into their original sequence.  

In addition to being connectionless, IP does not guarantee the delivery of packets.  
So there's no guarantee that the packets actually arrive at the destination, or that they arrive in the correct order, or free from errors.  

Higher layer protocols (above layer 3) need to ensure the reordering of packets and their successful delivery to the destination.  

# TCP and UDP

TCP and UDP reside at layer 4 of the OSI model, the Transport layer.  
- UDP stands for User Datagram Protocol  
- TCP stands for Transmission Control Protocol  

Like IP, **UDP** is **connectionless**, it does not guarantee the delivery of packets.  
UDP requires higher layer protocols to ensure the successful delivery of packets.

TCP does provide **delivery acknowledgement** and **reliability**, but with the disadvantage of additional overhead.  
Once the 3-way handshake has taken place, the two parties can exchange data.  

TCP is connection-oriented, and every **segment** transmitted is **acknowledged** by the receiver.  
If a segment went missing, it is **retransmitted**. 

# What is a socket?

It's the combination of:
- the IP address of a host
- the port number used
- the transport protocol used (TCP or UDP)

Sockets are used to identify a connection point.

# TCP and UDP (part 2)

TCP and UDP allow for session multiplexing, which is when a single computer with a single IP address is able to communicate with  
multiple devices and have multiple sessions occur simultaneously.  

A session is created when a source host needs to send data to a destination host. Replies are often received but aren't mandatory.  
The session is created and controlled within the network application which contains the functionality of OSI layers 5 through 7.  

In a **best effort** environment, the settings are very simple. Session parameters are sent to **UDP** which, as we know now, is a best effort  
protocol. Information is just sent to a destination IP address and destination port number. It's important to remember that each  
transmission is a totally separate event, with no memory or association retained between various transmissions.  

When using a reliable service like TCP, a connection must first be established between the sender and the receiver.  
TCP will open a connection and negotiate various connection parameters before actually transmitting any data.  
During data flow, TCP will maintain reliable delivery of the data and will close the connection once complete.

# MTU, MSS and Path MTU Discovery

Information may be segmented for transmission across a network.  
The **maximum transmission unit** (MTU) is the maximum size of an IP packet that can be sent over a link.  
The MTU depends on the physical medium.  

The MTU of FastEthernet is 1500 bytes.  
TCP can theoretically support 65495 bytes in a single packet.  

When data is sent to the lower layers, it will be broken up into fragments for transmission across the physical medium.  
The receiver, using TCP, will need to put those fragments together again.  

The **maximum segment size** (MSS) is the largest amount of data (in bytes) that TCP is willing to send in a single segment.  
For best performance, the MSS should be set small enough to avoid IP fragmentation, which can lead to excessive retransmissions  
if there's packet loss.  

**Path MTU discovery** (PMTUD) is a standardized technique in computer networking for determining the MTU size on the network path  
between two Internet Protocol hosts, usually with the goal of avoiding IP fragmentation.  
Thanks to PMTUD, the sender and the receiver can automatically determine the MTU on a path between them.  
And TCP will only put enough data into a single packet that fits that MTU, thus avoiding fragmentation of packets and the resulting  
overhead associated with fragmentation and the putting together of the IP fragments.  

Path MTU Discovery is optional in IPv4, but has now become mandatory in IPv6, because of the efficiency that it brings to the TCP  
transmissions and the fact that IPv6 does not support fragmentation on routers along the path between two hosts.  

UDP does not support this and requires higher layer protocols to sort out the fragments.  

# Flow Control

TCP uses end-to-end flow control to avoid sending the data too quickly, so the receiver can process the data reliably.  
If the sender transmits the data faster than the receiver can handle it, the receiver will drop the data and require retransmission.  
Retransmissions will waste time and network resources.  

You may as an example have a PC with a powerful CPU sending data to a PDA which can only process data at a much lower rate.  
The PDA should therefore regulate the data flow so it's not overwhelmed.  

With TCP, the flow control is implemented by acknowledgement from the receiver when data has been transmitted.
TCP uses what is called a "**sliding window**" to control the flow of data.  

**Windowing** will allow a receiving computer to advertise how much data it's able to receive before transmitting an acknowledgement  
to the sending computer.  

In each TCP segment, the receiver will specify in the '**receive window**' field the amount of additional data in bytes that it is  
willing to buffer for the connection.  
The sending host can only send up to that amount of data before it must wait for an acknowledgement (ACK) and window size update from  
the receiving host.  

UDP does not implement flow control. And in a **VoIP** environment, as an example, which **uses UDP**, the call will stay up and the  
sender will merrily continue sending huge amounts of data, even though the receiver cannot process the received data.  

**UDP relies on higher layer protocols to implement flow control.**  

---

# Comparison between UDP and TCP

![image](https://github.com/fastoch/Networking/assets/89261095/773b0484-ac3b-4d73-99b2-ad968366732c)

---



---
EOF
