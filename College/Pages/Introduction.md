#college 
The word **data** refers to information presented in whatever form is agreed upon by the parties creating and using the data.

**Data communications** are the exchange of data between two devices via some form of transmission medium such as a wire cable.

**The effectiveness of a data communications system** depends on four fundamental characteristics - 
1. Delivery: The system must deliver data to the correct destination.
2. Accuracy: Data that have been altered in transmission and left uncorrected are unusable.
3. Timeliness: Data delivered late are useless. In the case of video and audio, timely delivery means delivering data as they are produced, in the same order that they are produced, and without significant delay. This kind of delivery is called real-time transmission.
4. Jitter. Jitter refers to the variation in the packet arrival time. It is the uneven delay in the delivery of audio or video packets.


A data communications system has five components - 
![[Pasted image 20260328095307.png]]
1. Message- The message is the information (data) to be communicated. Popular forms of information include text, numbers, pictures, audio, and video.
2. Sender- The sender is the device that sends the data message. It can be a computer, workstation, telephone handset, video camera, and so on.
3. Receiver- The receiver is the device that receives the message. It can be a computer, workstation, telephone handset, television, and so on.
4. Transmission medium- The transmission medium is the physical path by which a message travels from sender to receiver. Some examples of transmission media include twisted-pair wire, coaxial cable, fiber-optic cable, and radio waves.
5. Protocol- A protocol is a set of rules that govern data communications. It represents an agreement between the communicating devices.

# Data Flow
Communication between two devices can be simplex, half-duplex, or full-duplex.

In **simplex mode**, the communication is unidirectional. Only one
of the two devices on a link can transmit; the other can only receive. Keyboards and traditional monitors are examples of simplex devices. Simplex can use the entire capacity of the channel to send data in one direction.

In **half-duplex mode**, each station can both transmit and receive, but not at the same instance of time. In a half-duplex transmission, the entire capacity of a channel is taken over by whichever of the two devices is transmitting at the time. Walkie-talkies and CB (citizens band) radios are both half-duplex systems.

In **full-duplex mode**, both stations can transmit and receive simultaneously. In full-duplex mode, signals going in one direction share the capacity of the link with signals going in the other direction. This sharing can occur in two ways: Either the link must contain two physically separate transmission paths, one for sending and the other for receiving; or the capacity of the channel is divided between signals traveling in both directions. One common example of full-duplex communication is the telephone network.

==See advantages and disadvantages of each==

# Type of Signalling
Serial transmission occurs in one of three ways: asynchronous, synchronous, and isochronous.

**Asynchronous transmission** is so named because the timing of a signal is unimportant. Instead, information is received and translated by agreed upon patterns. As long as those patterns are followed, the receiving device can retrieve the information without regard to the rhythm in which it is sent. Patterns are based on grouping the bit stream into
bytes. Each group, usually 8 bits, is sent along the link as a unit. The sending system handles each group independently, relaying it to the link whenever ready, without regard to a timer.
Without synchronization, the receiver cannot use timing to predict when the next group will arrive. Therfore, start and stop bits are used which increases the total bits to 10.

The addition of stop and start bits and the insertion of gaps into the bit stream make asynchronous transmission slower than other forms of transmission that can operate without the addition of control information. But it is cheap and effective, two advantages that make it an attractive choice for situations such as low-speed communication.

In **synchronous transmission**, the bit stream is combined into longer "frames," which may contain multiple bytes. Each byte, however, is introduced onto the transmission link without a gap between it and the next one. It is left to the receiver to separate the bit stream into bytes for decoding purposes. In other words, data are transmitted as an unbroken string of 1s and Os, and the receiver separates that string into the bytes, or characters, it needs to reconstruct the information.

The advantage of synchronous transmission is speed. With no extra bits or gaps to introduce at the sending end and remove at the receiving end, and, by extension, with fewer bits to move across the link, synchronous transmission is faster than asynchronous transmission. For this reason, it is more useful for high-speed applications such as the transmission of data from one computer to another. Byte synchronization is accomplished in the data link layer.

==Although there is no gap between characters
in synchronous serial transmission, there may be uneven gaps between frames.==

The **isochronous transmission** guarantees that the data arrive at a fixed rate. The entire stream of bits is synchronized and there are no delays between frames. This is used in real-time audio and video, in which uneven delays between frames are not acceptable.

# Physical Structure
## Types of Connections
A **point-to-point** connection provides a dedicated link between two devices. The entire capacity of the link is reserved for transmission between those two devices. Most point-to-point connections use an actual length of wire or cable to connect the two ends, but other options, such as microwave or satellite links, are also possible(eg IR remotes).

A **multipoint** (also called multidrop) connection is one in which more than two specific devices share a single link. In a multipoint environment, the capacity of the channel is shared, either spatially or temporally. If several devices can use the link simultaneously, it is a spatially shared connection. If users must take turns, it is a timeshared connection.
![[Pasted image 20260328122714.png|422]]
## Topology
The term physical topology refers to the way in which a network is laid out physically; two or more devices connect to a link and two or more links form a topology. There are four basic topologies - 

==Also see Tree topology==
### Mesh
Here every device has a dedicated point-to-point link to every
other device. The number of physical links in a fully connected mesh network with $n$ nodes, we need $n(n - 1)$ physical links since each node is connect to $n - 1$ other nodes. However, if each physical link allows communication in both directions (duplex mode), we can divide the number of links by 2. In other words, we need $\frac{n(n -1)}{2}$ duplex-mode links. To accommodate that many links, every device on the network must have $n - 1$ input/output (VO) ports.

A mesh offers several advantages over other network topologies - 
1. Dedicated links for each connection
2. If one link becomes unusable, it does not incapacitate the entire system
3. Dedicated lines make sure that only the intended recipient sees a message, thus providing security
4. Point-to-point links make fault identification and fault isolation easy.

Disadvantages are - 
1. Difficulty in installation and reconnection.
2. Large amount of wiring make it expensive and takes up a lot of space.
3. Expensive hardware(IO ports, cables) increase expense
 
They are used in mesh WiFi systems, critical data centers etc

### Star
Here, each device has a dedicated point-to-point link only to a central controller, usually called a hub. The devices are not directly linked to one another. Unlike a mesh topology, a star topology does not allow direct traffic between devices. The controller acts as an exchange: If one device wants to send data to another, it sends the data to the controller, which then relays the data to the other connected device.

Advantages-
1. Less expensive because each device needs only one connection(IO port and cable)
2. It is therefore also easy to install and reconfigure
3. If one link fails, only that link is affected and all others remain ooperational
4. Therefore, fault identification and isolation is easy

Disadvantages - 
1. The dependency of the whole topology on one single point, the hub. If the hub goes down, the whole system is dead.
2. Still requires more cabling than Rings or Buses

High-speed LANs often use a star topology with a central hub.

### Bus 
A bus topology is multipoint. One long cable acts as a backbone to link all the devices in a network.Nodes are connected to the bus cable by drop lines and taps. 

==A drop line is a connection running between the device and the main cable. A tap is a connector that either splices into the main cable or punctures the sheathing of a cable to create a contact with the metallic core.==

Due to heat generation, there is a limit on the number of taps a bus can support and on the distance between those taps.

Advantages-
1. Ease of installation
2. A bus uses less cabling than mesh or star topologies and requires less space because only the backbone cable stretches through the entire facility.

Disadvantages - 
1. Difficult reconnection and fault isolation.
2. Degradation in quality due to presence of taps.
3. A fault or break in the bus cable stops all transmission

Bus topology was the one of the first topologies used in the design of early local-area networks. Ethernet LANs can used to use bus topology.

### Ring
Here, each device has a dedicated point-to-point connection with only the two devices on either side of it. A signal is passed along the ring in one direction, from device to device, until it reaches its destination. Each device in the ring incorporates a repeater. When a device receives a signal intended for another device, its repeater regenerates the bits and passes them along.

Advantages - 
1. Easy to install and reconfigure.
2. Fault isolation is simplified. If a device does not recieve a message, it alerts the network operator to the problem and its location.

Disadvantages - 
1. Dues to unidirectional traffic, a break in the ring (such as a disabled station) can disable the entire network.

Ring topology was prevalent when IBM introduced its local-area network Token Ring.

### Hybrid

Hybrid Topology A network can be hybrid. For example, we can have a main star topology with each branch connecting several stations in a bus topology.
![[Pasted image 20260328130156.png|426]]


## LANs
A local area network (LAN) is usually privately owned and links the devices in a single office, building, or campus. Currently, LAN size is limited to a few kilometers.The resources to be shared can include hardware (e.g., a printer), software (e.g., an application program), or data.

A common example of a LAN, found in many business environments, links a workgroup of task-related computers, for example, engi-
neering workstations or accounting PCs.

The most common LAN topologies are bus, ring, and star. LAN speeds are normally 100 or 1000 Mbps. Wireless LANs are the newest evolution in LAN technology.

==Today, it is very rare to see a LAN, a MAN, or a LAN in isolation; they are connected to one another. When two or more networks are connected, they become an internetwork, or internet.==

