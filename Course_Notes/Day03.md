# Day 03 | How the TCP/IP Model Actually Works

## Miscellaneous Abbreviations
+ ARPA = Advanced Research Projects Agency
+ IEEE = Institute of Electrical and Electronic Engineers
+ IETF = Internet Engineering Task Force
+ RFC = Request for Comments
+ MAC = Media Access Control
+ NIC = Network Interface Card
+ ICMP = Internet Control Message Protocol
+ UDP = User Datagram protocol
+ TCP = Transmission Control protocol.
+ IP = Internet Protocol
+ PDU = Protocol Data Unit
+ OSI = Open Systems Interconnection
+ ISO = International Organization for Standardization

## Definitions
+ **Standard** An agreed-upon specification that describes how a protocol or technology should work.
+ **Hop** One step along the path between 2 devices. Switches don't count as hops, because they just extend the local network.

## History
+ Since the early days of computer networking, there have been several attempts to define the functions needed for computers to communicate with each other.
  + Often developed by specific vendors (e.g., IBM) to be used with their own products.
  + With a proprietary approach, enabling communications between different vendors’ products was difficult.
+ With vendor neutral standards, devices of all types can communicate with each other.
+ Early work on the computer networks that would evolve into today's Internet began in the 1960s.
  + The US Department of Defense's ARPA funded ARPANET, which came online in 1969 to connect mainframes at universities and labs.
  + Originally used a protocol called Network Control Program (NCP).
+ Vint Cerf and Bob Kahn (working at DARPA) began developing TCP in 1974.
  + Later divided into 2 protocols still used today: TCP and IP.
+ These 2 protocols form the foundation of the protocol suite known as TCP/IP today.
  + ARPANET fully switched to it on 1983-01-01.
+ TCP/IP began dominant over proprietary solutions because it was published as a set of open standards that any vendor could implement, and it could run over many different types of networks.

## Who Defines Standards?
+ Most networking standards are developed by independant standards organizations, not by a single vendor, with participation from engineers at many companies.
+ IEEE develops many of the technologies used on LANs: Ethernet (802.3) and Wi-Fi (802.11).
+ IETF defines protcols used on the Intenet (e.g., TCP, IP, UDP) and publishes standards in documents called RFCs.

## Layered Models
+ Networks do a lot of different jobs to move data between devices.
+ A model lets us group related jobs into layers.
  + Each layer has a specific job.
  + Each layer uses the services of the layer below and provides services to the layer above.
+ Proctols (mostly) live in one layer and together they form a stack of protocols that work as a team (the network stack).
+ The model is a description, not a law; different sources slightly different models.

## TCP/IP Model
![image](\CCNA_Course_Notes\Graphics\day03_image01.png)

+ Layers
  + Application (Layer 5): Procotols for communication between application processes; creates and interprets data.
    + Defnies how applications processes format, send, and interpret data.
    + Protocols at this layer define message formats and rules for specific tasks.
    + Key Protcols: HTTP, HTTPS, FTP, TFTP, SMTP, POP3, IMAP.
    + Network infrastructure devices (e.g., routers, switches) don't care about Application layer details.
      + They just move messages across the network.
      + Only the communicating hosts interpret the data.
  + Transport (Layer 4): Provides end-to-end communication between application processes using port numbers.
    + Uses port numbers to identify the processes on each host.
    + Runs mainly on the communicating host; routers normally operate based on IP addresses (Layer 3), not on Transport layer information.
    + Key Protocols: UDP, TCP.
  + Network (Layer 3): Provides end-to-end communication between hosts across networks using IP addresses and routers.
    + Uses IP addresses to identify hosts in a network.
    + Routers operate mainly at this layer, using the message's destination IP address to forward the message towards its final destination host.
    + Key Protcols: IPv4, IPv6, ICMP. 
  + Data Link (Layer 2): Provides hop-to-hop delivery within a local network using MAC addresses and switches.
    + Uses MAC addresses to identify interfaces.
    + Key Protcols: Ethernet (802.3) and Wi-Fi (802.11).
  + Physical (Layer 1): Sends bits as electrical, optical, or radio signals over the physical medium.
    + Defines things like cables, connectors, signal levels, and link speeds.
    + E.g., copper UTP cables, fiber-optic cables, Wi-Fi radio antennas, NICs.
+ Encapsulation
  1. The Application layer prepares the data to be sent over the network.
  2. As the message moves down the stack, each layer encapsulates the data with a header including the information needed for that layer.
    + E.g., port numbers, IP addresses.
    + Layer 2 also adds a trailer that the receiving device uses to check for transmission errors.
  3. The Physical layer transmits the bits as signals over the physical medium.
    + The L2 header is transmitted first, and te L2 trailer is transmitted last.
+ As the message moves down the stack, each layer encapsulates the data with a header including the information needed for that layer.
+ Decapsulation
  1. The receiving device receives the message as a stream of bits at Layer 1.
  2. The device examines the information in the Layer 2 header and trailer, and then removes them.
  3. The headers are continually removed as the message moves up the stack, until the data is delivered to the Application layer.
  4. The application presses the data and, if needed, generates a response that goes down back the stack to the sender.

## PDUs
+ At each stage in the encapsulation/decapsulation process, there's a name given to the message.
+ **Segment** The combination of data and a L4 header in TCP. AKA Layer 4 PDU (L4PDU).
+ **Datagram** The combination of data and a L4 header is called a datagram in UDP. AKA Layer 4 PDU (L4PDU).
+ **Packet** The combination of a segment/datagram and a L3 header. AKA Layer 3 PDU (L3PDU).
+ **Frame** The combination of a packet and a L2 header/trailer. What's sent over the wire. AKA Layer 2 PDU (L2PDU).
+ **Payload** The contents of each PDU (everything encapsulated by that layer's header/trailer).

## Layer Interactions
+ Adjacent Layer Interactions: Each layer provides a service to the layer above it, and is serviced by the layer below it.
  + Layer 4 provides a service to Layer 5 by delivering data to the correct application using port numbers.
  + Layer 3 provides a service to Layer 4 by delivering segments/datagrams to the correct destination using host IP addresses.
  + Layer 2 provides a service to Layer 3 by delivering packets to the next hop using MAC addresses.
  + Layer 1 provides a service to Layer 2 by sending and receiving frames as electrical, optical, or radio signals.
+ Same-Layer Interaction: Each layer communicates with the same layer on other devices.
  + E.g., A packet is addressed to the Layer 3 IP address of the destination host.
+ Separation of Layers: Each layer has its own job and provides a specific service to the layers above.
  + They are modular.
  + As long as each layer keeps its "contract" with the other layers, we can improve or replace protcols at different layers without redesigning everything.
  + This flexibility is one of the main benefits of a layered model.

## OSI Model
!!! ![image](Graphics\day03_image02.png)
+ In the late 1970s and 1980s, the ISO designed a 7-layer OSI model and a matching protocol suite.
  + The goal was to create an international, vendor-neutral networking standard that could unify existing proprietary stacks and potentially replace TCP/IP.
+ Governments promoted OSI as the preferred/recommended stack for new deployments.
+ OSI protocols ended up being late and complex, and never gained the same deployment as TCP/IP.
+ Today, almost al real networks use TCP/IP, but the OSI model survives as a reference/teaching model and a common way to talk about "layers".
+ Layers
  7. Application
  6. Presentation
  5. Session
  4. Transport
  3. Network
  2. Data Link: Provides node-to-node connectivity and data transfer (e.g., PC to switch).
    + Defines how data is formatted for transmission over a physical medium.
    + Detects and (possibly) corrects Physical layer errors.
  1. Physical
+ Defines physical characteristics of the medium used to transfer data between devices.
  + E.g., voltage levels, transmission distance, physical connectors, cable specifications, etc.
+ Digital bits are converted into electrical (for wired connections) or radio (for wireless connections) signals.