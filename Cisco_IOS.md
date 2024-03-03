>[!Note]
>Cisco IOS = Internetworking Operating System

source = https://www.youtube.com/watch?v=xOqwxluUCc8&list=PLDQaRcbiSnqF5U8ffMgZzS7fq1rHUI3Q8&index=12

---

# Basics

By default, the command prompt ends with a greater than sign **>**, which means you're in **user exec mode**.

## move from user exec mode to privileged exec mode
`enable`  
you should be prompted for entering a pwd, unless this is a brand new switch/router  
cmd prompt now ends with a pawn sign **#**

## display current time and date
`show clock`  

## display software version
`show version`  

if there's too much information to fit on the screen, you'll see the **--More--** line at the bottom.  
you can use **space** to move through this information page by page, or you can use **enter** to move through it line by line  
just press **Q** to quit without seeing everything  

## if we don't know the exact cmd we want to run
`show ?`  
as soon as we press enter, the CLI gives us all the available options  

>[!tip]
>we can use the **tab** key for leveraging **autocompletion** capabilities

>[!tip]
>we can also use the **arrow keys** to browse the list of recent commands (history)

>[!note]
>we can also **shorten** commands

>[!warning]
>sometimes we shorten commands too far and we get the "ambiguous command" message

## go up a level (from config-if to config for example)
`exit`  

>[!tip]
>Keyboard shortcut to go back to user exec mode = Ctrl + Z

## reboot the Cisco switch or router
`reload`

## show running config (currently active config on the switch|router)
`do show running-config`  
`do sh run`

---

# Config mode

## once in privileged exec mode, you can enter config mode
`configure terminal`  
`conf t`  

>[!tip]
>if you put a **do** keyword before your cmd while in config mode, you can run user exec commands
>>That's a lot faster than jumping in & out of config mode

## change the hostname
`hostname <new_name>`

## show available interfaces and their current status (while in config mode)
`do show ip interface brief`  
`do show interface description`

>[!note]
>When a port is disabled, the interface status is 'administratively down'.

# Interface Configuration

## enter interface config mode (config-if) for the specified interface  
`interface gigabit 0/1`  
`int gi0/1`

## add a description to an interface (while in config-if)
`description Corporate Network`

## assign an IP address and a subnet mask (config-if)
`ip address 192.168.0.1 255.255.255.0`  

## disable an interface while in config-if mode
`shutdown`

## enable an interface while in config-if mode
`no shutdown`

## create a virtual interface while in config mode (loopback example)
`interface loopback 0`  
This interface will be enabled by default. 0 is just an example, we can use any number.  
We then need to assign an IP address to this interface. When done, we can check with `show ip int brief`.

---

# Remote administration

Our goal is to be able to connect to this router/switch over the network.  
We don't want to use the console cable every time, but only when configuring the device for the first time.  
The next thing we should configure is **authentication**.

## First thing is to secure the enable command
`conf t`  
`enable secret pass123`

## then, create an admin account and set its password
`username admin privilege 15 secret pass456`  
On a Cisco router, **privilege 15** means **full access**. 

## to allow remote logins, we need to configure a virtual terminal line

A virtual terminal line is like a virtual console port.  
Configuring a virtual terminal line is very much like configuring an interface.  
`line vty 0 4`  

Routers have 5 vty lines, which is why we specify the range 0-4, so we can configure them all at once.  
Switches have 16 vty lines, so that would be 0 through to 15.  

Now, we tell the router which protocols we want our users to log in with.  
The common ones are SSH and telnet. Both of these protocols use TCP to send terminal information across the network.  
In most cases, we prefer to use SSH rather than telnet, because SSH is encrypted and secure.  
`transport input ssh`  

Finally, we tell the router to look for local user accounts (like the admin account we've created earlier)  
`login local`  

## Now we need to configure SSH

Firstly, SSH needs a domain name:  
`ip domain-name fakedomain.net`  

Next, specify the RSA key:  
`crypto key generate RSA`  

You can see the full router name when creating the key, which is <hostname.domain-name>  
SSH will use this key to encrypt & decrypt the traffic.  
The default length for the key is 512 bits. It is recommended to use 2048 bits nowadays.  
NIST deems RSA 2048 sufficient until 2030, balancing security strength and computational efficiency.  

Check the SSH version and turn it up to version 2 if needed:  
`show ip ssh`  
`ip ssh version 2`  

Then, let's configure the login banner (with # as the delimiter):  
`banner login #`  
The delimiter character can be any character.  
Enter the text message of your banner:  
```
Authorise logins only! 
Intruders, stay out!!!
#
```
Everything between the two delimiters is the banner.  

The login banner is only shown when the router asks you for login details.  
There's another kind of banner: the message of the day, or motd for short.  
`banner motd #`
```
Your access has been logged
Have a nice day
#
```

The router is now ready to be accessed over the network.  
- Launch Putty (or any other terminal emulator)
- select SSH as the connection type
- enter the IP address
- click Open

Since we're using an admin account with privilege level 15, we won't even need the enable command.

---

# Regular Expressions

## show lines of the running config that begin with i
`sh run | include ^i`

## show lines of the running config that end with a 0
`sh run | include 0$`

## show lines with any single character between two ones
`sh run | include 1.1`

## show lines with 1.1
`sh run | include 1\.1`

## show lines that include eigrp or ospf or network
`sh run | include eigrp|ospf|network`  
>[!tip]
>Note that 'include' can be replaced with 'inc'

## show running config with line numbers
`sh run linenum`

## show line 173 
`sh run | inc 173`
>[!warning]
>This also shows lines that include 173

## show only line 173  
`sh run | inc __173`
>[!note]
>We use 2 undescores to represent spaces before the line number



