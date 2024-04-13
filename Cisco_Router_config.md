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
- creating an Access List
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

Port Gi0/0/0 is connected to my home ISP router.  
To make this interface receive an IP address from my home ISP router:
```
en
conf t
int G0/0/0
ip address dhcp
exit
```




---
EOF
