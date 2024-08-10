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

Devices connected to the Internet are called _nodes_. Nodes that are computers are called _hosts_. Each node or host is identified by at least one unique number called an Internet address or an IP address. Most current IP addresses are 4-byte-long IPv4 addresses. However, a small but growing number of IP addresses are 16-byte-long IPv6 addresses. Both IPv4 and IPv6 addresses are ordered sequences of bytes, like an array. They aren’t numbers, and they aren’t ordered in any predictable or useful sense.

An IPv4 address is normally written as four unsigned bytes, each ranging from 0 to 255, with the most significant byte first. Bytes are separated by periods for the convenience of human eyes. For example, the address for _login.ibiblio.org_ is 152.19.134.132. This is called the _dotted quad_ format.

An IPv6 address is normally written as eight blocks of four hexadecimal digits separated by colons. For example, at the time of this writing, the address of _www.hamiltonweather.tk_ is _2400:cb00:2048:0001:0000:0000:6ca2:c665_

IP addresses are great for computers, but they are a problem for humans, who have a hard time remembering long numbers. To avoid the need to carry around Rolodexes full of IP addresses, the Internet’s designers invented the Domain Name System (DNS). DNS associates hostnames that humans can remember (such as _login.ibiblio.org_) with IP addresses that computers can remember (such as _152.19.134.132_). Servers usually have at least one hostname. Clients often have a hostname, but often don’t, especially if their IP address is dynamically assigned at startup.

---

 **TIP**

**Colloquially, people often use “Internet address” to mean a hostname (or even an email address, or full URL). In a book about network programming, it is crucial to be precise about addresses and hostnames. In this book, an address is always a numeric IP address, never a human-readable hostname.**

---

Some machines have multiple names. For instance, _www.beand.com_ and _xom.nu_ are really the same Linux box. The name _www.beand.com_ really refers to a website rather than a particular machine. In the past, when this website moved from one machine to another, the name was reassigned to the new machine so it always pointed to the site’s current server. This way, URLs around the Web don’t need to be updated just because the site has moved to a new host.

On occasion, one name maps to multiple IP addresses. It is then the responsibility of the DNS server to randomly choose machines to respond to each request. This feature is most frequently used for very high-traffic websites, where it splits the load across multiple systems

Every computer connected to the Internet should have access to a machine called a _domain name server_, generally a Unix box running special DNS software that knows the mappings between different hostnames and IP addresses. Most domain name servers only know the addresses of the hosts on their local network, plus the addresses of a few domain name servers at other sites. If a client asks for the address of a machine outside the local domain, the local domain name server asks a domain name server at the remote location and relays the answer to the requester.

**==Most of the time, you can use hostnames and let DNS handle the translation to IP addresses.==**

## The InetAddress Class

The `java.net.InetAddress` class is Java’s high-level representation of an IP address, both IPv4 and IPv6. It is used by most of the other networking classes, including `Socket`, `ServerSocket`, `URL`, `DatagramSocket`, `DatagramPacket`, and more. **==Usually, it includes both a hostname and an IP address.==**

### Creating New InetAddress Objects

There are no public constructors in the `InetAddress` class. Instead, `InetAddress` has static factory methods that connect to a DNS server to resolve a hostname. The most common is `InetAddress.getByName()`.

```java
InetAddress address = InetAddress.getByName("www.oreilly.com");
```

If the DNS server can’t find the address, this method throws an `UnknownHostException`, a subclass of `IOException`.

Example 4-1. A program that prints the address of www.oreilly.com

```java
import java.net.*;

public class OReillyByName {

  public static void main (String[] args) {
    try {
      InetAddress address = InetAddress.getByName("www.oreilly.com");
      System.out.println(address);
    } catch (UnknownHostException ex) {
      System.out.println("Could not find www.oreilly.com");
    }
  }
}
```

```shell
% java OReillyByName
www.oreilly.com/208.201.239.36
```

You can also do a reverse lookup by IP address.

```java
InetAddress address = InetAddress.getByName("208.201.239.100");
System.out.println(address.getHostName());
```

If the address you look up does not have a hostname, `getHostName()` simply returns the dotted quad address you supplied. If, for some reason, you need all the addresses of a host, call `getAllByName()` instead, which returns an array:

```java
try {
  InetAddress[] addresses = InetAddress.getAllByName("www.oreilly.com");
  for (InetAddress address : addresses) {
    System.out.println(address);
  }
} catch (UnknownHostException ex) {
  System.out.println("Could not find www.oreilly.com");
}
```

Finally, the `getLocalHost()` method returns an `InetAddress` object for the host on which your code is running:

```java
InetAddress me = InetAddress.getLocalHost();
```

This method tries to connect to DNS to get a real hostname and IP address such as “elharo.laptop.corp.com” and “192.1.254.68”; but if that fails it may return the _loopback_ address instead. This is the hostname “localhost” and the dotted quad address “127.0.0.1”.

Example 4-2. Find the address of the local machine

```java
import java.net.*;

public class MyAddress {

  public static void main (String[] args) {
    try {
      InetAddress address = InetAddress.getLocalHost();
      System.out.println(address);
    } catch (UnknownHostException ex) {
      System.out.println("Could not find this computer's address.");
    }
  }
}
```

```shell
% java MyAddress
titan.oit.unc.edu/152.2.22.14
```

If you’re not connected to the Internet, and the system does not have a fixed IP address or domain name, you’ll probably see _localhost_ as the domain name and 127.0.0.1 as the IP address.

If you know a numeric address, you can create an `InetAddress` object from that address without talking to DNS using `InetAddress.getByAddress()`. This method can create addresses for hosts that do not exist or cannot be resolved:

```java
public static InetAddress getByAddress(byte[] addr) throws UnknownHostException
public static InetAddress getByAddress(String hostname, byte[] addr)
    throws UnknownHostException
```

```java
byte[] address = {107, 23, (byte) 216, (byte) 196};
InetAddress lessWrong = InetAddress.getByAddress(address);
InetAddress lessWrongWithname = InetAddress.getByAddress(
   "lesswrong.com", address);
```

Unlike the other factory methods, these two methods make no guarantees that such a host exists or that the hostname is correctly mapped to the IP address. They throw an `UnknownHostException` only if a byte array of an illegal size (neither 4 nor 16 bytes long) is passed as the `address` argument.
#### Caching

Because DNS lookups can be relatively expensive the `InetAddress` class caches the results of lookups. Once it has the address of a given host, it won’t look it up again, even if you create a new `InetAddress` object for the same host. As long as IP addresses don’t change while your program is running, this is not a problem.

Negative results (host not found errors) are slightly more problematic. It’s not uncommon for an initial attempt to resolve a host to fail, but the immediately following one to succeed. The first attempt timed out while the information was still in transit from the remote DNS server. Then the address arrived at the local server and was immediately available for the next request. For this reason, Java only caches unsuccessful DNS queries for 10 seconds.

These times can be controlled by the system properties `networkaddress.cache.ttl` and `networkaddress.cache.negative.ttl`. The first of those, `networkaddress.cache.ttl`, specifies the number of seconds a successful DNS lookup will remain in Java’s cache. `networkaddress.cache.negative.ttl` is the number of seconds an unsuccessful lookup will be cached.

Besides local caching inside the `InetAddress` class, the local host, the local domain name server, and other DNS servers elsewhere on the Internet also cache the results of various queries. Java provides no way to control this.

#### Lookups by IP address

When you call `getByName()` with an IP address string as an argument, it creates an `InetAddress` object for the requested IP address without checking with DNS. This means it’s possible to create `InetAddress` objects for hosts that don’t really exist and that you can’t connect to. The hostname of an `InetAddress` object created from a string containing an IP address is initially set to that string. A DNS lookup for the actual hostname is only performed when the hostname is requested, either explicitly via a `getHostName()` or implicitly by `toString()`. That’s how _www.oreilly.com_ was determined from the dotted quad address 208.201.239.37. If, at the time the hostname is requested and a DNS lookup is finally performed, the host with the specified IP address can’t be found, the hostname remains the original dotted quad string. However, no `UnknownHostException` is thrown.

Hostnames are much more stable than IP addresses. If you have a choice between using a hostname such as _www.oreilly.com_ or an IP address such as 208.201.239.37, always choose the hostname. **==Use an IP address only when a hostname is not available.==**

#### Security issues

Creating a new `InetAddress` object from a hostname is potentially insecure because it requires a DNS lookup, which untrusted code cannot perform for arbitrary hosts due to security restrictions. This prevents untrusted applets from communicating covertly with third-party hosts via DNS. Untrusted code can only resolve its own codebase and localhost addresses, with the `checkConnect()` method in `SecurityManager` determining whether DNS resolution or network connections are permitted.

```java
public void checkConnect(String hostname, int port)
```

### Getter Methods

The `InetAddress` class contains four getter methods that return the hostname as a string and the IP address as both a string and a byte array:

```java
public String getHostName()
public String getCanonicalHostName()
public byte[] getAddress()
public String getHostAddress()
```

**==There are no corresponding `setHostName()` and `setAddress()` methods, which means that packages outside of `java.net` can’t change an `InetAddress` object’s fields behind its back. This makes `InetAddress` immutable and thus thread safe.==**

```java
InetAddress machine = InetAddress.getLocalHost();
String localhost = machine.getHostName();
```

The `getCanonicalHostName()` method is similar, but it’s a bit more aggressive about contacting DNS. `getHostName()` will only call DNS if it doesn’t think it already knows the hostname. **==`getCanonicalHostName()` calls DNS if it can, and may replace the existing cached hostname==**. For example:

```java
InetAddress machine = InetAddress.getLocalHost();
String localhost = machine.getCanonicalHostName();
```

The `getCanonicalHostName()` method is particularly useful when you’re starting with a dotted quad IP address rather than the hostname.

Example 4-3. Given the address, find the hostname

```java
import java.net.*;

public class ReverseTest {

  public static void main (String[] args) throws UnknownHostException {
    InetAddress ia = InetAddress.getByName("208.201.239.100");
    System.out.println(ia.getCanonicalHostName());
  }
}
```

```shell
% java ReverseTest
oreilly.com
```

Example 4-4. Find the IP address of the local machine

```java
import java.net.*;

public class MyAddress {

  public static void main(String[] args) {
    try {
      InetAddress me = InetAddress.getLocalHost();
      String dottedQuad = me.getHostAddress();
      System.out.println("My address is " + dottedQuad);
    } catch (UnknownHostException ex) {
      System.out.println("I'm sorry. I don't know my own address.");
    }
  }
}
```

```shell
% java MyAddress
My address is 152.2.22.14.
```

If you want to know the IP address of a machine (and you rarely do), then use the `getAddress()` method, which returns an IP address as an array of bytes in network byte order. The most significant byte (i.e., the first byte in the address’s dotted quad form) is the first byte in the array, or element zero. To be ready for IPv6 addresses, try not to assume anything about the length of this array. If you need to know the length of the array

```java
InetAddress me = InetAddress.getLocalHost();
byte[] address = me.getAddress();
```

The bytes returned are unsigned, which poses a problem. Unlike C, Java doesn’t have an unsigned byte primitive data type. Bytes with values higher than 127 are treated as negative numbers. Therefore, if you want to do anything with the bytes returned by `getAddress()`, you need to promote the bytes to `int`s and make appropriate adjustments.

```java
int unsignedByte = signedByte < 0 ? signedByte + 256 : signedByte;
```

One reason to look at the raw bytes of an IP address is to determine the type of the address. Test the number of bytes in the array returned by `getAddress()` to determine whether you’re dealing with an IPv4 or IPv6 address

Example 4-5. Determining whether an IP address is v4 or v6

```java
import java.net.*;

public class AddressTests {

  public static int getVersion(InetAddress ia) {
    byte[] address = ia.getAddress();
    if (address.length == 4) return 4;
    else if (address.length == 16) return 6;
    else return -1;
  }
}
```

### Address Types

Some IP addresses and some patterns of addresses have special meanings. Java includes 10 methods for testing whether an `InetAddress` object meets any of these criteria:

```java
public boolean isAnyLocalAddress()
public boolean isLoopbackAddress()
public boolean isLinkLocalAddress()
public boolean isSiteLocalAddress()
public boolean isMulticastAddress()
public boolean isMCGlobal()
public boolean isMCNodeLocal()
public boolean isMCLinkLocal()
public boolean isMCSiteLocal()
public boolean isMCOrgLocal()
```

The `isAnyLocalAddress()` method returns true if the address is a _wildcard address_, false otherwise. A wildcard address matches any address of the local system. This is important if the system has multiple network interfaces, as might be the case on a system with multiple Ethernet cards or an Ethernet card and an 802.11 WiFi interface.

The `isLoopbackAddress()` method returns true if the address is the loopback address, false otherwise. The loopback address connects to the same computer directly in the IP layer without using any physical hardware. Thus, connecting to the loopback address enables tests to bypass potentially buggy or nonexistent Ethernet, PPP, and other drivers, helping to isolate problems.

The `isLinkLocalAddress()` method returns true if the address is an IPv6 link-local address, false otherwise. This is an address used to help IPv6 networks self-configure, much like DHCP on IPv4 networks but without necessarily using a server.

The `isSiteLocalAddress()` method returns true if the address is an IPv6 site-local address, false otherwise. Site-local addresses are similar to link-local addresses except that they may be forwarded by routers within a site or campus but should not be forwarded beyond that site

The `isMulticastAddress()` method returns true if the address is a multicast address, false otherwise. Multicasting broadcasts content to all subscribed computers rather than to one particular computer.

The `isMCGlobal()` method returns true if the address is a global multicast address, false otherwise. A global multicast address may have subscribers around the world.

The `isMCOrgLocal()` method returns true if the address is an organization-wide multicast address, false otherwise. An organization-wide multicast address may have subscribers within all the sites of a company or organization, but not outside that organization.

The `isMCSiteLocal()` method returns true if the address is a site-wide multicast address, false otherwise. Packets addressed to a site-wide address will only be transmitted within their local site.

The `isMCLinkLocal()` method returns true if the address is a subnet-wide multicast address, false otherwise. Packets addressed to a link-local address will only be transmitted within their own subnet.

The `isMCNodeLocal()` method returns true if the address is an interface-local multicast address, false otherwise. Packets addressed to an interface-local address are not sent beyond the network interface from which they originate, not even to a different network interface on the same node.

---

 **TIP**

**The method name is out of sync with current terminology. Earlier drafts of the IPv6 protocol called this type of address “node-local,” hence the name “isMCNodeLocal.” The IPNG working group actually changed the name before this method was added to the JDK, but Sun didn’t get the memo in time.**

---

Example 4-6. Testing the characteristics of an IP address

```java
import java.net.*;

public class IPCharacteristics {

  public static void main(String[] args) {

    try {
      InetAddress address = InetAddress.getByName(args[0]);

      if (address.isAnyLocalAddress()) {
        System.out.println(address + " is a wildcard address.");
      }
      if (address.isLoopbackAddress()) {
        System.out.println(address + " is loopback address.");
      }

      if (address.isLinkLocalAddress()) {
        System.out.println(address + " is a link-local address.");
      } else if (address.isSiteLocalAddress()) {
        System.out.println(address + " is a site-local address.");
      } else {
        System.out.println(address + " is a global address.");
      }

      if (address.isMulticastAddress()) {
        if (address.isMCGlobal()) {
          System.out.println(address + " is a global multicast address.");
        } else if (address.isMCOrgLocal()) {
          System.out.println(address
           + " is an organization wide multicast address.");
        } else if (address.isMCSiteLocal()) {
          System.out.println(address + " is a site wide multicast
                             address.");
        } else if (address.isMCLinkLocal()) {
          System.out.println(address + " is a subnet wide multicast
                             address.");
        } else if (address.isMCNodeLocal()) {
          System.out.println(address
           + " is an interface-local multicast address.");
        } else {
          System.out.println(address + " is an unknown multicast
                             address type.");
        }
      } else {
        System.out.println(address + " is a unicast address.");
      }
    } catch (UnknownHostException ex) {
      System.err.println("Could not resolve " + args[0]);
    }
  }
}
```

```shell
$ java  IPCharacteristics 127.0.0.1
/127.0.0.1 is loopback address.
/127.0.0.1 is a global address.
/127.0.0.1 is a unicast address.
$ java  IPCharacteristics 192.168.254.32
/192.168.254.32 is a site-local address.
/192.168.254.32 is a unicast address.
$ java  IPCharacteristics www.oreilly.com
www.oreilly.com/208.201.239.37 is a global address.
www.oreilly.com/208.201.239.37 is a unicast address.
$ java  IPCharacteristics 224.0.2.1
/224.0.2.1 is a global address.
/224.0.2.1 is a global multicast address.
$ java  IPCharacteristics FF01:0:0:0:0:0:0:1
/ff01:0:0:0:0:0:0:1 is a global address.
/ff01:0:0:0:0:0:0:1 is an interface-local multicast address.
$ java  IPCharacteristics FF05:0:0:0:0:0:0:101
/ff05:0:0:0:0:0:0:101 is a global address.
/ff05:0:0:0:0:0:0:101 is a site wide multicast address.
$ java  IPCharacteristics 0::1
/0:0:0:0:0:0:0:1 is loopback address.
/0:0:0:0:0:0:0:1 is a global address.
/0:0:0:0:0:0:0:1 is a unicast address.
```

### Testing Reachability

The `InetAddress` class has two `isReachable()` methods that test whether a particular node is reachable from the current host (i.e., whether a network connection can be made). Connections can be blocked for many reasons, including firewalls, proxy servers, misbehaving routers, and broken cables, or simply because the remote host is not turned on when you try to connect.

```java
public boolean isReachable(int timeout) throws IOException
public boolean isReachable(NetworkInterface interface, int ttl, int timeout)
    throws IOException
```

These methods attempt to use traceroute (more specifically, ICMP echo requests) to find out if the specified address is reachable. If the host responds within `timeout` milliseconds, the methods return true; otherwise, they return false. An `IOException` will be thrown if there’s a network error. The second variant also lets you specify the local network interface the connection is made from and the “time-to-live” (the maximum number of network hops the connection will attempt before being discarded).

### Object Methods

Like every other class, `java.net.InetAddress` inherits from `java.lang.Object`. Thus, it has access to all the methods of that class. It overrides three methods to provide more specialized behavior:

```java
public boolean equals(Object o)
public int hashCode()
public String toString()
```

**==An object is equal to an `InetAddress` object only if it is itself an instance of the `InetAddress` class and it has the same IP address. It does not need to have the same hostname.==**

Example 4-7. Are www.ibiblio.org and helios.ibiblio.org the same?

```java
import java.net.*;

public class IBiblioAliases {

  public static void main (String args[]) {
    try {
      InetAddress ibiblio = InetAddress.getByName("www.ibiblio.org");
      InetAddress helios = InetAddress.getByName("helios.ibiblio.org");
      if (ibiblio.equals(helios)) {
        System.out.println
            ("www.ibiblio.org is the same as helios.ibiblio.org");
      } else {
        System.out.println
            ("www.ibiblio.org is not the same as helios.ibiblio.org");
      }
    } catch (UnknownHostException ex) {
      System.out.println("Host lookup failed.");
    }
  }
}
```

```shell
% java IBiblioAliases 
www.ibiblio.org is the same as helios.ibiblio.org
```

The `hashCode()` method is consistent with the `equals()` method. The `int` that `hashCode()` returns is calculated solely from the IP address. It does not take the hostname into account. If two `InetAddress` objects have the same address, then they have the same hash code, even if their hostnames are different.

## Inet4Address and Inet6Address

Java uses two classes, `Inet4Address` and `Inet6Address`, in order to distinguish IPv4 addresses from IPv6 addresses:

```java
public final class Inet4Address extends InetAddress
public final class Inet6Address extends InetAddress
```

Most of the time, you really shouldn’t be concerned with whether an address is an IPv4 or IPv6 address. In the application layer where Java programs reside, you simply don’t need to know this  `Inet4Address` overrides several of the methods in `InetAddress` but doesn’t change their behavior in any public way. `Inet6Address` is similar, but it does add one new method not present in the superclass, `isIPv4CompatibleAddress()`:

```java
public boolean isIPv4CompatibleAddress()
```

This method returns true if and only if the address is essentially an IPv4 address stuffed into an IPv6 container

## The NetworkInterface Class

The `NetworkInterface` class represents a local IP address. This can either be a physical interface such as an additional Ethernet card (common on firewalls and routers) or it can be a virtual interface bound to the same physical hardware as the machine’s other IP addresses. The `NetworkInterface` class provides methods to enumerate all the local addresses, regardless of interface, and to create `InetAddress` objects from them. These `InetAddress` objects can then be used to create sockets, server sockets, and so forth.

### Factory Methods

Because `NetworkInterface` objects represent physical hardware and virtual addresses, they cannot be constructed arbitrarily. As with the `InetAddress` class, there are static factory methods that return the `NetworkInterface` object associated with a particular network interface. You can ask for a `NetworkInterface` by IP address, by name, or by enumeration.

#### `public static NetworkInterface getByName(String name) throws SocketException`

The `getByName()` method returns a `NetworkInterface` object representing the network interface with the particular name. If there’s no interface with that name, it returns null. **==The format of the names is platform dependent.==**

```java
try {
  NetworkInterface ni = NetworkInterface.getByName("eth0");
  if (ni == null) {
    System.err.println("No such interface:  eth0");
  }
} catch (SocketException ex) {
  System.err.println("Could not list sockets.");
}
```

#### `public static NetworkInterface getByInetAddress(InetAddress address) throws SocketException`

The `getByInetAddress()` method returns a `NetworkInterface` object representing the network interface bound to the specified IP address. If no network interface is bound to that IP address on the local host, it returns null.

```java
try {
  InetAddress local = InetAddress.getByName("127.0.0.1");
  NetworkInterface ni = NetworkInterface.getByInetAddress(local);
  if (ni == null) {
    System.err.println("That's weird. No local loopback address.");
  }
} catch (SocketException ex) {
  System.err.println("Could not list network interfaces." );
} catch (UnknownHostException ex) {
  System.err.println("That's weird. Could not lookup 127.0.0.1.");
}
```

#### ``public static Enumeration getNetworkInterfaces() throws SocketException``

The `getNetworkInterfaces()` method returns a `java.util.Enumeration` listing all the network interfaces on the local host.

Example 4-8. A program that lists all the network interfaces

```java
import java.net.*;
import java.util.*;

public class InterfaceLister {

  public static void main(String[] args) throws SocketException {
    Enumeration<NetworkInterface> interfaces = NetworkInterface.
    getNetworkInterfaces();
    while (interfaces.hasMoreElements()) {
      NetworkInterface ni = interfaces.nextElement();
      System.out.println(ni);
    }
  }
}
```

```shell
% java InterfaceLister
name:eth1 (eth1) index: 3 addresses:
/192.168.210.122;

name:eth0 (eth0) index: 2 addresses:
/152.2.210.122;

name:lo (lo) index: 1 addresses:
/127.0.0.1;
```

### Getter Methods

Once you have a `NetworkInterface` object, you can inquire about its IP address and name. This is pretty much the only thing you can do with these objects.

#### ``public Enumeration getInetAddresses()``

A single network interface may be bound to more than one IP address. This situation isn’t common these days, but it does happen. The `getInetAddresses()` method returns a `java.util.Enumeration` containing an `InetAddress` object for each IP address the interface is bound to.

```java
NetworkInterface eth0 = NetworkInterrface.getByName("eth0");
Enumeration addresses = eth0.getInetAddresses();
while (addresses.hasMoreElements()) {
  System.out.println(addresses.nextElement());
}
```

#### public String getName()

The `getName()` method returns the name of a particular `NetworkInterface` object, such as eth0 or lo.

#### public String getDisplayName()

The `getDisplayName()` method allegedly returns a more human-friendly name for the particular `NetworkInterface`—something like “Ethernet Card 0.” However, in my tests on Unix, it always returned the same string as `getName()`. On Windows, you may see slightly friendlier names such as “Local Area Connection” or “Local Area Connection 2.”

## Some Useful Programs

### SpamCheck

Example 4-9. SpamCheck

```java
import java.net.*;

public class SpamCheck {

  public static final String BLACKHOLE = "sbl.spamhaus.org";

  public static void main(String[] args) throws UnknownHostException {
    for (String arg: args) {
      if (isSpammer(arg)) {
        System.out.println(arg + " is a known spammer.");
      } else {
        System.out.println(arg + " appears legitimate.");
      }
    }
  }

  private static boolean isSpammer(String arg) {
    try {
      InetAddress address = InetAddress.getByName(arg);
      byte[] quad = address.getAddress();
      String query = BLACKHOLE;
      for (byte octet : quad) {
        int unsignedByte = octet < 0 ? octet + 256 : octet;
        query = unsignedByte + "." + query;
      }
      InetAddress.getByName(query);
      return true;
    } catch (UnknownHostException e) {
      return false;
    }
  }
}
```

```shell
$ java SpamCheck 207.34.56.23 125.12.32.4 130.130.130.130
207.34.56.23 appears legitimate.
125.12.32.4 appears legitimate.
130.130.130.130 appears legitimate.
```

### Processing Web Server Logfiles

Example 4-10. Process web server logfiles

```java
import java.io.*;
import java.net.*;

public class Weblog {

  public static void main(String[] args) {
    try (FileInputStream fin =  new FileInputStream(args[0]);
      Reader in = new InputStreamReader(fin);
      BufferedReader bin = new BufferedReader(in);) {

      for (String entry = bin.readLine();
        entry != null;
        entry = bin.readLine()) {
        // separate out the IP address
        int index = entry.indexOf(' ');
        String ip = entry.substring(0, index);
        String theRest = entry.substring(index);

        // Ask DNS for the hostname and print it out
        try {
          InetAddress address = InetAddress.getByName(ip);
          System.out.println(address.getHostName() + theRest);
        } catch (UnknownHostException ex) {
          System.err.println(entry);
        }
      }
    } catch (IOException ex) {
      System.out.println("Exception: " + ex);
    }
  }
}
```

Example 4-11. ``LookupTask``

```java
import java.net.*;
import java.util.concurrent.Callable;

public class LookupTask implements Callable<String> {

  private String line;

  public LookupTask(String line) {
    this.line = line;
  }

  @Override
  public String call() {
    try {
      // separate out the IP address
      int index = line.indexOf(' ');
      String address = line.substring(0, index);
      String theRest = line.substring(index);
      String hostname = InetAddress.getByName(address).getHostName();
      return hostname + " " + theRest;
    } catch (Exception ex) {
      return line;
    }
  }
}
```

Example 4-12. ``PooledWebLog``

```java
import java.io.*;
import java.util.*;
import java.util.concurrent.*;

// Requires Java 7 for try-with-resources and multi-catch
public class PooledWeblog {

  private final static int NUM_THREADS = 4;

  public static void main(String[] args) throws IOException {
    ExecutorService executor = Executors.newFixedThreadPool(NUM_THREADS);
    Queue<LogEntry> results = new LinkedList<LogEntry>();

    try (BufferedReader in = new BufferedReader(
      new InputStreamReader(new FileInputStream(args[0]), "UTF-8"));) {
      for (String entry = in.readLine(); entry != null; entry = in.readLine()) {
        LookupTask task = new LookupTask(entry);
        Future<String> future = executor.submit(task);
        LogEntry result = new LogEntry(entry, future);
        results.add(result);
      }
    }

    // Start printing the results. This blocks each time a result isn't ready.
    for (LogEntry result : results) {
      try {
        System.out.println(result.future.get());
      } catch (InterruptedException | ExecutionException ex) {
        System.out.println(result.original);
      }
    }

    executor.shutdown();
  }

  private static class LogEntry {
    String original;
    Future<String> future;

    LogEntry(String original, Future<String> future) {
     this.original = original;
     this.future = future;
    }
  }
}
```

# Chapter 5. URLs and URIs

HTML is a _hypertext_ markup language because it includes a way to specify links to other documents identified by URLs. **==A URL unambiguously identifies the location of a resource on the Internet. A URL is the most common type of URI, or Uniform Resource Identifier. A URI can identify a resource by its network location, as in a URL, or by its name, number, or other characteristics.==**

The `URL` class is the simplest way for a Java program to locate and retrieve data from the network. You do not need to worry about the details of the protocol being used, or how to communicate with the server; you simply tell Java the URL and it gets the data for you.

## URIs

A Uniform Resource Identifier (URI) is a string of characters in a particular syntax that identifies a resource. The resource identified may be a file on a server; but it may also be an email address, a news message, a book, a person’s name, an Internet host, the current stock price of Oracle, or something else.

**==A resource is a thing that is identified by a URI. A URI is a string that identifies a resource.==** All you ever receive from a server is a _representation_ of a resource which comes in the form of bytes. However a single resource may have different representations. 

---

**TIP**

**One of the key principles of good web architecture is to be profligate with URIs. If anyone might want to address something or refer to something, give it a URI (and in practice a URL). Just because a resource is a part of another resource, or a collection of other resources, or a state of another resource at a particular time, doesn’t mean it can’t have its own URI. For instance, in an email service, every user, every message received, every message sent, every filtered view of the inbox, every contact, every filter rule, and every single page a user might ever look at should have a unique URI.**

**Although architecturally URIs are opaque strings, in practice it’s useful to design them with human-readable substructure. For instance, _http://mail.example.com/_ might be a particular mail server, _http://mail.example.com/johndoe_ might be John Doe’s mail box on that server, and _http://mail.example.com/johndoe?messageID=162977.1361. JavaMail.nobody%40meetup.com_ might be a particular message in that mailbox.**

---

The syntax of a URI is composed of a scheme and a scheme-specific part, separated by a colon, like this:

```java
scheme:scheme-specific-part
```

The syntax of the scheme-specific part depends on the scheme being used. Current schemes include:

data

Base64-encoded data included directly in a link; see RFC 2397

file

A file on a local disk

ftp

An FTP server

http

A World Wide Web server using the Hypertext Transfer Protocol

mailto

An email address

magnet

A resource available for download via peer-to-peer networks such as BitTorrent

telnet

A connection to a Telnet-based service

urn

A Uniform Resource Name

There is no specific syntax that applies to the scheme-specific parts of all URIs. However, many have a hierarchical form, like this:

```shell
//authority/path?query
```

**==The _authority_ part of the URI names the authority responsible for resolving the rest of the URI==**. For instance, the URI _http://www.ietf.org/rfc/rfc3986.txt_ has the scheme _http_, the authority _www.ietf.org_, and the path _/rfc/rfc3986.txt_ (initial slash included). This means the server at www.ietf.org is responsible for mapping the path _/rfc/rfc3986.txt_ to a resource. This URI does not have a query part. The URI _http://www.powells.com/cgi-bin/biblio?inkey=62-1565928709-0_ has the scheme _http_, the authority _www.powells.com_, the path _/cgi-bin/biblio_, and the query `inkey=62-1565928709-0`.

Although most current examples of URIs use an Internet host as an authority, future schemes may not. However, if the authority is an Internet host, optional usernames and ports may also be provided to make the authority more specific. For example, the URI _ftp://mp3:mp3@ci43198-a.ashvil1.nc.home.com:33/VanHalen-Jump.mp3_ has the authority _mp3:mp3@ci43198-a.ashvil1.nc.home.com:33_. This authority has the username _mp3_, the password _mp3_, the host _ci43198-a.ashvil1.nc.home.com_, and the port _33_. It has the scheme _ftp_ and the path _/VanHalen-Jump.mp3_.

The path is a string that the authority can use to determine which resource is identified. **==Different authorities may interpret the same path to refer to different resources==**. For instance, the path _/index.html_ means one thing when the authority is _www.landoverbaptist.org_ and something very different when the authority is _www.churchofsatan.com_. The path may be hierarchical, in which case the individual parts are separated by forward slashes, and the _._ and _.._ operators are used to navigate the hierarchy.

Some URIs aren’t at all hierarchical, at least in the filesystem sense. For example, _snews://secnews.netscape.com/netscape.devs-java_ has a path of _/netscape.devs-java_. Although there’s some hierarchy to the newsgroup names indicated by the period between _netscape_ and _devs-java_, it’s not encoded as part of the URI.

### URLs

A URL is a URI that, as well as identifying a resource, provides a specific network location for the resource that a client can use to retrieve a representation of that resource. **==By contrast, a generic URI may tell you what a resource is, but not actually tell you where or how to get that resource. In the physical world, it’s the difference between the title “Harry Potter and The Deathly Hallows” and the library location “Room 312, Row 28, Shelf 7”. In Java, it’s the difference between the `java.net.URI` class that only identifies resources and the `java.net.URL` class that can both identify and retrieve resources.==**

The network location in a URL usually includes the protocol used to access a server (e.g., FTP, HTTP), the hostname or IP address of the server, and the path to the resource on that server. A typical URL looks like _http://www.ibiblio.org/javafaq/javatutorial.html_. This specifies that there is a file called _javatutorial.html_ in a directory called _javafaq_ on the server _www.ibiblio.org_, and that this file can be accessed via the HTTP protocol.

The syntax of a URL is:

```shell
protocol://userInfo@host:port/path?query#fragment
```

Here the protocol is another word for what was called the scheme of the URI.

In a URL, the protocol part can be _file_, _ftp_, _http_, _https_, _magnet_, _telnet_, or various other strings (though not _urn_).

The _host_ part of a URL is the name of the server that provides the resource you want. It can be a hostname such as _www.oreilly.com_ or _utopia.poly.edu_ or an IP address, such as 204.148.40.9 or 128.238.3.21.

The _userInfo_ is optional login information for the server. If present, it contains a username and, rarely, a password.

The _port_ number is also optional. It’s not necessary if the service is running on its default port (port 80 for HTTP servers).

Together, the userInfo, host, and port constitute the _authority_.

**==The _path_ points to a particular resource on the specified server==**. It often looks like a filesystem path such as _/forum/index.php_. However, it may or may not actually map to a filesystem on the server. If it does map to a filesystem, the path is relative to the document root of the server, not necessarily to the root of the filesystem on the server. As a rule, servers that are open to the public do not show their entire filesystem to clients. Rather, they show only the contents of a specified directory. This directory is called the document root, and all paths and filenames are relative to it.

The _query_ string provides additional arguments for the server. It’s commonly used only in _http_ URLs, where it contains form data for input to programs running on the server.

Finally, the _fragment_ references a particular part of the remote resource. If the remote resource is HTML, the fragment identifier names an anchor in the HTML document.

```java
<h3 id="xtocid1902914">Comments</h3>
```

This tag identifies a particular point in a document. To refer to this point, a URL includes not only the document’s filename but the fragment identifier separated from the rest of the URL by a `#`:

```shell
http://www.cafeaulait.org/javafaq.html#xtocid1902914
```

### Relative URLs

**==A URL tells a web browser a lot about a document: the protocol used to retrieve the document, the host where the document lives, and the path to the document on that host.==** Most of this information is likely to be the same for other URLs that are referenced in the document. Therefore, rather than requiring each URL to be specified in its entirety, a URL may inherit the protocol, hostname, and path of its parent document (i.e., the document in which it appears). URLs that aren’t complete but inherit pieces from their parent are called _relative_ URLs. In contrast, a completely specified URL is called an _absolute URL_. In a relative URL, any pieces that are missing are assumed to be the same as the corresponding pieces from the URL of the document in which the URL is found. For example, suppose that while browsing _http://www.ibiblio.org/javafaq/javatutorial.html_ you click on this hyperlink:

```java
<a href="javafaq.html">
```

The browser cuts _javatutorial.html_ off the end of _http://www.ibiblio.org/javafaq/javatutorial.html_ to get _http://www.ibiblio.org/javafaq/_. Then it attaches _javafaq.html_ onto the end of _http://www.ibiblio.org/javafaq/_ to get _http://www.ibiblio.org/javafaq/javafaq.html_. Finally, it loads that document.

Relative URLs have a number of advantages. First—and least important—they save a little typing. More importantly, relative URLs allow a single document tree to be served by multiple protocols: for instance, both HTTP and FTP. HTTP might be used for direct surfing, while FTP could be used for mirroring the site. **==Most importantly of all, relative URLs allow entire trees of documents to be moved or copied from one site to another without breaking all the internal links.==**

## The URL Class

The `java.net.URL` class is an abstraction of a Uniform Resource Locator such as _http://www.lolcats.com/_ or _ftp://ftp.redhat.com/pub/_. It extends `java.lang.Object`, and it is a final class that cannot be subclassed. Rather than relying on inheritance to configure instances for different kinds of URLs, it uses the strategy design pattern. Protocol handlers are the strategies, and the `URL` class itself forms the context through which the different strategies are selected.

Although storing a URL as a string would be trivial, it is helpful to think of URLs as objects with fields that include the scheme (a.k.a. the protocol), hostname, port, path, query string, and fragment identifier (a.k.a. the ref), each of which may be set independently.

**==URLs are immutable. After a `URL` object has been constructed, its fields do not change. This has the side effect of making them thread safe.==**

### Creating New URLs

Unlike the `InetAddress`  you can construct instances of `java.net.URL`. The constructors differ in the information they require:

```java
public URL(String url) throws MalformedURLException
public URL(String protocol, String hostname, String file)
    throws MalformedURLException
public URL(String protocol, String host, int port, String file)
    throws MalformedURLException
public URL(URL base, String relative) throws MalformedURLException
```

Exactly which protocols are supported is implementation dependent. The only protocols that have been available in all virtual machines are http and file, and the latter is notoriously flaky.

---

 **TIP**

**If the protocol you need isn’t supported by a particular VM, you may be able to install a _protocol handler_ for that scheme to enable the URL class to speak that protocol. In practice, this is way more trouble than it’s worth. You’re better off using a library that exposes a custom API just for that protocol.**

---

Other than verifying that it recognizes the URL scheme, Java does not check the correctness of the URLs it constructs. The programmer is responsible for making sure that URLs created are valid.

#### Constructing a URL from a string

The simplest `URL` constructor just takes an absolute URL in string form as its single argument:

```java
public URL(String url) throws MalformedURLException
```

```java
try {
  URL u = new URL("http://www.audubon.org/");
} catch (MalformedURLException ex)  {
  System.err.println(ex);
}
```

Example 5-1. Which protocols does a virtual machine support?

```java
import java.net.*;

public class ProtocolTester {

  public static void main(String[] args) {

    // hypertext transfer protocol
    testProtocol("http://www.adc.org");

    // secure http
    testProtocol("https://www.amazon.com/exec/obidos/order2/");

    // file transfer protocol
    testProtocol("ftp://ibiblio.org/pub/languages/java/javafaq/");

    // Simple Mail Transfer Protocol
    testProtocol("mailto:elharo@ibiblio.org");

    // telnet
    testProtocol("telnet://dibner.poly.edu/");

    // local file access
    testProtocol("file:///etc/passwd");

    // gopher
    testProtocol("gopher://gopher.anc.org.za/");

    // Lightweight Directory Access Protocol
    testProtocol(
        "ldap://ldap.itd.umich.edu/o=University%20of%20Michigan,c=US?postalAddress");

    // JAR
    testProtocol(
        "jar:http://cafeaulait.org/books/javaio/ioexamples/javaio.jar!"
         + "/com/macfaq/io/StreamCopier.class");

    // NFS, Network File System
    testProtocol("nfs://utopia.poly.edu/usr/tmp/");

    // a custom protocol for JDBC
    testProtocol("jdbc:mysql://luna.ibiblio.org:3306/NEWS");

    // rmi, a custom protocol for remote method invocation
    testProtocol("rmi://ibiblio.org/RenderEngine");

    // custom protocols for HotJava
    testProtocol("doc:/UsersGuide/release.html");
    testProtocol("netdoc:/UsersGuide/release.html");
    testProtocol("systemresource://www.adc.org/+/index.html");
    testProtocol("verbatim:http://www.adc.org/");
  }

  private static void testProtocol(String url) {
    try {
      URL u = new URL(url);
      System.out.println(u.getProtocol() + " is supported");
    } catch (MalformedURLException ex) {
      String protocol = url.substring(0, url.indexOf(':'));
      System.out.println(protocol + " is not supported");
    }
  }
}
```

The results of this program depend on which virtual machine runs it.

```text
http is supported
https is supported
ftp is supported
mailto is supported
telnet is not supported
file is supported
gopher is not supported
ldap is not supported
jar is supported
nfs is not supported
jdbc is not supported
rmi is not supported
doc is not supported
netdoc is supported
systemresource is not supported
verbatim is not supported
```

#### Constructing a URL from its component parts

You can also build a `URL` by specifying the protocol, the hostname, and the file:

```java
public URL(String protocol, String hostname, String file)
    throws MalformedURLException
```

```java
try {
  URL u = new URL("http", "www.eff.org", "/blueribbon.html#intro");
} catch (MalformedURLException ex)  {
  throw new RuntimeException("shouldn't happen; all VMs recognize http");
}
```

This creates a `URL` object that points to _http://www.eff.org/blueribbon.html#intro_, using the default port for the HTTP protocol (port 80).

For the rare occasions when the default port isn’t correct, the next constructor lets you specify the port explicitly as an `int`. The other arguments are the same.

```java
try {
  URL u = new URL("http", "fourier.dur.ac.uk", 8000, "/~dma3mjh/jsci/");
} catch (MalformedURLException ex)  {
  throw new RuntimeException("shouldn't happen; all VMs recognize http");
}
```

#### Constructing relative URLs

This constructor builds an absolute `URL` from a relative `URL` and a base `URL`:

```java
public URL(URL base, String relative) throws MalformedURLException
```

```java
try {
  URL u1 = new URL("http://www.ibiblio.org/javafaq/index.html");
  URL u2 = new URL (u1, "mailinglists.html");
} catch (MalformedURLException ex) {
  System.err.println(ex);
}

```

#### Other sources of URL objects

Besides the constructors discussed here, a number of other methods in the Java class library return `URL` objects. In applets, `getDocumentBase()` returns the `URL` of the page that contains the applet and `getCodeBase()` returns the `URL` of the applet _.class_ file.

The `java.io.File` class has a `toURL()` method that returns a _file_ URL matching the given file

Class loaders are used not only to load classes but also to load resources such as images and audio files. The static `ClassLoader.getSystemResource(String name)` method returns a `URL` from which a single resource can be read. The `ClassLoader.getSystemResources(String name)` method returns an `Enumeration` containing a list of `URL`s from which the named resource can be read. And finally, the instance method `getResource(String name)` searches the path used by the referenced class loader for a URL to the named resource.

### Retrieving Data from a URL

Naked URLs aren’t very exciting. What’s interesting is the data contained in the documents they point to. The `URL` class has several methods that retrieve data from a URL:

```java
public InputStream openStream() throws IOException
public URLConnection openConnection() throws IOException
public URLConnection openConnection(Proxy proxy) throws IOException
public Object getContent() throws IOException
public Object getContent(Class[] classes) throws IOException
```

The most basic and most commonly used of these methods is `openStream()`, which returns an `InputStream` from which you can read the data. If you need more control over the download process, call `openConnection()` instead, which gives you a `URLConnection` which you can configure, and then get an `InputStream` from it.

#### ``public final InputStream openStream() throws IOException``

The `openStream()` method connects to the resource referenced by the `URL`, performs any necessary handshaking between the client and the server, and returns an `InputStream` from which data can be read. The data you get from this `InputStream` is the raw (i.e., uninterpreted) content the `URL` references: ASCII if you’re reading an ASCII text file, raw HTML if you’re reading an HTML file, binary image data if you’re reading an image file, and so forth.

```java
try {
  URL u = new URL("http://www.lolcats.com");
  InputStream in = u.openStream();
  int c;
  while ((c = in.read()) != -1) System.out.write(c);
  in.close();
} catch (IOException ex) {
  System.err.println(ex);
}
```

As with most network streams, reliably closing the stream takes a bit of effort. In Java 6 and earlier, we use the dispose pattern: declare the stream variable outside the `try` block, set it to null, and then close it in the `finally` block if it’s not null.

```java
InputStream in = null
try {
  URL u = new URL("http://www.lolcats.com");
  in = u.openStream();
  int c;
  while ((c = in.read()) != -1) System.out.write(c);
} catch (IOException ex) {
  System.err.println(ex);
} finally {
  try {
    if (in != null) {
      in.close();
    }
  } catch (IOException ex) {
    // ignore
  }
}
```

Java 7 makes this somewhat cleaner by using a nested try-with-resources statement:

```java
try {
  URL u = new URL("http://www.lolcats.com");
  try (InputStream in = u.openStream()) {
    int c;
    while ((c = in.read()) != -1) System.out.write(c);
  }
} catch (IOException ex) {
  System.err.println(ex);
}
```

Example 5-2. Download a web page

```java
import java.io.*;
import java.net.*;

public class SourceViewer {

  public static void main (String[] args) {

    if (args.length > 0) {
      InputStream in = null;
      try {
        // Open the URL for reading
        URL u = new URL(args[0]);
        in = u.openStream();
        // buffer the input to increase performance
        in = new BufferedInputStream(in);
        // chain the InputStream to a Reader
        Reader r = new InputStreamReader(in);
        int c;
        while ((c = r.read()) != -1) {
          System.out.print((char) c);
        }
      } catch (MalformedURLException ex) {
        System.err.println(args[0] + " is not a parseable URL");
      } catch (IOException ex) {
        System.err.println(ex);
      } finally {
        if (in != null) {
          try {
            in.close();
          } catch (IOException e) {
            // ignore
          }
        }
      }
    }
  }
}
```

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en-US" xml:lang="en-US">
<head>
<title>oreilly.com -- Welcome to O'Reilly Media, Inc. -- computer books,
software conferences, online publishing</title>
<meta name="keywords" content="O'Reilly, oreilly, computer books, technical
books, UNIX, unix, Perl, Java, Linux, Internet, Web, C, C++, Windows, Windows
NT, Security, Sys Admin, System Administration, Oracle, PL/SQL, online books,
books online, computer book online, e-books, ebooks, Perl Conference, Open Source
Conference, Java Conference, open source, free software, XML, Mac OS X, .Net, dot
net, C#, PHP, CGI, VB, VB Script, Java Script, javascript, Windows 2000, XP,
```

The shakiest part of this program is that it blithely assumes that the URL points to text, which is not necessarily true. It could well be pointing to a GIF or JPEG image, an MP3 sound file, or something else entirely. Even if does resolve to text, the document encoding may not be the same as the default encoding of the client system. The remote host and local client may not have the same default character set. As a general rule, for pages that use a character set radically different from ASCII, the HTML will include a `META` tag in the header specifying the character set in use. For instance, this `META` tag specifies the Big-5 encoding for Chinese:

```java
<meta http-equiv="Content-Type" content="text/html; charset=big5">
```

An XML document will likely have an XML declaration instead:

```java
<?xml version="1.0" encoding="Big5"?>
```

In practice, there’s no easy way to get at this information other than by parsing the file and looking for a header like this one, and even that approach is limited.

#### ``public URLConnection openConnection() throws IOException``

The `openConnection()` method opens a socket to the specified URL and returns a `URLConnection` object. A `URLConnection` represents an open connection to a network resource.


```java
try {
  URL u = new URL("https://news.ycombinator.com/");
  try {
    URLConnection uc = u.openConnection();
    InputStream in = uc.getInputStream();
    // read from the connection...
  } catch (IOException ex) {
    System.err.println(ex);
  }
} catch (MalformedURLException ex) {
  System.err.println(ex);
}
```

The `URLConnection` gives you access to everything sent by the server: in addition to the document itself in its raw form (e.g., HTML, plain text, binary image data), you can access all the metadata specified by the protocol.

An overloaded variant of this method specifies the proxy server to pass the connection through:

```java
public URLConnection openConnection(Proxy proxy) throws IOException
```

This overrides any proxy server set with the usual `socksProxyHost`, `socksProxyPort`, `http.proxyHost`, `http.proxyPort`, `http.nonProxyHosts`, and similar system properties. If the protocol handler does not support proxies, the argument is ignored and the connection is made directly if possible.

#### ``public final Object getContent() throws IOException
``
The `getContent()` method is the third way to download data referenced by a URL. The `getContent()` method retrieves the data referenced by the URL and tries to make it into some type of object. If the URL refers to some kind of text such as an ASCII or HTML file, the object returned is usually some sort of `InputStream`. If the URL refers to an image such as a GIF or a JPEG file, `getContent()` usually returns a `java.awt.ImageProducer`. What unifies these two disparate classes is that they are not the thing itself but a means by which a program can construct the thing:

```java
URL u = new URL("http://mesola.obspm.fr/");
Object o = u.getContent();
// cast the Object to the appropriate type
// work with the Object...
```

Example 5-3. Download an object

```java
import java.io.*;
import java.net.*;

public class ContentGetter {

  public static void main (String[] args) {

    if  (args.length > 0) {
      // Open the URL for reading
      try {
        URL u = new URL(args[0]);
        Object o = u.getContent();
        System.out.println("I got a " + o.getClass().getName());
      } catch (MalformedURLException ex) {
        System.err.println(args[0] + " is not a parseable URL");
      } catch (IOException ex) {
        System.err.println(ex);
      }
    }
  }
}
```

```text
% java ContentGetter http://www.oreilly.com/ I got a
sun.net.www.protocol.http.HttpURLConnection$HttpInputStream
```

the biggest problems with using `getContent()`: it’s hard to predict what kind of object you’ll get. You could get some kind of `InputStream` or an `ImageProducer` or perhaps an `AudioClip`; it’s easy to check using the `instanceof` operator. This information should be enough to let you read a text file or display an image.

#### ``public final Object getContent(Class[] classes) throws IOException``

A URL’s content handler may provide different views of a resource. This overloaded variant of the `getContent()` method lets you choose which class you’d like the content to be returned as. The method attempts to return the URL’s content in the first available format.

```java
URL u = new URL("http://www.nwu.org");
Class<?>[] types = new Class[3];
types[0] = String.class;
types[1] = Reader.class;
types[2] = InputStream.class;
Object o = u.getContent(types);
```

If the content handler knows how to return a string representation of the resource, then it returns a `String`. If it doesn’t know how to return a string representation of the resource, then it returns a `Reader`. And if it doesn’t know how to present the resource as a reader, then it returns an `InputStream`.

```java
if (o instanceof String) {
  System.out.println(o);
} else if (o instanceof Reader) {
  int c;
  Reader r = (Reader) o;
  while ((c = r.read()) != -1) System.out.print((char) c);
  r.close();
} else if (o instanceof InputStream) {
  int c;
  InputStream in = (InputStream) o;
  while ((c = in.read()) != -1) System.out.write(c);
  in.close();
} else {
  System.out.println("Error: unexpected type " + o.getClass());
}
```

### Splitting a URL into Pieces

**==URLs are composed of five pieces:**==

- ==**The scheme, also known as the protocol**==
- ==**The authority**==
- ==**The path**==
- ==**The fragment identifier, also known as the section or ref**==
- ==**The query string==**

Read-only access to these parts of a URL is provided by nine public methods: `getFile()`, `getHost()`, `getPort()`, `getProtocol()`, `getRef()`, `getQuery()`, `getPath()`, `getUserInfo()`, and `getAuthority()`.

#### public String ``getProtocol()``

The `getProtocol()` method returns a `String` containing the scheme of the URL (e.g., “http”, “https”, or “file”). For example, this code fragment prints _https_:

```java
URL u = new URL("https://xkcd.com/727/");
System.out.println(u.getProtocol());
```

#### public int ``getPort()``

The `getPort()` method returns the port number specified in the URL as an `int`. If no port was specified in the `URL`, `getPort()` returns -1 to signify that the URL does not specify the port explicitly, and will use the default port for the protocol.

```java
URL u = new URL("http://www.ncsa.illinois.edu/AboutUs/");
System.out.println("The port part of " + u + " is " + u.getPort());
```

#### public int ``getDefaultPort()``

The `getDefaultPort()` method returns the default port used for this `URL`’s protocol when none is specified in the URL. If no default port is defined for the protocol, then `getDefaultPort()` returns -1.

#### public String ``getFile()``

The `getFile()` method returns a `String` that contains the path portion of a URL; remember that Java does not break a URL into separate path and file parts. Everything from the first slash (/) after the hostname until the character preceding the # sign that begins a fragment identifier is considered to be part of the file.

```java
URL page = this.getDocumentBase();
System.out.println("This page's path is " + page.getFile());
```

If the URL does not have a file part, Java sets the file to the empty string.

#### public String ``getPath()``

The `getPath()` method is a near synonym for `getFile()`; that is, it returns a `String` containing the path and file portion of a URL. However, unlike `getFile()`, it does not include the query string in the `String` it returns, just the path.

---
 **WARNING**

**Note that the `getPath()` method does not return only the directory path and `getFile()` does not return only the filename, as you might expect. Both `getPath()` and `getFile()` return the full path and filename. The only difference is that `getFile()` also returns the query string and `getPath()` does not.**

---
#### public String ``getRef()``

The `getRef()` method returns the fragment identifier part of the URL. If the URL doesn’t have a fragment identifier, the method returns `null`.

```java
URL u = new URL(
    "http://www.ibiblio.org/javafaq/javafaq.html#xtocid1902914");
System.out.println("The fragment ID of " + u + " is " + u.getRef());
```

#### public String ``getQuery()``

The `getQuery()` method returns the query string of the URL. If the URL doesn’t have a query string, the method returns `null`.

```java
URL u = new URL(
    "http://www.ibiblio.org/nywc/compositions.phtml?category=Piano");
System.out.println("The query string of " + u + " is " + u.getQuery());
```

#### public String ``getUserInfo()``

Some URLs include usernames and occasionally even password information. This information comes after the scheme and before the host; an @ symbol delimits it. For instance, in the URL _http://elharo@java.oreilly.com/_, the user info is _elharo_. Some URLs also include passwords in the user info. For instance, in the URL _ftp://mp3:secret@ftp.example.com/c%3a/stuff/mp3/_, the user info is _mp3:secret_. However, most of the time, including a password in a URL is a security risk. If the URL doesn’t have any user info, `getUserInfo()` returns `null`.

#### public String ``getAuthority()``

Between the scheme and the path of a URL, you’ll find the authority. This part of the URI indicates the authority that resolves the resource. In the most general case, the authority includes the user info, the host, and the port.

Example 5-4. The parts of a URL

```java
import java.net.*;

public class URLSplitter {

  public static void main(String args[]) {

    for (int i = 0; i < args.length; i++) {
      try {
        URL u = new URL(args[i]);
        System.out.println("The URL is " + u);
        System.out.println("The scheme is " + u.getProtocol());
        System.out.println("The user info is " + u.getUserInfo());

        String host = u.getHost();
        if (host != null) {
          int atSign = host.indexOf('@');
          if (atSign != -1) host = host.substring(atSign+1);
          System.out.println("The host is " + host);
        } else {
          System.out.println("The host is null.");
        }

        System.out.println("The port is " + u.getPort());
        System.out.println("The path is " + u.getPath());
        System.out.println("The ref is " + u.getRef());
        System.out.println("The query string is " + u.getQuery());
      } catch (MalformedURLException ex) {
        System.err.println(args[i] + " is not a URL I understand.");
      }
      System.out.println();
    }
  }
}
```

```text
% java URLSplitter    \
ftp://mp3:mp3@138.247.121.61:21000/c%3a/                 \
http://www.oreilly.com                                   \
http://www.ibiblio.org/nywc/compositions.phtml?category=Piano \
http://admin@www.blackstar.com:8080/                     \

The URL is ftp://mp3:mp3@138.247.121.61:21000/c%3a/
The scheme is ftp
The user info is mp3:mp3
The host is 138.247.121.61
The port is 21000
The path is /c%3a/
The ref is null
The query string is null

The URL is http://www.oreilly.com
The scheme is http
The user info is null
The host is www.oreilly.com
The port is -1
The path is
The ref is null
The query string is null

The URL is http://www.ibiblio.org/nywc/compositions.phtml?category=Piano
The scheme is http
The user info is null
The host is www.ibiblio.org
The port is -1
The path is /nywc/compositions.phtml
The ref is null
The query string is category=Piano

The URL is http://admin@www.blackstar.com:8080/
The scheme is http
The user info is admin
The host is www.blackstar.com
The port is 8080
The path is /
The ref is null
The query string is null
```

### Equality and Comparison

The `URL` class contains the usual `equals()` and `hashCode()` methods. These behave almost as you’d expect. **==Two URLs are considered equal if and only if both `URL`s point to the same resource on the same host, port, and path, with the same fragment identifier and query string. However there is one surprise here. The `equals()` method actually tries to resolve the host with DNS==** so that, for example, it can tell that _http://www.ibiblio.org/_ and _http://ibiblio.org/_ are the same.

---

 **==WARNING**==

==**This means that `equals()` on a `URL` is potentially _a blocking I/O operation_! For this reason, you should avoid storing `URL`s in data structure that depend on `equals()` such as `java.util.HashMap`. Prefer `java.net.URI` for this, and convert back and forth from `URI`s to `URL`s when necessary.==**

---

On the other hand, `equals()` does not go so far as to actually compare the resources identified by two URLs.

Example 5-5. Are _http://www.ibiblio.org_ and _http://ibiblio.org_ the same?

```java
import java.net.*;

public class URLEquality {

  public static void main (String[] args) {
    try {
      URL www = new URL ("http://www.ibiblio.org/");
      URL ibiblio = new URL("http://ibiblio.org/");
      if (ibiblio.equals(www)) {
        System.out.println(ibiblio + " is the same as " + www);
      } else {
        System.out.println(ibiblio + " is not the same as " + www);
      }
    } catch (MalformedURLException ex) {
      System.err.println(ex);
    }
  }
}
```

**==`URL` does not implement `Comparable`.==**

The `URL` class also has a `sameFile()` method that checks whether two URLs point to the same resource:

```java
public boolean sameFile(URL other)
```

The comparison is essentially the same as with `equals()`, DNS queries included, except that `sameFile()` does not consider the fragment identifier.

```java
URL u1 = new URL("http://www.ncsa.uiuc.edu/HTMLPrimer.html#GS");
URL u2 = new URL("http://www.ncsa.uiuc.edu/HTMLPrimer.html#HD");
if (u1.sameFile(u2)) {
  System.out.println(u1 + " is the same file as \n" + u2);
} else {
  System.out.println(u1 + " is not the same file as \n" + u2);
}
```

```text
http://www.ncsa.uiuc.edu/HTMLPrimer.html#GS is the same file as
http://www.ncsa.uiuc.edu/HTMLPrimer.html#HD
```

### Conversion

`URL` has three methods that convert an instance to another form: `toString()`, `toExternalForm()`, and `toURI()`.

Like all good classes, `java.net.URL` has a `toString()` method. The `String` produced by `toString()` is always an absolute URL, such as _http://www.cafeaulait.org/javatutorial.html_. It’s uncommon to call `toString()` explicitly. Print statements call `toString()` implicitly. Outside of print statements, it’s more proper to use `toExternalForm()` instead:

```java
public String toExternalForm()
```

The `toExternalForm()` method converts a `URL` object to a string that can be used in an HTML link or a web browser’s Open URL dialog.

**==The `toExternalForm()` method returns a human-readable `String` representing the URL. It is identical to the `toString()` method. In fact, all the `toString()` method does is return `toExternalForm()`.==**

Finally, the `toURI()` method converts a `URL` object to an equivalent `URI` object:

```java
public URI toURI() throws URISyntaxException
```

In the meantime, the main thing you need to know is that the `URI` class provides much more accurate, specification-conformant behavior than the `URL` class. For operations like absolutization and encoding, you should prefer the `URI` class where you have the option. You should also prefer the `URI` class if you need to store URLs in a hashtable or other data structure, since its `equals()` method is not blocking. The `URL` class should be used primarily when you want to download content from a server.

## The URI Class

A URI is a generalization of a URL that includes not only Uniform Resource Locators but also Uniform Resource Names (URNs). Most URIs used in practice are URLs, but most specifications and standards such as XML are defined in terms of URIs. In Java, URIs are represented by the `java.net.URI` class. This class differs from the `java.net.URL` class in three important ways:

- ==**The `URI` class is purely about identification of resources and parsing of URIs. It provides no methods to retrieve a representation of the resource identified by its URI.**==
- ==**The `URI` class is more conformant to the relevant specifications than the `URL` class.**==
- ==**A `URI` object can represent a relative URI. The `URL` class absolutizes all URIs before storing them.==**

**==In brief, a `URL` object is a representation of an application layer protocol for network retrieval, whereas a `URI` object is purely for string parsing and manipulation. The `URI` class has no network retrieval capabilities. The `URL` class has some string parsing methods, such as `getFile()` and `getRef()`, but many of these are broken and don’t always behave exactly as the relevant specifications say they should.==**


### Constructing a URI

URIs are built from strings. You can either pass the entire URI to the constructor in a single string, or the individual pieces:

```java
public URI(String uri) throws URISyntaxException
public URI(String scheme, String schemeSpecificPart, String fragment)
    throws URISyntaxException
public URI(String scheme, String host, String path, String fragment)
    throws URISyntaxException
public URI(String scheme, String authority, String path, String query,
    String fragment) throws URISyntaxException
public URI(String scheme, String userInfo, String host, int port,
    String path, String query, String fragment) throws URISyntaxException
```

**==Unlike the `URL` class, the `URI` class does not depend on an underlying protocol handler. As long as the URI is syntactically correct, Java does not need to understand its protocol in order to create a representative `URI` object.==**

The first constructor creates a new `URI` object from any convenient string.

```java
URI voice = new URI("tel:+1-800-9988-9938");
URI web   = new URI("http://www.xml.com/pub/a/2003/09/17/stax.html#id=_hbc");
URI book  = new URI("urn:isbn:1-565-92870-9");
```

If the string argument does not follow URI syntax rules—for example, if the URI begins with a colon—this constructor throws a `URISyntaxException`. This is a checked exception, so either catch it or declare that the method where the constructor is invoked can throw it. However, one syntax rule is not checked. In contradiction to the URI specification, the characters used in the URI are not limited to ASCII. They can include other Unicode characters, such as ø and é.

The second constructor that takes a scheme specific part is mostly used for nonhierarchical URIs. The scheme is the URI’s protocol, such as http, urn, tel, and so forth. It must be composed exclusively of ASCII letters and digits and the three punctuation characters `+`, `-`, and `.`. It must begin with a letter. Passing null for this argument omits the scheme, thus creating a relative

```java
URI absolute = new URI("http", "//www.ibiblio.org" , null);
URI relative = new URI(null, "/javafaq/index.shtml", "today");
```

Because the `URI` class encodes illegal characters with percent escapes, there’s effectively no syntax error you can make in this part.

Finally, the third argument contains the fragment identifier, if any. Again, characters that are forbidden in a fragment identifier are escaped automatically. Passing null for this argument simply omits the fragment identifier.

The third constructor is used for hierarchical URIs such as http and ftp URLs. The host and path together (separated by a /) form the scheme-specific part for this URI.

```java
URI today= new URI("http", "www.ibiblio.org", "/javafaq/index.html", "today");
```

If the constructor cannot form a legal hierarchical URI from the supplied pieces—for instance, if there is a scheme so the URI has to be absolute but the path doesn’t start with /—then it throws a `URISyntaxException`.

The fourth constructor is basically the same as the third, with the addition of a query string.

```java
URI today = new URI("http", "www.ibiblio.org", "/javafaq/index.html",
    "referrer=cnet&date=2014-02-23",  "today");
```

The fifth constructor is the master hierarchical URI constructor that the previous two invoke. It divides the authority into separate user info, host, and port parts, each of which has its own syntax rules.

```java
URI styles = new URI("ftp", "anonymous:elharo@ibiblio.org",
    "ftp.oreilly.com",  21, "/pub/stylesheet", null, null);
```

### The Parts of the URI

**==A URI reference has up to three parts: a scheme, a scheme-specific part, and a fragment identifier==**. The general format is:

```java
scheme:scheme-specific-part:fragment
```

If the scheme is omitted, the URI reference is relative. If the fragment identifier is omitted, the URI reference is a pure URI. The `URI` class has getter methods that return these three parts of each `URI` object. The `getRawFoo()` methods return the encoded forms of the parts of the URI, while the equivalent `getFoo()` methods first decode any percent-escaped characters and then return the decoded part:

```java
public String getScheme()
public String getSchemeSpecificPart()
public String getRawSchemeSpecificPart()
public String getFragment()
public String getRawFragment()
```

---

 **TIP**

**There’s no `getRawScheme()` method because the URI specification requires that all scheme names be composed exclusively of URI-legal ASCII characters and does not allow percent escapes in scheme names.**

---

A URI that has a scheme is an _absolute_ URI. A URI without a scheme is _relative_. The `isAbsolute()` method returns true if the URI is absolute, false if it’s relative:

```java
public boolean isAbsolute()
```

in many useful URIs, including the very common _file_ and _http_ URLs, the scheme-specific part has a particular hierarchical format divided into an authority, a path, and a query string. The authority is further divided into user info, host, and port. The `isOpaque()` method returns false if the URI is hierarchical, true if it’s not hierarchical—that is, if it’s opaque:

```java
public boolean isOpaque()
```

**==If the URI is opaque, all you can get is the scheme, scheme-specific part, and fragment identifier==**. However, if the URI is hierarchical, there are getter methods for all the different parts of a hierarchical URI:

```java
public String getAuthority()
public String getFragment()
public String getHost()
public String getPath()
public String getPort()
public String getQuery()
public String getUserInfo()
```

```java
public String getRawAuthority()
public String getRawFragment()
public String getRawPath()
public String getRawQuery()
public String getRawUserInfo()
```

---

 **==TIP**==

==**There are no `getRawPort()` and `getRawHost()` methods because these components are always guaranteed to be made up of ASCII characters.==**

---

For various technical reasons that don’t have a lot of practical impact, Java can’t always initially detect syntax errors in the authority component. The immediate symptom of this failing is normally an inability to return the individual parts of the authority, port, host, and user info. In this event, you can call `parseServerAuthority()` to force the authority to be reparsed:

```java
public URI parseServerAuthority() throws URISyntaxException
```

The original `URI` does not change (`URI` objects are immutable), but the `URI` returned will have separate authority parts for user info, host, and port. If the authority cannot be parsed, a `URISyntaxException` is thrown.

Example 5-6. The parts of a URI

```java
import java.net.*;

public class URISplitter {

  public static void main(String args[]) {

    for (int i = 0; i < args.length; i++) {
      try {
        URI u = new URI(args[i]);
        System.out.println("The URI is " + u);
        if (u.isOpaque()) {
          System.out.println("This is an opaque URI.");
          System.out.println("The scheme is " + u.getScheme());
          System.out.println("The scheme specific part is "
              + u.getSchemeSpecificPart());
          System.out.println("The fragment ID is " + u.getFragment());
        } else {
          System.out.println("This is a hierarchical URI.");
          System.out.println("The scheme is " + u.getScheme());
          try {
            u = u.parseServerAuthority();
            System.out.println("The host is " + u.getHost());
            System.out.println("The user info is " + u.getUserInfo());
            System.out.println("The port is " + u.getPort());
          } catch (URISyntaxException ex) {
            // Must be a registry based authority
            System.out.println("The authority is " + u.getAuthority());
          }
          System.out.println("The path is " + u.getPath());
          System.out.println("The query string is " + u.getQuery());
          System.out.println("The fragment ID is " + u.getFragment());
        }
      } catch (URISyntaxException ex) {
        System.err.println(args[i] + " does not seem to be a URI.");
      }
      System.out.println();
    }
  }
}
```

```text
% java URISplitter tel:+1-800-9988-9938 \
  http://www.xml.com/pub/a/2003/09/17/stax.html#id=_hbc \
  urn:isbn:1-565-92870-9
The URI is tel:+1-800-9988-9938
This is an opaque URI.
The scheme is tel
The scheme specific part is +1-800-9988-9938
The fragment ID is null

The URI is http://www.xml.com/pub/a/2003/09/17/stax.html#id=_hbc
This is a hierarchical URI.
The scheme is http
The host is www.xml.com
The user info is null
The port is -1
The path is /pub/a/2003/09/17/stax.html
The query string is null
The fragment ID is id=_hbc

The URI is urn:isbn:1-565-92870-9
This is an opaque URI.
The scheme is urn
The scheme specific part is isbn:1-565-92870-9
The fragment ID is null
```

### Resolving Relative URIs

The `URI` class has three methods for converting back and forth between relative and absolute URIs:

```java
public URI resolve(URI uri)
public URI resolve(String uri)
public URI relativize(URI uri)
```

**==The `resolve()` methods compare the `uri` argument to this `URI` and use it to construct a new `URI` object that wraps an absolute URI.==**

```java
URI absolute = new URI("http://www.example.com/");
URI relative = new URI("images/logo.png");
URI resolved = absolute.resolve(relative);
```

After they’ve executed, `resolved` contains the absolute URI _http://www.example.com/images/logo.png_.

If the invoking `URI` does not contain an absolute URI itself, the `resolve()` method resolves as much of the URI as it can and returns a new relative URI object as a result.

```java
URI top = new URI("javafaq/books/");
URI resolved = top.resolve("jnp3/examples/07/index.html");
```

After they’ve executed, `resolved` now contains the relative URI _javafaq/books/jnp3/examples/07/index.html_ with no scheme or authority.

It’s also possible to reverse this procedure; that is, to go from an absolute URI to a relative one. The `relativize()` method creates a new `URI` object from the `uri` argument that is relative to the invoking `URI`. The argument is not changed.

```java
URI absolute = new URI("http://www.example.com/images/logo.png");
URI top = new URI("http://www.example.com/");
URI relative = top.relativize(absolute);
```

### Equality and Comparison

URIs are tested for equality pretty much as you’d expect. It’s not quite direct string comparison. **==Equal URIs must both either be hierarchical or opaque==**. The scheme and authority parts are compared without considering case. That is, _http_ and _HTTP_ are the same scheme, and _www.example.com_ is the same authority as _www.EXAMPLE.com_.

The `hashCode()` method is consistent with equals. Equal URIs do have the same hash code and unequal URIs are fairly unlikely to share the same hash code.

URI implements `Comparable`, and thus URIs can be ordered. The ordering is based on string comparison of the individual parts, in this sequence:

1. ==**If the schemes are different, the schemes are compared, without considering case.**==
2. ==**Otherwise, if the schemes are the same, a hierarchical URI is considered to be less than an opaque URI with the same scheme.**==
3. ==**If both URIs are opaque URIs, they’re ordered according to their scheme-specific parts.**==
4. ==**If both the scheme and the opaque scheme-specific parts are equal, the URIs are compared by their fragments.**==
5. ==**If both URIs are hierarchical, they’re ordered according to their authority components, which are themselves ordered according to user info, host, and port, in that order. Hosts are case insensitive.**==
6. ==**If the schemes and the authorities are equal, the path is used to distinguish them.**==
7. ==**If the paths are also equal, the query strings are compared.**==
8. ==**If the query strings are equal, the fragments are compared.==**

URIs are not comparable to any type except themselves. Comparing a `URI` to anything except another `URI` causes a `ClassCastException`.

### String Representations

Two methods convert URI objects to strings, `toString()` and `toASCIIString()`:

```java
public String toString()
public String toASCIIString()
```

The `toString()` method returns an _unencoded_ string form of the `URI` (i.e., characters like é and \ are not percent escaped). Therefore, the result of calling this method is not guaranteed to be a syntactically correct URI, though it is in fact a syntactically correct IRI. This form is sometimes useful for display to human beings, but usually not for retrieval.

The `toASCIIString()` method returns an _encoded_ string form of the `URI`. Characters like é and \ are always percent escaped whether or not they were originally escaped. This is the string form of the URI you should use most of the time

## x-www-form-urlencoded

One of the challenges faced by the designers of the Web was dealing with the differences between operating systems. These differences can cause problems with URLs:

 **==To solve these problems, characters used in URLs must come from a fixed subset of ASCII, specifically:**==

- ==**The capital letters A–Z**==
- ==**The lowercase letters a–z**==
- ==**The digits 0–9**==
- ==**The punctuation characters - _ . ! ~ * ' (and ,)**==

==**The characters : / & ? @ # ; $ + = and % may also be used, but only for their specified purposes.==** If these characters occur as part of a path or query string, they and all other characters should be encoded.

The `URL` class does not encode or decode automatically. You can construct `URL` objects that use illegal ASCII and non-ASCII characters and/or percent escapes. Such characters and escapes are not automatically encoded or decoded when output by methods such as `getPath()` and `toExternalForm()`. You are responsible for making sure all such characters are properly encoded in the strings used to construct a `URL` object.

Luckily, Java provides `URLEncoder` and `URLDecoder` classes to cipher strings in this format.

### URLEncoder

To URL encode a string, pass the string and the character set name to the `URLEncoder.encode()` method.

```java
String encoded = URLEncoder.encode("This*string*has*asterisks", "UTF-8");
```

`URLEncoder.encode()` returns a copy of the input string with a few changes.

Example 5-7. x-www-form-urlencoded strings

```java
import java.io.*;
import java.net.*;

public class EncoderTest {

  public static void main(String[] args) {

    try {
      System.out.println(URLEncoder.encode("This string has spaces",
                                              "UTF-8"));
      System.out.println(URLEncoder.encode("This*string*has*asterisks",
                                              "UTF-8"));
      System.out.println(URLEncoder.encode("This%string%has%percent%signs",
                                              "UTF-8"));
      System.out.println(URLEncoder.encode("This+string+has+pluses",
                                              "UTF-8"));
      System.out.println(URLEncoder.encode("This/string/has/slashes",
                                              "UTF-8"));
      System.out.println(URLEncoder.encode("This\"string\"has\"quote\"marks",
                                              "UTF-8"));
      System.out.println(URLEncoder.encode("This:string:has:colons",
                                              "UTF-8"));
      System.out.println(URLEncoder.encode("This~string~has~tildes",
                                              "UTF-8"));
      System.out.println(URLEncoder.encode("This(string)has(parentheses)",
                                              "UTF-8"));
      System.out.println(URLEncoder.encode("This.string.has.periods",
                                              "UTF-8"));
      System.out.println(URLEncoder.encode("This=string=has=equals=signs",
                                              "UTF-8"));
      System.out.println(URLEncoder.encode("This&string&has&ampersands",
                                              "UTF-8"));
      System.out.println(URLEncoder.encode("Thiséstringéhasé
                                              non-ASCII characters", "UTF-8"));
    } catch (UnsupportedEncodingException ex) {
      throw new RuntimeException("Broken VM does not support UTF-8");
    }
  }
}
```

```text
% javac -encoding UTF8 EncoderTest
% java EncoderTest
This+string+has+spaces
This*string*has*asterisks
This%25string%25has%25percent%25signs
This%2Bstring%2Bhas%2Bpluses
This%2Fstring%2Fhas%2Fslashes
This%22string%22has%22quote%22marks
This%3Astring%3Ahas%3Acolons
This%7Estring%7Ehas%7Etildes
This%28string%29has%28parentheses%29
This.string.has.periods
This%3Dstring%3Dhas%3Dequals%3Dsigns
This%26string%26has%26ampersands
This%C3%A9string%C3%A9has%C3%A9non-ASCII+characters
```

Notice in particular that this method encodes the forward slash, the ampersand, the equals sign, and the colon. It does not attempt to determine how these characters are being used in a URL. Consequently, you have to encode URLs piece by piece rather than encoding an entire URL in one method call. This is an important point, because the most common use of `URLEncoder` is preparing query strings for communicating with server-side programs that use `GET`.

```java
https://www.google.com/search?hl=en&as_q=Java&as_epq=I/O
```

This code fragment encodes it:

```java
String query = URLEncoder.encode(
    "https://www.google.com/search?hl=en&as_q=Java&as_epq=I/O", "UTF-8");
System.out.println(query);
```

Unfortunately, the output is:

```java
https%3A%2F%2Fwww.google.com%2Fsearch%3Fhl%3Den%26as_q%3DJava%26as_epq%3DI%2FO
```

The problem is that `URLEncoder.encode()` encodes blindly. It can’t distinguish between special characters used as part of the URL or query string, like `/` and `=`, and characters that need to be encoded. Consequently, URLs need to be encoded a piece at a time like this:

```java
String url = "https://www.google.com/search?";
url += URLEncoder.encode("hl", "UTF-8");
url += "=";
url += URLEncoder.encode("en", "UTF-8");
url += "&";
url += URLEncoder.encode("as_q", "UTF-8");
url += "=";
url += URLEncoder.encode("Java", "UTF-8");
url += "&";
url += URLEncoder.encode("as_epq", "UTF-8");
url += "=";
url += URLEncoder.encode("I/O", "UTF-8");

System.out.println(url);
```

```text
https://www.google.com/search?hl=en&as_q=Java&as_epq=I%2FO
```

Example 5-8. The ``QueryString`` class

```java
import java.io.UnsupportedEncodingException;
import java.net.URLEncoder;

public class QueryString {

  private StringBuilder query = new StringBuilder();

  public QueryString() {
  }

  public synchronized void add(String name, String value) {
    query.append('&');
    encode(name, value);
  }

  private synchronized void encode(String name, String value) {
    try {
      query.append(URLEncoder.encode(name, "UTF-8"));
      query.append('=');
      query.append(URLEncoder.encode(value, "UTF-8"));
    } catch (UnsupportedEncodingException ex) {
      throw new RuntimeException("Broken VM does not support UTF-8");
    }
  }

  public synchronized String getQuery() {
    return query.toString();
  }

  @Override
  public String toString() {
    return getQuery();
  }
}
```

```java
QueryString qs = new QueryString();
qs.add("hl", "en");
qs.add("as_q", "Java");
qs.add("as_epq", "I/O");
String url = "http://www.google.com/search?" + qs;
System.out.println(url);
```

### URLDecoder

The corresponding `URLDecoder` class has a static `decode()` method that decodes strings encoded in x-www-form-url-encoded format. That is, it converts all plus signs to spaces and all percent escapes to their corresponding character:

```java
public static String decode(String s, String encoding)
    throws UnsupportedEncodingException
```

```java
String input = "https://www.google.com/" +
    "search?hl=en&as_q=Java&as_epq=I%2FO";
String output = URLDecoder.decode(input, "UTF-8");
System.out.println(output);

```

## Proxies

Many systems access the Web and sometimes other non-HTTP parts of the Internet through _proxy servers_. A proxy server receives a request for a remote server from a local client. The proxy server makes the request to the remote server and forwards the result back to the local client. Sometimes this is done for security reasons, such as to prevent remote hosts from learning private details about the local network configuration. Other times it’s done to prevent users from accessing forbidden sites by filtering outgoing requests and limiting which sites can be viewed.

Java programs based on the `URL` class can work through most common proxy servers and protocols. Indeed, this is one reason you might want to choose to use the `URL` class rather than rolling your own HTTP or other client on top of raw sockets.

### System Properties

For basic operations, all you have to do is set a few system properties to point to the addresses of your local proxy servers. If you are using a pure HTTP proxy, set `http.proxyHost` to the domain name or the IP address of your proxy server and `http.proxyPort` to the port of the proxy server (the default is 80). There are several ways to do this, including calling `System.setProperty()` from within your Java code or using the `-D` options when launching the program.

```java
%  java -Dhttp.proxyHost=192.168.254.254  -Dhttp.proxyPort=9000
com.domain.Program
```

If the proxy requires a username and password, you’ll need to install an `Authenticator`

If you want to exclude a host from being proxied and connect directly instead, set the `http.nonProxyHosts` system property to its hostname or IP address. To exclude multiple hosts, separate their names by vertical bars.

```java
System.setProperty("http.proxyHost", "192.168.254.254");
System.setProperty("http.proxyPort", "9000");
System.setProperty("http.nonProxyHosts", "java.oreilly.com|xml.oreilly.com");
```

If you are using an FTP proxy server, set the `ftp.proxyHost`, `ftp.proxyPort`, and `ftp.nonProxyHosts` properties in the same way.

Java does not support any other application layer proxies, but if you’re using a transport layer SOCKS proxy for all TCP connections, you can identify it with the `socksProxyHost` and `socksProxyPort` system properties. Java does not provide an option for non-proxying with SOCKS. It’s an all-or-nothing decision.

### The Proxy Class

The `Proxy` class allows more fine-grained control of proxy servers from within a Java program. Specifically, it allows you to choose different proxy servers for different remote hosts. The proxies themselves are represented by instances of the `java.net.Proxy` class. There are still only three kinds of proxies, HTTP, SOCKS, and direct connections (no proxy at all), represented by three constants in the `Proxy.Type` enum:

- ==**`Proxy.Type.DIRECT`**==
- ==**`Proxy.Type.HTTP`**==
- ==**`Proxy.Type.SOCKS`==**

Besides its type, the other important piece of information about a proxy is its address and port, given as a `SocketAddress` object.

```java
SocketAddress address = new InetSocketAddress("proxy.example.com", 80);
Proxy proxy = new Proxy(Proxy.Type.HTTP, address);
```

### The ProxySelector Class

Each running virtual machine has a single `java.net.ProxySelector` object it uses to locate the proxy server for different connections. The default `ProxySelector` merely inspects the various system properties and the URL’s protocol to decide how to connect to different hosts. However, you can install your own subclass of `ProxySelector` in place of the default selector and use it to choose different proxies based on protocol, host, path, time of day, or other criteria.

The key to this class is the abstract `select()` method:

```java
public abstract List<Proxy> select(URI uri)
```

Java passes this method a `URI` object (not a `URL` object) representing the host to which a connection is needed. For a connection made with the URL class, this object typically has the form _http://www.example.com/_ or _ftp://ftp.example.com/pub/files/_

The second abstract method in this class you must implement is `connectFailed()`:

```java
public void connectFailed(URI uri, SocketAddress address, IOException ex)
```

This is a callback method used to warn a program that the proxy server isn’t actually making the connection.

Example 5-9. A ``ProxySelector`` that remembers what it can connect to
```java
import java.io.*;
import java.net.*;
import java.util.*;

public class LocalProxySelector extends ProxySelector {

  private List<URI> failed = new ArrayList<URI>();

  public List<Proxy> select(URI uri) {

    List<Proxy> result = new ArrayList<Proxy>();
    if (failed.contains(uri)
        || !"http".equalsIgnoreCase(uri.getScheme())) {
      result.add(Proxy.NO_PROXY);
    } else {
      SocketAddress proxyAddress
          = new InetSocketAddress( "proxy.example.com", 8000);
      Proxy proxy = new Proxy(Proxy.Type.HTTP, proxyAddress);
      result.add(proxy);
    }

    return result;
  }

  public void connectFailed(URI uri, SocketAddress address, IOException ex) {
    failed.add(uri);
  }
}
```

As I said, each virtual machine has exactly one `ProxySelector`. To change the `ProxySelector`, pass the new selector to the static `ProxySelector.setDefault()` method

```java
ProxySelector selector = new LocalProxySelector():
ProxySelector.setDefault(selector);
```

From this point forward, all connections opened by that virtual machine will ask the `ProxySelector` for the right proxy to use. You normally shouldn’t use this in code running in a shared environment.

## Communicating with Server-Side Programs Through GET

The `URL` class makes it easy for Java applets and applications to communicate with server-side programs such as CGIs, servlets, PHP pages, and others that use the `GET` method.

All you need to know is what combination of names and values the program expects to receive. Then you can construct a URL with a query string that provides the requisite names and values. All names and values must be x-www-form-url-encoded—as by the `URLEncoder.encode()` method

Many programs are designed to process form input. If this is the case, it’s straightforward to figure out what input the program expects. The method the form uses should be the value of the `METHOD` attribute of the `FORM` element. This value should be either `GET`, in which case you use the process described here, or `POST`, in which case you use the process. The part of the URL that precedes the query string is given by the value of the `ACTION` attribute of the `FORM` element. Note that this may be a relative URL, in which case you’ll need to determine the corresponding absolute URL. Finally, the names in the name-value pairs are simply the values of the `NAME` attributes of the `INPUT` elements. The values of the pairs are whatever the user types into the form.

```html
<form name="search" action="http://www.google.com/search" method="get">
  <input name="q" />
  <input type="hidden" value="cafeconleche.org" name="domains" />
  <input type="hidden" name="sitesearch" value="cafeconleche.org" />
  <input type="hidden" name="sitesearch2" value="cafeconleche.org" />
   <br />
   <input type="image" height="22" width="55"
      src="images/search_blue.gif" alt="search" border="0"
      name="search-image" />
</form>
```

In some cases, the program you’re talking to may not be able to handle arbitrary text strings for values of particular inputs. However, since the form is meant to be read and filled in by human beings, it should provide sufficient clues to figure out what input is expected; for instance, that a particular field is supposed to be a two-letter state abbreviation or a phone number. Sometimes the inputs may not have such obvious names. There may not even be a form, just links to follow. In this case, you have to do some experimenting, first copying some existing values and then tweaking them to see what values are and aren’t accepted. You don’t need to do this in a Java program. You can simply edit the URL in the address or location bar of your web browser window.

---

 **==TIP**==

==**The likelihood that other hackers may experiment with your own server-side programs in such a fashion is a good reason to make them extremely robust against unexpected input.==**

---

Regardless of how you determine the set of name-value pairs the server expects, communicating with it once you know them is simple. All you have to do is create a query string that includes the necessary name-value pairs, then form a URL that includes that query string. Send the query string to the server and read its response using the same methods you use to connect to a server and retrieve a static HTML page. There’s no special protocol to follow once the URL is constructed.

The Open Directory interface is a simple form with one input field named `search`; input typed in this field is sent to a program at _http://search.dmoz.org/cgi-bin/search_, which does the actual search. The HTML for the form looks like this:

```java
<form class="center mb1em" action="search" method="GET">
  <input style="*vertical-align:middle;" size="45" name="q" value="" class="qN">
  <input style="*vertical-align:middle; *padding-top:1px;" value="Search"
        class="btn" type="submit">
  <a href="search?type=advanced"><span class="advN">advanced</span></a>
</form>
```

Example 5-10. Do an Open Directory search

```java
import java.io.*;
import java.net.*;

public class DMoz {

  public static void main(String[] args) {

    String target = "";
    for (int i = 0; i < args.length; i++) {
      target += args[i] + " ";
    }
    target = target.trim();

    QueryString query = new QueryString();
    query.add("q", target);
    try {
      URL u = new URL("http://www.dmoz.org/search/?" + query)
      try (InputStream in = new BufferedInputStream(u.openStream())) {
        InputStreamReader theHTML = new InputStreamReader(in);
        int c;
        while ((c = theHTML.read()) != -1) {
          System.out.print((char) c);
        }
      }
    } catch (MalformedURLException ex) {
      System.err.println(ex);
    } catch (IOException ex) {
      System.err.println(ex);
    }
  }
}
```

## Accessing Password-Protected Sites

Many popular sites require a username and password for access. Some sites, such as the W3C member pages, implement this through HTTP authentication. Others, such as the _New York Times_ website, implement it through cookies and HTML forms. Java’s `URL` class can access sites that use HTTP authentication, although you’ll of course need to tell it which username and password to use.

Supporting sites that use nonstandard, cookie-based authentication is more challenging, not least because this varies a lot from one site to another. Implementing cookie authentication is hard short of implementing a complete web browser with full HTML forms and cookie support Accessing sites protected by standard HTTP authentication is much easier.

### The Authenticator Class

The `java.net` package includes an `Authenticator` class you can use to provide a username and password for sites that protect themselves using HTTP authentication:

```java
public abstract class Authenticator extends Object
```

Since `Authenticator` is an abstract class, you must subclass it. Different subclasses may retrieve the information in different ways.

To make the `URL` class use the subclass, install it as the default authenticator by passing it to the static `Authenticator.setDefault()` method:

```java
public static void setDefault(Authenticator a)
```

For example, if you’ve written an `Authenticator` subclass named `DialogAuthenticator`, you’d install it like this:

```java
Authenticator.setDefault(new DialogAuthenticator());
```

You only need to do this once. From this point forward, when the `URL` class needs a username and password, it will ask the `DialogAuthenticator` using the static `Authenticator.requestPasswordAuthentication()` method:

```java
public static PasswordAuthentication requestPasswordAuthentication(
    InetAddress address, int port, String protocol, String prompt, String scheme)
    throws SecurityException
```

The `address` argument is the host for which authentication is required. The `port` argument is the port on that host, and the `protocol` argument is the application layer protocol by which the site is being accessed. The HTTP server provides the `prompt`. It’s typically the name of the realm for which authentication is required. The `scheme` is the authentication scheme being used. 

Untrusted applets are not allowed to ask the user for a name and password. Trusted applets can do so, but only if they possess the `requestPasswordAuthentication` `NetPermission`. Otherwise, `Authenticator.requestPasswordAuthentication()` throws a `SecurityException`.

The `Authenticator` subclass must override the `getPasswordAuthentication()` method. Inside this method, you collect the username and password from the user or some other source and return it as an instance of the `java.net.PasswordAuthentication` class:

```java
protected PasswordAuthentication getPasswordAuthentication()
```

If you don’t want to authenticate this request, return `null`, and Java will tell the server it doesn’t know how to authenticate the connection. If you submit an incorrect username or password, Java will call `getPasswordAuthentication()` again to give you another chance to provide the right data. You normally have five tries to get the username and password correct; after that, `openStream()` throws a `ProtocolException`.

Usernames and passwords are cached within the same virtual machine session. Once you set the correct password for a realm, you shouldn’t be asked for it again unless you’ve explicitly deleted the password by zeroing out the `char` array that contains it.

You can get more details about the request by invoking any of these methods inherited from the `Authenticator` superclass:

```java
protected final InetAddress getRequestingSite()
protected final int         getRequestingPort()
protected final String      getRequestingProtocol()
protected final String      getRequestingPrompt()
protected final String      getRequestingScheme()
protected final String      getRequestingHost()
protected final String      getRequestingURL()
protected Authenticator.RequestorType getRequestorType()
```

These methods either return the information as given in the last call to `requestPasswordAuthentication()` or return `null` if that information is not available.

The `getRequestingURL()` method returns the complete URL for which authentication has been requested—an important detail if a site uses different names and passwords for different files. The `getRequestorType()` method returns one of the two named constants (i.e., `Authenticator.RequestorType.PROXY` or `Authenticator.RequestorType.SERVER`) to indicate whether the server or the proxy server is requesting the authentication.

### The PasswordAuthentication Class

`PasswordAuthentication` is a very simple final class that supports two read-only properties: username and password. The username is a `String`. The password is a `char` array so that the password can be erased when it’s no longer needed. A `String` would have to wait to be garbage collected before it could be erased, and even then it might still exist somewhere in memory on the local system, possibly even on disk if the block of memory that contained it had been swapped out to virtual memory at one point. Both username and password are set in the constructor:

```java
public PasswordAuthentication(String userName, char[] password)
```

Each is accessed via a `getter` method:

```java
public String getUserName()
public char[] getPassword()
```

### The JPasswordField Class

One useful tool for asking users for their passwords in a more or less secure fashion is the `JPasswordField` component from Swing:

```java
public class JPasswordField extends JTextField
```

his lightweight component behaves almost exactly like a text field. However, anything the user types into it is echoed as an asterisk. This way, the password is safe from anyone looking over the user’s shoulder at what’s being typed on the screen.

`JPasswordField` also stores the passwords as a `char` array so that when you’re done with the password you can overwrite it with zeros. It provides the `getPassword()` method to return this:

```java
public char[] getPassword()
```

Example 5-11. A GUI authenticator

```java
import java.awt.*;
import java.awt.event.*;
import java.net.*;
import javax.swing.*;

public class DialogAuthenticator extends Authenticator {

  private JDialog passwordDialog;
  private JTextField usernameField = new JTextField(20);
  private JPasswordField passwordField = new JPasswordField(20);
  private JButton okButton = new JButton("OK");
  private JButton cancelButton = new JButton("Cancel");
  private JLabel mainLabel
      = new JLabel("Please enter username and password: ");

  public DialogAuthenticator() {
    this("", new JFrame());
  }

  public DialogAuthenticator(String username) {
    this(username, new JFrame());
  }

  public DialogAuthenticator(JFrame parent) {
    this("", parent);
  }

  public DialogAuthenticator(String username, JFrame parent) {
    this.passwordDialog = new JDialog(parent, true);
    Container pane = passwordDialog.getContentPane();
    pane.setLayout(new GridLayout(4, 1));

    JLabel userLabel = new JLabel("Username: ");
    JLabel passwordLabel = new JLabel("Password: ");
    pane.add(mainLabel);
    JPanel p2 = new JPanel();
    p2.add(userLabel);
    p2.add(usernameField);
    usernameField.setText(username);
    pane.add(p2);
    JPanel p3 = new JPanel();
    p3.add(passwordLabel);
    p3.add(passwordField);
    pane.add(p3);
    JPanel p4 = new JPanel();
    p4.add(okButton);
    p4.add(cancelButton);
    pane.add(p4);
    passwordDialog.pack();

    ActionListener al = new OKResponse();
    okButton.addActionListener(al);
    usernameField.addActionListener(al);
    passwordField.addActionListener(al);
    cancelButton.addActionListener(new CancelResponse());
  }

  private void show() {
    String prompt = this.getRequestingPrompt();
    if (prompt == null) {
      String site     = this.getRequestingSite().getHostName();
      String protocol = this.getRequestingProtocol();
      int    port     = this.getRequestingPort();
      if (site != null & protocol != null) {
        prompt = protocol + "://" + site;
        if (port > 0) prompt += ":" + port;
      } else {
        prompt = "";
      }
    }

    mainLabel.setText("Please enter username and password for "
        + prompt + ": ");
    passwordDialog.pack();
    passwordDialog.setVisible(true);
  }

  PasswordAuthentication response = null;

  class OKResponse implements ActionListener {
    @Override
    public void actionPerformed(ActionEvent e) {
      passwordDialog.setVisible(false);
      // The password is returned as an array of
      // chars for security reasons.
      char[] password = passwordField.getPassword();
      String username = usernameField.getText();
      // Erase the password in case this is used again.
      passwordField.setText("");
      response = new PasswordAuthentication(username, password);
    }
  }

  class CancelResponse implements ActionListener {
    @Override
    public void actionPerformed(ActionEvent e) {
      passwordDialog.setVisible(false);
      // Erase the password in case this is used again.
      passwordField.setText("");
      response = null;
    }
  }

  public PasswordAuthentication getPasswordAuthentication() {
    this.show();
    return this.response;
  }
}
```

Example 5-12. A program to download password-protected web pages

```java
import java.io.*;
import java.net.*;

public class SecureSourceViewer {

  public static void main (String args[]) {

    Authenticator.setDefault(new DialogAuthenticator());

    for (int i = 0; i < args.length; i++) {
      try {
        // Open the URL for reading
        URL u = new URL(args[i]);
        try (InputStream in = new BufferedInputStream(u.openStream())) {
          // chain the InputStream to a Reader
          Reader r = new InputStreamReader(in);
          int c;
          while ((c = r.read()) != -1) {
            System.out.print((char) c);
          }
        }
      } catch (MalformedURLException ex) {
        System.err.println(args[0] + " is not a parseable URL");
      } catch (IOException ex) {
        System.err.println(ex);
      }

      // print a blank line to separate pages
      System.out.println();
    }

    // Since we used the AWT, we have to explicitly exit.
    System.exit(0);
  }
}
```


# Chapter 6. HTTP

**==The Hypertext Transfer Protocol (HTTP) is a standard that defines how a web client talks to a server and how data is transferred from the server back to the client.==** Although HTTP is usually thought of as a means of transferring HTML files and the pictures embedded in them, HTTP is data format agnostic. It can be used to transfer TIFF pictures, Microsoft Word documents, Windows _.exe_ files, or anything else that can be represented in bytes.

## The Protocol

HTTP is the standard protocol for communication between web browsers and web servers. HTTP specifies how a client and server establish a connection, how the client requests data from the server, how the server responds to that request, and finally, how the connection is closed. **==HTTP connections use the TCP/IP protocol for data transfer. For each request from client to server, there is a sequence of four steps:**==

1. ==**The client opens a TCP connection to the server on port 80, by default; other ports may be specified in the URL.**==
2. ==**The client sends a message to the server requesting the resource at a specified path. The request includes a header, and optionally (depending on the nature of the request) a blank line followed by data for the request.**==
3. ==**The server sends a response to the client. The response begins with a response code, followed by a header full of metadata, a blank line, and the requested document or an error message.**==
4. ==**The server closes the connection.==**

This is the basic HTTP 1.0 procedure. In HTTP 1.1 and later, multiple requests and responses can be sent in series over a single TCP connection. That is, steps 2 and 3 can repeat multiple times in between steps 1 and 4. Furthermore, in HTTP 1.1, requests and responses can be sent in multiple chunks. This is more scalable.

Each request and response has the same basic form: a header line, an HTTP header containing metadata, a blank line, and then a message body. A typical client request looks something like this:

```http
GET /index.html HTTP/1.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.8; rv:20.0)
 Gecko/20100101 Firefox/20.0
Host: en.wikipedia.org
Connection: keep-alive
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
```

`GET` requests like this one do not contain a message body, so the request ends with a blank line.

The first line is called the _request line_, and includes a method, a path to a resource, and the version of HTTP. The method specifies the operation being requested. The `GET` method asks the server to return a representation of a resource. _/index.html_ is the path to the resource requested from the server. `HTTP/1.1` is the version of the protocol that the client understands.

Although the request line is all that is required, a client request usually includes other information as well in a header. Each line takes the following form:

```java
Keyword: Value
```

Keywords are not case sensitive. Values sometimes are and sometimes aren’t. Both keywords and values should be ASCII only. If a value is too long, you can add a space or tab to the beginning of the next line and continue it.

Lines in the header are terminated by a carriage-return linefeed pair.

The last keyword in this example is `Accept`, which tells the server the types of data the client can handle (though servers often ignore this).

`MIME` types are classified at two levels: a type and a subtype. The type shows very generally what kind of data is contained: is it a picture, text, or movie? The subtype identifies the specific type of data: GIF image, JPEG image, TIFF image. For example, HTML’s content type is `text/html`; the type is `text`, and the subtype is `html`. The content type for a JPEG image is `image/jpeg`; the type is `image`, and the subtype is `jpeg`. Eight top-level types have been defined:

- ==**text/* for human-readable words**==
- ==**image/* for pictures**==
- ==**model/* for 3D models such as VRML files**==
- ==**audio/* for sound**==
- ==**video/* for moving pictures, possibly including sound**==
- ==**application/* for binary data**==
- ==**message/* for protocol-specific envelopes such as email messages and HTTP responses**==
- ==**multipart/* for containers of multiple documents and resources==**

Each of these has many different subtypes.

Finally, the request is terminated with a blank line—that is, two carriage return/linefeed pairs, `\r\n\r\n`.

Once the server sees that blank line, it begins sending its response to the client over the same connection. The response begins with a status line, followed by a header describing the response using the same “name: value” syntax as the request header, a blank line, and the requested resource

```http
HTTP/1.1 200 OK
Date: Sun, 21 Apr 2013 15:12:46 GMT
Server: Apache
Connection: close
Content-Type: text/html; charset=ISO-8859-1
Content-length: 115

<html>
<head>
<title>
A Sample HTML file
</title>
</head>
<body>
The rest of the document goes here
</body>
</html>
```

The first line indicates the protocol the server is using (`HTTP/1.1`), followed by a response code. `200 OK` is the most common response code, indicating that the request was successful. The other header lines identify the date the request was made in the server’s time frame, the server software (Apache), a promise that the server will close the connection when it’s finished sending, the MIME media type, and the length of the document delivered

**==Regardless of version, a response code from 100 to 199 always indicates an informational response, 200 to 299 always indicates success, 300 to 399 always indicates redirection, 400 to 499 always indicates a client error, and 500 to 599 indicates a server error.==**

### Keep-Alive

HTTP 1.0 opens a new connection for each request. In practice, the time taken to open and close all the connections in a typical web session can outweigh the time taken to transmit the data, especially for sessions with many small documents. This is even more problematic for encrypted HTTPS connections using SSL or TLS, because the handshake to set up a secure socket is substantially more work than setting up a regular socket.

In HTTP 1.1 and later, the server doesn’t have to close the socket after it sends its response. It can leave it open and wait for a new request from the client on the same socket. Multiple requests and responses can be sent in series over a single TCP connection. However, the lockstep pattern of a client request followed by a server response remains the same.

A client indicates that it’s willing to reuse a socket by including a _Connection_ field in the HTTP request header with the value _Keep-Alive_:

```java
Connection: Keep-Alive
```

The `URL` class transparently supports HTTP Keep-Alive unless explicitly turned off. That is, it will reuse a socket if you connect to the same server again before the server has closed the connection. You can control Java’s use of HTTP Keep-Alive with several system properties:

- Set `http.keepAlive` to “true or false” to enable/disable HTTP Keep-Alive. (It is enabled by default.)
- Set `http.maxConnections` to the number of sockets you’re willing to hold open at one time. The default is 5.
- Set `http.keepAlive.remainingData` to true to let Java clean up after abandoned connections (Java 6 or later). It is false by default.
- Set `sun.net.http.errorstream.enableBuffering` to true to attempt to buffer the relatively short error streams from 400- and 500-level responses, so the connection can be freed up for reuse sooner. It is false by default.
- Set `sun.net.http.errorstream.bufferSize` to the number of bytes to use for buffering error streams. The default is 4,096 bytes.
- Set `sun.net.http.errorstream.timeout` to the number of milliseconds before timing out a read from the error stream. It is 300 milliseconds by default.

The defaults are reasonable, except that you probably do want to set `sun.net.http.errorstream.enableBuffering` to true unless you want to read the error streams from failed requests.

---

 **NOTE**

**HTTP 2.0, which is mostly based on the SPDY protocol invented at Google, further optimizes HTTP transfers through header compression, pipelining requests and responses, and asynchronous connection multiplexing. However, these optimizations are usually performed in a translation layer that shields application programmers from the details, so the code you write will still mostly follow the preceding steps 1–4. Java does not yet support HTTP 2.0; but when the capability is added, your programs shouldn’t need to change to take advantage of it, as long as you access HTTP servers via the `URL` and `URLConnection` classes.**

---

## HTTP Methods

**==Communication with an HTTP server follows a request-response pattern: one stateless request followed by one stateless response. Each HTTP request has two or three parts:**==

- ==**A start line containing the HTTP method and a path to the resource on which the method should be executed**==
- ==**A header of name-value fields that provide meta-information such as authentication credentials and preferred formats to be used in the request**==
- ==**A request body containing a representation of a resource (`POST` and `PUT` only)==**

There are four main HTTP methods, four verbs if you will, that identify the operations that can be performed:

- `GET`
- `POST`
- `PUT`
- `DELETE`

These four methods are not arbitrary. They have specific semantics that applications should adhere to. The `GET` method retrieves a representation of a resource. `GET` is side-effect free, and can be repeated without concern if it fails. Furthermore, its output is often cached, though that can be controlled with the right headers, as you’ll see shortly. In a properly architected system, `GET` requests can be bookmarked and prefetched without concern.

By contrast, a well-behaved browser or web spider will not `POST` to a link without explicit user action.

The `PUT` method uploads a representation of a resource to the server at a known URL. It is not side-effect free, but it is _idempotent_. That is, it can be repeated without concern if it fails. Putting the same document in the same place on the same server twice in a row leaves the server in the same state as only putting it once.

The `DELETE` method removes a resource from a specified URL. It, too, is not side-effect free, but is idempotent. If you aren’t sure whether a delete request succeeded—for instance, because the socket disconnected after you sent the request but before you received a response—just send the request again. Deleting the same resource twice is not a mistake.

The `POST` method is the most general method. It too uploads a representation of a resource to a server at a known URL, but it does not specify what the server is to do with the newly supplied resource.

In practice, `POST` is vastly overused on the Web today. Any safe operation that does not commit the user to anything should use `GET` rather than `POST`. Only operations that commit the user should use `POST`.

In addition to these four main HTTP methods, a few others are used in special circumstances. The most common such method is `HEAD`, which acts like a `GET` except it only returns the header for the resource, not the actual data. This is commonly used to check the modification date of a file, to see whether a copy stored in the local cache is still valid.

The other two that Java supports are `OPTIONS`, which lets the client ask the server what it can do with a specified resource; and `TRACE`, which echoes back the client request for debugging purposes, especially when proxy servers are misbehaving. Different servers recognize other nonstandard methods including `COPY` and `MOVE`, but Java does not send these.

The `URL` class described in the previous chapter uses `GET` to communicate with HTTP servers. The `URLConnection` class can use all four of these methods.

## The Request Body

The `GET` method retrieves a representation of a resource identified by a URL. The exact location of the resource you want to `GET` from a server is specified by the various parts of the path and query string. How different paths and query strings map to different resources is determined by the server. The `URL` class doesn’t really care about that. As long as it knows the URL, it can download from it.

`POST` and `PUT` are more complex. In these cases, the client supplies the representation of the resource, in addition to the path and the query string. T**==he representation of the resource is sent in the body of the request, after the header. That is, it sends these four items in order:**==

1. ==**A starter line including the method, path and query string, and HTTP version**==
2. ==**An HTTP header**==
3. ==**A blank line (two successive carriage return/linefeed pairs)**==
4. ==**The body==**

```http
POST /cgi-bin/register.pl HTTP 1.0
Date: Sun, 27 Apr 2013 12:32:36
Host: www.cafeaulait.org
Content-type: application/x-www-form-urlencoded
Content-length: 54

username=Elliotte+Harold&email=elharo%40ibiblio.org
```

In general, the body can contain arbitrary bytes. However, the HTTP header should include two fields that specify the nature of the body:

- A Content-length field that specifies how many bytes are in the body (54 in the preceding example)
- A Content-type field that specifies the MIME media type of the bytes (_application/x-www-form-urlencoded_ in the preceeding example).

The _application/x-www-form-urlencoded_ MIME type used in the preceding example is common because it’s how web browsers encode most form submissions. Thus it’s used by a lot of server-side programs that talk to browsers. However, it’s hardly the only possible type you can send in the body.

```html
PUT /blog/software-development/the-power-of-pomodoros/ HTTP/1.1
Host: elharo.com
User-Agent: AtomMaker/1.0
Authorization: Basic ZGFmZnk6c2VjZXJldA==
Content-Type: application/atom+xml;type=entry
Content-Length: 322

<?xml version="1.0"?>
<entry xmlns="http://www.w3.org/2005/Atom">
 <title>The Power of Pomodoros</title>
 <id>urn:uuid:101a41a6-722b-4d9b-8afb-ccfb01d77499</id>
 <updated>2013-02-22T19:40:52Z</updated>
 <author><name>Elliotte Harold</name></author>
 <content>I hadn’t paid much attention to Pomodoro...</content>
</entry>
```

## Cookies

Many websites use small strings of text known as _cookies_ to store persistent client-side state between connections. **==Cookies are passed from server to client and back again in the HTTP headers of requests and responses.==** Cookies can be used by a server to indicate session IDs, shopping cart contents, login credentials, user preferences, and more.

Usually the cookie values do not contain the data but merely point to it on the server.

Cookies are limited to non-whitespace ASCII text, and may not contain commas or semicolons.

To set a cookie in a browser, the server includes a `Set-Cookie` header line in the HTTP header. For example, this HTTP header sets the cookie “cart” to the value “ATVPDKIKX0DER”:

```http
HTTP/1.1 200 OK
Content-type: text/html
Set-Cookie: cart=ATVPDKIKX0DER
```

If a browser makes a second request to the same server, it will send the cookie back in a `Cookie` line in the HTTP request header like so:

```http
GET /index.html HTTP/1.1
Host: www.example.org
Cookie: cart=ATVPDKIKX0DER
Accept: text/html
```

As long as the server doesn’t reuse cookies, this enables it to track individual users and sessions across multiple, otherwise stateless, HTTP connections.

Servers can set more than one cookie.

```http
Set-Cookie:skin=noskin
Set-Cookie:ubid-main=176-5578236-9590213
Set-Cookie:session-token=Zg6afPNqbaMv2WmYFOv57zCU1O6Ktr
Set-Cookie:session-id-time=2082787201l
Set-Cookie:session-id=187-4969589-3049309
```

In addition to a simple name=value pair, cookies can have several attributes that control their scope including expiration date, path, domain, port, version, and security options. For example, this request sets a user cookie for the entire _foo.example.com_ domain:

```http
Set-Cookie: user=elharo;Domain=.foo.example.com
```

The browser will echo this cookie back not just to _www.foo.example.com_, but also to _lothar.foo.example.com_, _eliza.foo.example.com_, _enoch.foo.example.com_, and any other host somewhere in the _foo.example.com_ domain. However, a server can only set cookies for domains it immediately belongs to. _www.foo.example.com_ cannot set a cookie for _www.oreilly.com_, _example.com_, or _.com_, no matter how it sets the domain.

---

 **NOTE**

**Websites work around this restriction by embedding an image or other content hosted on one domain in a page hosted at a second domain. The cookies set by the embedded content, not the page itself, are called _third-party cookies_. Many users block all third-party cookies, and some web browsers are starting to block them by default for privacy reasons.**

---

Cookies are also scoped by path, so they’re returned for some directories on the server, but not all. The default scope is the original URL and any subdirectories. For instance, if a cookie is set for the URL _http://www.cafeconleche.org/XOM/_, the cookie also applies in _http://www.cafeconleche.org/XOM/apidocs/_, but not in _http://www.cafeconleche.org/slides/_ or _http://www.cafeconleche.org/_. However, the default scope can be changed using a `Path` attribute in the cookie.

```http
Set-Cookie: user=elharo; Path=/restricted
```

When requesting a document in the subtree _/restricted_ from the same server, the client echoes that cookie back. However, it does not use the cookie in other directories on the site.

A cookie can include both a domain and a path. For instance, this cookie applies in the _/restricted_ path on any servers within the _example.com_ domain:

```http
Set-Cookie: user=elharo;Path=/restricted;Domain=.example.com
```

**==The order of the different cookie attributes doesn’t matter, as long as they’re all separated by semicolons and the cookie’s own name and value come first. However, this isn’t true when the client is sending the cookie back to the server.==** In this case, the path must precede the domain, like so:

```http
Cookie: user=elharo; Path=/restricted;Domain=.foo.example.com
```

A cookie can be set to expire at a certain point in time by setting the `expires` attribute to a date in the form Wdy, DD-Mon-YYYY HH:MM:SS GMT. Weekday and month are given as three-letter abbreviations. The rest are numeric, padded with initial zeros if necessary. In the pattern language used by `java.text.SimpleDateFormat`, this is `E, dd-MMM-yyyy H:m:s z`.

```http
Set-Cookie: user=elharo; expires=Wed, 21-Dec-2015 15:23:00 GMT
```

The browser should remove this cookie from its cache after that date has passed.

The `Max-Age` attribute that sets the cookie to expire after a certain number of seconds have passed instead of at a specific moment. For instance, this cookie expires one hour (3,600 seconds) after it’s first set:

```http
Set-Cookie: user="elharo"; Max-Age=3600
```

Because cookies can contain sensitive information such as passwords and session keys, some cookie transactions should be secure. Most of the time this means using HTTPS instead of HTTP; but whatever it means, each cookie can have a secure attribute with no value, like so:

```http
Set-Cookie: key=etrogl7*;Domain=.foo.example.com; secure
```

Browsers are supposed to refuse to send such cookies over insecure channels.

For additional security against cookie-stealing attacks like XSRF, cookies can set the `HttpOnly` attribute. This tells the browser to only return the cookie via HTTP and HTTPS and specifically _not_ by JavaScript:

```http
Set-Cookie: key=etrogl7*;Domain=.foo.example.com; secure; httponly
```

Here’s a complete set of cookies sent by Amazon:

```http
Set-Cookie: skin=noskin; path=/; domain=.amazon.com;
 expires=Fri, 03-May-2013 21:46:43 GMT
Set-Cookie: ubid-main=176-5578236-9590213; path=/;
 domain=.amazon.com; expires=Tue, 01-Jan-2036 08:00:01 GMT
Set-Cookie: session-token=Zg6afPNqbaMv2WmYFOv57zCU1O6KtrMMdskcmllbZ
 cY4q6t0PrMywqO82PR6AgtfIJhtBABhomNUW2dITwuLfOZuhXILp7Toya+
 AvWaYJxpfY1lj4ci4cnJxiuUZTev1WV31p5bcwzRM1Cmn3QOCezNNqenhzZD8TZUnOL/9Ya;
 path=/; domain=.amazon.com; expires=Thu, 28-Apr-2033 21:46:43 GMT
Set-Cookie: session-id-time=2082787201l; path=/; domain=.amazon.com;
 expires=Tue, 01-Jan-2036 08:00:01 GMT
Set-Cookie: session-id=187-4969589-3049309; path=/; domain=.amazon.com;
 expires=Tue, 01-Jan-2036 08:00:01 GMT
```
### CookieManager

Java 5 includes an abstract `java.net.CookieHandler` class that defines an API for storing and retrieving cookies. However, it does not include an implementation of that abstract class, so it requires a lot of grunt work. Java 6 fleshes this out by adding a concrete `java.net.CookieManager` subclass of `CookieHandler` that you can use. However, it is not turned on by default. Before Java will store and return cookies, you need to enable it:

```java
CookieManager manager = new CookieManager();
CookieHandler.setDefault(manager);
```

If all you want is to receive cookies from sites and send them back to those sites, you’re done. That’s all there is to it. After installing a `CookieManager` with those two lines of code, Java will store any cookies sent by HTTP servers you connect to with the `URL` class, and will send the stored cookies back to those same servers in subsequent requests.

However, you may wish to be a bit more careful about whose cookies you accept. You can do this by specifying a `CookiePolicy`. **==Three policies are predefined:**==

- ==**`CookiePolicy.ACCEPT_ALL` All cookies allowed**==
- ==**`CookiePolicy.ACCEPT_NONE` No cookies allowed**==
- ==**`CookiePolicy.ACCEPT_ORIGINAL_SERVER` Only first party cookies allowed==**

```java
CookieManager manager = new CookieManager();
manager.setCookiePolicy(CookiePolicy.ACCEPT_ORIGINAL_SERVER);
CookieHandler.setDefault(manager);
```

That is, it will only accept cookies for the server that you’re talking to, not for any server on the Internet.

If you want more fine-grained control, for instance to allow cookies from some known domains but not others, you can implement the `CookiePolicy` interface yourself and override the `shouldAccept()` method:

```java
public boolean shouldAccept(URI uri, HttpCookie cookie)
```

Example 6-1. A cookie policy that blocks all .gov cookies but allows others

```java
import java.net.*;

public class NoGovernmentCookies implements CookiePolicy {

  @Override
  public boolean shouldAccept(URI uri, HttpCookie cookie) {
    if (uri.getAuthority().toLowerCase().endsWith(".gov")
        || cookie.getDomain().toLowerCase().endsWith(".gov")) {
      return false;
    }
    return true;
  }
}
```

### CookieStore

It is sometimes necessary to put and get cookies locally. For instance, when an application quits, it can save the cookie store to disk and load those cookies again when it next starts up. You can retrieve the store in which the `CookieManager` saves its cookies with the `getCookieStore()` method:

```java
CookieStore store = manager.getCookieStore();
```

The `CookieStore` class allows you to add, remove, and list cookies so you can control the cookies that are sent outside the normal flow of HTTP requests and responses:

```java
public void add(URI uri, HttpCookie cookie)
public List<HttpCookie> get(URI uri)
public List<HttpCookie> getCookies()
public List<URI> getURIs()
public boolean remove(URI uri, HttpCookie cookie)
public boolean removeAll()
```

Example 6-2. The ``HTTPCookie`` class

```java
package java.net;

public class HttpCookie implements Cloneable {
  public HttpCookie(String name, String value)

  public boolean hasExpired()
  public void setComment(String comment)
  public String getComment()
  public void setCommentURL(String url)
  public String getCommentURL()
  public void setDiscard(boolean discard)
  public boolean getDiscard()
  public void setPortlist(String ports)
  public String getPortlist()
  public void setDomain(String domain)
  public String getDomain()
  public void setMaxAge(long expiry)
  public long getMaxAge()
  public void setPath(String path)
  public String getPath()
  public void setSecure(boolean flag)
  public boolean getSecure()
  public String getName()
  public void setValue(String value)
  public String getValue()
  public int getVersion()
  public void setVersion(int v)

  public static boolean domainMatches(String domain, String host)
  public static List<HttpCookie> parse(String header)

  public String toString()
  public boolean equals(Object obj)
  public int hashCode()
  public Object clone()
}
```

#  Chapter 7. URLConnections

`URLConnection` is an abstract class that represents an active connection to a resource specified by a URL. The `URLConnection` class has two different but related purposes. **==First, it provides more control over the interaction with a server (especially an HTTP server) than the `URL` class.==** A `URLConnection` can inspect the header sent by the server and respond accordingly. It can set the header fields used in the client request. Finally, a `URLConnection` can send data back to a web server with `POST`, `PUT`, and other HTTP request methods.

**==Second, the `URLConnection` class is part of Java’s _protocol handler_ mechanism, which also includes the `URLStreamHandler` class. The idea behind protocol handlers is simple: they separate the details of processing a protocol from processing particular data types, providing user interfaces, and doing the other work that a monolithic web browser performs.==** The base `java.net.URLConnection` class is abstract; to implement a specific protocol, you write a subclass. These subclasses can be loaded at runtime by applications.

Only abstract `URLConnection` classes are present in the `java.net` package. The concrete subclasses are hidden inside the `sun.net` package hierarchy. Many of the methods and fields as well as the single constructor in the `URLConnection` class are _protected_. In other words, they can only be accessed by instances of the `URLConnection` class or its subclasses. It is rare to instantiate `URLConnection` objects directly in your source code; instead, the runtime environment creates these objects as needed, depending on the protocol in use. The class (which is unknown at compile time) is then instantiated using the `forName()` and `newInstance()` methods of the `java.lang.Class` class.

---

 **TIP**

**`URLConnection` does not have the best-designed API in the Java class library. One of several problems is that the `URLConnection` class is too closely tied to the HTTP protocol. For instance, it assumes that each file transferred is preceded by a MIME header or something very much like one. However, most classic protocols such as FTP and SMTP don’t use MIME headers.**

---

## Opening URLConnections

A program that uses the `URLConnection` class directly follows this basic sequence of steps:

1. ==**Construct a `URL` object.**==
2. ==**Invoke the `URL` object’s `openConnection()` method to retrieve a `URLConnection` object for that URL.**==
3. ==**Configure the `URLConnection`.**==
4. ==**Read the header fields.**==
5. ==**Get an input stream and read data.**==
6. ==**Get an output stream and write data.**==
7. ==**Close the connection.==**

You don’t always perform all these steps. For instance, if the default setup for a particular kind of URL is acceptable, you can skip step 3. If you only want the data from the server and don’t care about any metainformation, or if the protocol doesn’t provide any metainformation, you can skip step 4. If you only want to receive data from the server but not send data to the server, you’ll skip step 6. Depending on the protocol, steps 5 and 6 may be reversed or interlaced.

The single constructor for the `URLConnection` class is protected:

```java
protected URLConnection(URL url)
```

Consequently, unless you’re subclassing `URLConnection` to handle a new kind of URL (i.e., writing a protocol handler), you create one of these objects by invoking the `openConnection()` method of the `URL` class.

```java
try {
  URL u = new URL("http://www.overcomingbias.com/");
  URLConnection uc = u.openConnection();
  // read from the URL...
} catch (MalformedURLException ex) {
  System.err.println(ex);
} catch (IOException ex) {
  System.err.println(ex);
}
```

The `URLConnection` class is declared abstract. However, **==all but one of its methods are implemented. the single method that subclasses must implement is `connect()`==**, which makes a connection to a server and thus depends on the type of service (HTTP, FTP, and so on).

```java
public abstract void connect() throws IOException
```

When a `URLConnection` is first constructed, it is unconnected; that is, the local and remote host cannot send and receive data. There is no socket connecting the two hosts. The `connect()` method establishes a connection—normally using TCP sockets but possibly through some other mechanism—between the local and remote host so they can send and receive data. However, `getInputStream()`, `getContent()`, `getHeaderField()`, and other methods that require an open connection will call `connect()` if the connection isn’t yet open.

## Reading Data from a Server

The following is the minimal set of steps needed to retrieve data from a URL using a `URLConnection` object:

1. ==**Construct a `URL` object.**==
2. ==**Invoke the `URL` object’s `openConnection()` method to retrieve a `URLConnection` object for that URL.**==
3. ==**Invoke the `URLConnection`’s `getInputStream()` method.**==
4. ==**Read from the input stream using the usual stream API.==**

The `getInputStream()` method returns a generic `InputStream` that lets you read and parse the data that the server sends.

Example 7-1. Download a web page with a ``URLConnection``

```java
import java.io.*;
import java.net.*;

public class SourceViewer2 {

  public static void main (String[] args) {
    if  (args.length > 0) {
      try {
        // Open the URLConnection for reading
        URL u = new URL(args[0]);
        URLConnection uc = u.openConnection();
        try (InputStream raw = uc.getInputStream()) { // autoclose
          InputStream buffer = new BufferedInputStream(raw);
          // chain the InputStream to a Reader
          Reader reader = new InputStreamReader(buffer);
          int c;
          while ((c = reader.read()) != -1) {
            System.out.print((char) c);
          }
        }
      } catch (MalformedURLException ex) {
        System.err.println(args[0] + " is not a parseable URL");
      } catch (IOException ex) {
        System.err.println(ex);
      }
    }
  }
}
```

The differences between `URL` and `URLConnection` aren’t apparent with just a simple input stream as in this example. **==The biggest differences between the two classes are:**==

- ==**`URLConnection` provides access to the HTTP header.**==
- ==**`URLConnection` can configure the request parameters sent to the server.**==
- ==**`URLConnection` can write data to the server as well as read data from the server.==**

## Reading the Header

HTTP servers provide a substantial amount of information in the header that precedes each response.

```http
HTTP/1.1 301 Moved Permanently
Date: Sun, 21 Apr 2013 15:12:46 GMT
Server: Apache
Location: http://www.ibiblio.org/
Content-Length: 296
Connection: close
Content-Type: text/html; charset=iso-8859-1
```

In general, an HTTP header may include the content type of the requested document, the length of the document in bytes, the character set in which the content is encoded, the date and time, the date the content expires, and the date the content was last modified. However, the information depends on the server; some servers send all this information for each request, others send some information, and a few don’t send anything. The methods of this section allow you to query a `URLConnection` to find out what metadata the server has provided.

### Retrieving Specific Header Fields

The first six methods request specific, particularly common fields from the header. These are:

- Content-type
- Content-length
- Content-encoding
- Date
- Last-modified
- Expires

#### ``public String getContentType()``

The `getContentType()` method returns the MIME media type of the response body. It relies on the web server to send a valid content type. It throws no exceptions and returns `null` if the content type isn’t available. `text/html` will be the most common content type you’ll encounter when connecting to web servers.

If the content type is some form of text, this header may also contain a character set part identifying the document’s character encoding.

```http
Content-type: text/html; charset=UTF-8
```


Example 7-2. Download a web page with the correct character set

```java
import java.io.*;
import java.net.*;

public class EncodingAwareSourceViewer {

  public static void main (String[] args) {
    for (int i = 0; i < args.length; i++) {
      try {
        // set default encoding
        String encoding = "ISO-8859-1";
        URL u = new URL(args[i]);
        URLConnection uc = u.openConnection();
        String contentType = uc.getContentType();
        int encodingStart = contentType.indexOf("charset=");
        if (encodingStart != -1) {
            encoding = contentType.substring(encodingStart + 8);
        }
        InputStream in = new BufferedInputStream(uc.getInputStream());
        Reader r = new InputStreamReader(in, encoding);
        int c;
        while ((c = r.read()) != -1) {
          System.out.print((char) c);
        }
        r.close();
      } catch (MalformedURLException ex) {
        System.err.println(args[0] + " is not a parseable URL");
      } catch (UnsupportedEncodingException ex) {
        System.err.println(
            "Server sent an encoding Java does not support: " + ex.getMessage());
      } catch (IOException ex) {
        System.err.println(ex);
      }
    }
  }
}
```

#### ``public int getContentLength()``

The `getContentLength()` method tells you how many bytes there are in the content. If there is no Content-length header, `getContentLength()` returns –1. The method throws no exceptions. It is used when you need to know exactly how many bytes to read or when you need to create a buffer large enough to hold the data in advance.

As networks get faster and files get bigger, it is actually possible to find resources whose size exceeds the maximum `int` value (about 2.1 billion bytes). In this case, `getContentLength()` returns –1. Java 7 adds a `getContentLengthLong()` method that works just like `getContentLength()` except that it returns a `long` instead of an `int` and thus can handle much larger resources:

```java
public long getContentLengthLong // Java 7
```

HTTP servers don’t always close the connection exactly where the data is finished; therefore, you don’t know when to stop reading. To download a binary file, it is more reliable to use a `URLConnection`’s `getContentLength()` method to find the file’s length, then read exactly the number of bytes indicated.

Example 7-3. Downloading a binary file from a website and saving it to disk

```java
import java.io.*;
import java.net.*;

public class BinarySaver {

  public static void main (String[] args) {
    for (int i = 0; i < args.length; i++) {
      try {
        URL root = new URL(args[i]);
        saveBinaryFile(root);
      } catch (MalformedURLException ex) {
        System.err.println(args[i] + " is not URL I understand.");
      } catch (IOException ex) {
        System.err.println(ex);
      }
    }
  }

  public static void saveBinaryFile(URL u) throws IOException {
    URLConnection uc = u.openConnection();
    String contentType = uc.getContentType();
    int contentLength = uc.getContentLength();
    if (contentType.startsWith("text/") || contentLength == -1 ) {
      throw new IOException("This is not a binary file.");
    }

    try (InputStream raw = uc.getInputStream()) {
      InputStream in  = new BufferedInputStream(raw);
      byte[] data = new byte[contentLength];
      int offset = 0;
      while (offset < contentLength) {
         int bytesRead = in.read(data, offset, data.length - offset);
         if (bytesRead == -1) break;
         offset += bytesRead;
      }

      if (offset != contentLength) {
        throw new IOException("Only read " + offset
            + " bytes; Expected " + contentLength + " bytes");
      }
      String filename = u.getFile();
      filename = filename.substring(filename.lastIndexOf('/') + 1);
      try (FileOutputStream fout = new FileOutputStream(filename)) {
        fout.write(data);
        fout.flush();
      }
    }
  }
}
```

`saveBinaryFile()` opens a `URLConnection` `uc` to the `URL`. It puts the type into the variable `contentType` and the content length into the variable `contentLength`. Next, an `if` statement checks whether the content type is `text` or the Content-length field is missing or invalid (`contentLength == -1`). If either of these is `true`, an `IOException` is thrown. If these checks are both `false`, you have a binary file of known length: that’s what you want.

Now that you have a genuine binary file on your hands, you prepare to read it into an array of bytes called `data`. `data` is initialized to the number of bytes required to hold the binary object, `contentLength`. Ideally, you would like to fill `data` with a single call to `read()` but you probably won’t get all the bytes at once, so the read is placed in a loop. The number of bytes read up to this point is accumulated into the `offset` variable, which also keeps track of the location in the `data` array at which to start placing the data retrieved by the next call to `read()`. The loop continues until `offset` equals or exceeds `contentLength`; that is, the array has been filled with the expected number of bytes. You also break out of the `while` loop if `read()` returns –1, indicating an unexpected end of stream. The `offset` variable now contains the total number of bytes read, which should be equal to the content length. If they are not equal, an error has occurred, so `saveBinaryFile()` throws an `IOException`. This is the general procedure for reading binary files from HTTP connections.

#### ``public String getContentEncoding()``

The `getContentEncoding()` method returns a `String` that tells you how the content is encoded. If the content is sent unencoded (as is commonly the case with HTTP servers), this method returns `null`. It throws no exceptions. The most commonly used content encoding on the Web is probably x-gzip, which can be straightforwardly decoded using a `java.util.zip.GZipInputStream`.

---
 **TIP**

**The content encoding is not the same as the character encoding. The character encoding is determined by the Content-type header or information internal to the document, and specifies how characters are encoded in bytes. Content encoding specifies how the bytes are encoded in other bytes.**

---

#### ``public long getDate()``

The `getDate()` method returns a `long` that tells you when the document was sent, in milliseconds since midnight, Greenwich Mean Time (GMT), January 1, 1970. You can convert it to a `java.util.Date`.

```java
Date documentSent = new Date(uc.getDate());
```

#### ``public long getExpiration()``

Some documents have server-based expiration dates that indicate when the document should be deleted from the cache and reloaded from the server. `getExpiration()` is very similar to `getDate()`, differing only in how the return value is interpreted. It returns a `long` indicating the number of milliseconds after 12:00 A.M., GMT, January 1, 1970, at which the document expires. If the HTTP header does not include an Expiration field, `getExpiration()` returns 0, which means that the document does not expire and can remain in the cache indefinitely.

#### ``public long getLastModified()``

The final date method, `getLastModified()`, returns the date on which the document was last modified. Again, the date is given as the number of milliseconds since midnight, GMT, January 1, 1970. If the HTTP header does not include a Last-modified field (and many don’t), this method returns 0.

Example 7-4. Return the header

```java
import java.io.*;
import java.net.*;
import java.util.*;

public class HeaderViewer {

  public static void main(String[] args) {
    for (int i = 0; i < args.length; i++) {
      try {
        URL u = new URL(args[0]);
        URLConnection uc = u.openConnection();
        System.out.println("Content-type: " + uc.getContentType());
        if (uc.getContentEncoding() != null) {
          System.out.println("Content-encoding: "
              + uc.getContentEncoding());
        }
        if (uc.getDate() != 0) {
          System.out.println("Date: " + new Date(uc.getDate()));
        }
        if (uc.getLastModified() != 0) {
          System.out.println("Last modified: "
              + new Date(uc.getLastModified()));
        }
        if (uc.getExpiration() != 0) {
          System.out.println("Expiration date: "
              + new Date(uc.getExpiration()));
        }
        if (uc.getContentLength() != -1) {
          System.out.println("Content-length: " + uc.getContentLength());
        }
      } catch (MalformedURLException ex) {
        System.err.println(args[i] + " is not a URL I understand");
      } catch (IOException ex) {
        System.err.println(ex);
      }
      System.out.println();
    }
  }
}
```

Here’s the result when used to look at _http://www.oreilly.com_:

```http
% **`java HeaderViewer http://www.oreilly.com`**
Content-type: text/html; charset=utf-8
Date: Fri May 31 18:08:09 EDT 2013
Last modified: Fri May 31 17:04:14 EDT 2013
Expiration date: Fri May 31 22:08:09 EDT 2013
Content-length: 83273
```

### Retrieving Arbitrary Header Fields

The last six methods requested specific fields from the header, but there’s no theoretical limit to the number of header fields a message can contain. If the requested header is found, it is returned. Otherwise, the method returns `null`.

#### ``public String getHeaderField(String name)``

The `getHeaderField()` method returns the value of a named header field. The name of the header is not case sensitive and does not include a closing colon.

```java
String contentType = uc.getHeaderField("content-type");
String contentEncoding = uc.getHeaderField("content-encoding"));

String data = uc.getHeaderField("date");
String expires = uc.getHeaderField("expires");
String contentLength = uc.getHeaderField("Content-length");
```

**==Do not assume the value returned by `getHeaderField()` is valid. You must check to make sure it is nonnull.==**
#### ``public String getHeaderFieldKey(int n)``

This method returns the key (i.e., the field name) of the _n_th header field (e.g., `Content-length` or `Server`). The request method is header zero and has a null key. The first header is one.

```java
String header6 = uc.getHeaderFieldKey(6);
```

#### ``public String getHeaderField(int n)``

This method returns the value of the _n_th header field. In HTTP, the starter line containing the request method and path is header field zero and the first actual header is one.

Example 7-5. Print the entire HTTP header
```java
import java.io.*;
import java.net.*;

public class AllHeaders {

  public static void main(String[] args) {
    for (int i = 0; i < args.length; i++) {
      try {
        URL u = new URL(args[i]);
        URLConnection uc = u.openConnection();
        for (int j = 1; ; j++) {
          String header = uc.getHeaderField(j);
          if (header == null) break;
          System.out.println(uc.getHeaderFieldKey(j) + ": " + header);
        }
      } catch (MalformedURLException ex) {
        System.err.println(args[i] + " is not a URL I understand.");
      } catch (IOException ex) {
        System.err.println(ex);
      }
      System.out.println();
    }
  }
}
```

```http
% java AllHeaders http://www.oreilly.com
Date: Sat, 04 May 2013 11:28:26 GMT
Server: Apache
Last-Modified: Sat, 04 May 2013 07:35:04 GMT
Accept-Ranges: bytes
Content-Length: 80366
Content-Type: text/html; charset=utf-8
Cache-Control: max-age=14400
Expires: Sat, 04 May 2013 15:28:26 GMT
Vary: Accept-Encoding
Keep-Alive: timeout=3, max=100
Connection: Keep-Alive
```

Besides the headers with named getter methods, this server also provides Server, Accept-Ranges, Cache-control, Vary, Keep-Alive, and Connection headers. Other servers may have different sets of headers.

#### ``public long getHeaderFieldDate(String name, long default)``

This method first retrieves the header field specified by the `name` argument and tries to convert the string to a `long` that specifies the milliseconds since midnight, January 1, 1970, GMT. `getHeaderFieldDate()` can be used to retrieve a header field that represents a date (e.g., the Expires, Date, or Last-modified headers). To convert the string to an integer, `getHeaderFieldDate()` uses the `parseDate()` method of `java.util.Date`. The `parseDate()` method does a decent job of understanding and converting most common date formats, but it can be stumped—for instance, if you ask for a header field that contains something other than a date. If `parseDate()` doesn’t understand the date or if `getHeaderFieldDate()` is unable to find the requested header field, `getHeaderFieldDate()` returns the `default` argument.

```java
Date expires = new Date(uc.getHeaderFieldDate("expires", 0));
long lastModified = uc.getHeaderFieldDate("last-modified", 0);
Date now = new Date(uc.getHeaderFieldDate("date", 0));
```

#### ``public int getHeaderFieldInt(String name, int default)``

This method retrieves the value of the header field `name` and tries to convert it to an `int`. If it fails, either because it can’t find the requested header field or because that field does not contain a recognizable integer, `getHeaderFieldInt()` returns the `default` argument. This method is often used to retrieve the `Content-length` field.

```java
int contentLength = uc.getHeaderFieldInt("content-length", -1);
```

## Caches

Web browsers have been caching pages and images for years. If a logo is repeated on every page of a site, the browser normally loads it from the remote server only once, stores it in its cache, and reloads it from the cache whenever it’s needed rather than requesting it from the remote server every time the logo is encountered.

By default, the assumption is that a page accessed with `GET` over HTTP can and should be cached. A page accessed with HTTPS or `POST` usually shouldn’t be. However, HTTP headers can adjust this:

- ==**An Expires header (primarily for HTTP 1.0) indicates that it’s OK to cache this representation until the specified time.**==
- ==**The Cache-control header (HTTP 1.1) offers fine-grained cache policies:**==
    
    - ==**``max-age=[_`seconds`_]``: Number of seconds from now before the cached entry should expire**==
    - ==**``s-maxage=[_`seconds`_]``: Number of seconds from now before the cached entry should expire from a shared cache. Private caches can store the entry for longer.**==
    - ==**`public`: OK to cache an authenticated response. Otherwise authenticated responses are not cached.**==
    - ==**`private`: Only single user caches should store the response; shared caches should not.**==
    - ==**`no-cache`: Not quite what it sounds like. The entry may still be cached, but the client should reverify the state of the resource with an ETag or Last-modified header on each access.**==
    - ==**`no-store`: Do not cache the entry no matter what.**==
    
    ==**Cache-control overrides Expires if both are present. A server can send multiple Cache-control headers in a single header as long as they don’t conflict.**==
    
- ==**The Last-modified header is the date when the resource was last changed. A client can use a `HEAD` request to check this and only come back for a full `GET` if its local cached copy is older than the Last-modified date.**==
- ==**The ETag header (HTTP 1.1) is a unique identifier for the resource that changes when the resource does. A client can use a `HEAD` request to check this and only come back for a full `GET` if its local cached copy has a different ETag.==**

```http
HTTP/1.1 200 OK
Date: Sun, 21 Apr 2013 15:12:46 GMT
Server: Apache
Connection: close
Content-Type: text/html; charset=ISO-8859-1
Cache-control: max-age=604800
Expires: Sun, 28 Apr 2013 15:12:46 GMT
Last-modified: Sat, 20 Apr 2013 09:55:04 GMT
ETag: "67099097696afcf1b67e"
```

Example 7-6. How to inspect a Cache-control header

```java
import java.util.Date;
import java.util.Locale;


public class CacheControl {

  private Date maxAge = null;
  private Date sMaxAge = null;
  private boolean mustRevalidate = false;
  private boolean noCache = false;
  private boolean noStore = false;
  private boolean proxyRevalidate = false;
  private boolean publicCache = false;
  private boolean privateCache = false;

  public CacheControl(String s) {
    if (s == null || !s.contains(":")) {
      return; // default policy
    }

    String value = s.split(":")[1].trim();
    String[] components = value.split(",");

    Date now = new Date();
    for (String component : components) {
      try {
        component = component.trim().toLowerCase(Locale.US);
        if (component.startsWith("max-age=")) {
          int secondsInTheFuture = Integer.parseInt(component.substring(8));
          maxAge = new Date(now.getTime() + 1000 * secondsInTheFuture);
        } else if (component.startsWith("s-maxage=")) {
          int secondsInTheFuture = Integer.parseInt(component.substring(8));
          sMaxAge = new Date(now.getTime() + 1000 * secondsInTheFuture);
        } else if (component.equals("must-revalidate")) {
          mustRevalidate = true;
        } else if (component.equals("proxy-revalidate")) {
          proxyRevalidate = true;
        } else if (component.equals("no-cache")) {
          noCache = true;
        } else if (component.equals("public")) {
          publicCache = true;
        } else if (component.equals("private")) {
          privateCache = true;
        }
      } catch (RuntimeException ex) {
        continue;
      }
    }
  }

  public Date getMaxAge() {
    return maxAge;
  }

  public Date getSharedMaxAge() {
    return sMaxAge;
  }

  public boolean mustRevalidate() {
    return mustRevalidate;
  }

  public boolean proxyRevalidate() {
    return proxyRevalidate;
  }

  public boolean noStore() {
    return noStore;
  }

  public boolean noCache() {
    return noCache;
  }

  public boolean publicCache() {
    return publicCache;
  }

  public boolean privateCache() {
    return privateCache;
  }
}
```

A client can take advantage of this information:

- If a representation of the resource is available in the local cache, and its expiry date has not arrived, just use it. Don’t even bother talking to the server.
- If a representation of the resource is available in the local cache, but the expiry date has arrived, check the server with `HEAD` to see if the resource has changed before performing a full `GET`.

### Web Cache for Java

By default, Java does not cache anything. To install a system-wide cache of the `URL` class will use, you need the following:

- ==**A concrete subclass of `ResponseCache`**==
- ==**A concrete subclass of `CacheRequest`**==
- ==**A concrete subclass of `CacheResponse`==**

You install your subclass of `ResponseCache` that works with your subclass of `CacheRequest` and `CacheResponse` by passing it to the static method `ResponseCache.setDefault()`. This installs your cache object as the system default. A Java virtual machine can only support a single shared cache.

Once a cache is installed whenever the system tries to load a new URL, it will first look for it in the cache. If the cache returns the desired content, the `URLConnection` won’t need to connect to the remote server. However, if the requested data is not in the cache, the protocol handler will download it. After it’s done so, it will put its response into the cache so the content is more quickly available the next time that URL is loaded.

Two abstract methods in the `ResponseCache` class store and retrieve data from the system’s single cache:

```java
public abstract CacheResponse get(URI uri, String requestMethod,
    Map<String, List<String>> requestHeaders) throws IOException
public abstract CacheRequest put(URI uri, URLConnection connection)
    throws IOException
```

Example 7-7. The ``CacheRequest`` class

```java
package java.net;

public abstract class CacheRequest {
  public abstract OutputStream getBody() throws IOException;
  public abstract void abort();
}
```

Example 7-8. A concrete ``CacheRequest`` subclass

```java
import java.io.*;
import java.net.*;

public class SimpleCacheRequest extends CacheRequest {

  private ByteArrayOutputStream out = new ByteArrayOutputStream();

  @Override
  public OutputStream getBody() throws IOException {
    return out;
  }

  @Override
  public void abort() {
    out.reset();
  }

  public byte[] getData() {
    if (out.size() == 0) return null;
    else return out.toByteArray();
  }
}
```

Example 7-9. The ``CacheResponse`` class

```java
public abstract class CacheResponse {
  public abstract Map<String, List<String>> getHeaders() throws IOException;
  public abstract InputStream getBody() throws IOException;
}
```

Example 7-10. A concrete ``CacheResponse`` subclass

```java
import java.io.*;
import java.net.*;
import java.util.*;

public class SimpleCacheResponse extends CacheResponse {

  private final Map<String, List<String>> headers;
  private final SimpleCacheRequest request;
  private final Date expires;
  private final CacheControl control;

  public SimpleCacheResponse(
      SimpleCacheRequest request, URLConnection uc, CacheControl control)
      throws IOException {

    this.request = request;
    this.control = control;
    this.expires = new Date(uc.getExpiration());
    this.headers = Collections.unmodifiableMap(uc.getHeaderFields());
  }

  @Override
  public InputStream getBody() {
    return new ByteArrayInputStream(request.getData());
  }

  @Override
  public Map<String, List<String>> getHeaders()
      throws IOException {
      return headers;
  }

  public CacheControl getControl() {
    return control;
  }

  public boolean isExpired() {
    Date now = new Date();
    if (control.getMaxAge().before(now)) return true;
    else if (expires != null && control.getMaxAge() != null) {
      return expires.before(now);
    } else {
      return false;
    }
  }
}
```

Finally, you need a simple `ResponseCache` subclass that stores and retrieves the cached values as requested while paying attention to the original Cache-control header.

Example 7-11. An in-memory ``ResponseCache``

```java
import java.io.*;
import java.net.*;
import java.util.*;
import java.util.concurrent.*;

public class MemoryCache extends ResponseCache {

  private final Map<URI, SimpleCacheResponse> responses
      = new ConcurrentHashMap<URI, SimpleCacheResponse>();
  private final int maxEntries;

  public MemoryCache() {
    this(100);
  }

  public MemoryCache(int maxEntries) {
    this.maxEntries = maxEntries;
  }

  @Override
  public CacheRequest put(URI uri, URLConnection conn)
      throws IOException {

     if (responses.size() >= maxEntries) return null;

     CacheControl control = new CacheControl(conn.getHeaderField("Cache-Control"));
     if (control.noStore()) {
       return null;
     } else if (!conn.getHeaderField(0).startsWith("GET ")) {
       // only cache GET
       return null;
     }

     SimpleCacheRequest request = new SimpleCacheRequest();
     SimpleCacheResponse response = new SimpleCacheResponse(request, conn, control);

     responses.put(uri, response);
     return request;
  }

  @Override
  public CacheResponse get(URI uri, String requestMethod,
      Map<String, List<String>> requestHeaders)
      throws IOException {

     if ("GET".equals(requestMethod)) {
       SimpleCacheResponse response = responses.get(uri);
       // check expiration date
       if (response != null && response.isExpired()) {
         responses.remove(response);
         response = null;
       }
       return response;
     } else {
       return null;
     }
  }
}
```

Java only allows one URL cache at a time. To install or change the cache, use the static `ResponseCache.setDefault()` and `ResponseCache.getDefault()` methods:

```java
public static ResponseCache getDefault()
public static void setDefault(ResponseCache responseCache)
```

These set the single cache used by all programs running within the same Java virtual machine.

```java
ResponseCache.setDefault(new MemoryCache());
```

Each retrieved resource stays in the `HashMap` until it expires. This example waits for an expired document to be requested again before it deletes it from the cache. A more sophisticated implementation could use a low-priority thread to scan for expired documents and remove them to make way for others. Instead of or in addition to this, an implementation might cache the representations in a queue and remove the oldest documents or those closest to their expiration date as necessary to make room for new ones. An even more sophisticated implementation could track how often each document in the store was accessed and expunge only the oldest and least-used documents.

You could implement a cache on top of the filesystem instead of on top of the Java Collections API. You could also store the cache in a database, and you could do a lot of less-common things as well. For instance, you could redirect requests for certain URLs to a local server rather than a remote server halfway around the world, in essence using a local web server as the cache. Or a `ResponseCache` could load a fixed set of files at launch time and then only serve those out of memory. This might be useful for a server that processes many different SOAP requests, all of which adhere to a few common schemas that can be stored in the cache. The abstract `ResponseCache` class is flexible enough to support all of these and other usage patterns.

## Configuring the Connection

The `URLConnection` class has seven protected instance fields that define exactly how the client makes the request to the server. These are:

```java
protected URL     url;
protected boolean doInput = true;
protected boolean doOutput = false;
protected boolean allowUserInteraction = defaultAllowUserInteraction;
protected boolean useCaches = defaultUseCaches;
protected long    ifModifiedSince = 0;
protected boolean connected = false;
```

Because these fields are all protected, their values are accessed and modified via obviously named setter and getter methods:

```java
public URL     getURL()
public void    setDoInput(boolean doInput)
public boolean getDoInput()
public void    setDoOutput(boolean doOutput)
public boolean getDoOutput()
public void    setAllowUserInteraction(boolean allowUserInteraction)
public boolean getAllowUserInteraction()
public void    setUseCaches(boolean useCaches)
public boolean getUseCaches()
public void    setIfModifiedSince(long ifModifiedSince)
public long    getIfModifiedSince()
```

can modify these fields only before the `URLConnection` is connected (before you try to read content or headers from the connection). Most of the methods that set fields throw an `IllegalStateException` if they are called while the connection is open. **==In general, you can set the properties of a `URLConnection` object only before the connection is opened.==**

There are also some getter and setter methods that define the default behavior for all instances of `URLConnection`. These are:

```java
public boolean            getDefaultUseCaches()
public void               setDefaultUseCaches(boolean defaultUseCaches)
public static void        setDefaultAllowUserInteraction(
   boolean defaultAllowUserInteraction)
public static boolean     getDefaultAllowUserInteraction()
public static FileNameMap getFileNameMap()
public static void        setFileNameMap(FileNameMap map)
```

Unlike the instance methods, these methods can be invoked at any time. The new defaults will apply only to `URLConnection` objects constructed after the new default values are set.

### protected URL url

The `url` field specifies the URL that this `URLConnection` connects to. The constructor sets it when the `URLConnection` is created and it should not change thereafter. You can retrieve the value by calling the `getURL()` method.

Example 7-12. Print the URL of a ``URLConnection`` to _http://www.oreilly.com/_

```java
import java.io.*;
import java.net.*;

public class URLPrinter {

  public static void main(String[] args) {
    try {
      URL u = new URL("http://www.oreilly.com/");
      URLConnection uc = u.openConnection();
      System.out.println(uc.getURL());
    } catch (IOException ex) {
      System.err.println(ex);
    }
  }
}
```

### ``protected boolean connected``

The boolean field `connected` is `true` if the connection is open and `false` if it’s closed. Because the connection has not yet been opened when a new `URLConnection` object is created, its initial value is `false`. This variable can be accessed only by instances of `java.net.URLConnection` and its subclasses.

**==There are no methods that directly read or change the value of `connected`. However, any method that causes the `URLConnection` to connect should set this variable to true, including `connect()`, `getInputStream()`, and `getOutputStream()`. Any method that causes the `URLConnection` to disconnect should set this field to false.==** There are no such methods in `java.net.URLConnection`, but some of its subclasses, such as `java.net.HttpURLConnection`, have `disconnect()` methods.

If you subclass `URLConnection` to write a protocol handler, you are responsible for setting `connected` to `true` when you are connected and resetting it to `false` when the connection closes. Many methods in `java.net.URLConnection` read this variable to determine what they can do. If it’s set incorrectly, your program will have severe bugs that are not easy to diagnose.

### ``protected boolean allowUserInteraction``

Some `URLConnection`s need to interact with a user. This variable is protected, but the public `getAllowUserInteraction()` method can read its value and the public `setAllowUserInteraction()` method can change it:

```java
public void    setAllowUserInteraction(boolean allowUserInteraction)
public boolean getAllowUserInteraction()
```

The value `true` indicates that user interaction is allowed; `false` indicates that there is no user interaction. The value may be read at any time but may be set only before the `URLConnection` is connected. Calling `setAllowUserInteraction()` when the `URLConnection` is connected throws an `IllegalStateException`.

```java
URL u = new URL("http://www.example.com/passwordProtectedPage.html");
URLConnection uc = u.openConnection();
uc.setAllowUserInteraction(true);
InputStream in = uc.getInputStream();
```

The static methods `getDefaultAllowUserInteraction()` and `setDefaultAllowUserInteraction()` determine the default behavior for `URLConnection` objects that have not set `allowUserInteraction` explicitly. Because the `allowUserInteraction` field is `static` (i.e., a class variable instead of an instance variable), setting it changes the default behavior for all instances of the `URLConnection` class that are created after `setDefaultAllowUserInteraction()` is called.

For instance, the following code fragment checks to see whether user interaction is allowed by default with `getDefaultAllowUserInteraction()`. If user interaction is not allowed by default, the code uses `setDefaultAllowUserInteraction()` to make allowing user interaction the default behavior:

```java
if (!URLConnection.getDefaultAllowUserInteraction()) {
  URLConnection.setDefaultAllowUserInteraction(true);
}
```

### ``protected boolean doInput``
A `URLConnection` can be used for reading from a server, writing to a server, or both. The protected boolean field `doInput` is `true` if the `URLConnection` can be used for reading, `false` if it cannot be. The default is `true`. To access this protected variable, use the public `getDoInput()` and `setDoInput()` methods:

```java
public void    setDoInput(boolean doInput)
public boolean getDoInput()
```

```java
try {
  URL u = new URL("http://www.oreilly.com");
  URLConnection uc = u.openConnection();
  if (!uc.getDoInput()) {
    uc.setDoInput(true);
  }
  // read from the connection...
} catch (IOException ex) {
  System.err.println(ex);
}
```

### ``protected boolean doOutput``

Programs can use a `URLConnection` to send output back to the server. The protected boolean field `doOutput` is `true` if the `URLConnection` can be used for writing, `false` if it cannot be; it is `false` by default. To access this protected variable, use the `getDoOutput()` and `setDoOutput()` methods:

```java
public void    setDoOutput(boolean dooutput)
public boolean getDoOutput()
```

```java
try {
  URL u = new URL("http://www.oreilly.com");
  URLConnection uc = u.openConnection();
  if (!uc.getDoOutput()) {
    uc.setDoOutput(true);
  }
  // write to the connection...
} catch (IOException ex) {
  System.err.println(ex);
}
```

### ``protected boolean ifModifiedSince``

Many clients, especially web browsers and proxies, keep caches of previously retrieved documents. If the user asks for the same document again, it can be retrieved from the cache. However, it may have changed on the server since it was last retrieved. The only way to tell is to ask the server. Clients can include an If-Modified-Since in the client request HTTP header. This header includes a date and time. If the document has changed since that time, the server should send it. Otherwise, it should not. Typically, this time is the last time the client fetched the document.

```http
GET / HTTP/1.1
Host: login.ibiblio.org:56452
Accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
Connection: close
If-Modified-Since: Fri, 31 Oct 2014 19:22:07 GMT
```

The client then loads the document from its cache. Not all web servers respect the If-Modified-Since field. Some will send the document whether it’s changed or not.

The `ifModifiedSince` field in the `URLConnection` class specifies the date (in milliseconds since midnight, Greenwich Mean Time, January 1, 1970), which will be placed in the If-Modified-Since header field. Because `ifModifiedSince` is `protected`, programs should call the `getIfModifiedSince()` and `setIfModifiedSince()` methods to read or modify it:

```java
public long getIfModifiedSince()
public void setIfModifiedSince(long ifModifiedSince)
```

Example 7-13. Set ``ifModifiedSince`` to 24 hours prior to now

```java
import java.io.*;
import java.net.*;
import java.util.*;

public class Last24 {

  public static void main (String[] args) {

    // Initialize a Date object with the current date and time
    Date today = new Date();
    long millisecondsPerDay = 24 * 60 * 60 * 1000;

    for (int i = 0; i < args.length; i++) {
      try {
        URL u = new URL(args[i]);
        URLConnection uc = u.openConnection();
        System.out.println("Original if modified since: "
            + new Date(uc.getIfModifiedSince()));
        uc.setIfModifiedSince((new Date(today.getTime()
            - millisecondsPerDay)).getTime());
        System.out.println("Will retrieve file if it's modified since "
            + new Date(uc.getIfModifiedSince()));
        try (InputStream in = new BufferedInputStream(uc.getInputStream())) {
          Reader r = new InputStreamReader(in);
          int c;
          while ((c = r.read()) != -1) {
            System.out.print((char) c);
          }
          System.out.println();
        }
      } catch (IOException ex) {
        System.err.println(ex);
      }
    }
  }
}
```

### ``protected boolean useCaches``

Some clients, notably web browsers, can retrieve a document from a local cache, rather than retrieving it from a server. Applets may have access to the browser’s cache. Standalone applications can use the `java.net.ResponseCache` class. The `useCaches` variable determines whether a cache will be used if it’s available. The default value is `true`, meaning that the cache will be used; `false` means the cache won’t be used. Because `useCaches` is `protected`, programs access it using the `getUseCaches()` and `setUseCaches()` methods:

```java
public void    setUseCaches(boolean useCaches)
public boolean getUseCaches()
```

This code fragment disables caching to ensure that the most recent version of the document is retrieved by setting `useCaches` to `false`:

```java
try {
  URL u = new URL("http://www.sourcebot.com/");
  URLConnection uc = u.openConnection();
  uc.setUseCaches(false);
  // read the document...
} catch (IOException ex) {
  System.err.println(ex);
}
```

Two methods define the initial value of the `useCaches` field, `getDefaultUseCaches()` and `setDefaultUseCaches()`:

```java
public void    setDefaultUseCaches(boolean useCaches)
public boolean getDefaultUseCaches()
```

Although nonstatic, these methods do set and get a static field that determines the default behavior for all instances of the `URLConnection` class created after the change. The next code fragment disables caching by default; after this code runs, `URLConnection`s that want caching must enable it explicitly using `setUseCaches(true)`:

```java
if (uc.getDefaultUseCaches()) {
  uc.setDefaultUseCaches(false);
}
```

### Timeouts

Four methods query and modify the timeout values for connections; that is, how long the underlying socket will wait for a response from the remote end before throwing a `SocketTimeoutException`.

```java
public void setConnectTimeout(int timeout)
public int  getConnectTimeout()
public void setReadTimeout(int timeout)
public int  getReadTimeout()
```

The `setConnectTimeout()`/`getConnectTimeout()` methods control how long the socket waits for the initial connection. The `setReadTimeout()`/`getReadTimeout()` methods control how long the input stream waits for data to arrive. All four methods measure timeouts in milliseconds. All four interpret zero as meaning never time out. Both setter methods throw an `IllegalArgumentException` if the timeout is negative.

```java
URL u = new URL("http://www.example.org");
URLConnuction uc = u.openConnection();
uc.setConnectTimeout(30000);
uc.setReadTimeout(45000);
```

## Configuring the Client Request HTTP Header

