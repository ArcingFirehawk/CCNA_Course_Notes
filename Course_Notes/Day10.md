# Day 10 | IPv4 Header

## Miscellaneous Abbreviations
+ QoS = Quality of Service
+ MTU = Maximum Transmission Unit
+ OSPF = Open Shortest Path First

## Review
INTERNET PROTOCOL version 4 HEADER or IPv4 HEADER

HEADER is used at LAYER 3 to help send data between devices on separate networks, even on other sides of the world over the Internet.

This is known as ROUTING.

THE IPv4 HEADER is used to ENCAPSULATE a TCP or UDP Segment.

To Review:

![image](https://github.com/psaumur/CCNA/assets/106411237/64906e3c-0bae-4c2c-96ca-4e6850f3844a)


---

## IPv4 Header Fields

![image](https://github.com/psaumur/CCNA/assets/106411237/f2667488-2769-4e62-bee7-eddbf9e00058)


| Field | # of Bits |
| --- | --- |
| VERSION | 4 |
| IHL | 4 |
| DSCP | 6 |
| ECN | 2 |
| TOTAL LENGTH | 16 |
| IDENTIFICATION | 16 |
| FLAGS | 3 |
| FRAGMENT OFFSET | 13 |
| TIME TO LIVE | 8 |
| PROTOCOL | 8 |
| HEADER CHECKSUM | 16 |
| SOURCE ADDRESS | 32 |
| DESTINATION ADDRESS | 32 |
| OPTIONS | 320 Max |

## Version
+ Length: 4 bits
+ Identifies the version of IP used—either IPv4 or IPv6.
+ IP IDs
  + IPv4 = 0100 in Binary (Decimal 4)
  + IPv6 = 0110 in Binary (Decimal 6)

---

## Internet Header Length (IHL)
+ Length: 4 bits
+ Final field of IPv4 Header (Options) is variable in length, so this field is necessary to indicate the total length of the header.
+ Identifies length of  header <mark>in 4-byte increments</mark>.
  + E.g., Value of 5 = 5 * 4-bytes = 20 bytes
+ Minimum Value: 5 (5 * 4-bytes = 20 bytes); indicates an empty Options field.
+ Maximum Value: 15 (15 * 4-bytes = 60 bytes)
+ Minimum IPv4 Header length is 20 bytes.
+ Maximum IPv4 Header length is 60 bytes.

## Differentiated Services Code Point (DSCP)
+ Length: 6 bits
+ Used for QoS.
+ Used to prioritize delay-sensitive data.
  + E.g., streaming voice, video, etc.

## Explicit Congestion Notification (ECN)
+ Length: 2 bits
+ Provides end-to-end (between two endpoints) notification of network congestion <mark>without dropping packets</mark>.
+ Optional feature that requires both endpoints, as well as the underlying network infrastructure to support it.

## Total Length
+ Length: 16 bits
+ Indicates the <mark>total</mark> length of the packet (L3 Header + L4 Segment).
+ Measured in singular bytes.
+ Minimum Value: 20 bytes; indicates an IPv4 header with no encapsulated data.
+ Maximum Value: 65,535; the maximum 16-bit value.

## Identification
+ Length: 16 bits
+ If a packet is fragmented, this field is used to identify which packet the fragment belongs to.
+ All fragments of the same packet will have their own IPv4 header with the same value in this field.
+ Packets are fragmented, if larger than the MTU.
+ The MTU is usually 1500 bytes (max size of an Ethernet frame).
+ Fragments are reassembled by the receiving host.

## Flags
+ Length: 3 bits
+ Used to control/identify fragments.
+ Bit 0: Reserved, always set to 0.
+ Bit 1: Don't Fragment (DF-bit), used to indicate a packet that should not be fragmented.
+ Bit 2: More Fragments (MF-bit), set to 1 if there are more fragments in the packet, set to 0 for the last fragment or no fragments.
+ If you send pings larger than the the MTU and set the DF-bit, it'll fail to send.

## Fragment Offset
+ Length: 13 bits
+ Used to indicated the position of the fragment within the original, unfragmented IP packet.
+ Allows fragmented packets to be reassembled even if the fragments arrive out of order.


## Time to Live (TTL)
+ Length: 8 bits
+ A router will drop a packet with a TTL of 0.
+ Used to prevent infinite loops.
+ Originally designed to indicated a packets maximum lifetime in seconds.
+ In practice, indicates a "hop count"; where each time the packet arrives at a router, the router decreases the TTL by 1.
+ Recommended default TTL is 64. 

## Protocol
+ Length: 8 bits
- Indicates the protocol of the encapsulated L4PDU.
+ Values
  + 1: ICMP
  + 6: TCP
  + 17: UDP
  + 89: OSPF
- Full List of protocol numbers on Wikipedia (https://en.wikipedia.org/wiki/List_of_IP_protocol_numbers).

## Header Checksum
+ Length: 16 bits
- A calculated checksum used to check for errors in the IPv4 header.
- When a router receives a packet, it calculates the checksum of the header and compares it to the one in this field of a header.
- If they don't not match, there was an error in tansmission and router drops packet.
- <mark>Only</mark> checks for errors in IPv4 Header.
- IP relies on the encapsulated protocol to detect errors in the encapsulated data.
- Both TCP and UDP have their own checksum fields to detect errors in the encapsulated data.

## Source/Destination IP Address
+ Length: 32 bits each
- Source IP is IPv4 address of packet's sender.
- Destination IP is IPv4 address of packet's intended receiver.

## Options
- Length: 0-320 bits
- Optional/Rarely Used
- If the IHL field is greater than 5, it means that Options are present.