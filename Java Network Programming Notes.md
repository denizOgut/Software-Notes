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

