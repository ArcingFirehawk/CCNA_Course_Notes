# Day 11A | Routing Fundamentals

## Routing
+ **Routing** The process that a router uses to determine the path that an IP packet should take reach their destination.
+ Routers store routes to all their known destinations in a Routing Table.
+ When routers receive packets, they look in the Routing Table to find the best route to forward that packet.
+ 2 Main Routing Methods
  + Dynamic Routing: Routers use Dynamic Routing Protocols (e.g., OSPF) to share routing information with each other automatically and build their routing tables.
  + Static Routing: Routes are mannually configured on a router.
+ A route tells the router:
  + To send a packet to Destination X, you should send the pack to next-hop Y.
  + Or if the destination is directly connected to the router, send the packet directly to the destination.
  + Or if the destination is the router’s own IP address, receive the packet for yourself (don’t forward it).

![image](https://github.com/psaumur/CCNA/assets/106411237/8ceefb10-d70d-4530-969d-40347ed34297)


+ **Wide Area Network (WAN)** A network that extends over a large geographic area.

## Cisco Router CLI
+ `show ip route` command displays the Codes Legend (lists the different protocols which routers can use to learn routes) and the router's Routing Table.
+ Some Codes
  + Local (L): A route to the actual IP address configured on the interface. Has a /32 netmask.
  + Connected (C): A route to the network the interface is connected to. Has the actual netmask configued on the interface.
+ When you configure an IP address on an interface and enable it, 2 routes (per interface) will automatically be added to the routing table: a connected and local route.
+ **Connected Route** A route to the network the interface is connected to.
  + + A router matches a packet's destination if the packet's destination IP address is part of the network specified in the route.
+ **Local Route** A route to the exact IP address configured on the interface. Specified by a /32 netmask.

## Router Behaviors
+ If a packet is matched by mutliple routes, it'll use the most specific one.
  + This is different to switches, which look for an exact match in the MAC Address Table to forward frames.
+ If a router has a packet no matching routes to its routing table, it'll drop it.
  + Switches flood frames if they don't know where the destination is.




---

![image](https://github.com/psaumur/CCNA/assets/106411237/b3555fdd-37a4-4bc8-b998-76e0b5455bb1)

![image](https://github.com/psaumur/CCNA/assets/106411237/99e75230-de1c-4f48-acd0-3482bba256af)

![image](https://github.com/psaumur/CCNA/assets/106411237/13a77d5c-497d-49ca-9717-ea3bb4a560d0)

![image](https://github.com/psaumur/CCNA/assets/106411237/6e3a2b3b-1590-4625-9bcf-cdaed95738d2)

![image](https://github.com/psaumur/CCNA/assets/106411237/891fcfbe-7dc5-4fb2-9b02-c6905236761e)
