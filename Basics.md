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
Anything related to data formats lives here. This layer is responsible for data conversion and formatting.  

The **Session** layer tracks application processes. This includes remote procedure calls and service requests.  
Think of this layer as building a session between a local application and a remote one.  

**What if the data you're transferring is very large?**  
What happens if you get right to the end of the transfer and the connection is interrupted?  
You would have to start the whole transfer again.  
Also, any application that wants to use the network would to wait until this transfer is complete.  

Fortunately, when the data reaches the **Transport** layer, it is broken into manageable chunks.  
Now, if there's a problem, only one chunk of data needs to be re-sent, not the entire file.  
Also, apps can take turns at sending chunks of data, rather than one app hogging the hosts ressources. This is called **multiplexing**.  
If we're using TCP, each block of data is called a "**segment**". If it's UDP, each block is called a "**datagram**".  

We have many blocks of data probably going to different hosts for different applications.
**So how can we track what goes where?**  
The answer is: through **port numbers**.  

Each flow of data has a port number associated with the source and destination host.  
These values are added as part of a **header** to each block of data.

In order to successfully transfer our data, we need to add more information, we call this **"metadata"**.  
Metadata is **"data that provides information about other data"**.
Adding the source and destination address is an example of this.  
Any information we add to the front of our data is called a **header**.  
Any information we add to the back of our data is called a **trailer**.  

The **Network** layer adds IP addresses to **packets** of data, source and destination addresses.  
This is required to properly **route** the data and deliver it to the remote hosts.  

Now, we need to think about getting the data from one device to another. This is where the **Data Link** layer comes in.  
This layer does not try to get data to the end device, that's the responsibility of layer 3 & 4.  
The Data Link layer creates a logical link between devices on the same network segment.  
We need to have a **logical link** as devices probably aren't directly connected.  
They're usually connected with a shared medium like a **switch** or over Wi-Fi.

Eventually, the data reaches the **Physical** layer, where it is transmitted over cable or wireless to the remote host.  
The remote host receives the data at the physical layer. The process is then **reversed**. The data flows back up through the layers.  
Each layer does its job, removing headers and trailers, and converting the data until it is in a form that the application can understand.  

Each layer will only communicate with the layer above and the layer below.  
Each layer has its own purpose and doesn't get involved with other layers, other than to pass and receive data.



