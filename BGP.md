# Boarder Gateway Protocol

## Autonomous Systems 

We use the term **Autonomous System** (AS) to describe a network under a single administrative control.  
Your company might have its own Autonomous System.  
You connect out to a service provider that is in its own AS.  
And for redundancy, you connect out to another service provider that also is in its own AS.  

When you're **routing between Autonomous Systems**, that's where you need an Exterior Gateway Protocol.  
BGP is the one that's in use today.  

## BGP characteristics

- **Exterior** Gateway Protocol
- Forms neighborships
- Neighbor's IP address is **explicitly** configured
- Establishes a **TCP session** between neighbors on port 179, which is uncommon for a routing protocol
- Advertises address prefix and length (called Network Layer Reachability Information or NLRI)
- Advertises a Collection of Path Attributes used for path selection



---
EOF
