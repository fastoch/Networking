Hardware = Cisco Catalyst 3550  

resources:  
https://www.youtube.com/watch?v=7dXBN8a-X2U  
https://www.youtube.com/watch?v=ThmwyyY-p5g  

---

## Summary

- change the hostname
- set the enable mode password
- create a VLAN
- naming a VLAN
- assign an interface to a VLAN
- assign an IP address to a VLAN
- enable inter-VLAN routing
- configure DHCP server and exclude a range of IP addresses 

---

## Changing the hostname and setting a password for the enable mode

By default, all Cisco switches are named "Switch".
```
enable
configure terminal
hostname Lab-Switch
```
As soon as you press Enter to run the hostname cmd, the prompt will show you the new name.  

While still in config mode:
```
enable password ComplicatedPassword
exit
exit
en
```
The first exit cmd exits the config mode, and the second exits the enable mode.  
When I enter `en` (shorthand for `enable`), I'm now prompted for the password I've just set.  

---

## Create VLANs and naming them

To see the current VLANs (while in enable mode): `show vlan`  
On a brand new switch (or one that was reset), all physical interfaces belong to the default VLAN (VLAN 1).  

To create VLANs on your Cisco switch and give them a name:
```
en
conf t
vlan 10
name Voice
exit
vlan 20
name Printers
exit
vlan 30
name HR
exit
vlan 40
name IT
exit
exit
show vlan
```
We name the VLANs to remember why we created them.  
At the end, we make sure that we've created our VLANs as we wanted to.  

All interfaces still belong to VLAN 1 though. Next step is to assign interfaces to our different VLANs.

---

## Assigning interfaces to our VLANs

```
conf t
interface range fastEthernet 0/1-10
switchport mode access
switchport access vlan 10
exit
interface range fastEthernet 0/11-20
switchport mode access
switchport access vlan 20
exit
int range fa0/21-30
switchport mode access
switchport access vlan 30
exit
int range fa0/31-40
switchport mode access
switchport access vlan 40
exit
exit
show vlan
```
The `switchport mode` command allows us to configure the trunking operational mode on a Layer 2 interface on a Cisco IOS device.  
By entering the command `switchport mode access` we configure the interface to operate in access mode.  
This ensures that the interface will pass traffic for a single VLAN only.  

The remaining interfaces (Fa0/41-48, Gi0/1 and Gi0/2) still belong to VLAN 1 (the default VLAN).  

---

## Assigning IP addresses to VLANs

```
en
conf t
interface vlan 10
ip address 10.10.10.1 255.255.255.0
exit
interface vlan 20
ip address 10.10.20.1 255.255.255.0
exit
interface vlan 30
ip address 10.10.30.1 255.255.255.0
exit
interface vlan 40
ip address 10.10.40.1 255.255.255.0
exit
exit
show ip interface brief
```

---

## Enable inter-VLAN Routing

```
en
conf t
ip routing
```

To check if inter-VLAN routing is configured properly:
- I physically connect a laptop to a port that belongs to VLAN 10, and another laptop to a port that belongs to VLAN 20
- Then I manually assign an IP address to the first laptop: 10.10.10.5 255.255.255.0 with a gateway of 10.10.10.1 (VLAN 10)
- I also assign an IP address to the second laptop: 10.10.20.5 255.255.255.0 with a gateway of 10.10.20.1 (VLAN 20)
- Now, I can try pinging laptop 2 from laptop 1 and vice-versa
- if pings get responses, it means that inter-VLAN routing works well between VLAN 10 and VLAN 20

To apply and save the new config:
`wr mem`

---

## Configure DHCP server 

To show the running config:
`show run`

```
en
conf t
ip dhcp pool vlan10
network 10.10.10.0 /24
default-router 10.10.10.1
exit
ip dhcp pool vlan20
network 10.10.20.0 /24
default-router 10.10.20.1
exit
ip dhcp pool vlan30
network 10.10.30.0 /24
default-router 10.10.30.1
exit
ip dhcp pool vlan40
network 10.10.40.0 /24
default-router 10.10.40.1
exit
```

## Exclude a range of IP addresses from DHCP server





---
EOF
