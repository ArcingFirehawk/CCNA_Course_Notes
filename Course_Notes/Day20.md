# 20. Day 20 | STP Pt. 1

## Abbreviations
+ NIC = Network Interface Card
+ BDPU = Bridge Protocol Data Unit
+ STP = Spanning Tree Protocol

## Redundancy in Networks
+ Essential part of network design.
+ Modern networks are expected to run 24/7/365; even a short downtime can be disastrous for business.
+ If one network component fails, you must ensure that other components will take over with little or no downtime.
+ As much as possible, you must implement redundancy at every possible point in the network.

+ Graphic: Poorly Designed Network Example
  ![image](https://github.com/psaumur/CCNA/assets/106411237/b3b76af5-11e6-495b-8c40-40eb5800704b)

  + Note the many single-point failures that could occur (single connections).
<br></br>

+ Graphic: Better Designed Network Example
  ![image](https://github.com/psaumur/CCNA/assets/106411237/01c20d92-2cf6-4d1f-a193-ded7753aeb38)
<br></br>

+ Most PCs only have a single network interface card (NIC), so they can only be plugged into a single single. However, important servers typically have multiple NICs, so they can be plugged into multiple switches for redundancy.

## Problems in Redundant Networks Without STP
+ Broadcast Storm
  + The Ethernet header doesn't have a TTL field, so broadcast frames will loop around the network indefinitely.
  + If enough of these looped broadcasts accumulate in the network, the network will be too congested for legitimate traffic to use the network.
  + Graphic: Broadcast Storm Example
    ![image](https://github.com/psaumur/CCNA/assets/106411237/f719de69-df9e-4549-b3cb-914d7c5aabc4)
+ MAC Address Flipping
  + Each time a frame arrives on a switchport, the switch uses the source MAC address field to “learn” the mac address and update it’s MAC Address Table.
  + When frames with the same source MAC address repeatedly arrive on different interfaces, the switch is continuously updating the interface in it’s MAC Address Table.
+ Spanning Tree Protocol is one solution.

## Spanning Tree Protocol (STP)
+ Classic Spanning Tree Protocol is IEEE 802.1D.
+ Switches from <mark>all</mark> vendors run STP by default.
+ STP prevents layer 2 loops by placing redundant ports in a blocking state, essentially disabling the interface
+ These interfaces act as backups that can enter a forwarding state if an active (currently forwarding) interface fails.
+ Interfaces in a blocking state only send or receive STP messages (called BDPUs).
+ STP still uses the term "bridge". However, when we use it, we really mean "switch". bridges aren't used in modern networks.
+ If changes occur in the connections, the traffic will adjust the topology.
+  By selecting which ports are forwarding and which ports are blocking, STP creates a single path to/from each point in the network. this prevents L2 loops.
+ There's a set process that STP uses to determine which ports should be forwarding and which should be blocking.
+ STP-enabled switches send/receive Hello BDPUs out of all interfaces. The default timer is 2 seconds.
+ if a switch receives a Hello BDPU on an interface, it knows that interface is connected to another switch.
  + Routers, PCs, etc. don't use STP so they don't send Hello BDPUs.

## What are BDPUs used for?
  + Switches use one field in the STP BDPU: the Bridge ID field, to elect a root bridge for the network.
  + The switch with the lowest Bridge ID becomes the root bridge.
  + All ports on the root bridge are put in a forwarding state, and other switches in the topology must have a path to reach the root bridge.
+ Bridge ID v1 Field
  + Bridge Priority
    + Length: 4 bits
    + The default value is 32768 on all switches, so by default the MAC address is used as a tie-breaker.
  + Extended System ID
    + AKA VLAN ID
    + Length: 12 bits
    + Cisco switches use a version of STP called PVST. It runs a separate STP "instance" in a VLAN, so in each VLAN different interfaces can be forwarding/blocking.
  + MAC Address 
    + Length: 48 bits
    + Lowest value becomes the root bridge.
  + The bridge priority is compared first, if they tie the MAC address is then compared.
+ Bridge ID v2 Field
  + Bridge Priority
    + Length: 16 bits
    + The default value is 32768 on all switches, so by default the MAC address is used as a tie-breaker.
  + MAC Address 
    + Length: 48 bits
    + Lowest value becomes the root bridge.
  + The bridge priority is compared first, if they tie the MAC address is then compared.
+ Graphic: Bridge ID Field
  ![image](day20_image01!!!)

+ In the default VLAN of 1, the default bridge priority is actually 32769.
+ The bridge priority + extended system ID is a single field of the bridge ID, however the latter is set and cannot be changed (because it's determined by the VLAN ID).
  + Therefore, you can only change the bridge priority (bridge priority + extended system ID) in units 4096, the value of the least significant bit of the bridge priority.
+ Graphic: Changing Bridge Priority Demo
  ![image](https://github.com/psaumur/CCNA/assets/106411237/bb49a034-9f6d-4e92-9ea0-8bc71c4f2ec8)
+ All interfaces on the root bridge are designated ports. Designated ports are in a forwarding state.

## Root Bridge
+ When a switch is powered on, it assumes it is the root bridge
+ It'll only give up its position if it receives a “superior” BDPU (lower Bridge ID).
+ Once the topology has converged and all switches agree on the root bridge, only the root bridge sends BDPUs.
+ Other switches in the network will forward these BDPUs, but will not generate their own original BDPUs.

## Root Cost
+ The total cost of the outgoing interfaces along the path to the root bridge.
+ Each interface has an associated spanning tree cost.
+ Only outgoing interfaces toward the root bridge have a STP cost; not receiving interfaces.
+ Graphic: STP Cost Chart
  ![image](https://github.c77om/psaumur/CCNA/assets/106411237/0ee95883-aed8-42a3-ba82-11209ef8cd40)
+ The root bridge's interfaces have a cost of 0.
+ The ports connected to another switch’s root port <mark>must</mark> be designated.
  + Because the root port is the switch’s path to the root bridge, another switch must not block it.

## Port ID
+ `show spanning-tree` lists, among other things, the spanning tree port ID on each interface on the switch.
+ STP Port ID = Port Priority (default 128) + Port #

## Preventing L2 Loops
+ Every collision domain has a single STP designated port.
+ 

## STP Steps
1. One switch is elected as root bridge. All ports on the root bridge are designated ports (forwarding state). Root bridge selection order:
    1. Lowest Bridge ID
    2. Lowest MAC Address
2. Each remaining switch will select <mark>one</mark> of its interfaces to be it’s root port (forwarding state). Ports across from the root port are always designated ports. Root port selection order:
  1. Lowest root cost
  2. Lowest neighbour bridge ID
  3. Lowest neighbour port ID
3. The remaining collision domain will select <mark>one</mark> interface to be a designation port (forwarding state). The other port in the collision domain will non-designated (blocking). Designated port selection:
  1. Interface on switch with lowest root cost
  2. Interface on switch with lowest bridge ID










!!!

ALL SWITCHES have the same PRIORITY NUMBER (32769)

Tie-breaker goes to the LOWEST MAC ADDRESS

SW3 has the LOWEST so it’s the ROOT BRIDGE and ALL it’s INTERFACES become DESIGNATED

Connections from SW1 (G0/1) and S4 (G0/0) to SW3 become ROOT INTERFACES

Because SW2 has TWO connections to SW1, both of SW1’s INCOMING interfaces become DESIGNATED.

SW2 G0/2 INTERFACE becomes a ROOT INTERFACE because the G0/0 INTERFACE of SW1 is LOWER than it’s G0/2 INTERFACE

The remaining interfaces on SW2 become NON-DESIGNATED because it has the HIGHEST ROOT COST (12 = 4x 1 GB connection). INTERFACES they are attached to on other SWITCHES become DESIGNATED

#2

![image](https://github.com/psaumur/CCNA/assets/106411237/ae382ec2-9c0f-4673-94b5-5d1411c8db6b)


SW4 has the LOWEST Priority Number so it is designated ROOT BRIDGE

All of SW4 INTERFACES become DESIGNATED

SW2 G0/0 becomes ROOT PORT because SW4 G0/0 connection is a LOWER NUMBER than G0/1. 

SW3 G0/1 becomes ROOT PORT

SW1 G0/1 becomes ROOT PORT because G0/1 cost is LESS than Fa1/0 and 2/0

EACH remaining PORT will be either DESIGNATED or NON-DESIGNATED

SW1 Fa1/0 and 2/0 become NON-DESIGNATED since they have a HIGHER STP COST (38) than SW2 outbound ports (8) making SW2 Fa1/0 and 2/0 DESIGNATED

SW2 remaining connection, G0/1, NON-DESIGNATED


