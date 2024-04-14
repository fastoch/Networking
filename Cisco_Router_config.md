# How to configure a Cisco router for Internet Access

source = https://www.youtube.com/watch?v=vIVZ_CYC484  
Hardware = Cisco ISR-4331  

**Steps**:
- setting the hostname
- configuring the enable password
- configuring IP addresses on both interfaces (one connected to my ISP router and one connected to my LAN)
- creating a DHCP server for my LAN
- configuring the default route of my Cisco router
- configuring IP NAT for inside and outside sources
- creating a standard Access Control List (ACL)
- applying the overload command to the router uplink port
- saving the settings

>[!note]
>Uplink Ports are high-speed connections that interconnect switches and enable connections to higher-level devices like core switches and routers, ideal for expanding network capacity. Normal Ports are designed for end devices, providing direct LAN access for devices like computers and printers.

---

## Setting the hostname and the enable password

```
en
conf t
hostname ISR4331
enable secret strongPassword
```

---

## Configuring IP addresses on both interfaces

Port Gi0/0/0 is connected to my home ISP router. This interface will receive an IP address from my home ISP router:
```
en
conf t
int gigabitEthernet 0/0/0
ip address dhcp
exit
```

Port Gi0/0/1 is connected to my home LAN switch. We will manually set the IP address for this interface:
```
en
conf t
int g0/0/1
ip address 192.168.100.1 255.255.255.0
exit
```

---

## Configuring DHCP server and default route

```
ip dhcp pool LAN
network 192.168.100.0 255.255.255.0
default-router 192.168.100.1
dns-server 8.8.8.8
exit
ip route 0.0.0.0 0.0.0.0 192.168.1.1
```
In this example, "LAN" is the name of our DHCP pool. The default gateway is the IP address of the interface connected to our LAN.  
The ip route command forwards traffic from any source (any address and any subnet mask) to the home ISP router.  

---

## Configuring NAT on both interfaces for inside and outside sources

```
en
conf t
int g0/0/0
ip nat outside
exit
```
Since interface gigabitEthernet 0/0/0 is connected to ISP router, we've configured the outside part of NAT.  

Now let's configure the inside part of NAT:
```
int g0/0/1
ip nat inside
exit
```
  
Now, we're going to create an ACL. From the config mode:
```
ip access-list standard acl-name
permit 192.168.100.0 0.0.0.255
exit
```
This ACL allows traffic from my LAN to traverse my Cisco router.  
0.0.0.255 is the **wildcard mask**. It is applied to the network address to determine the range of allowed IP addresses.  

Finally, we will apply the overload command to the uplink interface (the one connected to our ISP router):
```
en
conf t
ip nat inside source list acl-name int g0/0/0 overload
exit
copy running-config startup-config
```
'**Overloading**' means that the single public IP assigned to your router can be used by multiple internal hosts concurrently.


---
EOF
