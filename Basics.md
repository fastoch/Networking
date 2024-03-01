## What's a network?
A system that allows multiple devices to communicate with one another.

---

## Vocabulary

**Port mural** = wall socket  

**Baie de brassage** = patch panel  

Each wall socket that we plug a computer into connects back to one of the ports available on the patch panel.  
We can then connect each of these ports directly into the switch.  

---

## Protocols

802 = LAN technologies  
>802.3 = Ethernet

---

## The OSI model

The OSI model is not about specific technologies, but rather how they fit into the network stack.

- Application
- Presentation
- Session
- Transport
- Network
- Data Link
- Physical

>[!tip]
>Please Do Not Throw Sausage Pizza Away

Imagine that we have an application on one host that needs to send data to an application on another host.  
Let's now see how this data moves through the OSI model.  

The data starts at the **Application** layer. This is where network APIs and apps that access the network live.  
For example, this includes FTP and web browsing.  

The data needs to be in a format that can be easily undesrtood. That's what the **Presentation** layer is for.  
Anything related to data formats lives here, such as image and video files.  

The **Session** layer tracks application processes. This includes remote procedure calls and service requests.  
Think of this layer as building a session between a local application and a remote one.  

**What if the data you're transferring is very large?**  
What happens if you get right to the end of the transfer and the connection is interrupted?  
You would have to start the whole transfer again.  
Also, any application that wants to use the network would to wait until this transfer is complete.  

Fortunately, when the data reaches the **Transport** layer, it is broken into manageable chunks.  
Now, if there's a problem, only one chunk of data needs to be re-sent, not the entire file.  
Also, apps can take turns at sending chunks of data, rather than one app hogging the hosts ressources. This is called **multiplexing**.  

In order to successfully transfer our data, we need to add more information, we call this **"metadata"**.  
Metadata is **"data that provides information about other data"**.
Adding the source and destination address is an example of this.  
Any information we add to the front of our data is called the **header**.  
Any information we add to the back of our data is called the **trailer**.  


