source = https://www.youtube.com/watch?v=tBswpi22q_0  

---

# Introduction

Proprietary tools like Packet Tracer and VIRL are limited, in addition to being paid.  
What you need is a network emulator that is capable of network equipment and end device virtualization regardless of the brand.  

GNS3 stands for **Graphical Network Simulator**. It's completely free and open-source.  

---

# Installation

To install GNS3 on Archlinux you will need **yay**, an AUR helper.  
https://itsfoss.com/install-yay-arch-linux/  

Then, run the following cmd to install required dependencies:  
`yay -S qemu docker vpcs dynamips libvirt ubridge inetutils wireshark-qt`

Now, you can install GNS3 packages:  
`yay -S gns3-server gns3-gui`

Finally, we must add our user account to several groups:  
```
sudo usermod -aG kvm fastoch
sudo usermod -aG libvirt fastoch
sudo usermod -aG docker fastoch
sudo usermod -aG wireshark fastoch
```

---

# Running GNS3

Now you should be able to start GNS3.  
On the first startup, it will ask you where you want to be running the images on.  
![image](https://github.com/fastoch/Networking/assets/89261095/3b9afcb1-2dc1-4131-b933-3c0f8bd949c6)  

Since I've installed GNS3 on my Linux laptop, I will run it directly on my machine.  
Then, leave the settings as default by clicking Next, Next, and Finish.  

>[!warning]
>GNS3 might not start up correctly the very first time. Just close it and reopen it.

The interesting thing about GNS3 is that it is actually not an emulator in the same sense as Virtualbox or QEMU+KVM.  
Instead it's a solution that can get the job done using several other emulators in the background.  
For example, it could have a VMware image and a Docker image working with one another in the same network topology.  

A cool thing about GNS3 is that it uses an open-source solution for networking that was not inherently available in virt-manager.  
When using QEMU in combination with KVM, you'll have to manually create isolated networks in order to link your virtual machines.  

When installing GNS3, we have installed a solution called "ubridge", and GNS3 will use it to emulate wired connections.  
So connecting 2 devices will be as simple as point and click.  

However, ubridge behaves in a similar manner to isolated networks, where the Ethernet ports show up as running as long as they  
have a wire plugged into them, even if the device at the other end is down.





---
EOF
