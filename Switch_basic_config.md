hardware = Cisco Catalyst 3550  

---

## Summary

- change the hostname
- set the enable mode password
- create a VLAN
- naming a VLAN
- assign an interface to a VLAN
- assign an IP address to a VLAN
- enable inter-VLAN routing

---

## Changing the hostname and setting a password for the enable mode

By default, all Cisco switches are named "Switch".
```
en
conf t
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

## Create a VLAN and naming it

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
```
We name the VLANs to remember why we created them.

---
EOF
