# Understanding ACLs

## Introduction

Sometimes we need to control or influence traffic that flows through our network.  
Maybe we want to restrict access to some sensitive resources, or limit the amount of non-business traffic to conserve bandwidth.  
In either case, we need to use Access Control Lists, also known as ACLs.  

ACLs are a versatile tool which can be used for many different purposes.  
But while they have many uses, their most obvious function is as a **packet filter**, that is to allow or deny traffic.  
Packet filters add security to the network.  

Perhaps we want to limit the workstations that are allowed to log on to routers.  
Or maybe we want to allow only HTTPS traffic to a server.  
We can use ACLs in bothe cases, to allow some traffic but to deny others.

---

## Anatomy of an ACL

An ACL is really a collection or a list of rules.  
Each of the rules is called an **Access Control Entry** or **ACE**, and is used to permit or deny traffic.  

Each entry in the list is evaluated **in order** from the top to the bottom.  
Every entry contains some match criteria. This may include information like:
- source address
- destination address
- protocols (such as TCP & UDP)
- port numbers

When a packet comes into a router, the router looks at the information in the packet header.  
It will compare this against each entry in order to see if it matches any of the rules.  
If the router finds a match, it will then look at the action. The simplest actions are permit and deny.  
Obviously, if the action is 'permit', the traffic is allowed through. Else, it will be blocked.  

There's a number next to each entry, it's called **the sequence number**.  
This number determines the order the rules are evaluated in. 

As soon as in incoming packet matches one of these entries, the action is applied.  
At this time, the router stops evaluating more rules. The **keypoint** from this is that the **first match wins**.  
So when you create ACLs, it's essential to consider the order of the rules, otherwise you may not get the expected results.  

**What happens if none of our entries match incoming traffic?**  
There's an **invisible rule** at the end of the list called **the implicit deny**.  
This rule will make the router drop the traffic when none of our rules match.  
This rule is written: `deny any any`, and there's no sequence number in front of it.  

**When no ACL is configured on an interface, all the traffic is allowed.**

---

## Wildcard masks

A subnet mask uses binary ones and zeros to determine which part of an IP address is the network and which part is the host.  

A wilcard mask is used to match IP addresses.  
The zeros refer to the parts of the address that need to match the address in our rule.  
The ones are the parts that don't need to match.  

For example, if our IP address is 192.168.10.0 and our wildcard mask is 0.0.0.255, this means that we're looking for  
any IP address that starts with 192.168.10.  

**Why can't we use a subnet mask instead?**  
A subnet mask requires all the ones and the zeros to be grouped together.  
A wildcard mask does not have any such restriction, which means we can perform some advanced matching by mixing up the bits which are turned on or off.  

Here's a more complicated example: 10.22.32.0 with a wildcard mask of 0.0.15.255  
Matching addresses go from 10.22.32.0 to 10.22.47.255  
You can check on https://subnetonline.com/pages/subnet-calculators/ipv4-wildcard-calculator.php  

---

## Types of ACLs

Example of an extended ACL:
![image](https://github.com/fastoch/Networking/assets/89261095/1f441372-184d-4036-b80e-638c7e4bec82)

There are many types of ACLs, each having a different functionality:
- standard
- extended
- dynamic
- IP-named
- reflexive
- time-based
- commented IP
- context-based
- turbo
- distributed
- receive
- infrastructure protection
- transit

The **standard** ACL can only match based on source address. This is the first one that Cisco created.  
It can't look at the destination, the protocol or the ports used.  

### Numbered ACL

One way we can configure ACLs is to give them a number.  
We configure each entry individually, and any entries sharing the same number are part of the same ACL.  
This number also determines if this is a standard or extended ACL, as you can see in this table:
![image](https://github.com/fastoch/Networking/assets/89261095/14dd45a4-57f3-40a2-9676-084b1a6275aa)

Aside from picking a number in the right range, no particular number is any better than any other number.  
They just act as labels to organize the entries into a list.  

### Named ACL

The more modern (and recommended) alternative to numbered ACLs is **named ACLs**.  
Every list has a name and acts like a container. Entries are nested inside the container.  

In addition, there's no ranges or numbers to worry about.  
During configuration, we simply tell the router if this a standard or extended ACL.  

On its own, an ACL does nothing. We must tell the router that we want to use the ACL as a packet filter.  
So we need to apply the ACL to one or more of the router's interfaces.  

When we **apply an ACL to an interface**, we also have to apply it in a **direction**.  
There are 2 directions called **ingress** and **egress**.  
- ingress is when traffic is coming into the router
- egress is when traffic is leaving the router

**There can only be one ACL per interface per direction.**  

---

## Lab

We're still using the same topology with 2 VLANs:
- VLAN 10 for workstations, subnet 192.168.10.0 /24
- VLAN 20 for servers, subnet 192.168.20.0 /24
- A router configured as Router on a stick (ROAS), 
- 



---
EOF
