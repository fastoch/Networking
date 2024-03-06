# VLAN Trunk Links

Using VLANs is like breaking a physical switch into a few virtual ones.  
But eventually we'll need more physical ports, which means more physical switches.  

## How do get our VLANs to work across several switches?

Like the many branches on a tree trunk, we can use a **trunk link** to carry many VLANs.  

If the company we work for grows, then they're going to need more computers, printers, servers, and other devices.  
Which means we have to buy more switches.  

Normally, we would connect one switch to another to extend our number of ports.  
But we have cut our network into VLANs now. So how do we connect the two switches together?  

**Should we run a link between our switches for each VLAN?**  
We could, but what happens if we have many VLANs? We would be out of ports pretty quickly.  
And then what happens if we want to add a third switch?  
Clearly this method is not scalable.  

Instead, we can use **a single link** which is capable of carrying all of our VLANs.  
This uses a technology called **trunking** or **tagging**.  

In VLANs.md, we saw how to add devices to a VLAN. The type of port they connect to is called an **access** port.  
Typically, we would connect workstations, printers, servers and phones to an access port.  
When we connect 2 switches together, we configure these ports as **trunk** ports.  

Trunk ports are able to have many VLANs configured on them at one time.  

---

### Why do we want to use VLANs to separate traffic if a trunk link just mixes them all together again?

The traffic doesn't fully get mixed together. It goes over the same link, but it won't leave its VLAN.  
This is thanks to our good friend Ethernet.  

Think of a device on a VLAN sending a frame to a device on another VLAN.  
The switch knows which VLAN this frame belongs to.  
When the frame reaches the trunk link, the switch adds a 4 byte tag to the Ethernet header.  

This tag contains (amongst other things) the VLAN ID. When the frame arrives at the destination trunk port,  
the switch looks at the tag and knows the VLAN that this frame belongs to. It can now strip the tag from the  
frame and deliver it to the destination workstation. 

>[!note]
>VLAN names are locally significant to each switch. They don't have to match on 2 different switches.

**A trunk link extends VLANs from one switch to another.**  

As VLANs are in a broadcast domain, trunk links also extend broadcast domains across switches.  
So broadcast messages will stay within a VLAN but will pass over a trunk to other switches.  

And the same is true for flooding. Any frame that needs to be flooded will stay within the VLAN, but will   
travel over the trunk links to other switches.  

Once again, Cisco's terminology is a little bit different to everyone else's.  
To start with, a trunk port is called a **"tagged port"**, because of the tag that is added to the frame as it passes between the switches.

Also, an access port is really an **"untagged port"**.  

When it comes to tagging, there are two ways it can be done:
- **802.1q** - IEEE standard (well supported): a trunk between switches from different manufacturers is possible
- **ISL** - Cisco's original trunking standard (rare): inter-switch link

---

## Voice VLANs

These are important if you have IP telephony in your network.  
Workstations belong to a **data VLAN**, whereas IP phones belong to a **voice VLAN**.  

Usually, phones are a little bit special. They have a miniature 3 port switch built-in.  
So we can connect the phone to the switch, and the workstation to the phone.  
The third port is hidden from sight, it's inside the phone, connecting to the phone hardware.  

**Why do phones have a built-in switch?**  
For one, there's less need for ports on the main switch.  
Secondly, you don't normally connect phones and workstations directly into a switch.  
They normally go into a wall socket, with cabling through the wall which is eventually connected to the switch.  

The link from the phone to the switch is like a mini-trunk link, except it carries only 2 VLANs:
- the data VLAN
- the voice VLAN

Voice networking is a subject entirely of its own (see Voice_networking.md).

---

## LAB

![image](https://github.com/fastoch/Networking/assets/89261095/5a7a92da-6d8d-47cc-bc31-499a1d335e08)

We've added an extra switch, which implies we have to configure a trunk link.  

First, we create a voice vlan and we configure the interface Gi 2/2 onto switch 1:
```
en
conf t
vlan 110
name voice
exit
int gi 2/2
switchport mode access
switchport voice vlan 110
switchport access vlan 10
```
With this config, port Gi 2/2 is used for VLANs 10 and 110.
- vlan 110 is for IP phones  
- vlan 10 is for workstations  

**Keep in mind that when you have a phone connected, you set the voice vlan as well as a separate access vlan.**  

At this stage, if we try to ping workstation 2 from workstation 1, its' going to fail.  
Workstation 1 is connected to switch 1 while workstation 2 is connected to switch 2.  
We've configured ports on both switches so that our workstations are in the same vlan.
But until we create our trunk link, these devices won't be able to talk to each other.  

Let's configure our trunk link onto switch 1:
```
en
conf t
int gi 0/2
switchport trunk encapsulation dot1q
switchport mode trunk
no shut
```
**This trunk link allows frames to be tagged (with a VLAN id) when passing between the switches.**  

We need to do the same over on switch 2:
```
en
conf t
int gi 0/2
switchport trunk encapsulation dot1q
switchport mode trunk
no shut
```

When we configure trunk links, we have the option of allowing some VLANs while disallowing others.  
This is called **pruning**, and we do this with the `switchport trunk allowed vlan` command.   
If we don't use this command, all VLANs are allowed over the link.  

To allow VLANs 10 and 20 on interface gi 0/2:
```
enable
config terminal
int gi 0/2
switchport trunk allowed vlan 10,20
```

To check our config:
`show interfaces switchport | begin Gi0/2`
`show interfaces trunk`

But the best way to prove that this is working is to head over to workstation 1 and issue the following commands:
```
ping 192.168.10.2
ping 192.168.20.1
ping 192.168.20.2
```
From here, we can see the traffic is successfully flowing across the trunk link to workstation 2 and both servers.  

---

## Special VLANs

### VLAN 1

When you first turn on a switch, all the ports will, by default, belong to VLAN 1.  
We don't do anything to configure VLAN 1, it's just always there.  
**Control traffic between Cisco switches uses VLAN 1.**

>[!note]
>Other switch vendors may have a different way of approaching this.  

It's a **good practice** to keep your devices (workstations, printers, etc.) on a separate VLAN.  
Just leave VLAN 1 for this control traffic.  

---

### Native VLAN

There's another special VLAN that we need to consider. This is called the **native VLAN**.  
The native VLAN was created to support devices that don't support VLANs.

Think of a hub or a cheap switch, for example. If you connect one of these devices to a trunk link, they won't be able  
to tag any of the traffic they send. So, which VLAN is this traffic a part of? The answer is: **the native VLAN**.  

By default, the native VLAN is VLAN 1. But we can change this to another VLAN if we want to.  

What happens if traffic passes from a switch to a hub?  
Any frames that are part of the native VLAN will be sent out **untagged**.  
This keeps compatibility with these non-VLAN-enabled devices.  

---

## LAB (part 2) - CDP & LLDP

`show vlan brief` to see the vlans on the switch.  

Under interface config mode (config-if), we can use the following cmd to change trunking parameters:
`switchport trunk native vlan 2`  
The native vlan became vlan 2 instead of vlan 1.

It's not mandatory, but it is a good idea to have both switches use the same native VLAN.  
**But how do the two switches know that there is a mismatch?**  
How does one switch know how the other is configured?  
It does this by using a protocol called "CDP" or "**Cisco Discovery Protocol**".  

CDP is one of those types of traffic that flows between the switches themselves and will always use VLAN 1.  
If two devices that are connected together support it, they can learn about each other.  
On most Cisco switches, it is enabled by default, which we can confirm with `show cdp neighbors detail`.  

We can disable CDP globally (for security reasons) with `no cdp run`.  
We could also disable it on some individual ports while leaving it active on others.  
CPD can help when troubleshooting the network, or if your network documentation is not up to date.  
Also, if you're connecting Cisco phones, CDP helps you setting your voice network.  

**But what happens when you connect a device made by another manufacturer?**
Some other vendors like VMware do support CDP, but a lot of vendors don't.  
Fortunately, there's an alternative called LLDP or **Link Layer Discovery Protocol**.  

LLDP is vendor-neutral, so it's supported by a lot of vendors, including Cisco.  
It does the same basic job as CDP, and we can enable or disable it globally (config) or per interface (config-if):
```
lldp run
no lldp run
```

If we're particularly security-conscious, we can configure interfaces to only send or receive lldp traffic:
```
no lldp transmit
no lldp receive
lldp transmit
lldp receive
```
lldp commands are basically the same as cdp.

---

## Trunk links on routers

In a previous lab, we connected a router to each VLAN to enable workstations and servers to communicate.  
There were 2 VLANs, so we used 2 links. But what if we have 10 VLANs? Do we need 10 ports on our router?  
This is the same concern we faced with our switches earlier. We solved this by using a trunk link.  
The good news is that router can also use trunk links.  
This might sound surprising as trunking is a switching technology, but you'll find that the line between  
routers and switches is sometimes blurry.




---
EOF
