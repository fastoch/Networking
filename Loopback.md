# What is a loopback? Why is it used?

A loopback interface is a logical interface that typically only has one IP address.  

You can create many loopbacks. For example: `interface loopback 0`  
As soon as I create this logical interface, it comes up.  

I can then give that interface an IP address: `ip address 2.2.2.2 255.255.255.255`  
Notice that the subnet mask is /32, which means this is the only IP address on that interface.  

The first advantage of a loopback interface is that it doesn't go down unless you explicitly shut it down.

On a router, if for some reason an interface goes down, you can't use it anymore for a telnet or SSH connection.  
However, if you have a loopback interface, and you advertise that loopback through a routing protocol such as OSPF,  
you can always SSH or telnet to that loopback.  

---

First, you need to enable EIGRP on the routers you want to interconnect: 
```
conf t
router eigrp 100
network 0.0.0.0  
```

Check config with `sh ip eigrp neighbors`  



---
EOF
