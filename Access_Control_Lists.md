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

We're still using the same topology (see VLAN_Trunk_Links.md) with 2 VLANs:
- VLAN 10 for workstations, subnet 192.168.10.0 /24
- VLAN 20 for servers, subnet 192.168.20.0 /24
- A router configured as Router on a stick (ROAS) to pass traffic between the 2 subnets
  
![image](https://github.com/fastoch/Networking/assets/89261095/47ebd45f-d0e8-4529-956f-ac9f8761a9d3)

Right now, all traffic is allowed between these subnets, but we want to restrict this a bit.  

**Goal #1**:
- block regular HTTP traffic to the servers
- allow https traffic to the servers
- block all other traffic to the servers

**Goal #2**:
- allow the servers to SSH to the router
- don't let the workstations SSH to the router
- prevent telnet to the router from any location
- do not block any other IP traffic to the router

The starting configuration has already been done, so we won't need to worry about that.  

To block HTTP traffic to the servers, we'll use the **access-list** command to configure a **numbered ACL**.  
Onto the router:
```
conf t
access-list ?
acces-list 150 ?
access-list 150 deny ?
access-list 150 deny tcp ?
access-list 150 deny tcp any ?
access-list 150 deny tcp any 192.168.20.0 0.0.0.255 eq www
```
`access-list ?` shows us the different ranges we can use and the corresponding types of ACL  
150 is for an extended ACL  
HTTP uses TCP  
eq = equals, other operators are gt (greater than), lt, range, etc.  
www could be replaced with 80 since HTTP uses port 80

Syntax is: `access-list number protocol source destination operator port`  
The above ACL denies http traffic from any source when destination address is 192.168.20.x and port number is 80.  

>[!tip]
>Use the **question mark** as often as needed. It shows you the available options for completing your command.

Our first entry is done. We can check this with `do show access-lists`.  
We use the `do` keyword to be able to run this cmd from within the config mode.  

We have one ACL #150 with a single entry. This is good, but our ACL is not done.  
We now need an entry to allow HTTPS traffic:  
`access-list 150 permit tcp any 192.168.20.0 0.0.0.255 eq 443`  

While we're at it, we can add a **remark** to the ACL.  
A remark is just a comment that makes it easier for us to understand what we've configured later.  
`access-list remark WORKSTATION-ACL`  

We now have 2 entries for our ACL:  
![image](https://github.com/fastoch/Networking/assets/89261095/248bd71a-b1c1-43a5-ac97-cd31befc7e88)  
The new entry has been added to the bottom of the list.  

Lastly, we have to block all other traffic to the servers.  
Although it's not shown as an entry in our list, there is that **implicit deny** rule at the end.  
Any traffic that we haven't matched in our ACL will automatically be blocked.  
**In fact, we don't even need a rule to block HTTP, but it can be handy as we'll see soon.**  

We still need to apply this ACL to an interface.  
In this case, gi 0/1.10, the interface that connects vlan 10 (workstations) to the router.  

Onto the router:  
```
conf t
int gi 0/1.10
ip access-group ?
ip access-group 150 ?
ip access-group 150 in
```

To verify this: `do show ip interface gi 0/1.10`  
Look for the outgoing and inbound access list entries:  
![image](https://github.com/fastoch/Networking/assets/89261095/44746483-690e-4a7a-bbe4-fdff4348a312)

Over on the workstation, we can use the following Linux command to try to retrieve a web page from the server:  
`curl 192.168.20.1:80` it fails because HTTP traffic is blocked ("no route to host")  
`curl 192.168.20.1:443` it fails because the server doesn't have a web page, but the traffic is reaching the server this time

A ping from the workstation to the server would not get a response either, as the traffic isn't getting past the packet filter.  
That's because of the implicit deny rule at the end of our ACL.  

**We didn't block pings on purpose**, which shows that applying ACLs can sometimes lead to unwanted results.  
So, it's really important that we **test our changes thoroughly** before pushing our new config to the running config.  

If we take another look at our ACL on the router with `do show access-lists`, we can see that each rule now has 1 match.  
This is a result of the traffic that we've just generated with our previous `curl` commands.  
This is another way to see that our ACL is working.  

You'll notice though that there's **no match counter for the implicit deny rule**.  
**This is one reason why sometimes it's useful to create a deny rule like we did for HTTP.**  

As we already mentioned, each rule in our ACL starts with a sequence number. In our case, it's 10 and 20.  
These numbers show the order the rules are evaluated in.  
We can give rules specific sequence numbers.  
But if we don't, Cisco IOS will automatically assign numbers like it has done here.  

---

Let's move on to **Goal #2**, where we only allow SSH from the servers and not the workstations.  

If we try to SSH to the router on a workstation, you can see that part of our job is already done:  
`ssh cisco@192.168.10.254` > "no route to host"  
The ACL we've already configured is already (implicitly) denying SSH to the router.  
This is the same implicit rule that will also blog ping and telnet.  

To block telnet and allow ssh from the servers, we need to create a new ACL.  
We'll then apply this ACL to interface Gi 0/1.20.  

For some variety, we'll configure this one as a **named ACL**.  
Named ACLs are configure with `ip access-list`.  
Onto the router:
```
ip access-list ?
ip access-list extended ?
ip access-list extended SERVER-ACL
deny tcp any ?
deny tcp any host ?
deny tcp any host 192.168.20.254 eq telnet
```
After the 3rd line, we enter the named-ACL subconfiguration mode. The prompt becomes (config-ext-nacl).  
We deny telnet traffic from any source to the router (host) only on specified IP (the router's IP on vlan 20, the gateway).  
To simplify things, we use the 'host' keyword as the destination and enter our single IP address.  
This means we don't need to worry about a wildcard mask (wildcard masks are only required when there are several IP addresses).  

Now we can add a rule to allow ssh to the routers from the servers:
```
permit tcp 192.168.20.0 0.0.0.255 host 192.168.20.254 eq ssh
```








---
EOF
