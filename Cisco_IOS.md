>[!Note]
>Cisco IOS = Internetworking Operating System

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
>we can also use the **tab** key for leveraging **autocompletion** capabilities

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
>if you put a **do** keyword before your command while in config mode, 

## enter interface config mode for the specified fast ethernet interface
`interface fastethernet/number`  
`int gi0/1`

## return to previous mode
`exit`

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



