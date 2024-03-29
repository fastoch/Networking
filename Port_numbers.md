When a PC is connecting to a web server, traffic will be sent from a source IP address to a destination IP address.  
When the traffic arrives at the server, the server needs a way to "decide" which application to send this traffic to.  

**Well-known port numbers** are used for various every day applications, like HTTPS.  

The source will use a random port number in a specific range, depending on the OS and whether the IANA standards are followed.  
And a well-known port number is used as the destination.  

## Well-known ports

Those port numbers are in the range <= 1023.

- HTTP uses TCP port 80 
- HTTPS uses TCP port 443 
- FTP uses TCP port 21 for server and client negotiation
- FTP Data uses TCP port 20 for the actual transmission of data
- Telnet uses TCP port 23
- DNS uses TCP or UDP port 53 
- TFTP uses UDP port 69 
- SNMP uses UDP port 161 
- DHCP uses UDP port 67 on the server side and UDP port 68 on the client side
- 

---
EOF
