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

ACL example:
![image](https://github.com/fastoch/Networking/assets/89261095/1f441372-184d-4036-b80e-638c7e4bec82)


**What happens if none of our entries match incoming traffic?**  
There's an invisible rule at the end of the list called **the implicit deny**. This will drop the traffic when none of our rules match.  
This rule is written: `deny any any`, and there's no sequence number in front of it.  

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
EOF
