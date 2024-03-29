When a PC is connecting to a web server, traffic will be sent from a source IP address to a destination IP address.  
When the traffic arrives at the server, the server needs a way to "decide" which application to send this traffic to.  

**Well-known port numbers** are used for various every day applications, like HTTPS.  

The source will use a random port number in a specific range, depending on the OS and whether the IANA standards are followed.  
And a well-known port number is used as the destination.  

## Well-known ports

Those port numbers are in the range <= 1023.

- HTTP uses port 80 and TCP as its transport layer protocol
- HTTPS uses port 443 and TCP 
- FTP uses port 21 and TCP (for server and client negotiation)
- FTP Data uses port 20 and TCP (for the actual transmission of data)
- Telnet uses port 23 and TCP
- DNS uses port 53 and both TCP and UDP
- TFTP uses port 69 and UDP
- SNMP uses port 161 and UDP
- 

---
EOF
