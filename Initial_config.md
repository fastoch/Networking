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
>DO NOT connect the other side of the rollover cable directly to the Ethernet port of your computer.
>This would blow the console port of your switch or router. We are not sending TCP/IP traffic across the rollover cable.

If your laptop is recent and doesn't have a serial port, then use an RJ45-to-DB9 cable and a USB-to-Serial converter.  

Modern networking devices now have a USB port, so it's very easy to connect your computer to it.

---

# Initial configuration of a switch

Once your computer is physically connected to the switch, you can power on the switch and start the configuration.  
If you're on Windows, install and open a terminal emulator such as Putty on your laptop.  
On Linux and Mac you've already got a built-in **terminal emulator**.  

On Windows, you've launched Putty, select 'Serial' as the connection type.  
Open the device manager to get the serial port number (Ports COM) and enter the proper serial line in Putty.  
Click 'Open' to initiate the connection to the switch.  

Since it's a brand new switch, you're automatically logged in, no credentials required.  
Type `enable` and press Enter to quit **user mode** and enter **privileged mode**.  

To erase the current configuration: `erase startup-config`  
Once the config has been erased and the switch has rebooted, go back to Putty.

>[!warning]
>A Windows PC might display a blue screen when the switch is rebooted, especially when using a rollover cable.
>Just unplug the console cable while it's booting up, and replug it once the boot process is over.

In your terminal, the switch prompts you to enter the inital config dialog. Say no.  
Enter the command `en`, which is short for `enable`.  

Run `show version` to display information about the switch (OS, model, etc.).  
`conf t` to enter the global configuration mode (short for `configure terminal`).  
`hostname newName` to rename the device.

>[!tip]
>Use **question mark** when you're not sure about a command or when you want to see available options to complete a command.

When the output of a command is too long:
- press Enter to show next entry,
- press Space to show next page,
- press Q to quit and go back to the prompt



---
EOF
