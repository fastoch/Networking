## SPAN Ports or Port Mirroring

To monitor traffic within my network, I can use a dedicated machine connected to one of my switches.  
I will then run Wireshark on this machine to capture traffic on the link between the switch and this monitoring device.  
But in order to make this work, I have to configure **SPAN ports**, also referred to as **Port Mirroring**.  

On the switch:
```
en
conf t
monitor session 1 source interface gigabitEthernet 0/0
monitor session 1 destination interface gigabitEthernet 0/3
```

The switch will copy the traffic from the source interface to the destination interface.  
In this example, we're spanning (or mirroring) the port gi0/0 to the port gi0/3 (to which we've connected the monitoring device).  
This way, we're seeing all the traffic that goes through gi0/0, because now it also goes through gi0/3.  

**Recap**:
- locate the port on which you want to monitor traffic
- connect a monitoring device to another port of the same switch
- mirror the port you want to monitor to the one used to connect the monitoring device
- install Wireshark on the monitoring device and capture traffic


