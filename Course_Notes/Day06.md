# Day 05 | Ethernet LAN Switching Pt. 2

## Miscellaneous Abbreviations
+ VLAN = Virtual Local Area Network

## Definitions
+ **Broadcast** A method of transferring a message to all connected devices simultaneously.
+ **Unicast** A method of transferring a message to a single connected device..

## Miscellaneous Notes
+ If an interface is labeled with "G" it means Gigabit Ethernet so it runs at !!!.
+ Each hexadecimal digit is 4 bits; 2 digits = 1 byte.

## Ethernet Frame (Cont.)
+ The Preamble and SFD aren't usually considered part of the Ethernet header, but is sent with every Ethernet frame.
  + Therefore the size of the Ethernet header + trailer = 18 bytes.
+ The minimum size for an Ethernet Frame (Header + Payload [PACKET] + Trailer) is 64 bytes.
+ 64 Bytes - 18 Bytes (Header + Trailer size) = 46 bytes.
+ Therefore the minimum payload (packet) size is 46 bytes.
+ If the payload is less than 46 bytes, padding bytes (all 0s) are added.

## Address Resolution Protcol (ARP)
+ When a PC wants to send a packet to a destination with a known IP address but unknown MAC address, it first needs to send an ARP Request to learn the  destination's MAC address.

![image](https://github.com/psaumur/CCNA/assets/106411237/e2d0e5d2-7c98-4671-b356-903132fd7525)

+  It's used to discover the Layer 2 address (MAC address) of a known Layer 3 address (IP address).
+ Process consists of 2 messages:
  + ARP Request: Broadcast.
  + ARP Reply: Unicast.
+ ARP Table: Stores IP address-MAC address associations.
  + Use the `arp -a` command to view it. On Cisco devices use `show arp` in priviledged EXEC mode.
  + Displays IP addresses, MAC addresses, and a Type (denotes how the association was learned).
+ ARP Request Frame
  + Source IP Address
  + Destination IP Address
  + Source MAC address
  + BROADCAST MAC Address - FFFF.FFFF.FFFF

An ARP REPLY frame has:

- Source IP Address
- Destination IP Address
- Source MAC address
- Destination MAC Address

ARP REPLY is a known UNICAST frame = Sent only to the host that sent the ARP REQUEST.

![image](https://github.com/psaumur/CCNA/assets/106411237/914cdf2a-c631-47e5-80f9-46e32ebed311)

## Ping
+ A network utility that is used to test reachability.
+ Measures round-trip time.
+ The PC sending this must know the MAC address of the destination host.
+ Process consists of 2 messages:
  + ICMP Echo Request: 
  + ICMP Echo Reply
+ Unicast
+  Command: `ping <ip-address>`

## MAC Address Table
+ Use `show mac address-table` in priviledged EXEC mode to show the MAC Address Table on Cisco devices.
+ Displays: VLAN, MAC Addresses, Type, and Ports.
+ **Aging** On Cisco switches, dynamic MAC addresses are automaticallly removed from the MAC address table after 5 minutes of inactivity.
+ `clear mac address-table dynamic` to clear the table's dynamic MAC addresses.
+ `clear mac address-table dynamic address <MAC Address>` to clear a specific MAC address.
+ `clear mac address-table dynamic interface <Interface>` to clear all MAC addresses for a specific interface.