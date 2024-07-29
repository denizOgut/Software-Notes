# Chapter 1. Basic Network Concepts

Besides classic applications like email, web browsers, and remote login, most major applications have some level of networking built in. For example:

- Text editors like BBEdit save and open files directly from FTP servers.
- IDEs like Eclipse and IntelliJ IDEA communicate with source code repositories like GitHub and Sourceforge.
- Word processors like Microsoft Word open files from URLs.
- Antivirus programs like Norton ``AntiVirus`` check for new virus definitions by connecting to the vendor’s website every time the computer is started.
- Music players like Winamp and iTunes upload CD track lengths to CDDB and download the corresponding track titles.
- Gamers playing multiplayer first-person shooters like Halo gleefully frag each other in real time.
- Supermarket cash registers running IBM SurePOS ACE communicate with their store’s server in real time with each transaction. The server uploads its daily receipts to the chain’s central computers each night.
- Schedule applications like Microsoft Outlook automatically synchronize calendars among employees in a company.

## Networks

**==A _network_ is a collection of computers and other devices that can send data to and receive data from one another, more or less in real time.==** A network is often connected by wires, and the bits of data are turned into electromagnetic waves that move through the wires

There’s nothing sacred about any particular physical medium for the transmission of data. Theoretically, data could be transmitted by coal-powered computers that send smoke signals to one another.

**==Each machine on a network is called a _node_.==** Most nodes are computers, but printers, routers, bridges, gateways, dumb terminals, and Coca-Cola™ machines can also be nodes. **==Nodes that are fully functional computers are also called _hosts_.==**

Every network node has an _address_, a sequence of bytes that uniquely identifies it. You can think of this group of bytes as a number, but in general the number of bytes in an address or the ordering of those bytes is not guaranteed to match any primitive numeric data type in Java. The more bytes there are in each address, the more addresses there are available and the more devices that can be connected to the network simultaneously(IPv4 Address - IPv6 Address).

Addresses are assigned differently on different kinds of networks. Ethernet addresses are attached to the physical Ethernet hardware

Internet addresses are normally assigned to a computer by the organization that is responsible for it. However, the addresses that an organization is allowed to choose for its computers are assigned by the organization’s Internet service provider (ISP). ISPs get their IP addresses from one of four regional Internet registries which are in turn assigned IP addresses by the Internet Corporation for Assigned Names and Numbers ([ICANN](http://www.icann.org/)).

On some kinds of networks, nodes also have text names that help human beings identify them such as “www.elharo.com” or “Beth Harold’s Computer.” At a set moment in time, a particular name normally refers to exactly one address. However, names are not locked to addresses. Names can change while addresses stay the same; likewise, addresses can change while the names stay the same. One address can have several names and one name can refer to several different addresses.

All modern computer networks are _packet-switched_ networks: data traveling on the network is broken into chunks called _packets_ and each packet is handled separately. Each packet contains information about who sent it and where it’s going. The most important advantage of breaking data into individually addressed packets is that packets from many ongoing exchanges can travel on one wire, which makes it much cheaper to build a network: many computers can share the same wire without interfering.

> ***Packet-switched networks break data into small packets that are transmitted independently over the network and reassembled at the destination. This method allows for efficient use of network resources and can handle variable transmission rates and paths.***

Another advantage of packets is that checksums can be used to detect whether a packet was damaged in transit.

> ***A checksum is a value calculated from a data set to detect errors in the data. When the data is received, a new checksum is calculated and compared to the original to ensure the data was not corrupted during transmission.***

We’re still missing one important piece: some notion of what computers need to say to pass data back and forth. **==A _protocol_ is a precise set of rules defining how computers communicate: the format of addresses, how data is split into packets, and so on.==**

## The Layers of a Network

Sending data across a network is a complex operation that must be carefully tuned to the physical characteristics of the network as well as the logical character of the data being sent. Software that sends data across a network must understand how to avoid collisions between packets, convert digital data to analog signals, detect and correct errors, route packets from one host to another, and more. The process is further complicated when the requirement to support multiple operating systems and heterogeneous network cabling is added.

To hide most of this complexity from the application developer and end user, the different aspects of network communication are separated into multiple layers. Each layer represents a different level of abstraction between the physical hardware (i.e., the wires and electricity) and the information being transmitted. In theory, each layer only talks to the layers immediately above and immediately below it. Separating the network into layers lets you modify or even replace the software in one layer without affecting the others, as long as the interfaces between the layers stay the same.

![[Pasted image 20240729121945.png]]

There are several different layer models, each organized to fit the needs of a particular kind of network. 

![[Pasted image 20240729122044.png]]

The host-to-network layer on the remote system decodes the analog signals into digital data, then passes the resulting IP datagrams to the server’s internet layer. The internet layer does some simple checks to see that the IP datagrams aren’t corrupt, reassembles them if they’ve been fragmented, and passes them to the server’s transport layer. The server’s transport layer checks to see that all the data arrived and requests retransmission of any missing or corrupt pieces. Once the server’s transport layer has received enough contiguous, sequential datagrams, it reassembles them and writes them onto a stream read by the web server running in the server application layer. The server responds to the request and sends its response back down through the layers on the server system for transmission back across the Internet and delivery to the web client.

> ***The host-to-network layer is by far the most complex, and a lot has been deliberately hidden***

90% of the time your Java code will work in the application layer and only need to talk to the transport layer. The other 10% of the time, you’ll be in the transport layer and talking to the application layer or the internet layer. The complexity of the host-to-network layer is hidden from you; that’s the point of the layer model.

---   
**==TIP**==

==**If you read the network literature, you’re likely to encounter an alternative seven-layer model called the Open Systems Interconnection (OSI) Reference Model. For network programs in Java, the OSI model is overkill. The biggest difference between the OSI model and the TCP/IP model used in this book is that the OSI model splits the host-to-network layer into data link and physical layers and inserts presentation and session layers in between the application and transport layers. The OSI model is more general and better suited for non-TCP/IP networks, although most of the time it’s still overly complex. In any case, Java’s network classes only work on TCP/IP networks and always in the application or transport layers, so for the purposes of this book, absolutely nothing is gained by using the more complicated OSI model.==**

----

To the application layer, it seems as if it is talking directly to the application layer on the other system; the network creates a logical path between the two application layers. **==Everything more than one layer deep is effectively invisible, and that is exactly the way it should be.==**

### The Host-to-Network Layer

In the standard reference model for IP-based Internets (the only kind of network Java really understands), the hidden parts of the network belong to the _host-to-network layer_ (also known as the link layer, data link layer, or network interface layer). The host-to-network layer defines how a particular network interface—such as an Ethernet card or a WIFI antenna—sends IP datagrams over its physical connection to the local network and the world.

The part of the host-to-network layer made up of the hardware that connects different computers (wires, fiber-optic cables, radio waves, or smoke signals) is sometimes called the physical layer of the network. As a Java programmer, you don’t need to worry about this layer unless something goes wrong—the plug falls out of the back of your computer, or someone drops a backhoe through the T–1 line between you and the rest of the world. **==In other words, Java never sees the physical layer.==**

**==The primary reason you’ll need to think about the host-to-network layer and the physical layer, if you need to think about them at all, is performance.==**

### The Internet Layer

The next layer of the network, and the first that you need to concern yourself with, is the _internet layer_. In the OSI model, the internet layer goes by the more generic name _network layer_. A network layer protocol defines how bits and bytes of data are organized into the larger groups called packets, and the addressing scheme by which different machines find one another. The Internet Protocol (IP) is the most widely used network layer protocol in the world and **==the only network layer protocol Java understands.==**

In both IPv4 and IPv6, data is sent across the internet layer in packets called _datagrams_. Each IPv4 datagram contains a header between 20 and 60 bytes long and a payload that contains up to 65,515 bytes of data. An IPv6 datagram contains a larger header and up to four gigabytes of data.

>**==A datagram is a self-contained packet of data that is sent independently through a network, without establishing a connection beforehand. Each datagram contains all the necessary information for routing to its destination.==**

![[Pasted image 20240729123008.png]]

**==Besides routing and addressing, the second purpose of the Internet layer is to enable different types of Host-to-Network layers to talk to each other.==** Internet routers translate between WiFi and Ethernet, Ethernet and DSL, DSL and fiber-optic backhaul protocols, and so forth. Without the internet layer or something like it, each computer could only talk to other computers that shared its particular type of network. **==The internet layer is responsible for connecting heterogenous networks to each other using homogeneous protocols.==**

### The Transport Layer

Raw datagrams have some drawbacks. Most notably, there’s no guarantee that they will be delivered. Even if they are delivered, they may have been corrupted in transit. The header checksum can only detect corruption in the header, not in the data portion of a datagram. Finally, even if the datagrams arrive uncorrupted, they do not necessarily arrive in the order in which they were sent. Individual datagrams may follow different routes from source to destination. Just because datagram A is sent before datagram B does not mean that datagram A will arrive before datagram B.

**==The _transport layer_ is responsible for ensuring that packets are received in the order they were sent and that no data is lost or corrupted.==** If a packet is lost, the transport layer can ask the sender to retransmit the packet. IP networks implement this by adding an additional header to each datagram that contains more information. There are two primary protocols at this level. The first, the Transmission Control Protocol (TCP), is a high-overhead protocol that allows for retransmission of lost or corrupted data and delivery of bytes in the order they were sent. The second protocol, the User Datagram Protocol (UDP), allows the receiver to detect corrupted packets but does not guarantee that packets are delivered in the correct order (or at all). However, UDP is often much faster than TCP. **==TCP is called a _reliable_ protocol; UDP is an _unreliable_ protocol==**

### The Application Layer

The layer that delivers data to the user is called the _application layer_. The three lower layers all work together to define how data is transferred from one computer to another. **==The application layer decides what to do with the data after it’s transferred.==** The application layer is where most of the network parts of your programs spend their time.

## IP, TCP, and UDP

- IP was designed to allow multiple routes between any two points and to route packets of data around damaged routers. 

 - IP had to be open and platform-independent; it wasn’t good enough to have one protocol for IBM mainframes and another for PDP-11s. The IBM mainframes needed to talk to the PDP-11s and any other strange computers that might be lying around.

Because there are multiple routes between two points, and because the quickest path between two points may change over time as a function of network traffic and other factors. The packets that make up a particular data stream may not all take the same route. Furthermore, they may not arrive in the order they were sent, if they even arrive at all. To improve on the basic scheme, TCP was layered on top of IP to give each end of a connection the ability to acknowledge receipt of IP packets and request retransmission of lost or corrupted packets. Furthermore, **==TCP allows the packets to be put back together on the receiving end in the same order they were sent.==**

TCP, however, carries a fair amount of overhead. Therefore, if the order of the data isn’t particularly important and if the loss of individual packets won’t completely corrupt the data stream, packets are sometimes sent without the guarantees that TCP provides using the UDP protocol. **==UDP is an unreliable protocol that does not guarantee that packets will arrive at their destination or that they will arrive in the same order they were sent.==** Although this would be a problem for uses such as file transfer, it is perfectly acceptable for applications where the loss of some data would go unnoticed by the end user. For example, losing a few bits from a video or audio signal won’t cause much degradation; it would be a bigger problem if you had to wait for a protocol like TCP to request a retransmission of missing data. Furthermore, error-correcting codes can be built into UDP data streams at the application level to account for missing data.

**==The only protocols Java supports are TCP and UDP, and application layer protocols built on top of these.==** All other transport layer, internet layer, and lower layer protocols such as ICMP, IGMP, ARP, RARP, RSVP, and others can only be implemented in Java programs by linking to native code.

### IP Addresses and Domain Names