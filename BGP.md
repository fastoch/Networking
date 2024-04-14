# Boarder Gateway Protocol

BGP is an **Exterior** Gateway Protocol.  

We use the term **Autonomous System** (AS) to describe a network under a single administrative control.  
Your company might have its own Autonomous System.  
You connect out to a service provider that is in its own AS.  
And for redundancy, you connect out to another service provider that also is in its own AS.  

When you're **routing between Autonomous Systems**, that's where you need an Exterior Gateway Protocol.  
BGP is the one that's in use today.  

Much like OSPF and EIGRP, we do form neighborships.  
But what is different in some cases is we need to specify the IP address of our neigbor.  

Something else that makes BGP unique is that it establishes a TCP session between neighbors, which is uncommon for  
a routing protocol. Specifically, it uses TCP port 179.

---
EOF
