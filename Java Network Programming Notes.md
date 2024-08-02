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

Every computer on an IPv4 network is identified by a four-byte number. This is normally written in a _dotted quad_ format like 199.1.32.90, where each of the four numbers is one unsigned byte ranging in value from 0 to 255. Every computer attached to an IPv4 network has a unique four-byte address. When data is transmitted across the network, the packet’s header includes the address of the machine for which the packet is intended Routers along the way choose the best route on which to send the packet by inspecting the destination address. The source address is included so the recipient will know who to reply to.

There are a little more than four billion possible IP addresses, not even one for every person on the planet, much less for every computer. A slow transition is under way to IPv6, which will use 16-byte addresses. This provides enough IP addresses to identify every person, every computer, and indeed every device on the planet. **==IPv6 addresses are customarily written in eight blocks of four hexadecimal digits separated by colons, such as _FEDC:BA98:7654:3210:FEDC:BA98:7654:3210_. Leading zeros do not need to be written. A double colon, at most one of which may appear in any address, indicates multiple zero blocks. For example, _FEDC:0000:0000:0000:00DC:0000:7076:0010_ could be written more compactly as _FEDC::DC:0:7076:10_.==** In mixed networks of IPv6 and IPv4, the last four bytes of the IPv6 address are sometimes written as an IPv4 dotted quad address. For example, _FEDC:BA98:7654:3210:FEDC:BA98:7654:3210_ could be written as _FEDC:BA98:7654:3210:FEDC:BA98:118.84.50.16_.

Although computers are very comfortable with numbers, human beings aren’t very good at remembering them. Therefore, **==the Domain Name System (DNS) was developed to translate hostnames that humans can remember, such as “www.oreilly.com,” into numeric Internet addresses such as 208.201.239.101.==** When Java programs access the network, they need to process both these numeric addresses and their corresponding hostnames. Methods for doing this are provided by the `java.net.InetAddress` class

Some computers, especially servers, have fixed addresses. Others, especially clients on local area networks and wireless connections, receive a different address every time they boot up, often provided by a DHCP server. **==Mostly you just need to remember that IP addresses may change over time, and not write any code that relies on a system having the same IP address.==** For instance, don’t store the local IP address when saving application state. Instead, look it up fresh each time your program starts. It’s also possible, although less likely, for an IP address to change while the program is running (e.g., if a DHCP lease expires), so you may want to check the current IP address every time you need it rather than caching it. Otherwise, the difference between a dynamically and manually assigned address is not significant to Java programs.

Several address blocks and patterns are special. All IPv4 addresses that begin with 10., 172.16. through 172.31. and 192.168. are unassigned. They can be used on internal networks, but no host using addresses in these blocks is allowed onto the global Internet. These _non-routable_ addresses are useful for building private networks that can’t be seen on the Internet. IPv4 addresses beginning with 127 (most commonly 127.0.0.1) always mean the _local loopback address_. That is, these addresses always point to the local computer, no matter which computer you’re running on. The hostname for this address is often _localhost_. In IPv6, 0:0:0:0:0:0:0:1 (a.k.a. ::1) is the loopback address. The address 0.0.0.0 always refers to the originating host, but may only be used as a source address, not a destination. Similarly, any IPv4 address that begins with 0. (eight zero bits) is assumed to refer to a host on the same local network.

> **A local loopback address is a special IP address (typically 127.0.0.1 for IPv4) used to test network software on the same machine. It allows a device to communicate with itself for testing and diagnostics.**

The IPv4 address that uses the same number for each of the four bytes (i.e., 255.255.255.255), is a broadcast address. Packets sent to this address are received by all nodes on the local network, though they are not routed beyond the local network. This is commonly used for discovery. For instance, when an ephemeral client such as a laptop boots up, it will send a particular message to 255.255.255.255 to find the local DHCP server. All nodes on the network receive the packet, but only the DHCP server responds. In particular, it sends the laptop information about the local network configuration, including the IP address that laptop should use for the remainder of its session and the address of a DNS server it can use to resolve hostnames.

### Ports

Addresses would be all you needed if each computer did no more than one thing at a time. However, modern computers do many different things at once. Email needs to be separated from FTP requests, which need to be separated from web traffic. This is accomplished through _ports_. Each computer with an IP address has several thousand logical ports (65,535 per transport layer protocol, to be precise). These are purely abstractions in the computer’s memory and do not represent anything physical, like a USB port. **==Each port is identified by a number between 1 and 65535. Each port can be allocated to a particular service.==**

Port numbers between 1 and 1023 are reserved for well-known services like finger, FTP, HTTP, and IMAP. On Unix systems, including Linux and Mac OS X, only programs running as root can receive data from these ports, but all programs may send data to them. On Windows, any program may use these ports without special privileges.

These assignments are not absolutely guaranteed; in particular, web servers often run on ports other than 80, either because multiple servers need to run on the same machine or because the person who installed the server doesn’t have the root privileges needed to run it on port 80. On Unix systems, a fairly complete listing of assigned ports is stored in the file _/etc/services_.

## The Internet

The _Internet_ is the world’s largest IP-based network. It is an amorphous group of computers in many different countries on all seven continents (Antarctica included) that talk to one another using IP protocols. Each computer on the Internet has at least one IP address by which it can be identified. Many of them also have at least one name that maps to that IP address.  It is simply a very large collection of computers that have agreed to talk to one another in a standard way.

The Internet is not the only IP-based network, but it is the largest one. Other IP networks are called _internets_ with a little _i_: for example, a high-security internal network that is not connected to the global Internet. _Intranet_ loosely describes corporate practices of putting lots of data on internal web servers that are not visible to users outside the local network.

To make sure that hosts on different networks on the Internet can communicate with each other, a few rules need to be followed that don’t apply to purely internal internets. **==The most important rules deal with the assignment of addresses to different organizations, companies, and individuals.==** If everyone picked the Internet addresses they wanted at random, conflicts would arise almost immediately when different computers showed up on the Internet with the same address.

### Internet Address Blocks

To avoid this problem, blocks of IPv4 addresses are assigned to Internet service providers (ISPs) by their regional Internet registry. When a company or an organization wants to set up an IP-based network connected to the Internet, their ISP assigns them a block of addresses. Each block has a fixed prefix. For instance if the prefix is 216.254.85, then the local network can use addresses from 216.254.85.0 to 216.254.85.255. Because this block fixes the first 24 bits, it’s called a /24. A /23 specifies the first 23 bits, leaving 9 bits for 29 or 512 total local IP addresses. A /30 subnet (the smallest possible) specifies the first 30 bits of the IP addresses within the subnetwork, leaving 2 bits for 22 or 4 total local IP addresses. However, the lowest address in a block is used to identify the network itself, and the largest address in a block is a broadcast address for the network, so you have two fewer available addresses than you might first expect.

### Network Address Translation

Because of the increasing scarcity of and demand for raw IP addresses, most networks today use Network Address Translation (NAT). In NAT-based networks most nodes only have local, non-routable addresses selected from either 10.x.x.x, 172.16.x.x to 172.31.x.x, or 192.168.x.x. The routers that connect the local networks to the ISP translate these local addresses to a much smaller set of routable addresses.

Eventually, IPv6 should make most of this obsolete. NAT will be pointless, though firewalls will still be useful. Subnets will still exist for routing, but they’ll be much larger.

### Firewalls

**==The hardware and software that sit between the Internet and the local network, checking all the data that comes in or out to make sure it’s kosher, is called a _firewall_.==** The firewall is often part of the router that connects the local network to the broader Internet and may perform other tasks, such as network address translation.

**==Filtering is usually based on network addresses and ports.==** For example, all traffic coming from the Class C network 193.28.25.x may be rejected because you had bad experiences with hackers from that network in the past. Outgoing SSH connections may be allowed, but incoming SSH connections may not. Incoming connections on port 80 (web) may be allowed, but only to the corporate web server.

### Proxy Servers

_Proxy servers_ are related to firewalls. If a firewall prevents hosts on a network from making direct connections to the outside world, a proxy server can act as a go-between. Thus, a machine that is prevented from connecting to the external network by a firewall would make a request for a web page from the local proxy server instead of requesting the web page directly from the remote web server. The proxy server would then request the page from the web server and forward the response back to the original requester. Proxies can also be used for FTP services and other connections. **==One of the security advantages of using a proxy server is that external hosts only find out about the proxy server. They do not learn the names and IP addresses of the internal machines, making it more difficult to hack into internal systems.==**

Whereas firewalls generally operate at the level of the transport or internet layer, proxy servers normally operate at the application layer. A proxy server has a detailed understanding of some application-level protocols, such as HTTP and FTP. Packets that pass through the proxy server can be examined to ensure that they contain data appropriate for their type.

![[Pasted image 20240729202104.png]]

As long as all access to the Internet is forwarded through the proxy server, access can be tightly controlled.

**==Proxy servers can also be used to implement local caching.==** When a file is requested from a web server, the proxy server first checks to see if the file is in its cache. If the file is in the cache, the proxy serves the file from the cache rather than from the Internet. If the file is not in the cache, the proxy server retrieves the file, forwards it to the requester, and stores it in the cache for the next time it is requested. This scheme can significantly reduce load on an Internet connection and greatly improve response time.

**==The biggest problem with proxy servers is their inability to cope with all but a few protocols==**. Generally established protocols like HTTP, FTP, and SMTP are allowed to pass through, while newer protocols like BitTorrent are not. (Some network administrators consider this a feature.) In the rapidly changing world of the Internet, this is a significant disadvantage. It’s a particular disadvantage for Java programmers because it limits the effectiveness of custom protocols. In Java, it’s easy and often useful to create a new protocol that is optimized for your application. However, no proxy server will ever understand these one-of-a-kind protocols. Consequently, some developers have taken to tunneling their protocols through HTTP, most notably with SOAP.

## The Client/Server Model

Most modern network programming is based on a client/server model. A client/server application typically stores large quantities of data on an expensive, high-powered server or cloud of servers while most of the program logic and the user interface is handled by client software running on relatively cheap personal computers. **==In most cases, a server primarily sends data while a client primarily receives it; but it is rare for one program to send or receive exclusively. A more reliable distinction is that a client initiates a conversation while a server waits for clients to start conversations with it.==**

![[Pasted image 20240729202605.png]]

Not all applications fit easily into a client/server model. For instance, in networked games, it seems likely that both players will send data back and forth roughly equally (at least in a fair game). These sorts of connections are called _peer-to-peer_. The telephone system is the classic example of a peer-to-peer network. Each phone can either call another phone or be called by another phone. You don’t have to buy one phone to send calls and another to receive them.

> A peer-to-peer (P2P) network is a decentralized network where each device (peer) can act as both a client and a server. This allows for direct data sharing and communication between devices without the need for a central server.

Java does not have explicit peer-to-peer communication in its core networking API. However, applications can easily offer peer-to-peer communications in several ways, most commonly by acting as both a server and a client. Alternatively, the peers can communicate with each other through an intermediate server program that forwards data from one peer to the other peers. This neatly solves the discovery problem of how two peers find each other.

## Internet Standards

If you need detailed information about any protocol, the definitive source is the standards document for the protocol.

Although there are many standards organizations in the world, the two that produce most of the standards relevant to application layer network programming and protocols are the Internet Engineering Task Force (IETF) and the World Wide Web Consortium (W3C)

### IETF RFCs

IETF standards and near-standards are published as Requests for Comments (RFCs). Despite the name, a published RFC is a finished work. It may be obsoleted or replaced by a new RFC, but it will not be changed. IETF working documents that are subject to revision and open for development are called “Internet drafts.”

The IETF has traditionally worked behind the scenes to codify and standardize existing practice. Although its activities are completely open to the public, it’s been very low profile

### W3C Recommendations

the W3C standardization process is similar to the IETF process the W3C is a fundamentally different organization. Whereas the IETF is open to participation by anyone, only corporations and other organizations may become members of the W3C.

The W3C has five basic levels of standards:

Note

A note is generally one of two things: either an unsolicited submission by a W3C member (similar to an IETF Internet draft) or random musings by W3C staff or related parties that do not actually describe a full proposal (similar to an IETF informational RFC). Notes will not necessarily lead to the formation of a working group or a W3C recommendation.

Working drafts

A working draft is a reflection of the current thinking of some (not necessarily all) members of a working group. It should eventually lead to a proposed recommendation, but by the time it does so it may have changed substantially.

Candidate recommendation

A candidate recommendation indicates that the working group has reached consensus on all major issues and is ready for third-party comment and implementations. If the implementations do not uncover any obstructions, the spec can be promoted to a proposed recommendation.

Proposed recommendation

A proposed recommendation is mostly complete and unlikely to undergo more than minor editorial changes. The main purpose of a proposed recommendation is to work out bugs in the specification document rather than in the underlying technology being documented.

Recommendation

A recommendation is the highest level of W3C standard. However, the W3C is very careful not to actually call this a “standard” for fear of running afoul of antitrust statutes. The W3C describes a recommendation as a “work that represents consensus within W3C and has the Director’s stamp of approval. W3C considers that the ideas or technology specified by a Recommendation are appropriate for widespread deployment and promote W3C’s mission.”

# Chapter 2. Streams

A large part of what network programs do is simple input and output: moving bytes from one system to another. Bytes are bytes; to a large extent, reading data a server sends you is not all that different from reading a file.

I/O in Java is built on _streams_. Input streams read data; output streams write data. Different stream classes, like `java.io.FileInputStream` and `sun.net.TelnetOutputStream`, read and write particular sources of data. However, all output streams have the same basic methods to write data and all input streams use the same basic methods to read data. After a stream is created, you can often ignore the details of exactly what it is you’re reading or writing.

Filter streams can be chained to either an input stream or an output stream. Filters can modify the data as it’s read or written—for instance, by encrypting or compressing it—or they can simply provide additional methods for converting the data that’s read or written into other formats.

Readers and writers can be chained to input and output streams to allow programs to read and write text (i.e., characters) rather than bytes. Used properly, readers and writers can handle a wide variety of character encodings, including multibyte character sets such as SJIS and UTF-8.

Streams are synchronous; that is, when a program (really a thread) asks a stream to read or write a piece of data, it waits for the data to be read or written before it does anything else. Java also offers nonblocking I/O using channels and buffers. Nonblocking I/O is a little more complicated, but can be much faster in some high-volume applications

## Output Streams

Java’s basic output class is `java.io.OutputStream`:

```java
public abstract class OutputStream 
```

This class provides the fundamental methods needed to write data. These are:

```java
public abstract void write(int b) throws IOException
public void write(byte[] data) throws IOException
public void write(byte[] data, int offset, int length)  throws IOException
public void flush() throws IOException
public void close() throws IOException
```

Subclasses of `OutputStream` use these methods to write data onto particular media. whichever medium you’re writing to, you mostly use only these same five methods.

`OutputStream`’s fundamental method is `write(int b)`. This method takes an integer from 0 to 255 as an argument and writes the corresponding byte to the output stream. This method is declared abstract because subclasses need to change it to handle their particular medium. For instance, a `ByteArrayOutputStream` can implement this method with pure Java code that copies the byte into its array. However, a `FileOutputStream` will need to use native code that understands how to write data in files on the host platform.

Take note that although this method takes an `int` as an argument, it actually writes an unsigned byte. Java doesn’t have an unsigned byte data type, so an `int` has to be used here instead. The only real difference between an unsigned byte and a signed byte is the interpretation. They’re both made up of eight bits, and when you write an `int` onto a network connection using `write(int b)`, only eight bits are placed on the wire. If an `int` outside the range 0–255 is passed to `write(int b)`, the least significant byte of the number is written and the remaining three bytes are ignored.

---
 **TIP**

**On rare occasions, you may find a buggy third-party class that does something different when writing a value outside the range 0–255—for instance, throwing an `IllegalArgumentException` or always writing 255—so it’s best to avoid writing `int`s outside the range 0–255 if possible.**

---

For example, the character-generator protocol defines a server that sends out ASCII text. The most popular variation of this protocol sends 72-character lines containing printable ASCII characters.

this protocol is straightforward to implement using the basic `write()` methods, as the next code fragment demonstrates:

```java
public static void generateCharacters(OutputStream out)
    throws IOException {

   int firstPrintableCharacter     = 33;
   int numberOfPrintableCharacters = 94;
   int numberOfCharactersPerLine   = 72;

   int start = firstPrintableCharacter;
   while (true) { /* infinite loop */
     for (int i = start; i < start + numberOfCharactersPerLine; i++) {
       out.write((
           (i - firstPrintableCharacter) % numberOfPrintableCharacters)
            + firstPrintableCharacter);
     }
     out.write('\R'); // carriage return
     out.write('\N'); // linefeed
     start = ((start + 1) - firstPrintableCharacter)
         % numberOfPrintableCharacters + firstPrintableCharacter;
   }
}
```

An `OutputStream` is passed to the `generateCharacters()` method in the `out` argument. Bytes are written onto `out` one at a time. These bytes are given as integers in a rotating sequence from 33 to 126. Most of the arithmetic here is to make the loop rotate in that range.

Writing a single byte at a time is often inefficient. For example, every TCP segment contains at least 40 bytes of overhead for routing and error correction. If each byte is sent by itself, you may be stuffing the network with 41 times more data than you think you are! Add overhead of the host-to-network layer protocol, and this can be even worse. Consequently, most TCP/IP implementations buffer data to some extent. That is, they accumulate bytes in memory and send them to their eventual destination only when a certain number have accumulated or a certain amount of time has passed. However, **==if you have more than one byte ready to go, it’s not a bad idea to send them all at once.==** Using `write(byte[] data)` or `write(byte[] data, int offset, int length)` is normally much faster than writing all the components of the `data` array one at a time.

```java
public static void generateCharacters(OutputStream out)
    throws IOException {

  int firstPrintableCharacter = 33;
  int numberOfPrintableCharacters = 94;
  int numberOfCharactersPerLine = 72;
  int start = firstPrintableCharacter;
  byte[] line = new byte[numberOfCharactersPerLine + 2];
  // the +2 is for the carriage return and linefeed

  while (true) { /* infinite loop */
    for (int i = start; i < start + numberOfCharactersPerLine; i++) {
      line[i - start] = (byte) ((i - firstPrintableCharacter)
          % numberOfPrintableCharacters + firstPrintableCharacter);
    }
    line[72] = (byte) '\R'; // carriage return
    line[73] = (byte) '\N'; // line feed
    out.write(line);
    start = ((start + 1) - firstPrintableCharacter)
        % numberOfPrintableCharacters + firstPrintableCharacter;
  }
}
```

The algorithm for calculating which bytes to write when is the same as for the previous implementation. The crucial difference is that the bytes are packed into a byte array before being written onto the network.

Streams can also be buffered in software, directly in the Java code as well as in the network hardware. Typically, this is accomplished by chaining a `BufferedOutputStream` or a `BufferedWriter` to the underlying stream, a technique **==Consequently, if you are done writing data, it’s important to flush the output stream.==**

The `flush()` method breaks the deadlock by forcing the buffered stream to send its data even if the buffer isn’t yet full.

![[Pasted image 20240730210523.png]]

It’s important to flush your streams whether you think you need to or not. Depending on how you got hold of a reference to the stream, you may or may not know whether it’s buffered.

If flushing isn’t necessary for a particular stream, it’s a very low-cost operation. However, if it is necessary, it’s very necessary. Failing to flush when you need to can lead to unpredictable, unrepeatable program hangs that are extremely hard to diagnose if you don’t have a good idea of what the problem is in the first place. As a corollary to all this, you should flush all streams immediately before you close them. Otherwise, data left in the buffer when the stream is closed may get lost.

==Finally, when you’re done with a stream, close it by invoking its `close()` method.==
Failure to close a stream in a long-running program can leak file handles, network ports, and other resources.

```java
OutputStream out = null;
try {
  out = new FileOutputStream("/tmp/data.txt");
  // work with the output stream...
} catch (IOException ex) {
  System.err.println(ex.getMessage());
} finally {
  if (out != null) {
    try {
      out.close();
    } catch (IOException ex) {
      // ignore
    }
  }
}
```

This technique is sometimes called **==the _dispose pattern_==**; and it’s common for any object that needs to be cleaned up before it’s garbage collected.

Java 7 introduces the _try with resources_ construct to make this cleanup neater. Instead of declaring the stream variable outside the `try` block, you declare it inside an argument list of the `try` block.

```java
try (OutputStream out = new FileOutputStream("/tmp/data.txt")) {
  // work with the output stream...
} catch (IOException ex) {
  System.err.println(ex.getMessage());
}
```

The `finally` clause is no longer needed. Java automatically invokes `close()` on any `AutoCloseable` objects declared inside the argument list of the `try` block.

## Input Streams

Java’s basic input class is `java.io.InputStream`:

```java
public abstract class InputStream
```

```java
public abstract int read() throws IOException
public int read(byte[] input) throws IOException
public int read(byte[] input, int offset, int length) throws IOException
public long skip(long n) throws IOException
public int available() throws IOException
public void close() throws IOException
```

Concrete subclasses of `InputStream` use these methods to read data from particular media. ut whichever source you’re reading, you mostly use only these same six methods. Sometimes you don’t know exactly what kind of stream you’re reading from.

The basic method of `InputStream` is the no-args `read()` method. This method reads a single byte of data from the input stream’s source and returns it as an `int` from 0 to 255. End of stream is signified by returning –1. The `read()` method waits and blocks execution of any code that follows it until a byte of data is available and ready to be read. Input and output can be slow, so **==if your program is doing anything else of importance, try to put I/O in its own thread.==**

The `read()` method is declared abstract because subclasses need to change it to handle their particular medium.

```java
byte[] input = new byte[10];
for (int i = 0; i < input.length; i++) {
  int b = in.read();
  if (b == -1) break;
  input[i] = (byte) b;
}
```

Although `read()` only reads a byte, it returns an `int`. Thus, a cast is necessary before storing the result in the byte array.

Reading a byte at a time is as inefficient as writing data one byte at a time. Consequently, there are two overloaded `read()` methods that fill a specified array with multiple bytes of data read from the stream `read(byte[] input)` and `read(byte[] input,` `int` `offset,` `int length)`. The first method attempts to fill the specified array `input`. The second attempts to fill the specified subarray of `input`, starting at `offset` and continuing for `length` bytes.

**==Notice I said these methods _attempt_ to fill the array==**, not that they necessarily succeed. An attempt may fail in several ways. For instance, it’s not unheard of that while your program is reading data from a remote web server over DSL, a bug in a switch at a phone company central office will disconnect you and several hundred of your neighbors from the rest of the world. This would cause an `IOException`.

To account for this, the multibyte read methods return the number of bytes actually read.

```java
byte[] input  = new byte[1024];
int bytesRead = in.read(input);
```

**==To guarantee that all the bytes you want are actually read, place the read in a loop that reads repeatedly until the array is filled.==**

```java
int bytesRead   = 0;
int bytesToRead = 1024;
byte[] input    = new byte[bytesToRead];
while (bytesRead < bytesToRead) {
  bytesRead += in.read(input, bytesRead, bytesToRead - bytesRead);
}
```

This technique is especially crucial for network streams. Chances are that if a file is available at all, all the bytes of a file are also available. However, because networks move much more slowly than CPUs, it is very easy for a program to empty a network buffer before all the data has arrived. In fact, if one of these two methods tries to read from a temporarily empty but open network buffer, it will generally return 0, indicating that no data is available but the stream is not yet closed. This is often preferable to the behavior of the single-byte `read()` method, which blocks the running thread in the same circumstances.

All three `read()` methods return –1 to signal the end of the stream. If the stream ends while there’s still data that hasn’t been read, the multibyte `read()` methods return the data until the buffer has been emptied.

The previous code fragment had a bug because it didn’t consider the possibility that all 1,024 bytes might never arrive (as opposed to not being immediately available). Fixing that bug requires testing the return value of `read()` before adding it to `bytesRead`

```java
int bytesRead = 0;
int bytesToRead = 1024;
byte[] input = new byte[bytesToRead];
while (bytesRead < bytesToRead) {
  int result = in.read(input, bytesRead, bytesToRead - bytesRead);
  if (result == -1) break; // end of stream
  bytesRead += result;
}
```

If you do not want to wait until all the bytes you need are immediately available, you can use the `available()` method to determine how many bytes can be read without blocking. This returns the minimum number of bytes you can read.

```java
int bytesAvailable = in.available();
byte[] input = new byte[bytesAvailable];
int bytesRead = in.read(input, 0, bytesAvailable);
// continue with rest of program immediately...
```

In this case, you can expect that `bytesRead` is exactly equal to `bytesAvailable`.

On rare occasions, you may want to skip over data without reading it. The `skip()` method accomplishes this task. It’s less useful on network connections than when reading from files. Network connections are sequential and normally quite slow, so it’s not significantly more time consuming to read data than to skip over it.

**==As with output streams, once your program has finished with an input stream, it should close it by invoking its `close()` method.==**

### Marking and Resetting

The `InputStream` class also has three less commonly used methods that allow programs to back up and reread data they’ve already read. These are:

```java
public void mark(int readAheadLimit)
public void reset() throws IOException
public boolean markSupported()
```

In order to reread data, mark the current position in the stream with the `mark()` method. At a later point, you can reset the stream to the marked position using the `reset()` method. Subsequent reads then return data starting from the marked position. **==However, you may not be able to reset as far back as you like. The number of bytes you can read from the mark and still reset is determined by the `readAheadLimit` argument to `mark()`==**. If you try to reset too far back, an `IOException` is thrown. Furthermore, **==there can be only one mark in a stream at any given time. Marking a second location erases the first mark.==**

 **==Before trying to use marking and resetting, check whether the `markSupported()` method returns true. If it does, the stream supports marking and resetting. Otherwise, `mark()` will do nothing and `reset()` will throw an `IOException`.==**

The only input stream classes in `java.io` that always support marking are `BufferedInputStream` and `ByteArrayInputStream`.
## Filter Streams

`InputStream` and `OutputStream` are fairly raw classes. Deciding what those bytes mean—whether they’re integers or IEEE 754 floating-point numbers or Unicode text—is completely up to the programmer and the code. However, there are certain extremely common data formats that can benefit from a solid implementation in the class library. For example, many integers passed as parts of network protocols are 32-bit big-endian integers. Much of the text sent over the Web is either 7-bit ASCII, 8-bit Latin-1, or multibyte UTF-8. Many files transferred by FTP are stored in the ZIP format. Java provides a number of filter classes you can attach to raw streams to translate the raw bytes to and from these and other formats.

The filters come in two versions: the filter streams, and the readers and writers. The filter streams still work primarily with raw data as bytes: for instance, by compressing the data or interpreting it as binary numbers. The readers and writers handle the special case of text in a variety of encodings such as UTF-8 and ISO 8859-1.

Filters are organized in a chain Each link in the chain receives data from the previous filter or stream and passes the data along to the next link in the chain

![[Pasted image 20240730212451.png]]

Every filter output stream has the same `write()`, `close()`, and `flush()` methods as `java.io.OutputStream`. Every filter input stream has the same `read()`, `close()`, and `available()` methods as `java.io.InputStream`. 

The filtering is purely internal and does not expose any new public interface. However, in most cases, the filter stream adds public methods with additional purposes. Sometimes these are intended to be used in addition to the usual `read()` and `write()` methods, like the `unread()` method of `PushbackInputStream`. At other times, they almost completely replace the original interface.
### Chaining Filters Together

**==Filters are connected to streams by their constructors.==**

```java
FileInputStream     fin = new FileInputStream("data.txt");
BufferedInputStream bin = new BufferedInputStream(fin);
```

From this point forward, it’s possible to use the `read()` methods of both `fin` and `bin` to read data from the file _data.txt_. However, intermixing calls to different streams connected to the same source may violate several implicit contracts of the filter streams. **==Most of the time, you should only use the last filter in the chain to do the actual reading or writing.==**

```java
InputStream in = new FileInputStream("data.txt");
in = new BufferedInputStream(in);
```

After these two lines execute, there’s no longer any way to access the underlying file input stream, so you can’t accidentally read from it and corrupt the buffer. This example works because it’s not necessary to distinguish between the methods of `InputStream` and those of `BufferedInputStream` given that `BufferedInputStream` is simply used polymorphically as an instance of `InputStream`. In cases where it is necessary to use the additional methods of the filter stream not declared in the superclass, you may be able to construct one stream directly inside another.

```java
DataOutputStream dout = new DataOutputStream(new BufferedOutputStream(
    new FileOutputStream("data.txt")));
```

```java
DataOutputStream dout = new DataOutputStream(
                         new BufferedOutputStream(
                          new FileOutputStream("data.txt")
                         )
                        );
```

==**Connection is permanent. Filters cannot be disconnected from a stream.**== **==under no circumstances should you ever read from or write to anything other than the last filter in the chain.==**

### Buffered Streams

**==The `BufferedOutputStream` class stores written data in a buffer (a protected byte array field named `buf`) until the buffer is full or the stream is flushed. Then it writes the data onto the underlying output stream all at once. A single write of many bytes is almost always much faster than many small writes that add up to the same thing.==** This is especially true of network connections because each TCP segment or UDP packet carries a finite amount of overhead, generally about 40 bytes’ worth. This means that sending 1 kilobyte of data 1 byte at a time actually requires sending 40 kilobytes over the wire, whereas sending it all at once only requires sending a little more than 1K of data. Most network cards and TCP implementations provide some level of buffering themselves, so the real numbers aren’t quite this dramatic. Nonetheless, buffering network output is generally a huge performance win.

The `BufferedInputStream` class also has a protected byte array named `buf` that serves as a buffer. When one of the stream’s `read()` methods is called, it first tries to get the requested data from the buffer. Only when the buffer runs out of data does the stream read from the underlying source. At this point, it reads as much data as it can from the source into the buffer, whether it needs all the data immediately or not. Data that isn’t used immediately will be available for later invocations of `read()`. When reading files from a local disk, it’s almost as fast to read several hundred bytes of data from the underlying stream as it is to read one byte of data. Therefore, **==buffering can substantially improve performance.==** **==Nonetheless, buffering input rarely hurts and will become more important over time as network speeds increase.==**

```java
public BufferedInputStream(InputStream in)
public BufferedInputStream(InputStream in, int bufferSize)
public BufferedOutputStream(OutputStream out)
public BufferedOutputStream(OutputStream out, int bufferSize)
```

The first argument is the underlying stream from which unbuffered data will be read or to which buffered data will be written. The second argument, if present, specifies the number of bytes in the buffer. Otherwise, the buffer size is set to 2,048 bytes for an input stream and 512 bytes for an output stream. The ideal size for a buffer depends on what sort of stream you’re buffering.

`BufferedInputStream` does not declare any new methods of its own. It only overrides methods from `InputStream`. It does support marking and resetting. The two multibyte `read()` methods attempt to completely fill the specified array or subarray of data by reading from the underlying input stream as many times as necessary. **==They return only when the array or subarray has been completely filled, the end of stream is reached, or the underlying stream would block on further reads==**. Most input streams do not behave like this. They read from the underlying stream or data source only once before returning.

`BufferedOutputStream` also does not declare any new methods of its own. You invoke its methods exactly as you would in any output stream. The difference is that each write places data in the buffer rather than directly on the underlying output stream. Consequently, it is essential to flush the stream when you reach a point at which the data needs to be sent.
### PrintStream

The `PrintStream` class is the first filter output stream most programmers encounter because `System.out` is a `PrintStream`. However, other output streams can also be chained to print streams, using these two constructors:

```java
public PrintStream(OutputStream out)
public PrintStream(OutputStream out, boolean autoFlush)
```

By default, print streams should be explicitly flushed. However, if the `autoFlush` argument is `true`, the stream will be flushed every time a byte array or linefeed is written or a `println()` method is invoked.

As well as the usual `write()`, `flush()`, and `close()` methods, `PrintStream` has 9 overloaded `print()` methods and 10 overloaded `println()` methods:

```java
public void print(boolean b)
public void print(char c)
public void print(int i)
public void print(long l)
public void print(float f)
public void print(double d)
public void print(char[] text)
public void print(String s)
public void print(Object o)
public void println()
public void println(boolean b)
public void println(char c)
public void println(int i)
public void println(long l)
public void println(float f)
public void println(double d)
public void println(char[] text)
public void println(String s)
public void println(Object o)
```

---

 ==**WARNING**==
==**`PrintStream` is evil and network programmers should avoid it like the plague!**==

---

**==The first problem is that the output from `println()` is platform dependent. Depending on what system runs your code, lines may sometimes be broken with a linefeed, a carriage return, or a carriage return/linefeed pair.==** This doesn’t cause problems when writing to the console, but it’s a disaster for writing network clients and servers that must follow a precise protocol. Most network protocols such as HTTP and Gnutella specify that lines should be terminated with a carriage return/linefeed pair. Using `println()` makes it easy to write a program that works on Windows but fails on Unix and the Mac. Although many servers and clients are liberal in what they accept and can handle incorrect line terminators, there are occasional exceptions.

**==The second problem is that `PrintStream` assumes the default encoding of the platform on which it’s running. However, this encoding may not be what the server or client expects. whether the client expects or understands those encodings or not. `PrintStream` doesn’t provide any mechanism for changing the default encoding.==** This problem can be patched over by using the related `PrintWriter` class instead. But the problems continue.

**==The third problem is that `PrintStream` eats all exceptions.==** This makes `PrintStream` suitable for textbook programs such as HelloWorld, because simple console output can be taught without burdening students with first learning about exception handling and all that implies. However, network connections are much less reliable than the console. Connections routinely fail because of network congestion, phone company misfeasance, remote systems crashing, and many other reasons. Network programs must be prepared to deal with unexpected interruptions in the flow of data. The way to do this is by handling exceptions. However, `PrintStream` catches any exceptions thrown by the underlying output stream. **==`PrintStream` does not have the usual `throws IOException` declaration:==**

```java
public abstract void write(int b)
public void write(byte[] data)
public void write(byte[] data, int offset, int length)
public void flush()
public void close()
```

If the underlying stream throws an exception, this internal error flag is set. The programmer is relied upon to check the value of the flag using the `checkError()` method:

```java
public boolean checkError()
```

### Data Streams

The `DataInputStream` and `DataOutputStream` classes provide methods for reading and writing Java’s primitive data types and strings in a binary format. **==The binary formats used are primarily intended for exchanging data between two different Java programs through a network connection, a datafile, a pipe, or some other intermediary.==** What a data output stream writes, a data input stream can read. However, it happens that the formats are the same ones used for most Internet protocols that exchange binary numbers. For instance, the time protocol uses 32-bit big-endian integers, just like Java’s `int` data type. The controlled-load network element service uses 32-bit IEEE 754 floating-point numbers, just like Java’s `float` data type. However, this isn’t true for all network protocols, so check the details of any protocol you use.

The `DataOutputStream` class offers these 11 methods for writing particular Java data types:

```java
public final void writeBoolean(boolean b) throws IOException
public final void writeByte(int b) throws IOException
public final void writeShort(int s) throws IOException
public final void writeChar(int c) throws IOException
public final void writeInt(int i) throws IOException
public final void writeLong(long l) throws IOException
public final void writeFloat(float f) throws IOException
public final void writeDouble(double d) throws IOException
public final void writeChars(String s) throws IOException
public final void writeBytes(String s) throws IOException
public final void writeUTF(String s) throws IOException
```

All data is written in big-endian format. Integers are written in two’s complement in the minimum number of bytes possible. Thus, a `byte` is written as one byte, a `short` as two bytes, an `int` as four bytes, and a `long` as eight bytes. Floats and doubles are written in IEEE 754 form in four and eight bytes, respectively. Booleans are written as a single byte with the value 0 for false and 1 for true. Chars are written as two unsigned bytes.

The last three methods are a little trickier. The `writeChars()` method simply iterates through the `String` argument, writing each character in turn as a two-byte, big-endian Unicode character The `writeBytes()` method iterates through the `String` argument but writes only the least significant byte of each character. Thus, information will be lost for any string with characters from outside the Latin-1 character set. This method may be useful on some network protocols that specify the ASCII encoding, but it should be avoided most of the time.

Neither `writeChars()` nor `writeBytes()` encodes the length of the string in the output stream. As a result, you can’t really distinguish between raw characters and characters that make up part of a string. The `writeUTF()` method does include the length of the string. It encodes the string itself in a _variant_ of the UTF-8 encoding of Unicode. Because this variant is subtly incompatible with most non-Java software, it should be used only for exchanging data with other Java programs that use a `DataInputStream` to read strings

Along with these methods for writing binary numbers and strings, `DataOutputStream` of course has the usual `write()`, `flush()`, and `close()` methods any `OutputStream` class has.

Every format that `DataOutputStream` writes, `DataInputStream` can read. In addition, `DataInputStream` has the usual `read()`, `available()`, `skip()`, and `close()` methods, as well as methods for reading complete arrays of bytes and lines of text.

```java
public final boolean readBoolean() throws IOException
public final byte readByte() throws IOException
public final char readChar() throws IOException
public final short readShort() throws IOException
public final int readInt() throws IOException
public final long readLong() throws IOException
public final float readFloat() throws IOException
public final double readDouble() throws IOException
public final String readUTF() throws IOException
```

In addition, `DataInputStream` provides two methods to read unsigned bytes and unsigned shorts and return the equivalent `int`. Java doesn’t have either of these data types, but you may encounter them when reading binary data written by a C program:

```java
public final int readUnsignedByte() throws IOException
public final int readUnsignedShort() throws IOException
```

`DataInputStream` has the usual two multibyte `read()` methods that read data into an array or subarray and return the number of bytes read.

```java
public final int read(byte[] input) throws IOException
public final int read(byte[] input, int offset, int length)
    throws IOException
public final void readFully(byte[] input) throws IOException
public final void readFully(byte[] input, int offset, int length)
    throws IOException
```

Finally, `DataInputStream` provides the popular `readLine()` method that reads a line of text as delimited by a line terminator and returns a string:

```java
public final String readLine() throws IOException
```

**==However, this method should not be used under any circumstances, both because it is deprecated==** and because it is buggy. It’s deprecated because it doesn’t properly convert non-ASCII characters to bytes in most circumstances. That task is now handled by the `readLine()` method of the `BufferedReader` class.

This problem isn’t obvious when reading files because there will almost certainly be a next character: –1 for end of stream, if nothing else. However, on persistent network connections such as those used for FTP and late-model HTTP, a server or client may simply stop sending data after the last character and wait for a response without actually closing the connection. If you’re lucky, the connection may eventually time out on one end or the other and you’ll get an `IOException`, although this will probably take at least a couple of minutes, and cause you to lose the last line of data from the stream. If you’re not lucky, the program will hang indefinitely.
## Readers and Writers

Java provides an almost complete mirror of the input and output stream class hierarchy designed for working with characters instead of bytes In this mirror image hierarchy, two abstract superclasses define the basic API for reading and writing characters. The `java.io.Reader` class specifies the API by which characters are read. The `java.io.Writer` class specifies the API by which characters are written. Wherever input and output streams use bytes, readers and writers use Unicode characters. Concrete subclasses of `Reader` and `Writer` allow particular sources to be read and targets to be written. Filter readers and writers can be attached to other readers and writers to provide additional services or interfaces.

**==The most important concrete subclasses of `Reader` and `Writer` are the `InputStreamReader` and the `OutputStreamWriter` classes.==**

In addition to these two classes, the `java.io` package provides several raw reader and writer classes that read characters without directly requiring an underlying input stream, including:

- `FileReader`
- `FileWriter`
- `StringReader`
- `StringWriter`
- `CharArrayReader`
- `CharArrayWriter`

The first two classes in this list work with files and the last four work inside Java, so they aren’t of great use for network programming. However, aside from different constructors, these classes have pretty much the same public interface as all other reader and writer classes.
### Writers

The `Writer` class mirrors the `java.io.OutputStream` class. It’s abstract and has two protected constructors. Like `OutputStream`, the `Writer` class is never used directly; instead, it is used polymorphically, through one of its subclasses. It has five `write()` methods as well as a `flush()` and a `close()` method:

```java
protected Writer()
protected Writer(Object lock)
public abstract void write(char[] text, int offset, int length)
    throws IOException
public void write(int c) throws IOException
public void write(char[] text) throws IOException
public void write(String s) throws IOException
public void write(String s, int offset, int length) throws IOException
public abstract void flush() throws IOException
public abstract void close() throws IOException
```

The `write(char[] text, int offset, int length)` method is the base method in terms of which the other four `write()` methods are implemented. For example, given a `Writer` object `w`, you can write the string “Network” like this:

```java
char[] network = {'N', 'E', 'T', 'W', 'O', 'R', 'K'};
w.write(network, 0, network.length);
```

The same task can be accomplished with these other methods, as well:

```java
w.write(network);
for (int i = 0;  i < network.length;  i++) w.write(network[i]);
w.write("Network");
w.write("Network", 0, 7);
```

All of these examples are different ways of expressing the same thing.

Writers may be buffered, either directly by being chained to a `BufferedWriter` or indirectly because their underlying output stream is buffered. To force a write to be committed to the output medium, invoke the `flush()` method:

```java
w.flush();
```

The `close()` method behaves similarly to the `close()` method of `OutputStream`. `close()` flushes the writer, then closes the underlying output stream and releases any resources associated with it:

```java
public abstract void close() throws IOException
```

### OutputStreamWriter

`OutputStreamWriter` is the most important concrete subclass of `Writer`. An `OutputStreamWriter` receives characters from a Java program. It converts these into bytes according to a specified encoding and writes them onto an underlying output stream.

```java
public OutputStreamWriter(OutputStream out, String encoding)
    throws UnsupportedEncodingException
```

If no encoding is specified, the default encoding for the platform is used. For example, this code fragment writes the first few words of Homer’s Odyssey in the CP1253 Windows Greek encoding:

```java
OutputStreamWriter w = new OutputStreamWriter(
    new FileOutputStream("OdysseyB.txt"), "Cp1253");
w.write("ἦμος δ΄ ἠριγένεια φάνη ῥοδοδάκτυλος Ἠώς");
```

Other than the constructors, `OutputStreamWriter` has only the usual `Writer` methods and one method to return the encoding of the object: 

```java
public String getEncoding()
```
### Readers

The `Reader` class mirrors the `java.io.InputStream` class. It’s abstract with two protected constructors. Like `InputStream` and `Writer`, the `Reader` class is never used directly, only through one of its subclasses. It has three `read()` methods, as well as `skip()`, `close()`, `ready()`, `mark()`, `reset()`, and `markSupported()` methods:

```java
protected Reader()
protected Reader(Object lock)
public abstract int read(char[] text, int offset, int length)
    throws IOException
public int read() throws IOException
public int read(char[] text) throws IOException
public long skip(long n) throws IOException
public boolean ready()
public boolean markSupported()
public void mark(int readAheadLimit) throws IOException
public void reset() throws IOException
public abstract void close() throws IOException
```

The `read(char[] text, int offset, int length)` method is the fundamental method through which the other two `read()` methods are implemented.

The exception to the rule of similarity is `ready()`, which has the same general purpose as `available()` but not quite the same semantics, even modulo the byte-to-char conversion. Whereas `available()` returns an `int` specifying a minimum number of bytes that may be read without blocking, `ready()` only returns a `boolean` indicating whether the reader may be read without blocking. The problem is that some character encodings, such as UTF-8, use different numbers of bytes for different characters. Thus, it’s hard to tell how many characters are waiting in the network or filesystem buffer without actually reading them out of the buffer.

`InputStreamReader` is the most important concrete subclass of `Reader`. It converts these into characters according to a specified encoding and returns them. The constructor specifies the input stream to read from and the encoding to use:

```java
public InputStreamReader(InputStream in)
public InputStreamReader(InputStream in, String encoding)
    throws UnsupportedEncodingException
```

If no encoding is specified, the default encoding for the platform is used

```java
public static String getMacCyrillicString(InputStream in)
    throws IOException {

  InputStreamReader r = new InputStreamReader(in, "MacCyrillic");
  StringBuilder sb = new StringBuilder();
  int c;
  while ((c = r.read()) != -1) sb.append((char) c);
  return sb.toString();
}
```
### Filter Readers and Writers

The `InputStreamReader` and `OutputStreamWriter` classes act as decorators on top of input and output streams that change the interface from a byte-oriented interface to a character-oriented interface. Once this is done, additional character-oriented filters can be layered on top of the reader or writer using the `java.io.FilterReader` and `java.io.FilterWriter` classes. As with filter streams, there are a variety of subclasses that perform specific filtering, including:

- `BufferedReader`
- `BufferedWriter`
- `LineNumberReader`
- `PushbackReader`
- `PrintWriter`

The `BufferedReader` and `BufferedWriter` classes are the character-based equivalents of the byte-oriented `BufferedInputStream` and `BufferedOutputStream` classes. Where `BufferedInputStream` and `BufferedOutputStream` use an internal array of bytes as a buffer, `BufferedReader` and `BufferedWriter` use an internal array of chars.

When a program reads from a `BufferedReader`, text is taken from the buffer rather than directly from the underlying input stream or other text source. When the buffer empties, it is filled again with as much text as possible, even if not all of it is immediately needed, making future reads much faster. When a program writes to a `BufferedWriter`, the text is placed in the buffer. The text is moved to the underlying output stream or other target only when the buffer fills up or when the writer is explicitly flushed, which can make writes much faster than would otherwise be the case.

```java
public BufferedReader(Reader in, int bufferSize)
public BufferedReader(Reader in)
public BufferedWriter(Writer out)
public BufferedWriter(Writer out, int bufferSize)
```

```java
public static String getMacCyrillicString(InputStream in)
    throws IOException {

  Reader r = new InputStreamReader(in, "MacCyrillic");
  r = new BufferedReader(r, 1024);
  StringBuilder sb = new StringBuilder();
  int c;
  while ((c = r.read()) != -1) sb.append((char) c);
  return sb.toString();
}
```

All that was needed to buffer this method was one additional line of code. None of the rest of the algorithm had to change, because the only `InputStreamReader` methods used were the `read()` and `close()` methods declared in the `Reader` superclass and shared by all `Reader` subclasses, including `BufferedReader`.

The `BufferedWriter()` class adds one new method not included in its superclass, called `newLine()`, also geared toward writing lines:

```java
public void newLine() throws IOException
```

This method inserts a platform-dependent line-separator string into the output. The `line.separator` system property determines exactly what the string is: probably a linefeed on Unix and Mac OS X, and a carriage return/linefeed pair on Windows. Because network protocols generally specify the required line terminator, you should not use this method for network programming. Instead, explicitly write the line terminator the protocol requires.

### PrintWriter

The `PrintWriter` class is a replacement for Java 1.0’s `PrintStream` class that properly handles multibyte character sets and international text.

Aside from the constructors, the `PrintWriter` class has an almost identical collection of methods to `PrintStream`. These include:

```java
public PrintWriter(Writer out)
public PrintWriter(Writer out, boolean autoFlush)
public PrintWriter(OutputStream out)
public PrintWriter(OutputStream out, boolean autoFlush)
public void flush()
public void close()
public boolean checkError()
public void write(int c)
public void write(char[] text, int offset, int length)
public void write(char[] text)
public void write(String s, int offset, int length)
public void write(String s)
public void print(boolean b)
public void print(char c)
public void print(int i)
public void print(long l)
public void print(float f)
public void print(double d)
public void print(char[] text)
public void print(String s)
public void print(Object o)
public void println()
public void println(boolean b)
public void println(char c)
public void println(int i)
public void println(long l)
public void println(float f)
public void println(double d)
public void println(char[] text)
public void println(String s)
public void println(Object o)
```

# Chapter 3. Threads

threads are easier on resources because they share memory. Using threads instead of processes can buy you another factor of three in server performance. By combining this with a pool of reusable threads (as opposed to a pool of reusable processes), your server can run nine times faster, all on the same hardware and network connection! The impact of running many different threads on the server hardware is _relatively_ minimal because they all run within one process. Most Java virtual machines keel over due to memory exhaustion somewhere between 4,000 and 20,000 simultaneous threads. However, by using a thread pool instead of spawning new threads for each connection, fewer than a hundred threads can handle thousands of short connections per minute.

Unfortunately, this increased performance doesn’t come for free. There’s a cost in program complexity. In particular, multithreaded servers (and other multithreaded programs) require developers to address concerns that aren’t issues for single-threaded programs, particularly issues of safety and liveness. Because different threads share the same memory, it’s entirely possible for one thread to stomp all over the variables and data structures used by another thread.

Consequently, different threads have to be extremely careful about which resources they use when. Generally, each thread must agree to use certain resources only when it’s sure those resources can’t change or that it has exclusive access to them. However, it’s also possible for two threads to be too careful, each waiting for exclusive access to resources it will never get. This can lead to deadlock, in which two threads are each waiting for resources the other possesses. Neither thread can proceed without the resources that the other thread has reserved, but neither is willing to give up the resources it has already.

## Running Threads

A _thread_ with a little _t_ is a separate, independent path of execution in the virtual machine. A `Thread` with a capital _T_ is an instance of the `java.lang.Thread` class. There is a one-to-one relationship between threads executing in the virtual machine and `Thread` objects constructed by the virtual machine. Most of the time it’s obvious from the context which one is meant if the difference is really important.

To start a new thread running in the virtual machine, you construct an instance of the `Thread` class and invoke its `start()` method, like this:

```java
Thread t = new Thread();
t.start();
```

To give a thread something to do, you either subclass the `Thread` class and override its `run()` method, or implement the `Runnable` interface and pass the `Runnable` object to the `Thread` constructor **==In both cases, the key is the `run()` method, which has this signature:==**

```java
public void run()
```

This method may invoke other methods; it may construct other objects; it may even spawn other threads. However, the thread starts here and it stops here. When the `run()` method completes, the thread dies. **==In essence, the `run()` method is to a thread what the `main()` method is to a traditional nonthreaded program==**. A single-threaded program exits when the `main()` method returns. A multithreaded program exits when both the `main()` method and the `run()` methods of all nondaemon threads return.

### Subclassing Thread

Consider a program that calculates the Secure Hash Algorithm (SHA) digest for many files. To a large extent, this is an I/O-bound program (i.e., its speed is limited by the amount of time it takes to read the files from the disk). If you write it as a standard program that processes the files in series, the program is going to spend a lot of time waiting for the hard drive to return the data. This limit is even more characteristic of network programs: they execute faster than the network can supply input. Consequently, they spend a lot of time blocked. This is time that other threads could use, either to process other input sources or to do something that doesn’t rely on slow input.

Example 3-1. ``DigestThread``

```java
import java.io.*;
import java.security.*;
import javax.xml.bind.*; // for DatatypeConverter; requires Java 6 or JAXB 1.0

public class DigestThread extends Thread {

  private String filename;

  public DigestThread(String filename) {
   this.filename = filename;
  }

  @Override
  public void run() {
    try {
      FileInputStream in = new FileInputStream(filename);
      MessageDigest sha = MessageDigest.getInstance("SHA-256");
      DigestInputStream din = new DigestInputStream(in, sha);
      while (din.read() != -1) ;
      din.close();
      byte[] digest = sha.digest();

      StringBuilder result = new StringBuilder(filename);
      result.append(": ");
      result.append(DatatypeConverter.printHexBinary(digest));
      System.out.println(result);
    } catch (IOException ex) {
      System.err.println(ex);
    } catch (NoSuchAlgorithmException ex) {
      System.err.println(ex);
    }
  }

  public static void main(String[] args) {
    for (String filename : args) {
      Thread t = new DigestThread(filename);
      t.start();
    }
  }
}
```

The `main()` method reads filenames from the command line and starts a new `DigestThread` for each one. The work of the thread is actually performed in the `run()` method.

**==Because the signature of the `run()` method is fixed, you can’t pass arguments to it or return values from it.==** Consequently, you need different ways to pass information into the thread and get information out of it. The simplest way to pass information in is to pass arguments to the constructor, which sets fields in the `Thread` subclass, as done here.

Getting information out of a thread back into the original calling thread is trickier because of the asynchronous nature of threads. however, you’ll want to pass the information to other parts of the program. You can store the result of the calculation in a field and provide a getter method to return the value of that field. However, how do you know when the calculation of that value is complete? What do you return if somebody calls the getter method before the value has been calculated

---

**==If you subclass `Thread`, you should override `run()` _and nothing else!_ The various other methods of the `Thread` class—for example, `start()`, `interrupt()`, `join()`, `sleep()`, and so on—all have very specific semantics and interactions with the virtual machine that are difficult to reproduce in your own code. You should override `run()` and provide additional constructors and other methods as necessary, but you should not replace any of the other standard `Thread` methods.==**

---

### Implementing the Runnable Interface

One way to avoid overriding the standard `Thread` methods is not to subclass `Thread`. Instead, write the task you want the thread to perform as an instance of the `Runnable` interface. This interface declares the `run()` method, exactly the same as the `Thread` class:

```java
public void run()
```

Other than this method, which any class implementing this interface must provide, you are completely free to create any other methods with any other names you choose, all without any possibility of unintentionally interfering with the behavior of the thread.

```java
Thread t = new Thread(myRunnableObject);
t.start();
```

Example 3-2. ``DigestRunnable``

```java
import java.io.*;
import java.security.*;
import javax.xml.bind.*; // for DatatypeConverter; requires Java 6 or JAXB 1.0

public class DigestRunnable implements Runnable {

  private String filename;

  public DigestRunnable(String filename) {
   this.filename = filename;
  }

  @Override
  public void run() {
    try {
      FileInputStream in = new FileInputStream(filename);
      MessageDigest sha = MessageDigest.getInstance("SHA-256");
      DigestInputStream din = new DigestInputStream(in, sha);
      while (din.read() != -1) ;
      din.close();
      byte[] digest = sha.digest();

      StringBuilder result = new StringBuilder(filename);
      result.append(": ");
      result.append(DatatypeConverter.printHexBinary(digest));
      System.out.println(result);
    } catch (IOException ex) {
      System.err.println(ex);
    } catch (NoSuchAlgorithmException ex) {
      System.err.println(ex);
    }
  }

  public static void main(String[] args) {
    for (String filename : args) {
      DigestRunnable dr = new DigestRunnable(filename);
      Thread t = new Thread(dr);
      t.start();
    }
  }
}
```

There’s no strong reason to prefer implementing `Runnable` to extending `Thread` or vice versa in the general case. some object-oriented purists argue that the task that a thread undertakes is not really a kind of `Thread`, and therefore should be placed in a separate class or interface such as `Runnable` rather than in a subclass of `Thread`.

## Returning Information from a Thread

Getting information out of a finished thread is one of the most commonly misunderstood aspects of multithreaded programming. The `run()` method and the `start()` method don’t return any values.

Example 3-3. A thread that uses an accessor method to return the result

```java
import java.io.*;
import java.security.*;

public class ReturnDigest extends Thread {

  private String filename;
  private byte[] digest;

  public ReturnDigest(String filename) {
    this.filename = filename;
  }

  @Override
  public void run() {
    try {
      FileInputStream in = new FileInputStream(filename);
      MessageDigest sha = MessageDigest.getInstance("SHA-256");
      DigestInputStream din = new DigestInputStream(in, sha);
      while (din.read() != -1) ; // read entire file
      din.close();
      digest = sha.digest();
    } catch (IOException ex) {
      System.err.println(ex);
    } catch (NoSuchAlgorithmException ex) {
      System.err.println(ex);
    }
  }

  public byte[] getDigest() {
    return digest;
  }
}
```

Example 3-4. A main program that uses the accessor method to get the output of the thread

```java
import javax.xml.bind.*; // for DatatypeConverter

public class ReturnDigestUserInterface {

  public static void main(String[] args) {
    for (String filename : args) {
      // Calculate the digest
      ReturnDigest dr = new ReturnDigest(filename);
      dr.start();

      // Now print the result
      StringBuilder result = new StringBuilder(filename);
      result.append(": ");
      byte[] digest = dr.getDigest();
      result.append(DatatypeConverter.printHexBinary(digest));
      System.out.println(result);
    }
  }
}
```

when you run this program, the result may not be what you expect:

```shell
D:\JAVA\JNP4\examples\03>java ReturnDigestUserInterface *.java
Exception in thread "main" java.lang.NullPointerException
  at javax.xml.bind.DatatypeConverterImpl.printHexBinary
  (DatatypeConverterImpl.java:358)
  at javax.xml.bind.DatatypeConverter.printHexBinary(DatatypeConverter.java:560)
  at ReturnDigestUserInterface.main(ReturnDigestUserInterface.java:15)
```

The problem is that the main program gets the digest and uses it before the thread has had a chance to initialize it. Although this flow of control would work in a single-threaded program in which `dr.start()` simply invoked the `run()` method in the same thread, that’s not what happens here. The calculations that `dr.start()` kicks off may or may not finish before the `main()` method reaches the call to `dr.getDigest()`. If they haven’t finished, `dr.getDigest()` returns `null`, and the first attempt to access `digest` throws a `NullPointerException`.

### Race Conditions

One possibility is to move the call to `dr.getDigest()` later in the `main()` method, like this:

```java
public static void main(String[] args) {

  ReturnDigest[] digests = new ReturnDigest[args.length];

  for (int i = 0; i < args.length; i++) {
    // Calculate the digest
    digests[i] = new ReturnDigest(args[i]);
    digests[i].start();
  }

  for (int i = 0; i < args.length; i++) {
    // Now print the result
    StringBuffer result = new StringBuffer(args[i]);
    result.append(": ");
    byte[] digest = digests[i].getDigest();
    result.append(DatatypeConverter.printHexBinary(digest));

    System.out.println(result);
  }
}
```

If you’re lucky, this will work and you’ll get the expected output, like this:
```shell
D:\JAVA\JNP4\examples\03>java ReturnDigest2 *.java
AccumulatingError.java: 7B261F7D88467A1D30D66DD29EEEDE495EA16FCD3ADDB8B613BC2C5DC
BenchmarkScalb.java: AECE2AD497F11F672184E45F2885063C99B2FDD41A3FC7C7B5D4ECBFD2B0
CanonicalPathComparator.java: FE0AACF55D331BBF555528A876C919EAD826BC79B659C489D62
Catenary.java: B511A9A507B43C9CDAF626D5B3A8CCCD80149982196E66ED1BFFD5E55B11E226
...
```

let me emphasize that point about being _lucky_. You may not get this output. In fact, you may still get a `NullPointerException`. Whether this code works is completely dependent on whether every one of the `ReturnDigest` threads finishes before its `getDigest()` method is called. If the first `for` loop is too fast and the second `for` loop is entered before the threads spawned by the first loop start finishing, you’re back where you started. Worse yet, the program may appear to hang with no output at all, not even a stack trace.

Whether you get the correct results, an exception, or a hung program depends on many factors, including how many threads the program spawns, the speed of the CPU and disk on the system where this is run, how many CPUs the system uses, and the algorithm the Java virtual machine uses to allot time to different threads. This is called a _race condition_. Getting the correct result depends on the relative speeds of different threads, and you can’t control those!

### Polling

The solution most novices adopt is to make the getter method return a flag value (or perhaps throw an exception) until the result field is set. Then the main thread periodically polls the getter method to see whether it’s returning something other than the flag value.

```java
public static void main(String[] args) {

  ReturnDigest[] digests = new ReturnDigest[args.length];

  for (int i = 0; i < args.length; i++) {
    // Calculate the digest
    digests[i] = new ReturnDigest(args[i]);
    digests[i].start();
  }

  for (int i = 0; i < args.length; i++) {
    while (true) {
      // Now print the result
      byte[] digest = digests[i].getDigest();
      if (digest != null) {
        StringBuilder result = new StringBuilder(args[i]);
        result.append(": ");
        result.append(DatatypeConverter.printHexBinary(digest));
        System.out.println(result);
        break;
      }
    }
  }
}
```

This solution may work. If it works at all, it gives the correct answers in the correct order irrespective of how fast the individual threads run relative to each other. However, it’s doing a lot more work than it needs to.

Worse yet, this solution is not guaranteed to work. On some virtual machines, the main thread takes all the time available and leaves no time for the actual worker threads. The main thread is so busy checking for job completion that there’s no time left to actually complete the job!
### Callbacks

In fact, there’s a much simpler, more efficient way to handle the problem. The infinite loop that repeatedly polls each `ReturnDigest` object to see whether it’s finished can be eliminated. The trick is that rather than having the main program repeatedly ask each `ReturnDigest` thread whether it’s finished you let the thread tell the main program when it’s finished. It does this by invoking a method in the main class that started it. This is called a _callback_ because the thread calls its creator back when it’s done. This way, the main program can go to sleep while waiting for the threads to finish and not steal time from the running threads.

Example 3-5. ``CallbackDigest``

```java
import java.io.*;
import java.security.*;

public class CallbackDigest implements Runnable {

  private String filename;

  public CallbackDigest(String filename) {
   this.filename = filename;
  }

  @Override
  public void run() {
    try {
      FileInputStream in = new FileInputStream(filename);
      MessageDigest sha = MessageDigest.getInstance("SHA-256");
      DigestInputStream din = new DigestInputStream(in, sha);
      while (din.read() != -1) ; // read entire file
      din.close();
      byte[] digest = sha.digest();
      CallbackDigestUserInterface.receiveDigest(digest, filename);
    } catch (IOException ex) {
      System.err.println(ex);
    } catch (NoSuchAlgorithmException ex) {
      System.err.println(ex);
    }
  }
}
```

Instead, it is invoked by each thread separately. That is, `receiveDigest()` runs inside the digesting threads rather than inside the main thread of execution.

Example 3-6. ``CallbackDigestUserInterface``

```java
import javax.xml.bind.*; // for DatatypeConverter; requires Java 6 or JAXB 1.0

public class CallbackDigestUserInterface {

  public static void receiveDigest(byte[] digest, String name) {
    StringBuilder result = new StringBuilder(name);
    result.append(": ");
    result.append(DatatypeConverter.printHexBinary(digest));
    System.out.println(result);
  }

  public static void main(String[] args) {
    for (String filename : args) {
      // Calculate the digest
      CallbackDigest cb = new CallbackDigest(filename);
      Thread t = new Thread(cb);
      t.start();
    }
  }
}
```

Examples 3-5 and 3-6 use static methods for the callback so that `CallbackDigest` only needs to know the name of the method in `CallbackDigestUserInterface` to call. However, it’s not much harder (and it’s considerably more common) to call back to an instance method. In this case, the class making the callback must have a reference to the object it’s calling back. Generally, this reference is provided as an argument to the thread’s constructor. When the `run()` method is nearly done, the last thing it does is invoke the instance method on the callback object to pass along the result.

Example 3-7. ``InstanceCallbackDigest``

```java
import java.io.*;
import java.security.*;

public class InstanceCallbackDigest implements Runnable {

  private String filename;
  private InstanceCallbackDigestUserInterface callback;

  public InstanceCallbackDigest(String filename,
   InstanceCallbackDigestUserInterface callback) {
    this.filename = filename;
    this.callback = callback;
  }

  @Override
  public void run() {
    try {
      FileInputStream in = new FileInputStream(filename);
      MessageDigest sha = MessageDigest.getInstance("SHA-256");
      DigestInputStream din = new DigestInputStream(in, sha);
      while (din.read() != -1) ;  // read entire file
      din.close();
      byte[] digest = sha.digest();
      callback.receiveDigest(digest);
    } catch (IOException | NoSuchAlgorithmException ex) {
      System.err.println(ex);
    }
  }
}
```

Example 3-8. ``InstanceCallbackDigestUserInterface``

```java
import javax.xml.bind.*; // for DatatypeConverter; requires Java 6 or JAXB 1.0

public class InstanceCallbackDigestUserInterface {

  private String filename;
  private byte[] digest;

  public InstanceCallbackDigestUserInterface(String filename) {
    this.filename = filename;
  }

  public void calculateDigest() {
    InstanceCallbackDigest cb = new InstanceCallbackDigest(filename, this);
    Thread t = new Thread(cb);
    t.start();
  }

  void receiveDigest(byte[] digest) {
    this.digest = digest;
    System.out.println(this);
  }

  @Override
  public String toString() {
    String result = filename + ": ";
    if (digest != null) {
      result += DatatypeConverter.printHexBinary(digest);
    } else {
      result += "digest not available";
    }
    return result;
  }

  public static void main(String[] args) {
    for (String filename : args) {
      // Calculate the digest
      InstanceCallbackDigestUserInterface d
          = new InstanceCallbackDigestUserInterface(filename);
      d.calculateDigest();
    }
  }
}
```

Using instance methods instead of static methods for callbacks is a little more complicated but has a number of advantages. First, each instance of the main class (`InstanceCallbackDigestUserInterface`, in this example) maps to exactly one file and can keep track of information about that file in a natural way without needing extra data structures. Furthermore, the instance can easily recalculate the digest for a particular file, if necessary. In practice, this scheme proves a lot more flexible. However, there is one caveat. 

**==starting threads in a constructor is dangerous, especially threads that will call back to the originating object. There’s a race condition here that may allow the new thread to call back before the constructor is finished and the object is fully initialized.==** It’s unlikely in this case, because starting the new thread is the last thing this constructor does. Nonetheless, it’s at least theoretically possible. Therefore, it’s good form to avoid launching threads from constructors.

**==The first advantage of the callback scheme over the polling scheme is that it doesn’t waste so many CPU cycles. However, a much more important advantage is that callbacks are more flexible and can handle more complicated situations involving many more threads, objects, and classes.==**

### Futures, Callables, and Executors

Java 5 introduced a new approach to multithreaded programming that makes it somewhat easier to handle callbacks by hiding the details. Instead of directly creating a thread, you create an `ExecutorService` that will create threads for you as needed. You submit `Callable` jobs to the `ExecutorService` and for each one you get back a `Future`. At a later point, you can ask the `Future` for the result of the job. If the result is ready, you get it immediately. If it’s not ready, the polling thread blocks until it is ready. The advantage is that you can spawn off many different threads, then get the answers you need in the order you need them.

Example 3-9. ``FindMaxTask``

```java
import java.util.concurrent.Callable;

class FindMaxTask implements Callable<Integer> {

  private int[] data;
  private int start;
  private int end;

  FindMaxTask(int[] data, int start, int end) {
    this.data = data;
    this.start = start;
    this.end = end;
  }

  public Integer call() {
    int max = Integer.MIN_VALUE;
    for (int i = start; i < end; i++) {
      if (data[i] > max) max = data[i];
    }
    return max;
  }
}
```

Although you could invoke the `call()` method directly, that is not its purpose. Instead, you submit `Callable` objects to an `Executor` that spins up a thread for each one.

Example 3-10. ``MultithreadedMaxFinder``

```java
import java.util.concurrent.*;

public class MultithreadedMaxFinder {

  public static int max(int[] data) throws InterruptedException, ExecutionException {

    if (data.length == 1) {
      return data[0];
    } else if (data.length == 0) {
      throw new IllegalArgumentException();
    }

    // split the job into 2 pieces
    FindMaxTask task1 = new FindMaxTask(data, 0, data.length/2);
    FindMaxTask task2 = new FindMaxTask(data, data.length/2, data.length);

    // spawn 2 threads
    ExecutorService service = Executors.newFixedThreadPool(2);

    Future<Integer> future1 = service.submit(task1);
    Future<Integer> future2 = service.submit(task2);

    return Math.max(future1.get(), future2.get());
  }
}
```

Each subarray is searched at the same time, so on suitable hardware and a large input this program can run almost twice as fast. Nonetheless, the code is almost as simple and straightforward as finding the maximum in the first half of the array and then finding the maximum in the second half of the array, without ever worrying about threads or asynchronicity. However, there’s one key difference. In the last statement of Example 3-10, when `future1.get()` is called, the method blocks and waits for the first `FindMaxTask` to finish. Only when this has happened does it call `future2.get()`. It’s possible that the second thread has already finished, in which case the value is immediately returned; but if not, execution waits for that thread to finish too. Once both threads have finished, their results are compared and the maximum is returned.

**==Futures are a very convenient means of launching multiple threads to work on different pieces of a problem, and then waiting for them all to finish before proceeding. Executors and executor services let you assign jobs to different threads with different strategies.==**

## Synchronization

A thread is like a borrower at a library; the thread borrows from a central pool of resources. Threads make programs more efficient by sharing memory, file handles, sockets, and other resources. As long as two threads don’t want to use the same resource at the same time, a multithreaded program is much more efficient than the multiprocess alternative, in which each process has to keep its own copy of every resource. The downside of a multithreaded program is that if two threads want the same resource at the same time, one of them will have to wait for the other to finish. If one of them doesn’t wait, the resource may get corrupted.

```shell
Triangle.java: B4C7AF1BAE952655A96517476BF9DAC97C4AF02411E40DD386FECB58D94CC769
InterfaceLister.java: 267D0EFE73896CD550DC202935D20E87CA71536CB176AF78F915935A6
Squares.java: DA2E27EA139785535122A2420D3DB472A807841D05F6C268A43695B9FDFE1B11
UlpPrinter.java: C8009AB1578BF7E730BD2C3EADA54B772576E265011DF22D171D60A1881AFF51
```

Four threads run in parallel to produce this output. Each writes one line to the console. The order in which the lines are written is unpredictable because thread scheduling is unpredictable, but each line is written as a unified whole. Suppose, however, you used this variation of the `run()` method, which, rather than storing intermediate parts of the result in the `String` variable `result`, simply prints them on the console as they become available:

```java
@Override
public void run() {
  try {
    FileInputStream in = new FileInputStream(filename);
    MessageDigest sha = MessageDigest.getInstance("SHA-256");
    DigestInputStream din = new DigestInputStream(in, sha);
    while (din.read() != -1) ; // read entire file
    din.close();
    byte[] digest = sha.digest();
    System.out.print(input + ": ");
    System.out.print(DatatypeConverter.printHexBinary(digest));
    System.out.println();
  } catch (IOException ex) {
    System.err.println(ex);
  } catch (NoSuchAlgorithmException ex) {
    System.err.println(ex);
  }
}
```

When you run the program on the same input, the output looks something like this:

```shell
Triangle.java: B4C7AF1BAE952655A96517476BF9DAC97C4AF02411E40DD386FECB58D94CC769
InterfaceLister.java: Squares.java: UlpPrinter.java:
C8009AB1578BF7E730BD2C3EADA54B772576E265011DF22D171D60A1881AFF51
267D0EFE73896CD550DC202935D20E87CA71536CB176AF78F915935A6E81B034
DA2E27EA139785535122A2420D3DB472A807841D05F6C268A43695B9FDFE1B11
```

The digests of the different files are all mixed up!

The reason this mix-up occurs is that `System.out` is shared between the four different threads. When one thread starts writing to the console through several `System.out.print()` statements, it may not finish all its writes before another thread breaks in and starts writing its output. The exact order in which one thread preempts the other threads is indeterminate. You’ll probably see slightly different output every time you run this program.

You need a way to assign exclusive access to a shared resource to one thread for a specific series of statements. In this example, that shared resource is `System.out`, and the statements that need exclusive access are:

```java
System.out.print(input + ": ");
System.out.print(DatatypeConverter.printHexBinary(digest));
System.out.println();
```
### Synchronized Blocks

To indicate that these five lines of code should be executed together, wrap them in a `synchronized` block that synchronizes on the `System.out` object, like this:

```java
synchronized (System.out) {
  System.out.print(input + ": ");
  System.out.print(DatatypeConverter.printHexBinary(digest));
  System.out.println();
}
```

Once one thread starts printing out the values, all other threads will have to stop and wait for it to finish before they can print out their values. **==Synchronization forces all code that synchronizes on the same object to run in series, never in parallel.==** For instance, if some other code in a different class and different thread also happened to synchronize on `System.out`, it too would not be able to run in parallel with this block. However, other code that synchronizes on a different object or doesn’t synchronize at all can still run in parallel with this code. It can do so even if it also uses `System.out`. Java provides no means to stop all other threads from using a shared resource. It can only prevent other threads that synchronize on the same object from using the shared resource.

---

 **TIP**

**==In fact, the `PrintStream` class internally synchronizes most methods on the `PrintStream` object (`System.out`, in this example). In other words, every other thread that calls `System.out.println()` will be synchronized on `System.out` and will have to wait for this code to finish. `PrintStream` is unique in this respect. Most other `OutputStream` subclasses do not synchronize themselves.==**

---

Synchronization must be considered any time multiple threads share resources. These threads may be instances of the same `Thread` subclass or use the same `Runnable` class, or they may be instances of completely different classes. The key is the resources they share, not what classes they are. **==Synchronization becomes an issue only when two threads both possess references to the same object==**. In the previous example, the problem was that several threads had access to the same `PrintStream` object, `System.out`. In this case, it was a static class variable that led to the conflict. However, instance variables can also have problems.

Example 3-11. ``LogFile``

```java
import java.io.*;
import java.util.*;

public class LogFile {

  private Writer out;

  public LogFile(File f) throws IOException {
    FileWriter fw = new FileWriter(f);
    this.out = new BufferedWriter(fw);
  }

  public void writeEntry(String message) throws IOException {
    Date d = new Date();
    out.write(d.toString());
    out.write('\T');
    out.write(message);
    out.write("\r\n");
  }

  public void close() throws IOException {
    out.flush();
    out.close();
  }
}
```

A problem occurs if two or more threads each have a reference to the same `LogFile` object and one of those threads interrupts another in the process of writing the data. One thread may write the date and a tab, then the next thread might write three complete entries; then, the first thread could write the message, a carriage return, and a linefeed. The solution, once again, is synchronization. However, here there are two good choices for which object to synchronize on. The first choice is to synchronize on the `Writer` object `out`. For example:

```java
public void writeEntry(String message) throws IOException {
    synchronized (out) {
      Date d = new Date();
      out.write(d.toString());
      out.write('\T');
      out.write(message);
      out.write("\r\n");
    }
  }
```

This works because all the threads that use this `LogFile` object also use the same `out` object that’s part of that `LogFile`. It doesn’t matter that `out` is private. Although it is used by the other threads and objects, it’s referenced only within the `LogFile` class. Furthermore, although you’re synchronizing here on the `out` object, it’s the `writeEntry()` method that needs to be protected from interruption. The `Writer` classes all have their own internal synchronization, which protects one thread from interfering with a `write()` method in another thread. Each `Writer` class has a `lock` field that specifies the object on which writes to that writer synchronize.

The second possibility is to synchronize on the `LogFile` object itself. This is simple enough to arrange with the `this` keyword. For example:Each `Writer` class has a `lock` field that specifies the object on which writes to that writer synchronize.

The second possibility is to synchronize on the `LogFile` object itself. This is simple enough to arrange with the `this` keyword. For example:

```java
public void writeEntry(String message) throws IOException {
  synchronized (this) {
    Date d = new Date();
    out.write(d.toString());
    out.write('\T');
    out.write(message);
    out.write("\r\n");
  }
}
```

### Synchronized Methods

Because synchronizing the entire method body on the object itself is such a common thing to do, Java provides a shortcut. You can synchronize an entire method on the current object (the `this` reference) by adding the `synchronized` modifier to the method declaration. For example:

```java
public synchronized void writeEntry(String message) throws IOException {
  Date d = new Date();
  out.write(d.toString());
  out.write('\T');
  out.write(message);
  out.write("\r\n");
}
```

==**Simply adding the `synchronized` modifier to all methods is not a catchall solution for synchronization problems. For one thing, it exacts a severe performance penalty in many VMs (though more recent VMs have improved greatly in this respect), potentially slowing down your code by a factor of three or more. Second, it dramatically increases the chances of deadlock. Third, and most importantly, it’s not always the object itself you need to protect from simultaneous modification or access, and synchronizing on the instance of the method’s class may not protect the object you really need to protect.**==

### Alternatives to Synchronization

Synchronization is not always the best solution to the problem of inconsistent behavior caused by thread scheduling. There are a number of techniques that avoid the need for synchronization entirely. **==The first is to use local variables instead of fields wherever possible. Local variables do not have synchronization problems. Every time a method is entered, the virtual machine creates a completely new set of local variables for the method. These variables are invisible from outside the method and are destroyed when the method exits.==**

**==Method arguments of primitive types are also safe from modification in separate threads because Java passes arguments by value rather than by reference.==** A corollary of this is that pure functions such as `Math.sqrt()` that take zero or more primitive data type arguments, perform some calculation, and return a value without ever interacting with the fields of any class are inherently thread safe. These methods often either are or should be declared static.

Method arguments of object types are a little trickier because the actual argument passed by value is a reference to the object. Suppose, for example, you pass a reference to an array into a `sort()` method. While the method is sorting the array, there’s nothing to stop some other thread that also has a reference to the array from changing the values in the array.

`String` arguments are safe because they’re _immutable_ (i.e., once a `String` object has been created, it cannot be changed by any thread). **==An immutable object never changes state. The values of its fields are set once when the constructor runs and never altered thereafter.==** `StringBuilder` arguments are not safe because they’re not immutable; they can be changed after they’re created.

A constructor normally does not have to worry about issues of thread safety. Until the constructor returns, no thread has a reference to the object, so it’s impossible for two threads to have a reference to the object.

You can take advantage of immutability in your own classes. It’s usually the easiest way to make a class thread safe, often much easier than determining exactly which methods or code blocks to synchronize. To make an object immutable, simply declare all its fields private and final and don’t write any methods that can change them.

**==A third technique is to use a thread-unsafe class but only as a private field of a class that is thread safe. As long as the containing class accesses the unsafe class only in a thread-safe fashion and as long as it never lets a reference to the private field leak out into another object, the class is safe.==**

In some cases, you can use a designedly thread-safe but mutable class from the `java.util.concurrent.atomic` package. In particular, rather than using an `int`, you can use an `AtomicInteger`. Rather than using a `long`, you can use an `AtomicLong`. Rather than using a `boolean`, you can use an `AtomicBoolean`. Rather than using an `int[]`, you can use an `AtomicIntegerArray`. Rather than a reference variable, you can store an object inside an `AtomicReference`, though note well that this doesn’t make the object itself thread safe, just the getting and setting of the reference variable.

For collections such as maps and lists, you can wrap them in a thread-safe version using the methods of `java.util.Collections` 

In all cases, realize that it’s just a single method invocation that is atomic. If you need to perform two operations on the atomic value in succession without possible interruption, you’ll still need to synchronize. Thus, for instance, even if a list is synchronized via `Collections.synchronizedList()`, you’ll still need to synchronize on it if you want to iterate through the list because that involves many consecutive atomic operations. Although each method call is safely atomic, the sequence of operations is not without explicit synchronization.

## Deadlock

Synchronization can lead to another possible problem: _deadlock_. **==Deadlock occurs when two threads need exclusive access to the same set of resources and each thread holds the lock on a different subset of those resources. If neither thread is willing to give up the resources it has, both threads come to an indefinite halt.==**

**==The most important technique for preventing deadlock is to avoid unnecessary synchronization. If there’s an alternative approach for ensuring thread safety, such as making objects immutable or keeping a local copy of an object, use it. Synchronization should be a last resort for ensuring thread safety. If you do need to synchronize, keep the synchronized blocks small and try not to synchronize on more than one object at a time.==**

The best you can do in the general case is carefully consider whether deadlock is likely to be a problem and design your code around it. If multiple objects need the same set of shared resources to operate, make sure they request them in the same order. For instance, if class A and class B need exclusive access to object X and object Y, make sure that both classes request X first and Y second. If neither requests Y unless it already possesses X, deadlock is not a problem.

## Thread Scheduling

When multiple threads are running at the same time you have to consider issues of thread scheduling. You need to make sure that all important threads get at least some time to run and that the more important threads get more time. Furthermore, you want to ensure that the threads execute in a reasonable order. If your web server has 10 queued requests, each of which requires 5 seconds to process, you don’t want to process them in series. If you do, the first request will finish in 5 seconds but the second will take 10, the third 15, and so on until the last request, which will have to wait almost a minute to be serviced. By that point, the user has likely gone to another page. By running threads in parallel, you might be able to process all 10 requests in only 10 seconds total. The reason this strategy works is that there’s a lot of dead time in servicing a typical web request, time in which the thread is simply waiting for the network to catch up with the CPU—time the VM’s thread scheduler can put to good use by other threads.
### Priorities

Not all threads are created equal. Each thread has a priority, specified as an integer from 0 to 10. When multiple threads are ready to run, the VM will generally run only the highest-priority thread, although that’s not a hard-and-fast rule. In Java, 10 is the highest priority and 0 is the lowest. The default priority is 5, and this is the priority that your threads will have unless you deliberately set them otherwise.

---

 **WARNING**

**This is the exact opposite of the normal Unix way of prioritizing processes, in which the higher the priority number of a process, the less CPU time the process gets.**

---

These three priorities (1, 5, and 10) are often specified as the three named constants `Thread.MIN_PRIORITY`, `Thread.NORM_PRIORITY`, and `Thread.MAX_PRIORITY`:

```java
public static final int MIN_PRIORITY  = 1;
public static final int NORM_PRIORITY = 5;
public static final int MAX_PRIORITY  = 10;
```

Sometimes you want to give one thread more time than another. Threads that interact with the user should get very high priorities so that perceived responsiveness will be very quick. On the other hand, threads that calculate in the background should get low priorities. Tasks that will complete quickly should have high priorities. **==Tasks that take a long time should have low priorities so that they won’t get in the way of other tasks.==**

```java
public final void setPriority(int newPriority)
```

Attempting to exceed the maximum priority or set a nonpositive priority throws an `IllegalArgumentException`.

```java
public void calculateDigest() {
    ListCallbackDigest cb = new ListCallbackDigest(filename);
    cb.addDigestListener(this);
    Thread t = new Thread(cb);
    t.setPriority(8);
    t.start();
  }
```

### Preemption

Every virtual machine has a thread scheduler that determines which thread to run at any given time. **==There are two main kinds of thread scheduling: _preemptive_ and _cooperative_. A preemptive thread scheduler determines when a thread has had its fair share of CPU time, pauses that thread, and then hands off control of the CPU to a different thread. A cooperative thread scheduler waits for the running thread to pause itself before handing off control of the CPU to a different thread.==** A virtual machine that uses cooperative thread scheduling is much more susceptible to thread starvation than a virtual machine that uses preemptive thread scheduling, because one high-priority, uncooperative thread can hog an entire CPU.

All Java virtual machines are guaranteed to use preemptive thread scheduling between priorities. That is, if a lower-priority thread is running when a higher-priority thread becomes ready to run, the virtual machine will sooner or later (and probably sooner) pause the lower-priority thread to allow the higher-priority thread to run. The higher-priority thread _preempts_ the lower-priority thread.

The situation when multiple threads of the same priority are ready to run is trickier. A preemptive thread scheduler will occasionally pause one of the threads to allow the next one in line to get some CPU time. However, a cooperative thread scheduler will not. It will wait for the running thread to explicitly give up control or come to a stopping point. If the running thread never gives up control and never comes to a stopping point and if no higher-priority threads preempt the running thread, all other threads will starve. This is a bad thing. It’s important to make sure all your threads periodically pause themselves so that other threads have an opportunity to run.

---

 **WARNING**

**A starvation problem can be hard to spot if you’re developing on a VM that uses preemptive thread scheduling. Just because the problem doesn’t arise on your machine doesn’t mean it won’t arise on your customers’ machines if their VMs use cooperative thread scheduling. Most current VMs use preemptive thread scheduling, but some older VMs are cooperatively scheduled, and you may also encounter cooperative scheduling in special-purpose Java VMs such as for embedded environments.**

---

There are 10 ways a thread can pause in favor of other threads or indicate that it is ready to pause. These are:

- It can block on I/O.
- It can block on a synchronized object.
- It can yield.
- It can go to sleep.
- It can join another thread.
- It can wait on an object.
- It can finish.
- It can be preempted by a higher-priority thread.
- It can be suspended.
- It can stop.

#### Blocking

**==Blocking occurs any time a thread has to stop and wait for a resource it doesn’t have.==** The most common way a thread in a network program will voluntarily give up control of the CPU is by blocking on I/O. Because CPUs are much faster than networks and disks, a network program will often block while waiting for data to arrive from the network or be sent out to the network.

Threads can also block when they enter a synchronized method or block. If the thread does not already possess the lock for the object being synchronized on and some other thread does possess that lock, the thread will pause until the lock is released. If the lock is never released, the thread is permanently stopped.

Neither blocking on I/O nor blocking on a lock will release any locks the thread already possesses. For I/O blocks, this is not such a big deal, because eventually the I/O will either unblock and the thread will continue or an `IOException` will be thrown and the thread will then exit the synchronized block or method and release its locks. However, a thread blocking on a lock that it doesn’t possess will never give up its own locks. If one thread is waiting for a lock that a second thread owns and the second thread is waiting for a lock that the first thread owns, deadlock results.

#### Yielding

**==The second way for a thread to give up control is to explicitly yield.==** A thread does this by invoking the static `Thread.yield()` method. This signals to the virtual machine that it can run another thread if one is ready to run. Some virtual machines, particularly on real-time operating systems, may ignore this hint.

Before yielding, a thread should make sure that it or its associated `Runnable` object is in a consistent state that can be used by other objects. Yielding does not release any locks the thread holds. Therefore, ideally, a thread should not be synchronized on anything when it yields. If the only other threads waiting to run when a thread yields are blocked because they need the synchronized resources that the yielding thread possesses, then the other threads won’t be able to run. Instead, control will return to the only thread that can run, the one that just yielded, which pretty much defeats the purpose of yielding.

```java
public void run() {
  while (true) {
    // Do the thread's work...
    Thread.yield();
  }
}
```

If each iteration of the loop takes a significant amount of time, you may want to intersperse more calls to `Thread.yield()` in the rest of the code. This precaution should have minimal effect in the event that yielding isn’t necessary.

#### Sleeping

Sleeping is a more powerful form of yielding. Whereas yielding indicates only that a thread is willing to pause and let other equal-priority threads have a turn, a thread that goes to sleep will pause whether any other thread is ready to run or not. This gives an opportunity to run not only to other threads of the same priority, but also to threads of lower priorities. However, **==a thread that goes to sleep does hold onto all the locks it’s grabbed. Consequently, other threads that need the same locks will be blocked even if the CPU is available. Therefore, try to avoid sleeping threads inside a synchronized method or block.==**

```java
public static void sleep(long milliseconds) throws InterruptedException
public static void sleep(long milliseconds, int nanoseconds)
    throws InterruptedException
```

```java
public void run() {
  while (true) {
    if (!getPage("http://www.ibiblio.org/")) {
      mailError("webmaster@ibiblio.org");
    }
    try {
      Thread.sleep(300000); // 300,000 milliseconds == 5 minutes
    } catch (InterruptedException ex) {
      break;
    }
  }
}
```

The thread is not guaranteed to sleep as long as it wants to. On occasion, the thread may not wake up until some time after its requested wake-up call, simply because the VM is busy doing other things. It is also possible that some other thread will do something to wake up the sleeping thread before its time. Generally, this is accomplished by invoking the sleeping thread’s `interrupt()` method.

```java
public void interrupt()
```

**==This is one of those cases where the distinction between the thread and the `Thread` object is important. Just because the thread is sleeping doesn’t mean that other threads that are awake can’t work with the corresponding `Thread` object through its methods and fields. In particular, another thread can invoke the sleeping `Thread` object’s `interrupt()` method, which the sleeping thread experiences as an `InterruptedException`==**. From that point forward, the thread is awake and executes as normal, at least until it goes to sleep again. In the previous example

---

 **WARNING**

**If a thread is blocked on an I/O operation such as a read or write, the effect of interrupting the thread is highly platform dependent. More often than not, it is a noop. That is, the thread continues to be blocked. On Solaris, the `read()` or `write()` method may throw an `InterruptedIOException`, a subclass of `IOException` instead. However, this is unlikely to happen on other platforms, and may not work with all stream classes on Solaris. If your program architecture requires interruptible I/O, you should seriously consider using the nonblocking I/O  rather than streams. Unlike streams, buffers and channels are explicitly designed to support interruption while blocked on a read or write.**

--- 

#### Joining threads

It’s not uncommon for one thread to need the result of another thread. Java provides three `join()` methods to allow one thread to wait for another thread to finish before continuing. These are:

```java
public final void join() throws InterruptedException
public final void join(long milliseconds) throws InterruptedException
public final void join(long milliseconds, int nanoseconds)
    throws InterruptedException
```

The first variant waits indefinitely for the _joined_ thread to finish. The joining thread (i.e., the one that invokes the `join()` method) waits for the joined thread (i.e, the one whose `join()` method is invoked) to finish.

```java
double[] array = new double[10000];                         // 1
for (int i = 0; i < array.length; i++) {                    // 2
  array[i] = Math.random();                                 // 3
}                                                           // 4
SortThread t = new SortThread(array);                       // 5
t.start();                                                  // 6
try {                                                       // 7
  t.join();                                                 // 8
  System.out.println("Minimum: " + array[0]);               // 9
  System.out.println("Median: " + array[array.length/2]);   // 10
  System.out.println("Maximum: " + array[array.length-1]);  // 11
} catch (InterruptedException ex) {                         // 12
}                                                           // 13
```

A thread that’s joined to another thread can be interrupted just like a sleeping thread if some other thread invokes its `interrupt()` method. The thread experiences this invocation as an `InterruptedException`. From that point forward, it executes as normal, starting from the `catch` block that caught the exception.

Example 3-12. Avoid a race condition by joining to the thread that has a result you need

```java
import javax.xml.bind.DatatypeConverter;

public class JoinDigestUserInterface {

  public static void main(String[] args) {

    ReturnDigest[] digestThreads = new ReturnDigest[args.length];

    for (int i = 0; i < args.length; i++) {
      // Calculate the digest
      digestThreads[i] = new ReturnDigest(args[i]);
      digestThreads[i].start();
    }

    for (int i = 0; i < args.length; i++) {
      try {
        digestThreads[i].join();
        // Now print the result
        StringBuffer result = new StringBuffer(args[i]);
        result.append(": ");
        byte[] digest = digestThreads[i].getDigest();
        result.append(DatatypeConverter.printHexBinary(digest));
        System.out.println(result);
      } catch (InterruptedException ex) {
        System.err.println("Thread Interrupted before completion");
      }
    }
  }
}
```

---

 **==TIP**==

==**Joining is perhaps not as important as it was prior to Java 5. In particular, many designs that used to require `join()` can now more easily be implemented using an `Executor` and a `Future` instead.==**

---

#### Waiting on an object

A thread can _wait_ on an object it has locked. While waiting, it releases the lock on the object and pauses until it is notified by some other thread. Another thread changes the object in some way, notifies the thread waiting on that object, and then continues. This differs from joining in that neither the waiting nor the notifying thread has to finish before the other thread can continue. Waiting pauses execution until an object or resource reaches a certain state. Joining pauses execution until a thread finishes.

Waiting on an object is one of the lesser-known ways a thread can pause. That’s because it doesn’t involve any methods in the `Thread` class. Instead, to wait on a particular object, the thread that wants to pause must first obtain the lock on the object using `synchronized` and then invoke one of the object’s three overloaded `wait()` methods:

```java
public final void wait() throws InterruptedException
public final void wait(long milliseconds) throws InterruptedException
public final void wait(long milliseconds, int nanoseconds)
    throws InterruptedException
```

It remains asleep until one of three things happens:

- The timeout expires.
- The thread is interrupted.
- The object is notified.

_Interruption_ works the same way as `sleep()` and `join()`: some other thread invokes the thread’s `interrupt()` method. This causes an `InterruptedException`, and execution resumes in the `catch` block that catches the exception. The thread regains the lock on the object it was waiting on before the exception is thrown, however, so the thread may still be blocked for some time after the `interrupt()` method is invoked.

The third possibility, _notification_, is new. Notification occurs when some other thread invokes the `notify()` or `notifyAll()` method on the object on which the thread is waiting. Both of these methods are in the `java.lang.Object` class:

```java
public final void notify()
public final void notifyAll()
```

These must be invoked on the object the thread was waiting on, not generally on the `Thread` itself. Before notifying an object, a thread must first obtain the lock on the object using a synchronized method or block. The `notify()` method selects one thread more or less at random from the list of threads waiting on the object and wakes it up. The `notifyAll()` method wakes up every thread waiting on the given object.

Once a waiting thread is notified, it attempts to regain the lock of the object it was waiting on. If it succeeds, execution resumes with the statement immediately following the invocation of `wait()`. If it fails, it blocks on the object until its lock becomes available; then execution resumes with the statement immediately following the invocation of `wait()`.

```java
ManifestFile m = new ManifestFile();
JarThread    t = new JarThread(m, in);
synchronized (m) {
  t.start();
  try {
    m.wait();
    // work with the manifest file...
  } catch (InterruptedException ex) {
    // handle exception...
  }
}
```

The `JarThread` class works like this:

```java
ManifestFile theManifest;
InputStream in;

public JarThread(Manifest m, InputStream in) {
  theManifest = m;
  this.in= in;
}

@Override
public void run() {
  synchronized (theManifest) {
    // read the manifest from the stream in...
    theManifest.notify();
  }
  // read the rest of the stream...
}
```

Waiting and notification are more commonly used when multiple threads want to wait on the same object.

**==When all threads waiting on one object are notified, all will wake up and try to get the lock on the object. However, only one can succeed immediately. That one continues; the rest are blocked until the first one releases the lock. If several threads are all waiting on the same object, a significant amount of time may pass before the last one gets its turn at the lock on the object and continues. It’s entirely possible that the object on which the thread was waiting will once again have been placed in an unacceptable state during this time.==** 

**==Do not assume that just because the thread was notified, the object is now in the correct state. Check it explicitly if you can’t guarantee that once the object reaches a correct state it will never again reach an incorrect state.==**

```java
private List<String> entries;

public void processEntry() {

  synchronized (entries) { // must synchronize on the object we wait on
    while (entries.isEmpty()) {
      try {
        entries.wait();
        // We stopped waiting because entries.size() became non-zero
        // However we don't know that it's still non-zero so we
        // pass through the loop again to test its state now.
      } catch (InterruptedException ex) {
        // If interrupted, the last entry has been processed so
        return;
      }
    }
    String entry = entries.remove(entries.size()-1);
    // process this entry...
  }
}
```

```java
public void readLogFile() {
  while (true) {
    String entry = log.getNextEntry();
    if (entry == null) {
      // There are no more entries to add to the list so
      // we interrupt all threads that are still waiting.
      // Otherwise, they'll wait forever.
      for (Thread thread : threads) thread.interrupt();
      break;
    }
    synchronized (entries) {
      entries.add(0, entry);
      entries.notifyAll();
    }
  }
}
```

#### Finish

The final way a thread can give up control of the CPU in an orderly fashion is by _finishing_. When the `run()` method returns, the thread dies and other threads can take over. In network applications, this tends to occur with threads that wrap a single blocking operation, such as downloading a file from a server, so that the rest of the application won’t be blocked.

Otherwise, **==if your `run()` method is so simple that it always finishes quickly enough without blocking, there’s a very real question of whether you should spawn a thread at all. There’s a nontrivial amount of overhead for the virtual machine in setting up and tearing down threads. If a thread is finishing in a small fraction of a second anyway, chances are it would finish even faster if you used a simple method call rather than a separate thread.==**

## Thread Pools and Executors

Adding multiple threads to a program dramatically improves performance, especially for I/O-bound programs such as most network programs. However, threads are not without overhead of their own. Starting a thread and cleaning up after a thread that has died takes a noticeable amount of work from the virtual machine, especially if a program spawns hundreds of threads Even if the threads finish quickly, this can overload the garbage collector or other parts of the VM and hurt performance, just like allocating thousands of any other kind of object every minute. Even more importantly, switching between running threads carries overhead. If the threads are blocking naturally—for instance, by waiting for data from the network—there’s no real penalty to this; but if the threads are CPU-bound, then the total task may finish more quickly if you can avoid a lot of switching between threads. Finally, and most importantly, although threads help make more efficient use of a computer’s limited CPU resources, there is still only a finite amount of resources to go around. Once you’ve spawned enough threads to use all the computer’s available idle time, spawning more threads just wastes MIPS and memory on thread management.

The `Executors` class in `java.util.concurrent` makes it quite easy to set up thread pools. You simply submit each task as a `Runnable` object to the pool. You get back a `Future` object you can use to check on the progress of the task.

Example 3-13. The ``GZipRunnable`` class

```java
import java.io.*;
import java.util.zip.*;

public class GZipRunnable implements Runnable {

  private final File input;

  public GZipRunnable(File input) {
    this.input = input;
  }

  @Override
  public void run() {
    // don't compress an already compressed file
    if (!input.getName().endsWith(".gz")) {
      File output = new File(input.getParent(), input.getName() + ".gz");
      if (!output.exists()) { // Don't overwrite an existing file
        try ( // with resources; requires Java 7
          InputStream in = new BufferedInputStream(new FileInputStream(input));
        OutputStream out = new BufferedOutputStream(
          new GZIPOutputStream(
            new FileOutputStream(output)));
         ) {
            int b;
            while ((b = in.read()) != -1) out.write(b);
            out.flush();
        } catch (IOException ex) {
          System.err.println(ex);
        }
      }
    }
  }
}
```

Also notice the buffering of both input and output. This is very important for performance in I/O-limited applications, and especially important in network programs. At worst, buffering has no impact on performance, while at best it can give you an order of magnitude speedup or more.

Example 3-14 is the main program.

Example 3-14. The ``GZipThread`` user interface class

```java
import java.io.*;
import java.util.concurrent.*;

public class GZipAllFiles {

  public final static int THREAD_COUNT = 4;

  public static void main(String[] args) {

    ExecutorService pool = Executors.newFixedThreadPool(THREAD_COUNT);

    for (String filename : args) {
      File f = new File(filename);
      if (f.exists()) {
        if (f.isDirectory()) {
          File[] files = f.listFiles();
          for (int i = 0; i < files.length; i++) {
            if (!files[i].isDirectory()) { // don't recurse directories
              Runnable task = new GZipRunnable(files[i]);
              pool.submit(task);
            }
          }
        } else {
          Runnable task = new GZipRunnable(f);
          pool.submit(task);
        }
      }
    }

    pool.shutdown();
  }
}
```

Once you have added all the files to the pool, you call `pool.shutdown()`. Chances are this happens while there’s still work to be done. This method does not abort pending jobs. It simply notifies the pool that no further tasks will be added to its internal queue and that it should shut down once it has finished all pending work.

**==Shutting down like this is mostly atypical of the heavily threaded network programs you’ll write because it does have such a definite ending point: the point at which all files are processed. Most network servers continue indefinitely until shut down through an administration interface. In those cases, you may want to invoke `shutdownNow()` instead to abort currently processing tasks and skip any pending tasks.==**

# Chapter 4. Internet Addresses

