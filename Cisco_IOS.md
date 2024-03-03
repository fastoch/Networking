>[!Note]
>Cisco IOS = Internetworking Operating System

source = https://www.youtube.com/watch?v=xOqwxluUCc8&list=PLDQaRcbiSnqF5U8ffMgZzS7fq1rHUI3Q8&index=12

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

---

# Config mode

## once in privileged exec mode, you can enter config mode
`configure terminal`  
`conf t`  

>[!tip]
>if you put a **do** keyword before your cmd while in config mode, you can run global exec commands
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
``

---

## exit config mode
`exit`  
Keyboard shortcut = Ctrl + Z

## reboot the Cisco switch or router
`reload`

## show running config
`show running-config`  
`sh run`

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



