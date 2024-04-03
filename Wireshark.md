## SPAN Ports or Port Mirroring

To monitor traffic within my network, I can use a dedicated machine connected to one of my switches.  
I will then run Wireshark on this machine to capture traffic on the link between the switch and this monitoring device.  
But in order to make this work, I have to configure **SPAN ports**, also referred to as **Port Mirroring**.  

On the switch:
```
en
conf t
monitor session 1 source int g0/0
monitor session 1 destination
```

The source interface is  
