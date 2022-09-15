# NETWORK
- A network is a collection of devices connected to each other to allow the sharing of data.
- Example of a network is an internet. An internet connects the millions of people across the world.

# COMPUTER NERWORK 
- Computer Networks is a communication network established between many electronic devices, for sharing resources and data.

## Open system - 
- A system that is connected to the network and is ready for communication.

## Closed system - 
- A system that is not connected to the network and can’t be communicated with.

## Network devices
- devices or mediums which helps in the communication between two different devices
- e.g. Router, Switch, Hub, Bridge.

# TOPOLOGIES:
1. `PHYSICAL TOPOLOGY`
    - Physical Topology: A physical topology describes the way in which the computers or nodes are connected with each other in a computer network.
2. `Network topology`
    - it is the way in which the devices communicate internally, i.e how the data flow from one computer to another
    - Network topology can be categorized into – Bus Topology, Ring Topology, Star Topology, Mesh Topology, Tree Topology.
    - B R M S T (B R a M .. Sarovar The)

# NETWORK TOPOLOGY
- Network topology is a physical layout of the network, connecting the different nodes using the links. It depicts the connectivity between the computers, devices, cables, etc.
1. BUS

![](https://user-images.githubusercontent.com/86204416/188299091-695142d7-6d0a-4a9c-b192-a696fe6eadcf.png)

- Bus topology is a network topology in which all the nodes are connected to a single cable known as a central cable or bus.
- It acts as a shared communication medium, i.e., if any device wants to send the data to other devices, then it will send the data over the bus which in turn sends the data to all the attached devices.
- Bus topology is useful for a small number of devices. As if the bus is damaged then the whole network fails.

2. STAR

![](https://user-images.githubusercontent.com/86204416/188299116-d85fb114-0e7a-4ebe-a874-b9a33075c432.png)

- Star topology is a network topology in which all the nodes are connected to a single device known as a central device.
- Star topology requires more cable compared to other topologies. Therefore, it is more strong as a failure in one cable will only disconnect a specific computer connected to this cable.
- If the central device is damaged, then the whole network fails.
- Star topology is very easy to install, manage and troubleshoot.
- Star topology is commonly used in office and home networks.

3. RING

![](https://user-images.githubusercontent.com/86204416/188299137-a466bae4-c445-4e14-a622-d364c40b067b.png)

- Ring topology is a network topology in which nodes are exactly connected to two or more nodes and thus, forming a single continuous path for the transmission.
- It does not need any central server to control the connectivity among the nodes.
- If the single node is damaged, then the whole network fails.
- Ring topology is very rarely used as it is expensive, difficult to install and manage.
- Examples of Ring topology are SONET network, SDH network, etc.

4. MESH

![](https://user-images.githubusercontent.com/86204416/188299164-8c19f246-2d3d-41fc-b49b-17536e35a4f2.png)

- Mesh topology is a network topology in which all the nodes are individually connected to other nodes.
- It does not need any central switch or hub to control the connectivity among the nodes.
- Mesh topology is categorized into two parts:
- Fully connected mesh topology: In this topology, all the nodes are connected to each other.
- Partially connected mesh topology: In this topology, all the nodes are not connected to each other.
- It is a robust as a failure in one cable will only disconnect the specified computer connected to this cable.
- Mesh topology is rarely used as installation and configuration are difficult when connectivity gets more.
- Cabling cost is high as it requires bulk wiring.

5. TREE

![](https://user-images.githubusercontent.com/86204416/188299177-02d5a409-ee35-454c-8348-d8b2e5c23acc.png)

- Tree topology is a combination of star and bus topology. It is also known as the expanded star topology.
- In tree topology, all the star networks are connected to a single bus.
- Ethernet protocol is used in this topology.
- In this, the whole network is divided into segments known as star networks which can be easily maintained. If one segment is damaged, but there is no effect on other segments.
- Tree topology depends on the "main bus," and if it breaks, then the whole network gets damaged.

6. HYBRID

- A hybrid topology is a combination of different topologies to form a resulting topology.
- If star topology is connected with another star topology, then it remains star topology. If star topology is connected with different topology, then it becomes a Hybrid topology.
- It provides flexibility as it can be implemented in a different network environment.
- The weakness of a topology is ignored, and only strength will be taken into consideration.

# How are Network types classified?/Explain different types of networks.
- `PLMWG`

![](https://user-images.githubusercontent.com/86204416/188309000-a28a748d-5600-4410-8490-e19aa1f9ee58.png)

![](https://user-images.githubusercontent.com/86204416/188309026-cebda001-3623-4776-91c6-2e09cc5fca2d.png)


# LAN
- Local area network is a network which is designed to operate over a small physical area such as office factory or group of building
- When LANs are used by companies or organizations, they are called enterprise networks.
- There are two different types of LAN networks i.e. wireless LAN (no wires involved achieved using Wi-Fi) and wired LAN (achieved using LAN cable).

# VPN (Virtual Private Network)

# What are nodes and links?
- `Node:` Any communicating device in a network is called a Node. Node is the point of intersection in a network. It can send/receive data and information within a network. Examples of the node can be computers, laptops, printers, servers, modems, etc.

- `Link:` A link or edge refers to the connectivity between two nodes in the network. It includes the type of connectivity (wired or wireless) between the nodes and protocols used for one node to be able to communicate with the other.
![](https://user-images.githubusercontent.com/86204416/188312289-1c813e1d-50f1-4030-a636-5a512f147926.png)


# GATEWAY
- A node that is connected to two or more networks is commonly known as a gateway. 
- It is also known as a router. 
- It is used to forward messages from one network to another.
- Both the gateway and router regulate the traffic in the network. 

> Differences between gateway and router: A router sends the data between two similar networks while gateway sends the data between two dissimilar networks.

# PING
- The “ping” is a utility program that allows us to check the connectivity between the network devices. we  can ping devices using its IP address or name.

# MAC (Media Access Control)
- MAC address is the physical address, which uniquely identifies each device on a given network. 
- To make communication between two networked devices, we need two addresses: IP address and MAC address.

# IP (Internet Protocol)
- An IP address is the identifier that enables your device to send or receive data packets across the internet. 
- It holds information related to your location and therefore making devices available for two-way communication.

# VPN (Virtual Private Network) : 
- VPN or the Virtual Private Network is a private WAN (Wide Area Network) built on the internet. 
- It allows the creation of a secured tunnel (protected network) between different networks using the internet (public network). 
- By using the VPN, a client can connect to the organisation’s network remotely.

### ADVANTAGES OF VPN
- VPN is used to connect offices in different geographical locations remotely and is cheaper when compared to WAN connections.
- VPN is used for secure transactions and confidential data transfer between multiple offices located in different geographical locations.
- VPN keeps an organization’s information secured against any potential threats or intrusions by using virtualization.
- VPN encrypts the internet traffic and disguises the online identity

# HUB v/s SWITCH
- `Hub` is a networking device which is used to transmit the signal to each port
(except one port) to respond from which the signal was received. 
- Hub is operated on a Physical layer. 
- In this packet filtering is not available. 
- It is of two types: Active Hub, Passive Hub.

- `Switch`: Switch is a network device which is used to enable the connection
establishment and connection termination on the basis of need. 
- Switch is operated on the Data link layer.

# TCP vs UDP
- TCP is a connection-oriented protocol, whereas UDP is a connectionless protocol.
- A key difference between TCP and UDP is speed, as TCP is comparatively slower than UDP. 
- Overall, UDP is a much faster, simpler, and efficient protocol, however, retransmission of lost data packets is only possible with TCP.

# DELAYS
1. Transmission delay
    - Time taken to put the data packet on the transmission link is called as transmission delay
2. Propagation delay
    - Time taken for one bit to travel from sender to receiver end of the link is called as propagation delay.
3. Queuing delay
     - Time spent by the data packet waiting in the queue before it is taken for execution is called as queuing delay.
4. Processing delay
     - Time taken by the processor to process the data packet is called as processing delay.


1. ISO - International Organization of Standardization
2. OSI - open system interconnection
3. Layers:
    - APS TN DP (A Pakistan Sun, Tu Nahi DP khel skta)\

# OSI - 
- OSI stands for Open Systems Interconnection. 
- It is a reference model that specifies standards for communications protocols and also the functionalities of each layer.

### Protocol - 
- A protocol is the set of rules or algorithms which define the way, how two devices can communicate across the network
- there exists different protocol defined at each layer of the OSI model. 
- A few of such protocols are TCP, IP, UDP, ARP, DHCP, FTP and so on.

## PHYSICAL LAYER
- It is responsible for actual physical transmission of data
- It recieves/transmits signals and then converts it to physical bits
- It handles transmission mode (simplex, half-duplex, full-duplex).

## Data Link Layer
- It is responsible for Node-to-Node delivery of packets
- The main function of this layer is to make sure data transfer is error free from one node to another, over the physical layer.

## Network Layer
- It is responsible for Logical Addressing (IPv4/v6) and Routing.
- It decides by which route data should be taken.
- Network Layer routes the signal through different channels from one node to other.
- It acts as a network controller. It manages the Subnet traffic.
- It divides the outgoing messages into packets and assembles the incoming packets into messages for higher levels.

## Transport Layer
- It is responsible for End-to-end delivery of packets.
- It receives messages from the Session layer above it, convert the message into smaller units and passes it on to the Network layer.
- Functions such as Multiplexing, Segmenting or Splitting on the data are done by this layer

## Session Layer
- Session Layer manages and synchronize the conversation between two different applications.

## Presentation Layer
- Presentation Layer takes care that the data is sent in such a way that the receiver will understand the information (data) and will be able to use the data.
- It perfroms Data compression, Data encryption, Data conversion etc.

## Application Layer
- Application Layer is the topmost layer.
- This layer mainly holds application programs to act upon the received and to be sent data.

# TCP/IP Model 
- It comprises of 4 layers with the following responsibilities (starting from the lowest layer):
## Network Access Layer: 
- It is a combination of the Physical and Data-Link Layer, and is responsible for data transmission and hardware addressing (MAC).
## Internet Layer: 
- It is the counterpart of OSI's Network layer, and is responsible for routing and logical addressing. (IP, ICMP, ARP).
## Transport Layer: 
- Maintains End-to-end connectivity. It is a counterpart of the OSI's transport layer, and has the same responsibilites (TCP vs. UDP).
## Application Layer: 
- Application-specific protocols are implemented here. (HTTP, HTTPS, FTP, SMTP etc.)

# DIFFERENCE 
![](https://user-images.githubusercontent.com/86204416/189894803-ac4121cf-2876-435a-93d7-f38e1e49a3dd.png)

# Network Criteria - The criteria that have to be met by a computer network are:
1. `Performance` 
- It is measured in terms of transit time and response time.
- Performance is dependent on the following factors:
- The number of users
- Type of transmission medium
- Capability of connected network
- Efficiency of software
3. `Reliability` - 
- It is measured in terms of
- Frequency of failure
- Recovery from failures
- Robustness during catastrophe
4. `Security` - 
- It means protecting data from unauthorized access.

## Goals of Computer Networks
1. `Resource Sharing` - Many organizations have a substantial number of computers in operations, which are located apart. e.g. A group of office workers can share a common printer, fax, modem, scanner, etc.
2. `High Reliability` - If there are alternate sources of supply, all files could be replicated on two or, machines. If one of them is not available, due to hardware failure, the other copies could be used.

3. `Inter-process Communication` - Network users, located geographically apart, may converse in an interactive session through the network. In order to permit this, the network must provide almost error-free communications.

4. `Flexible access` - Files can be accessed from any computer in the network. The project can be begun on one computer and finished on another.

## Manchaster Encoding

![Screenshot Capture - 2022-09-14 - 23-49-24](https://user-images.githubusercontent.com/35686407/190232178-485f26c1-0bca-4c2f-9230-b16dcae9da67.png)

## Repeaters:

![Screenshot Capture - 2022-09-14 - 23-52-01](https://user-images.githubusercontent.com/35686407/190232608-da2193ce-16b8-4345-ab43-9cbc9bc6b60f.png)

## HUB

![Screenshot Capture - 2022-09-14 - 23-51-12](https://user-images.githubusercontent.com/35686407/190232455-cf42af91-a3c5-488e-a5a4-b589d10acb81.png)

## Bridges:

![Gate Smashers - Lec-12 Bridges In Computer Networks Physical and data link layer device  dDP36_ZBs6A - 885x498 - 0m51s](https://user-images.githubusercontent.com/35686407/190232706-e6251f7b-499f-407d-b344-42280a491da5.png)

## Routers

![Screenshot Capture - 2022-09-14 - 23-53-48](https://user-images.githubusercontent.com/35686407/190232898-4758c4e2-d05a-4d83-ac2b-719ceb101031.png)

## TRANSMISSION MODES
1. `Simplex Communication` is uni-directional or one-way in Simplex Mode. i.e. Only one device is allowed to transfer data and the other device simply recieves it. e.g. Radio

2. `Half-Duplex Communication` is possible both-ways but not simultaneously. i.e. Both the devices/stations can transmit and recieve data but not at the same time. At an instant, only communication in a single direction is allowed. e.g. Walkie-Talkie.

3. `Full-Duplex` Bidirectional communication is possible both ways and  simultaneously. e.g mobile phone

# Flow Control in Computer Networks-
- A set of procedures which are used for restricting the amount of data that a sender can send to the receiver.
<img width="493" alt="image" src="https://user-images.githubusercontent.com/86204416/189919172-473019e0-6dfa-4bed-bc41-e7759307e623.png">

## Stop and Wait Protocol
> Stop and Wait Protocol is the simplest flow control protocol.

- Sender sends a data packet to the receiver.
- Sender stops and waits for the acknowledgement for the sent packet from the receiver.
- Receiver receives and processes the data packet.
- Receiver sends an acknowledgement to the sender.
- After receiving the acknowledgement, sender sends the next data packet to the receiver.
![](https://user-images.githubusercontent.com/86204416/189919539-27f7d467-de05-4d92-b479-2bfd48894628.png)

### PROBLEMS:
> Point-01:
It is extremely inefficient because-

- It makes the transmission process extremely slow.
- It does not use the bandwidth entirely as each single packet and acknowledgement uses the entire time to traverse the link.
 

> Point-02:
If the data packet sent by the sender gets lost, then-

- Sender will keep waiting for the acknowledgement for infinite time.
- Receiver will keep waiting for the data packet for infinite time.
 

> Point-03:
If acknowledgement sent by the receiver gets lost, then-

- Sender will keep waiting for the acknowledgement for infinite time.
- Receiver will keep waiting for another data packet for infinite time.

## Stop and Wait ARQ-
- Stop and Wait ARQ is an improved and modified version of Stop and Wait protocol.
- Stop and wait ARQ works similar to stop and wait protocol.
- It provides a solution to all the limitations of stop and wait protocol.
- Stop and wait ARQ includes the following three extra elements.

![](https://user-images.githubusercontent.com/86204416/189922369-4408212d-e1ae-493c-8788-9ff6c32ffee8.png)

![](https://user-images.githubusercontent.com/86204416/189924623-3bc35889-6db3-48f4-aef2-c425f06c118e.png)

#### working:
> Problem of Lost Data Packet-

- Time out timer helps to solve the problem of lost data packet.
- After sending a data packet to the receiver, sender starts the time out timer.
- If the data packet gets acknowledged before the timer expires, sender stops the time out timer.
- If the timer goes off before receiving the acknowledgement, sender retransmits the same data packet.
- After retransmission, sender resets the timer.
- This prevents the occurrence of deadlock.
![](https://user-images.githubusercontent.com/86204416/190035451-2af700b8-37ca-4185-86b0-367ffa900b2b.png)

> Problem of Lost Acknowledgement-
 
- Sequence number on data packets help to solve the problem of delayed acknowledgement.
- Consider the acknowledgement sent by the receiver gets lost.
- Then, sender retransmits the same data packet after its timer goes off.
- This prevents the occurrence of deadlock.
- The sequence number on the data packet helps the receiver to identify the duplicate data packet.
- Receiver discards the duplicate packet and re-sends the same acknowledgement.
![](https://user-images.githubusercontent.com/86204416/190035480-4eb6146c-72b4-4ce7-9223-e9a15584b7f0.png)

> Problem of Delayed Acknowledgement-
 
- Sequence number on acknowledgements help to solve the problem of delayed acknowledgement.
![](https://user-images.githubusercontent.com/86204416/190035600-ae5c8197-64da-4332-a8da-da6f0e74f30e.png)

## LIMITATIONS
- The major limitation of Stop and Wait ARQ is its very less efficiency.
- As the Sender window size is 1.
- This allows the sender to keep only one frame unacknowledged.
- So, sender sends one frame and then waits until the sent frame gets acknowledged.
- After receiving the acknowledgement from the receiver, sender sends the next frame.

## DIFFERENCE BETWEEN STOP&WAIT AND ARQ
![](https://user-images.githubusercontent.com/86204416/190035841-4237c257-55b5-454d-a85f-44b7d412d9f7.png)


# Sliding Window Protocol-
- It allows the sender to send multiple frames before needing the acknowledgements.
- Sender slides its window on receiving the acknowledgements for the sent frames.
- This allows the sender to send more frames.

![](https://user-images.githubusercontent.com/86204416/190040738-fbf7308c-10c1-42d8-8083-ab5d3bbdd712.png)

## Go back N Protocol-
- Go back N protocol is an implementation of a sliding window protocol.
- In Go back N, sender window size is N and receiver window size is always 1.
- Go back N uses cumulative acknowledgements.
- Go back N may use independent acknowledgements too.
- Go back N does not accept the corrupted frames and silently discards them.
- Go back N does not accept out of order frames and silently discards them.
- Go back N leads to retransmission of entire window if for any frame, no ACK is received by the sender.
- Go back N leads to retransmission of lost frames after expiry of time out timer.

## Selective Repeat Protocol-
- Selective Repeat protocol or SR protocol is an implementation of a sliding window protocol.
- In SR protocol, sender window size is always same as receiver window size.
- SR protocol uses independent acknowledgements only.
- SR protocol does not accept the corrupted frames but does not silently discard them.
- SR protocol accepts the out of order frames.
- SR protocol requires sorting at the receiver’s side.
- SR protocol requires searching at the sender’s side.
- SR protocol leads to retransmission of lost frames after expiry of time out timer.


## DIFFERENCES
![](https://user-images.githubusercontent.com/86204416/190128540-df620730-9fc2-44d7-9388-d3a0b4f418cd.png)


## ROUTING
- Routing: The network layer protocols determine which route is suitable from source to destination. This function of network layer is known as routing.

## FRAMING
- Framing is a function of the data link layer. 
- It provides a way for a sender to transmit a set of bits that are meaningful to the receiver. 
- This can be accomplished by attaching special bit patterns to the beginning and end of the frame.

## ERRORS
- A condition when the receiver’s information does not match with the sender’s information.
- During transmission, digital signals suffer from noise that can introduce errors in the binary bits travelling from sender to receiver.
- That means a 0 bit may change to 1 or a 1 bit may change to 0.
- Error Detecting Codes (Implemented either at Data link layer or Transport Layer of OSI Model)

## ERROR DETECTION METHODS
1. Simple Parity check
2. Two-dimensional Parity check
3. Checksum
4. Cyclic redundancy check
![](https://user-images.githubusercontent.com/86204416/190168656-4ec6cd14-6216-4c46-be04-5ef7968636a3.png)

## SINGLE PARITY CHECK
- One extra bit called as parity bit is sent along with the original data bits.
- Parity bit helps to check if any error occurred in the data during the transmission.

> Step-01:

- At sender side,

- Total number of 1’s in the data unit to be transmitted is counted.
- The total number of 1’s in the data unit is made even in case of even parity.
- The total number of 1’s in the data unit is made odd in case of odd parity.
- This is done by adding an extra bit called as parity bit.
 

> Step-02:
 
- The newly formed code word (Original data + parity bit) is transmitted to the receiver.
 

> Step-03:
 
- At receiver side,

- Receiver receives the transmitted code word.
- The total number of 1’s in the received code word is counted.

> Then, following cases are possible-

- If total number of 1’s is even and even parity is used, then receiver assumes that no error occurred.
- If total number of 1’s is even and odd parity is used, then receiver assumes that error occurred.
- If total number of 1’s is odd and odd parity is used, then receiver assumes that no error occurred.
- If total number of 1’s is odd and even parity is used, then receiver assumes that error occurred.

### Advantage-
- This technique is guaranteed to detect an odd number of bit errors (one, three, five and so on).

### DIS-ADVANTAGE
- This technique can not detect an even number of bit errors (two, four, six and so on).

## Cyclic Redundancy Check-
- Cyclic Redundancy Check (CRC) is an error detection method.
- It is based on binary division.

## CRC Generator-
- CRC generator is an algebraic polynomial represented as a bit pattern.
- The power of each term gives the position of the bit and the coefficient gives the value of the bit.
- eg: Consider the CRC generator is x7 + x6 + x4 + x3 + x + 1,  the corresponding binary pattern is 11011011.

> Step-01: Calculation Of CRC At Sender Side-

- At sender side,
- A string of n 0’s is appended to the data unit to be transmitted.
- Here, n is one less than the number of bits in CRC generator.
- Binary division is performed of the resultant string with the CRC generator.
- After division, the remainder so obtained is called as CRC.
- It may be noted that CRC also consists of n bits.

> Step-02: Appending CRC To Data Unit-

- At sender side,
- The CRC is obtained after the binary division.
- The string of n 0’s appended to the data unit earlier is replaced by the CRC remainder.

> Step-03: Transmission To Receiver-
 
- The newly formed code word (Original data + CRC) is transmitted to the receiver.

> Step-04: Checking at Receiver Side-
 
- At receiver side,
- The transmitted code word is received.
- The received code word is divided with the same CRC generator.
- On division, the remainder so obtained is checked.

> The following two cases are possible-

> Case-01: Remainder = 0
 
- If the remainder is zero,
- Receiver assumes that no error occurred in the data during the transmission.
Receiver accepts the data.
 

> Case-02: Remainder ≠ 0
 
- If the remainder is non-zero,
- Receiver assumes that some error occurred in the data during the transmission.
- Receiver rejects the data and asks the sender for retransmission.

## Checksum-
- Checksum is an error detection method.
- Error detection using checksum method involves the following steps-

> Step-01:
 
- At sender side,

- If m bit checksum is used, the data unit to be transmitted is divided into segments of m bits.
- All the m bit segments are added.
- The result of the sum is then complemented using 1’s complement arithmetic.
- The value so obtained is called as checksum.
 

> Step-02:

- The data along with the checksum value is transmitted to the receiver.

> Step-03:

- At receiver side,
- If m bit checksum is being used, the received data unit is divided into segments of m bits.
- All the m bit segments are added along with the checksum value.
The value so obtained is complemented and the result is checked.

> Then, following two cases are possible-

> Case-01: Result = 0
 
- If the result is zero,
- Receiver assumes that no error occurred in the data during the transmission.
Receiver accepts the data.

> Case-02: Result ≠ 0
 
- If the result is non-zero,
- Receiver assumes that error occurred in the data during the transmission.
Receiver discards the data and asks the sender for retransmission.

# MEDIUM/MULTIPLE ACCESS PROTOCOLS
- Consider a situation where-

- Multiple stations place their data packets on the link and starts transmitting simultaneously.
- Such a situation gives rise to a collision among the data packets.
- Collision of data packets causes the data to get corrupt.
- So, to prevent collisions we need Access Control

## METHODS:
![](https://user-images.githubusercontent.com/86204416/190206345-3362f44b-2de6-417c-bbe0-2b6ac850c8ec.png)

## Pure Aloha-
- It allows the stations to transmit data at any time whenever they want.
- After transmitting the data packet, station waits for some time.
- Then, following 2 cases are possible

> Case-01:

- Transmitting station receives an acknowledgement from the receiving station.
- In this case, transmitting station assumes that the transmission is successful.

> Case-02:

- Transmitting station does not receive any acknowledgement within specified time from the receiving station.
- In this case, transmitting station assumes that the transmission is unsuccessful.
- Then,
- Transmitting station uses a Back Off Strategy and waits for some random amount of time.
- After back off time, it transmits the data packet again.
- It keeps trying until the back off limit is reached after which it aborts the transmission.


## Slotted Aloha-
- Slotted Aloha divides the time of shared channel into discrete intervals called as time slots.
- Any station can transmit its data in any time slot.
- The only condition is that station must start its transmission from the beginning of the time slot.
- If the beginning of the slot is missed, then station has to wait until the beginning of the next time slot.
- A collision may occur if two or more stations try to transmit data at the beginning of the same time slot




## Terms:

- Congestion: Being Full / Not having Enough Space
    - Congestion, in the context of networks, refers to a network state where a node or link carries so much data that it may break down network service quality, resulting in queuing delay, frame or data packet loss and the blocking of new connections.

- Framing: Data Link Layer needs to pack bits into frames, So that each Frame is distinguishable from another
    - Example: We pack our letter in envolope and send it to the postal services.

## Unicasting - BroadCasting - Multicasting

- Cast : Kitne log, kitne bndo ko send kr rhe hai data

- Unicasting: (Uni - one, Cast - How many persons)
    - One to one Communication
    - This type of information transfer is useful when there is a participation of a single sender and a single recipient. 
    - So, in short, you can term it as a one-to-one transmission. 

- Broadcast: (To All)
    - Limited Broadcast
    - Direct Broadcast
    - Limited BroadCast - Sb logo ko send krna hai same network A ke andar hi, 90.0.0.0 is network and in network A, m1 want to send msg to all computer in same network A, we use Limited Broadcast, IP : 255.255.255.255
    - Direct Broadcast - Network A ke andar m1 want to send the msg to all computer network B, then IP : 92.255.255.255 where 92.0.0.0 is the network B IP
    - Example: News Channel is BroadCast

- Multicast: (paritcular group target) - Multicasting
    - IGMP Protocol Messaging
    - Class D IP's Used for Multicast

# Data Link Layer

## Bit Stuffing vs Byte Stuffing
- ![Gate Smashers - Lec-26 Framing in Data Link Layer Bit Stuffing vs Byte(Character) Stuffing  2U6kPu0dfqI - 885x498 - 2m24s](https://user-images.githubusercontent.com/35686407/190214844-663cdf0d-cf43-474d-9565-51afc96d8541.png)
- if there is flag in data then in data link layer we have to put ESC before flag in Data, to Distinguish between data flag and datalink layer flag.
- ![Gate Smashers - Lec-26 Framing in Data Link Layer Bit Stuffing vs Byte(Character) Stuffing  2U6kPu0dfqI - 885x498 - 2m51s](https://user-images.githubusercontent.com/35686407/190215103-6f9e0cdd-42dc-4546-989e-9f53a115a3e5.png)
- Byte Stuffing is the process of adding 1 extra byte whenever there is a flag or esc char in text
- 0 ke baad 5 one, we put 0 just after that
- 5 one ke baad 6 one aagye,, then it thinks it is not data it is header data
- ![Gate Smashers - Lec-26 Framing in Data Link Layer Bit Stuffing vs Byte(Character) Stuffing  2U6kPu0dfqI - 853x480 - 6m52s](https://user-images.githubusercontent.com/35686407/190215854-21fffbe2-6f9c-4198-a234-d40b4b84b5c5.png)
- above is bit studding

## Access Controls (Comes under Data Link Layer)

#### Links
1. Point to Point Link
    - dedicated link that exists between the two stations.
    - The entire capacity of the link is used for transmission between the two connected stations only.
    - ![](https://www.gatevidyalay.com/wp-content/uploads/2018/09/Point-to-Point-Link.png)

2. Broadcast Link
    - common link to which multiple stations are connected.
    -  capacity of the link is shared among the connected stations for transmission.
    -  ![](https://www.gatevidyalay.com/wp-content/uploads/2018/09/Broadcast-Link-1.png)

#### Access Control:
- mechanism that controls the access of stations to the transmission link.
- Need ? To prevent the occurrence of collision or if the collision occurs, to deal with it.
    - Consider a situation where-
        - Multiple stations place their data packets on the link and starts transmitting simultaneously.
        - Such a situation gives rise to a collision among the data packets.
        - Collision of data packets causes the data to get corrupt.
        - ![](https://www.gatevidyalay.com/wp-content/uploads/2018/09/Access-Control-Need-1.png)

#### Access Control Methods:
- Access control methods are the methods used for providing access control.
- They prevent the collision or deal with it and ensures smooth flow of traffic on the network.
- They are implemented at the data link layer of the OSI reference model.
- ![](https://www.gatevidyalay.com/wp-content/uploads/2018/09/Access-Control-Methods.png)

### Aloha
- ![](https://www.gatevidyalay.com/wp-content/uploads/2018/09/Aloha.png)

####   Pure Aloha: 
- It allows the stations to **transmit data at any time whenever they want.**
- After transmitting the data packet, station waits for some time.
- `Case 01`:
    - Transmitting station receives an acknowledgement from the receiving station.
    - In this case, transmitting station assumes that the transmission is successful.
- `Case 02`:
    - Transmitting station does not receive any acknowledgement within specified time from the receiving station.
    - In this case, transmitting station assumes that the transmission is unsuccessful.
    - Then,
    - Transmitting station uses a Back Off Strategy and waits for some random amount of time.
    - After back off time, it transmits the data packet again.
    - It keeps trying until the back off limit is reached after which it aborts the transmission.

- Vulnerable time: 
    - Time Line mae t point pr khadehai, transmission start kia,
    - 1,1 krke bit travel kr rhi hai Transmission Time
    - sari bts suppose 10ms leti hai transmission line mae utrne mae
    - ab is 10ms mae koi bhi or stataion transmission krna start kr dega collision hogi,
    - pure 10ms mae koi or station transmit na kre
    - ye 10ms hi vulnerable time hai
    - esa bhi ho skta hai koi or station bhi pehle transmisison start kr chuka hai
    - suppose it is also 10ms
    - then mera or uska msg bhi collide ho skta hai
    - 10ms + picle ka bhi 10ms tk kisi nae tranmit na kia ho
    - 2 * transmission time

#### Slotted Aloha
- Slotted Aloha divides the time of shared channel into discrete intervals called as time slots.
- Any station can transmit its data in any time slot.
- The only condition is that station must start its transmission from the beginning of the time slot.
- If the beginning of the slot is missed, then station has to wait until the beginning of the next time slot.
- A collision may occur if two or more stations try to transmit data at the beginning of the same time slot.

### Time Division Multiplexing (TDM)

- Time of the link is divided into fixed size intervals called as time slots or time slices.
- Time slots are allocated to the stations in Round Robin manner.
- Each station transmit its data during the time slot allocated to it.
- In case, station does not have any data to send, its time slot goes waste.

![](https://www.gatevidyalay.com/wp-content/uploads/2018/09/Time-Division-Multiplexing-Example-1.png)

> Size Of Time Slots- 

- The size of each time slot is kept such that each station gets sufficient time for the following tasks:
    - To put its data packet on to the transmission link
    - Last bit of the packet is able to get out of the transmission link
    - Size of each time slot = Tt + Tp

Disadvantage-

- If any station does not have the data to send during its time slot, then its time slot goes waste.
- This reduces the efficiency.
- This time slot could have been allotted to some other station willing to send data.


### CSMA / CD (Carrier Sense Multiple Access / Collision Detection).
- Sense The Carrier:
- Detecting The Collision
    - Transmission delay >= 2 x Propagation delay
- Releasing Jam Signal
- Waiting for BackOff Time

#### Sense the Carrier:
- Any station willing to transmit the data senses the carrier.
- If it finds the carrier free, it starts transmitting its data packet otherwise not.
- Each station can sense the carrier only at its point of contact with the carrier.
- It is not possible to sense the entire carrier
- Thus, there is a huge possibility that a station might sense the carrier free even when it is actually not.
- ![](https://www.gatevidyalay.com/wp-content/uploads/2018/09/CSMA-CD-1.png)

#### Detecting The Collision:
- It is the responsibility of the transmitting station to detect the collision.
- condition is followed by each station-Transmission delay >= 2 x Propagation delay
- According to this condition,
    - Each station must transmit the data packet of size whose transmission delay is at least twice its propagation delay.
    - If the size of data packet is smaller, then collision detection would not be possible.
    - Transmission delay = Length of data packet (L) / Bandwidth (B)
    - Propagation delay = Distance between the two stations (D) / Propagation speed (V)

![Screenshot Capture - 2022-09-14 - 23-01-16](https://user-images.githubusercontent.com/35686407/190223300-a9385f96-2908-43c9-8a1e-e171d5c5664d.png)

> Two cases are possible-

`Case-01:`
- If no collided signal comes back during the transmission,
- It indicates that no collision has occurred.
- The data packet is transmitted successfully.

`Case-02:`
- If the collided signal comes back during the transmission,
- It indicates that the collision has occurred.
- The data packet is not transmitted successfully.
- Step-03 is followed.

#### Releasing Jam Signal-
- Jam signal is a 48 bit signal.
- It is released by the transmitting stations as soon as they detect a collision.
- It alerts the other stations not to transmit their data immediately after the collision.
- Otherwise, there is a possibility of collision again with the same data packet.
- Ethernet sends the jam signal at a frequency other than the frequency of data signals.
- This ensures that jam signal does not collide with the data signals undergone collision.

#### Waiting For Back Off Time-
- After the collision, the transmitting station waits for some random amount of time called as back off time.
- After back off time, it tries transmitting the data packet again.
- If again the collision occurs, then station again waits for some random back off time and then tries again.
- The station keeps trying until the back off time reaches its limit.
- After the limit is reached, station aborts the transmission.

> Points:

- CSMA /CD is used in wired LANs.
- CSMA / CD is standardized in IEEE 802.3
- CSMA / CD only minimizes the recovery time.
- It does not take any steps to prevent the collision until it has taken place.

### CSMA/CA - Collision Avoidance
- used in WLAN
- isme collision avoidance krte hai 
- signal travel : energy loose,
- signal collide hone ke baad weak hota hai then double energy vala singal milega ni, then we use signal avoidance


### Polling
- A polling is conducted in which all the stations willing to send data participates.
- The polling algorithm chooses one of the stations to send the data.
- The chosen station sends the data to the destination.
- After the chosen station has sent the data, the cycle repeats.

![](https://www.gatevidyalay.com/wp-content/uploads/2018/09/Polling-Access-Control-Method.png)

> Advantages-

- It leads to maximum efficiency and bandwidth utilization.

> Disadvantages-

- Time is wasted during polling.
- Link sharing is not fair since each station has the equal probability of winning in each round.
- Few stations might starve for sending the data.


### Token Passing
- All the stations are logically connected to each other in the form of a ring.
- The access of stations to the transmission link is governed by a token.
- A station is allowed to transmit a data packet if and only if it possess the token otherwise not.
- Each station passes the token to its neighboring station either clockwise or anti-clockwise.
![](https://www.gatevidyalay.com/wp-content/uploads/2018/09/Token-Passing-Diagram.png)

> Assumptions

- Token passing method assumes-
    - Each station in the ring has the data to send.
    - Each station sends exactly one data packet after acquiring the token.

### LAN Technologies

![](https://www.gatevidyalay.com/wp-content/uploads/2018/10/Standard-LAN-Technologies.png)
- Ethernet is one of the standard LAN technologies used for building wired LANs.
- Ethernet uses bus topology.
- In bus topology, all the stations are connected to a single half duplex link.
- Ethernet uses CSMA / CD as access control method to deal with the collisions.
- Ethernet uses Manchester Encoding Technique for converting data bits into signals.
- For Normal Ethernet, operational bandwidth is 10 Mbps.
- For Fast Ethernet, operational bandwidth is 100 Mbps.
- For Gigabit Ethernet, operational bandwidth is 1 Gbps.

#### Ethernet Frame Format-
![](https://www.gatevidyalay.com/wp-content/uploads/2018/10/Ethernet-Frame-Format-IEEE-802.3.png)

- Preamble and Start Frame Delimiter is added by Physical Layer
- Other's are added by Data Link Layer

[LINK](https://www.gatevidyalay.com/ethernet-ethernet-frame-format/)

![Gate Smashers - Lec-39 Token Ring (IEEE 802 5) in Computer Networks  -u4Dzu63eZc - 885x498 - 5m14s](https://user-images.githubusercontent.com/35686407/190229632-1cbb8a0f-0b7d-4499-abae-758dda68e933.png)

![Screenshot Capture - 2022-09-14 - 23-37-41](https://user-images.githubusercontent.com/35686407/190229880-1c4ee723-a5bf-49fc-b96d-271829efbef9.png)

# IP Address in Networking (Host to Host Delivery By IP Address)

- IP Address is short for **Internet Protocol Address**.
- It is a **unique address** assigned to each computing device in an IP network.
- ISP assigns IP Address to all the devices present on its network.
- Computing devices use IP Address to identify and communicate with other devices in the IP network.

## Types
![](https://www.gatevidyalay.com/wp-content/uploads/2018/09/IP-Address-1.png)
1. Static
    - Static IP Address is an IP Address that **once assigned** to a network element **always remains the same.**
    - They are configured manually.
    - Some ISPs do not provide static IP addresses.
    - Static IP Addresses are more costly than dynamic IP Addresses.

2. Dynamic:
    - Dynamic IP Address is a **temporarily assigned IP Address** to a network element.
    - It can be assigned to a different device if it is not in use.
    - DHCP or PPPoE assigns dynamic IP addresses.
    - DHCP (Dynamic Host Configuration Protocol):
        - Dynamic Host Configuration Protocol (DHCP) is a client/server protocol that automatically provides an Internet Protocol (IP) host with its IP address and other related configuration information such as the subnet mask and default gateway.

## IP Address Format-
 
- IP Address is a **32 bit binary address** written as **4 numbers** **separated by dots**.
The **4 numbers** are called as **octets** where **each octet has 8 bits**.
The **octets** are **divided** into **2 components**- **Net ID and Host ID**.

![](https://www.gatevidyalay.com/wp-content/uploads/2018/09/Format-of-an-IP-Address.png)

- **Network ID** :  represents the IP Address of the network and is **used to identify the network.**
- **Host ID** :  represents the IP Address of the host and is **used to identify the host within the network.**

## IP Address Example-
1. Binary Representation : 00000001.10100000.00001010.11110000
2. Decimal Representation : 1.160.10.240

## There are two systems in which IP Addresses are classified-

1. Classful Addressing System
2. Classless Addressing System

### Classful Addressing System:

> 5 Classes:

1. **Class A** : If the 32 bit binary address **starts** with a **bit 0**,
2. **Class B** : If the 32 bit binary address **starts** with **bits 10**
3. **Class C** : If the 32 bit binary address **starts** with **bits 110**
4. **Class D** : If the 32 bit binary address **starts** with **bits 1110**
5. **Class E** : If the 32 bit binary address **starts** with **bits 1111**

|Class of IP Address|Network ID|Host ID|Usage|
|---|---|---|---|
|Class A|8 Bits|24 Bits|Class A is used by organizations requiring very large size networks like NASA, Pentagon etc.|
|Class B|16 Bits|16 Bits|Class B is used by organizations requiring medium size networks like IRCTC, banks etc.|
|Class C|24 Bits|8 Bits|organizations requiring small to medium size networks, e.g. engineering colleges, small universities, small offices etc.|
|Class D|-|-|Class D is reserved for multicasting. In multicasting, there is no need to extract host address from the IP Address.This is because data is not destined for a particular host.|
|Class E|-|-|Class E is reserved for future or experimental purposes.|

Total number of networks available = Number of Bits in NET ID
Total number of Hosts available =  Numbers possible due to available the Host ID

> Note: Range of First Octet in Class A is [1,126], because 2 networks are reserved. 

![Screenshot Capture - 2022-09-15 - 09-28-13](https://user-images.githubusercontent.com/35686407/190310734-28f223c9-5c57-42eb-9ee4-045e59ed9d14.png)


#### Points:
- All the hosts in a single network always have the same network ID but different Host ID.
- However, two hosts in two different networks can have the same host ID.
- A single network interface can be associated with more than one IP Address.
- There is no relation between MAC Address and IP Address of a host.
- IP Address of the network called Net ID is obtained by setting all the bits for Host ID to zero.
- In class A, total number of IP Addresses available for networks are 2 less.
    - This is to account for the two reserved network IP Addresses 0.xxx.xxx.xxx and 127.xxx.xxx.xxx.
    - IP Address 0.0.0.0 is reserved for broadcasting requirements.
    - IP Address 127.0.0.1 is reserved for loopback address used for software testing.
- In all the classes, total number of hosts that can be configured are 2 less.
    - This is to account for the two reserved IP addresses in which all the bits for host ID are either zero or one.
    - When all Host ID bits are 0, it represents the Network ID for the network.
    - When all Host ID bits are 1, it represents the Broadcast Address.
- Only those devices which have the network layer will have IP Address.
- So, switches, hubs and repeaters does not have any IP Address.


### Disadvantages:
- Wastage of IP Address
    - Class A : 2^24 = 1 Crore HOST Address, itne use nhi hote bde organizations mae bhi
    - 1 Crore is Very Huge
    - if organization says i need 1024 IP address, Class B mae 65K hai
    - class C mae 256 hai only, So, Wastage of IP Address
- Maintainance is Time Consuming
- More Prone to Errors














































































