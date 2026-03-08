# Day 17 | VLANs Pt. 2

+ VLANs can be dispersed amoung switches.


+ Graphic: Network Topology Example
  ![image](https://github.com/psaumur/CCNA/assets/106411237/d73b8f0b-2154-4e7f-8057-7c5b3f5078cc)
  
  + Notice this one has TWO Switches (SW1 and SW2) and ENGINEERING (VLAN 10) has two separate locations on the network.

## Trunk Ports
+ In a small network with few VLANS, it’s possible to use a separate interface for each VLAN when connecting switches to switches, and switces to routers.
+ Howver, when the number of VLANS increases, this isn't viable. It'll result in wasted interfaces, and often routers won’t have enough interfaces for each VLAN.
+ You can use trunk ports to carry traffic from multiple VLANS over a single interface.
+ Switches will “tag” all frames that they send over a trunk link. This allows the receiving switch to know which VLAN the frame belongs to.
+ Trunk Port AKA Tagged port, Access Port AKA Untagged port

## VLAN Tagging
+ 2 main trunk protocols:
  + Inter-Switch Link (ISL): An old Cisco propriety protcol created before the industry standard 802.1Q.
  + IEEE 802.1Q (AKA “dot1q”): An industry standard protocol created by the IEEE.
+ You will probably <mark>never</mark> use ISL in the real world; even modern Cisco equipment doesn’t use it.
+ dot1q Tag
  + In an Ethernet header, it's inserted between the source and type/length fields.
  + Length: 4 bytes (32 bits)
  + Consists of 2 main fields:
    + Tag Protocol Identifier (TPID)
    + Tag Control Information (TCI)
  + TCI consists of 3 sub-fields:
    + Priority Code Point (PCP)
    + Drop Eligible Indicator (DEI)
    + VLAN ID (VID)
+ TPID
  + Length: 16 bits (2 bytes)
  + Always set to a value of 0x8100. This indicates that the frame is 802.1Q-tag.
+ PCP
  + Length: 3 bits
  + Used for Class of Service (CoS), which prioritizes important traffic in congested networks.
+ DEI
  + Length: 1 bit
  + Used to indicated frames that can be dropped if the network is congested.
+ VID
  + Length: 12 bits
  + Identifies the VLAN the frame belongs to.
  + Length: 12 bits
  + 4096 total VLANS (2^12), range of 0 - 4095.
  + VLANs 0 and 4095 are reserved and can’t be used; therefore, the actual range of VLANs is 1 - 4094.

+ Graphic: Ethernet Header with 802.1Q
  ![image](https://github.com/psaumur/CCNA/assets/106411237/00e817cd-1cac-44c5-a5f6-5459d383236d)

+ Graphic: 802.1Q Tag
  ![image](https://github.com/psaumur/CCNA/assets/106411237/8e52856b-58b9-448e-a007-254973fe707e)


## VLAN Ranges
+ The range on VLANs (1 - 4094) is divided into 2 sections:
  + Normal: 1 - 1005
  + Extended: 1006 - 4094
+ Some older devices cannot use the extended VLAN range, however it's safe to expect that modern switches will.

## Native VLAN
+ dot1q has a featured called native VLAN. ISL doesn't have this feature.
+ The native VLAN is VLAN 1 by default on all trunk ports, however this can be manually configured.
+ The switches doesn't add an dot1q tag to frames in the native VLAN.
+ When a switch receives an untagged frame on a trunk port, it assumes the frame belongs to the native VLAN.
+ It's important that the native VLAN matches between switches.
+ If there's a native VLAN mismatch between switch interfaces, the frame will be dropped because the "tag" and destination don't match.

## Trunk Ports
+ Many modern switches don't support Cisco’s ISL at all. They only support 802.1Q (dot1q).
+ However, switches that do support both have a trunk encapsulation of “AUTO” by default.
+ To manually configure the interface as a trunk port, you must first set the encapsulation to “802.1Q” or “ISL”. On switches that only support 802.1Q, this isn't necessary.
+ Process
  1. Select the interface to configure in global config mode.
  2. Use `switchport trunk encapsulation dot1q` to set the encapsulation mode to 802.1Q.
    + Only necessary on switches that support both ISL and dot1q.
  3. Use `switchport mode trunk` to manually configure the interface to trunk.

+ Graphic: `switchport mode trunk` Command
  ![image](https://github.com/psaumur/CCNA/assets/106411237/29313a87-cf16-439c-8a9e-90b518326954)

+ Use the `show interfaces trunk` command to confirm interfaces on trunk.
  ![image](https://github.com/psaumur/CCNA/assets/106411237/6b897fb0-14a3-4e6a-b4e8-e278a6aec08e)

+ `switchport trunk allow vlan <Option>` command allows VLANs on a trunk.
+ Graphic: `switchport trunk allow vlan ?` Command\
  ![image](https://github.com/psaumur/CCNA/assets/106411237/6a60f6ce-55be-4df5-a715-b871e5e461f4)

+ Security purposes and network performance purposes, it's best to makes sure only the necessary traffic and VLANs can use a connection.
+ For security purposes, it's best to change the native VLAN to an unused VLAN.
+ `switchport trunk native vlan <VLAN #>` command to change the native VLAN.
+ `show vlan brief` command shows the access ports assigned to each VLAN, and <mark>not</mark> the trunk ports that allow each VLAN.
+ Use the `show interfaces trunk` command to confirm trunk ports.

## Router on a Stick (ROAS)
+ You must use sub-interfaces on a router when trunking (where one physical interface is being used for mutiple VLANs).
+ No additional configurations are needed on the switch.
+ Process
  1. Enable the interface with `no shutdown` in interface config mode.
  2. Enter sub-interface config mode via `interface <Interface>.<Sub-Interface #>`.
    + E.g., g0/0.10
  3. `encapsulation dot1q <Sub-Interfaces #>`
  4. Assign an IP address to the sub-interface.

+ Graphic: ROAS Process
  ![image](day17_image1)

+ The sub-interface number doesn't have to match the VLAN number. However, it's recommended because it makes it easier to understand.
+ Use `show ip interface brief` command to show sub-interfaces.
  ![image](https://github.com/psaumur/CCNA/assets/106411237/9b7ecbd1-c5f4-4ed0-9988-8fd17e16c9ae)

+ They also appear in the Routing Table in the `show ip route` command.
  ![image](https://github.com/psaumur/CCNA/assets/106411237/1e9bb3fa-5aca-4883-8aff-52a554dcfba6)

+ ROAS is used to route between multiple VLANs using a single interface on a router and switch.
+ The switch interface is configured as a regular trunk.
+ The router interface is configured using sub-interrfaces. You configure the VLAN tag and IP address on each sub-interface.
+ The router will behave as if frames arriving with a certain VLAN tag have arrived on the sub-interface configured with that VLAN tag.
+ The router will tag frames sent out of each sub-interface with the VLAN TAG configured on the sub-interface.