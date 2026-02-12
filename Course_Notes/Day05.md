# Day 05 | Ethernet LAN Switching Pt. 1

## Miscellaneous Abbreviations
+ CRC = Cyclic Redundancy Check
+ OUI = Organizationally Unique Identifier

## Miscellaneous Notes
+ If an interface is labeled with "F" it means fast Ethernet so it runs at 100Mbps.


![image](https://github.com/psaumur/CCNA/assets/106411237/a40e81d9-c008-4fb4-8580-2eaf63003e63)

![image](https://github.com/psaumur/CCNA/assets/106411237/2db46525-98b8-4211-aeb3-efc34bd84222)


## LANs
+ A LAN is a network contained in a relatively small area.
+ Routers are used to connect separate LANs.
+ Switches don't separate LANs, but adding more can be used to expand an existing one.

![image](https://github.com/psaumur/CCNA/assets/106411237/2a4de9d4-3408-49b9-9492-42b7eb56fe27)


## Ethernet Frame

![image](https://github.com/psaumur/CCNA/assets/106411237/ad579917-f9a0-4cd8-be25-351ecbfc87af)

+ Header Fields
  + Preamble
    + Length: 7 bytes (56 bits)
    + Alternating 1's and 0's
    + 10101010 * 7x
    + Allows devices to synchronize their receiver clocks.
  + Start Frame Delimiter (SFD)
    + Length: 1 bytes (8 bits)
    + 10101011
    + Marks end of the Preamble and beginning of rest frame.
  + Destination: Layer 2 (MAC) address to which the frame is being sent.
  + Source: Layer 2 (MAC) address of the device which sent the frame.
  + Type: Indicates the Layer 3 protocol used in the encapsulated packet (almost always IP). Sometimes, and depending on the version of Ethernet, it's a length field that indicates the length of the encapsulated data.
    + 2 bytes (16-bit) field
    + A value of <mark>1500 or less</mark> in this field indicates the LENGTH of the encapsulated packet (in bytes).
    + A value of <mark>1536 or greater</mark> in this field indicates the TYPE of the encapsulated packet and length is determined via other methods.
    + IPv4 = 0x0800 (hexadecimal) = 2048 in decimal
    + IPv6 = 0x86DD (hexadecimal) = 34525 in decimal
    + Layer 3 protocol used in the encapsulated Packet, which is almost always Internet Protocol (IP) version 4 or version 6.
+ The Preamble and SFD are for synchronization and to allow the receiving deviceto be prepared to receive the rest of the data in the frame.
+ Trailer Fields
  + Frame Check Sequence (FCS): Used by the receiving device to detect any errors that might have occured during transmission.
    + 4 bytes (32 bits) in length
    + Detects corrupted data by running a CRC algorithm over the received data.
+ Total size of Ethernet frame is 26 bytes.

![image](https://github.com/psaumur/CCNA/assets/106411237/c8c1a143-0675-4aa4-83bc-6031d10cc0b8)


## MAC Address
+ **MAC Address** The 6 bytes (48-bit) address of the physical device. Assigned to a device when it's made.
+ AKA 'Burned-In Address'.
+ Globally unique
+ First 3 bytes are the OUI which is assigned to the company making the device
+ The last 3 bytes are unique to the device itself
+ Written as 12 hexadecimal characters.
+ Graphic: Decimal-Hexadecimal Chart
![image](https://github.com/psaumur/CCNA/assets/106411237/65a5e84a-b8db-46f5-b288-518139e99453)


## MAC ADDRESS TABLE

Each Switch stores a DYNAMICALLY LEARNED MAC ADDRESS TABLE, using the SOURCE MAC ADDRESS of frames it receives.

![image](https://github.com/psaumur/CCNA/assets/106411237/582421a9-6351-48b7-bfe1-c2153520920c)


When a Switch doesn't know the DESTINATION MAC ADDRESS of a frame (UNKNOWN UNICAST FRAME), it floods the frame— forward the frame out of all it's interfaces, except the one it received the packet from.

When a KNOWN Unicast Frame is known (MAC Address is recognized by the entry in the MAC ADDRESS TABLE), the frame is FORWARDED like normal.

![image](https://github.com/psaumur/CCNA/assets/106411237/ff731ab3-fad2-4e10-9fa7-ce583a6a0bb2)

+ On Cisco switches, dynamic MAC addresses are removed from its MAC Address Table after 5 minutes of inactivity.
+ A switch uses the source MAC address field of an Ethernet frame to populate its MAC Address Table.