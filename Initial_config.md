# How to connect to a Cisco router or switch

Once configured, you can access your device remotely via SSH.  
But when you configure it for the first time, you access it via its **console port**.  

Traditionally, a Cisco router or switch would only have an **RJ45 console port**.  
Fortunately, modern devices now have a **USB port**.  

When connecting via an RJ45 console port, you can use a rollover cable and an adapter.  
Connect one side of the rollover cable to the router or switch, and use a RJ45-to-DB9 (Ethernet to Serial) connector   
to connect the other side to your computer. This means you need a serial port available on your laptop.  
Nowadays, we use RJ45 to DB9 cables, where the DB9 connector is already included at one end of the cable.

>[!warning]
>DO NOT connect the other side of the rollover cable directly to the RJ45 port of your computer.
>This would blow the console port of the switch or router. We are not sending TCP/IP traffic across the rollover cable.

If your laptop is recent and doesn't have a serial port, then use an RJ45-to-DB9 cable and a USB-to-Serial converter.  

Modern networking devices now have a USB port, so it's very easy to connect your computer to it.

---

# Initial configuration of a switch

Once you physically connected your laptop to the switch, 
