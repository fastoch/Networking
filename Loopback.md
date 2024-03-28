# What is a loopback? Why is it used?

A loopback interface is a logical interface that typically only has one IP address.  

You can create many loopbacks. For example: `interface loopback 0`  
As soon as I create this logical interface, it comes up.  

I can then give that interface an IP address: `ip address 2.2.2.2 255.255.255.255`  
Notice that the subnet mask is /32, which means this is the only IP address on that interface.  

The first advantage of a loopback interface is that it doesn't go down unless you explicitly shut it down.

On a router, if for some reason an interface goes down, you can't use it anymore for a telnet connection.  
However, if you have a loopback interface, and you advertise that loopback through a routing protocol such as OSPF or EIGRP,  
you can always telnet to that loopback and manage the device from there.  

---

# Loopbacks for managing network devices - EIGRP

First, you need to enable EIGRP on each router of your network: 
```
conf t
router eigrp 100
network 0.0.0.0  
```

Check config with `sh ip eigrp neighbors`  

Once the neighbor relationships have been established, each router can ping the loopback of other routers.  
And now you can telnet from one router to another using their loopback.  

From a management point of view, it's a lot easier to use loopbacks.  

Imagine 3 interconnected routers, each having a loopback address: 1.1.1.1/32, 2.2.2.2/32 and 3.3.3.3/32  

To check routes between our routers: `sh ip route`  
If routes exist but telnet is not working ("connection refused by remote host"), check virtual connections:  
`sh run | begin vty`  

if transport input is set to none:
```
conf t
line vty 0 4
transport input all
```

Now you should be able to telnet into the remote router.

>[!tip]
>The abstract “0 4” means that the device can allow 5 simultaneous virtual connections which may be Telnet or SSH

In the real world, it's a good idea to have a separate network for management purposes:
```
int loop 192
ip address 192.168.1.x 255.255.255.255
```
Just replace x with the router's number (1 for router1, 2 for router2, etc.)  

---

# Another reason to use loopbacks - OSPF



---
EOF
