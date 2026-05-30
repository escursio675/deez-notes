#college 

A **network** is a combination of hardware and software that sends data from one location to another. The hardware consists of the physical equipment that carries signals from one point of the network to another. The software consists of instruction sets that provide the services that we expect from a network.

# The OSI Model
The Open Systems Interconnection(OSI) model is a layered framework for the design of network systems that allows communication between all types of computer systems. It consists of seven layers, each of which defines a part of the process of moving information across a network.

The OSI model is composed of seven ordered layers: physical(layer 1), data link(layer 2), network(layer 3), transport(layer 4), session(layer 5), presentation(layer 6), and application(layer 7). In a diagram, they are drawn from layer 1 at the bottom and layer 7 at the very top. These layers are simply the discrete groups of networking functions that are related to each other.

Most importantly, the OSI model allows complete interoperability between otherwise incompatible systems. Within a single machine, each layer calls upon the services of the layer just below it. Between machines, layer x on one machine communicates with layer $x$ on another machine. This communication is governed by an agreed-upon series of rules and conventions called protocols. The processes on each machine that communicate at a given layer are called _peer-to-peer processes_. Communication between machines is therefore a peer-to-peer process using the protocols appropriate to a given layer.

## Peer-to-Peer Processes
At the physical layer, communication is direct - from the physical layer of the sender to the physical layer of the reciever. At the higher layers, however, communication must move down through the layers on the sender, over to receiver, and then back up through the layers. Each layer in the sending device adds its own information to the message it receives from the layer just above it and passes the whole package to the layer just below it. At layer 1, the entire package is converted to a form that can be transmitted to the receiving device. At the receiving machine, the message is unwrapped layer by layer, with each process receiving and removing the data meant for it. For example, layer 2 removes the data meant for it, then passes the rest to layer 3. Layer 3 then removes the data meant for it and passes the rest to layer 4, and so on. This is made possible by an interface between each pair of adjacent layers. Each interface defines the information and services a layer must provide for the layer above it.
![[Pasted image 20260328182842.png|483]]

The seven layers can be thought of as belonging to three subgroups. Layers 1, 2, and 3 are the network support layers; they deal with the physical aspects of moving data from one device to another (such as electrical specifications, physical connections, physical addressing, and transport timing and reliability). Layers 5, 6, and 7 can be thought of as the user support layers; they allow interoperability among unrelated software systems. Layer 4 links the two subgroups and ensures that what the lower layers have transmitted is in a form that the upper layers can use. The upper OSI layers are almost always implemented in software; lower layers are a combination of hardware and software, except for the physical layer, which is mostly hardware.

At each layer, a header, or possibly a trailer, can be added to the data unit of its corresponding layer.

When the formatted data unit passes through the physical layer it is changed into an electromagnetic signal and transported along a physical link. Upon reaching its destination, the signal passes into layer 1 and is transformed back into digital form. The data units then move back up through the OSI layers. As each block of data reaches the next higher layer, the headers and trailers attached to it at the corresponding sending layer are removed, and actions appropriate to that layer are
taken. By the time it reaches layer 7, the message is again in a form appropriate to the application and is made available to the recipient.

==The OSI model implements **encapsulation**. A packet (header and data) at level 7 is encapsulated in a packet at level 6 and so on. Layer 6 is not aware of the different parts of the packet that is concerned with layer 7 and treats it as one unit of data.==


## Layers in the OSI Model
### Physical Layer
The physical layer coordinates the functions required to carry a bit stream over a physical medium. It deals with the mechanical and electrical specifications of the interface and transmission medium.
The physical layer is also concerned with the following:

1. The characteristics of the transmission medium.
2. The physical layer data consists of a stream of bits with no interpretation. To be transmitted, bits must be encoded into signals, electrical or optical. The physical layer defines the type of encoding (how Os and Is are changed to signals).
3. The transmission rate(the number of bits sent each second) is also defined by the physical layer. In other words, the physical layer defines the duration of a bit, which is how long it lasts.
4. Synchronization of bits between the sender and the reciever by synchronizing their clocks.
5. The physical layer is concerned with the connection of devices to the media(point-to-point or multipoint).
6. It defines the physical topology, ie, how devices are connected to make a network.
7. The physical layer also defines the direction of transmission between two devices: simplex, half-duplex, or full-duplex, ie, the transmission mode.
### Data Link Layer
The data link layer transforms the physical layer, a raw transmission facility, to a reliable link. It makes the physical layer appear error-free to the upper layer(network layer).
Other responsibilities of the data link layer include the following:

1. The data link layer divides the stream of bits received from the network layer into manageable data units called frames(the process is called framing).
2. It performs physical addressing. If frames are to be distributed to different systems on the network, the data link layer adds a header to the frame to define the sender and/or receiver of the frame. If the frame is intended for a system outside the sender's network, the receiver address is the address of the device that connects the network to the next one.
3. If the rate at which the data are absorbed by the receiver is less than the rate at which data are produced in the sender, the data link layer imposes a flow control mechanism to avoid overwhelming the receiver. This is called flow control.
4. It performs error control.  The data link layer adds reliability to the physical layer by adding mechanisms to detect and retransmit damaged or lost frames. It also uses a mechanism to recognize duplicate frames. Error control is normally achieved through a trailer added to the end of the frame.
5. When two or more devices are connected to the same link, data link layer protocols are necessary to determine which device has control over the link at any given time, thus implementing access control.

#### Hop-to-Hop delivery
To send data from systems A to D, three partial deliveries are made. First, the data link layer at A sends a frame to the data link layer at B (a router). Second, the data link layer at B sends a new frame to the data link layer at C. Finally, the data link layer at C sends a new frame to the data link layer at D. Note that the frames that are exchanged between the three nodes have different values in the headers. The frame from A to B has B as the destination address and A as the source address and so on.

The values of the trailers can also be different if error checking includes the header of the frame.



### Network Layer
The network layer is responsible for the source-to-destination delivery of a packet, possibly across multiple networks (links). Whereas the data link layer oversees the delivery of the packet between two systems on the same network (links), the network layer ensures that each packet gets from its point of origin to its final destination. If two systems are connected to the same link, there is usually no need for a network layer. However, if the two systems are attached to different networks (links) with connecting devices between the networks (links), there is often a need for the network layer to accomplish source-to-destination delivery.

Other responsibilities of the network layer include:
1. **Logical addressing.** The physical addressing implemented by the data link layer handles the addressing problem locally. If a packet passes the network boundary, we need another addressing system to help distinguish the source and destination systems. The network layer adds a header to the packet coming from the upperlayer that, among other things, includes the logical addresses of the sender and receiver.
2. **Routing.** When independent networks or links are connected to create internetworks (network of networks) or a large network, the connecting devices (called routers or switches) route or switch the packets to their final destination. One of the functions of the network layer is to provide this mechanism.

### Transport Layer
The transport layer is responsible for process-to-process delivery of the entire message. **A process is an application program running on a host**. Whereas the network layer oversees source-to-destination delivery of individual packets, it does not recognize any relationship between those packets. It treats each one independently, as though each piece belonged to a separate message. The transport layer ensures that the whole message arrives intact and in order, overseeing both error control and flow control at the source-to-destination level. 

Other responsibilities of the transport layer include:
1. **Service-point addressing**. Computers often run several programs at the same time. For this reason, source-to-destination delivery means delivery not only from one computer to the next but also from a specific process on one computer to a specific process on the other. The transport layer header must therefore include a type of address called a service-point address (or port address). The network layer gets each packet to the correct computer; the transport layer gets the entire message to the correct process on that computer.
2. **Segmentation and reassembly**. A message is divided into transmittable segments, with each segment containing a sequence number. These numbers enable the transport layer to reassemble the message correctly upon arriving at the destination and to identify and replace packets that were lost in transmission. 
3. **Connection control**. The transport layer can be either connectionless or connection-oriented. A connectionless transport layer treats each segment as an independent packet and delivers it to the transport layer at the destination machine. A connection-oriented transport layer makes a connection with the transport layer at the destination machine first before delivering the packets. After all the data are transferred,the connection is terminated.
4. **Flow control**. Like the data link layer, the transport layer is responsible for flow control. However, flow control at this layer is performed end to end rather than across a single link.
5. **Error control**. Like the data link layer, the transport layer is responsible for error control. However, error control at this layer is performed process-to-process rather than across a single link. The sending transport layer makes sure that the entire message arrives at the receiving transport layer without error (damage, loss, or duplication). Error correction is usually achieved through retransmission.
### Session Layer
The services provided by the first three layers are not sufficient for some processes. The session layer is the network dialog controller. It establishes, maintains, and synchronizes the interaction among communicating systems.

The responsibilities of the session layer include:
1. **Dialog control**. The session layer allows two systems to enter into a dialog. It allows the communication between two processes to take place in either half-duplex (one way at a time) or full-duplex (two ways at a time) mode.
2. **Synchronization**. The session layer allows a process to add checkpoints, or synchronization points, to a stream of data. For example, if a system is sending a file of 2000 pages, it is advisable to insert checkpoints after every 100 pages to ensure that each 100-page unit is received and acknowledged independently. In this case, if a crash happens during the transmission of page 523, the only pages that need to be resent after system recovery are pages 501 to 523.

### Presentation Layer
The presentation layer is concerned with the syntax and semantics of the information exchanged between two systems.

The responsibilities of the presentation layer include:
1. **Translation**. The processes (running programs) in two systems are usually exchanging information in the form of character strings, numbers, and so on. The information must be changed to bit streams before being transmitted. Because different computers use different encoding systems, the presentation layer is responsible for interoperability between these different encoding methods. The presentation layer at the sender changes the information from its sender-dependent format into a common format. The presentation layer at the receiving machine changes the common format into its receiver-dependent format.
2. **Encryption**. To carry sensitive information, a system must be able to ensure privacy. Encryption means that the sender transforms the original information to another form and sends the resulting message out over the network. Decryption reverses the original process to transform the message back to its original form.
3. **Compression**. Data compression reduces the number of bits contained in the information. Data compression becomes particularly important in the transmission of multimedia such as text, audio, and video.

### Application Layer
The application layer enables the user to access the network. It provides user interfaces and support for services such as electronic mail, remote file access and transfer, shared database management, and other types of distributed information services.

Services provided by the application layer include the following:
1. **Network virtual terminal**. A network virtual terminal is a software version of a physical terminal, and it allows a user to log on to a remote host. The user's computer talks to the software terminal which, in turn, talks to the host, and vice versa. The remote host believes it is communicating with one of its own terminals and allows the user to log on.
2. **File transfer, access, and management**. This application allows a user to access files in a remote host (to make changes or read data).

3. **Mail services**. This application provides the basis for e-mail forwarding and storage.
4. **Directory services**. This application provides distributed database sources and access for global information about various objects and services.

# TCP/IP Protocol Suite
The TCP/IP protocol suite was developed prior to the OSI model. Therefore, the layers in the TCP/IP protocol suite do not exactly match those in the OSI model. The original TCP/IP protocol suite was defined as having four layers: host-to-network, internet, transport, and application. However, when TCP/IP is compared to OSI, we can say that the host-to-network layer is equivalent to the combination of the physical and data link layers. The internet layer is equivalent to the network layer, and the application layer is roughly doing the job of the session, presentation, and application layers with the transport layer in TCP/IP taking care of part of the duties of the session layer.
Therefore, we can assume that the TCP/IP protocol suite is made of five layers: physical, data link, network, transport, and application. The first four layers provide physical standards, network interfaces, internetworking, and transport functions that correspond to the first four layers of the OSI model. The three topmost layers in the OSI model,
however, are represented in TCP/IP by a single layer called the application layer.

**TCP/IP is a hierarchical protocol made up of interactive modules, each of which provides a specific functionality**; however, the modules are not necessarily interdependent. Whereas the OSI model specifies which functions belong to each of its layers the layers of the TCP/IP protocol suite contain relatively independent protocols that can be mixed and matched depending on the needs of the system. The term hierarchical means that each upper-level protocol is supported by one or more lower-level protocols.

At the transport layer, TCP/IP defines three protocols: Transmission Control Protocol (TCP), User Datagram Protocol (UDP), and Stream Control Transmission Protocol (SCTP). At the network layer, the main protocol defined by TCP/IP is the Internetworking Protocol (IP); there are also some other protocols that support data movement in this layer.

## Physical and Data Link Layers
At the physical and data link layers, TCP/IP does not define any specific protocol. It supports all the standard and proprietary protocols. A network in a TCP/IP internetwork can be a local-area network or a wide-area network.

## Network Layer
At the network layer (or, more accurately, the internetwork layer), TCP/IP supports the Internetworking Protocol. IP, in turn, uses four supporting protocols: ARP, RARP, ICMP, and IGMP. Each of these protocols is described later.

### Internetworking Protocol (IP)
The Internetworking Protocol (IP) is the transmission mechanism used by the TCP/IP protocols. It is an unreliable and connectionless protocol-a best-effort delivery service. The term best effort means that IP provides no error checking or tracking. IP assumes the unreliability of the underlying layers and does its best to get a transmission through to its destination, but with no guarantees. IP transports data in packets called **datagrams**, each of which is transported separately. Datagrams can travel along different routes and can arrive out of sequence or be duplicated. IP does not keep track of the routes and has no facility for reordering datagrams once they arrive at their destination. The limited functionality of IP should not be considered a weakness, however. IP provides bare-bones transmission functions that free the user to add only those facilities necessary for a given application and thereby allows for maximum efficiency.

### Address Resolution Protocol
The Address Resolution Protocol (ARP) is used to associate a logical address with a physical address. On a typical physical network, such as a LAN, each device on a link is identified by a physical or station address, usually imprinted on the network interface card (NIC). ARP is used to find the physical address of the node when its Internet address is known.

### Reverse Address Resolution Protocol
The Reverse Address Resolution Protocol (RARP) allows a host to discover its Internet address when it knows only its physical address. It is used when a computer is connected to a network for the first time.

### Internet Control Message Protocol
The Internet Control Message Protocol (ICMP) is a mechanism used by hosts and gateways to send notification of datagram problems back to the sender. ICMP sends query and error reporting messages.

### Internet Group Message Protocol
The Internet Group Message Protocol (IGMP) is used to facilitate the simultaneous transmission of a message to a group of recipients.

## Transport Layer
Traditionally the transport layer was represented in TCP/IP by two protocols: TCP and UDP. IP is a host-to-host protocol, meaning that it can deliver a packet from one physical device to another. UDP and TCP are transport level protocols responsible for delivery of a message from a process (running program) to another process. A new transport layer protocol, SCTP, has been devised to meet the needs of some newer applications.

### User Datagram Protocol
The User Datagram Protocol (UDP) is the simpler of the two standard TCP/IP transport protocols. It is a process-to-process protocol that adds only port addresses, checksum error control, and length information to the data from the upper layer.

### Transmission Control Protocol
The Transmission Control Protocol (TCP) provides full transport-layer services to applications. TCP is a reliable stream transport protocol. The term stream, in this context, means connection-oriented: A connection must be established between both ends of a transmission before either can transmit data. At the sending end of each transmission, TCP divides a stream of data into smaller units called segments. Each segment includes a sequence number for reordering after
receipt, together with an acknowledgment number for the segments received. Segments are carried across the internet inside of IP datagrams. At the receiving end, TCP collects each datagram as it comes in and reorders the transmission based on sequence numbers.

### Stream Control Transmission Protocol
The Stream Control Transmission Protocol (SCTP) provides support for newer applications such as voice over the Internet. It is a transport layer protocol that combines the best features of UDP and TCP.

## Application Layer
The application layer in TCP/IP is equivalent to the combined session, presentation, and application layers in the OSI model. Many protocols are defined at this layer.

(also see 'Addressing')