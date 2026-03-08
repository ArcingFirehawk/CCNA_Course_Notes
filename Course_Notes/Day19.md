# Day 19 | DTP and VTP
+ NOTE: These topics aren't on the CCNA exam.

## Miscellaneous Abbreviations
+ NRAM = Non-Volatile RAM


## Dynamic Trunking Protocol (DTP)
+ A Cisco propriety protocol that allows Cisco switches to dynamically determine their interface status (access or trunk) without manual config.
  + Manually configuring switchports using `switchport mode access` or `switchport mode trunk is not needed.
  + Enabled by default on all Cisco switch interfaces.
+ For security purposes, manual configuration is recommended. DTP should be disabled on <mark>all</mark> switchports.
+ `show interfaces <interface-id> switchport` will show you a switchport’s settings.
  ![image](https://github.com/psaumur/CCNA/assets/106411237/bf716a33-8e11-4c09-bb0b-336ba48ef26d)
+ Modes
  + Dynamic Desireable: A switchport will actively try to form a trunk with other Cisco switches.
     + Will form a trunk if connected to another switchport in the following modes: `switchport mode trunk`, `switchport mode dynamic desirable`, and `switchport mode dynamic auto`.
     + If the other interface is set to "static access" (access mode), it won't form a trunk, it'll be an access port.
  + Dynamic Auto: A switchport will not actively try to form a trunk with other Cisco switches. However, it'll form a trunk if it's connected to a switch that's actively trying to form a trunk.
    + Will form a trunk if connected to another switchport in the following modes: `switchport mode trunk` and `switchport mode dynamic desireable`.
    + Trunk to access connection will operate in a mismatched mode. This configuration doesn't work; it should result in an error and traffic won't pass through.
+ Graphic: Resulting operational mode given 2 administrative modes.
  ![image](https://github.com/psaumur/CCNA/assets/106411237/93d5e4f4-cb24-4d3f-ba62-fd002581cfbb)
<br></br>

+ Will not form a trunk with a: router, PC, etc. The switchport will be in access mode.
+ On older switches, `switchport mode dynamic desirable` is the default administrative mode.
+ On newer switches, `switchport mode dynamic auto` is the default administrative mode.
+ You can disable DTP negotiation on an interface with the commands `switchport nonegotiate` and `switchport mode access`.
+ It's a security recommendation to disable DTP on all switchports and manually configure them as access or trunk ports.
+ Switches that support both 802.1Q and ISL trunk encapsulations can use DTP to negotiate the encapsulation they'll use.
+ Negotiation is Enabled by default as the trunk encapsulation mode is `switchport trunk encapsulation negotiate`.
+ ISL is favored over 802.1Q, so if both switches support ISL it will be selected.
- DTP frames are sent in VLAN1 when using ISL or in the native VLAN when using 802.1Q (the default native VLAN is VLAN1, however).

## VLAN Trunking Protocol (VTP)
+ Allows you to configure VLANs on a central VTP server switch, and other switches (VTP clients) will synchronize their VLAN database to the server.
+ Designed for large networks with many VLANs, so that you don't have to configure each VLAN on every switch.
+ It's rarely used, and it's recommended that you don't use it.
+ 3 Versions: 1, 2, and 3.
+ 3 Modes: server, client, and transparent.
+ Cisco switches operate in VTP server mode by default.
+ VTP Servers
  + Can add, modify, or delete VLANs.
  + Stores the VLAN database in NRAM.
  + Will increase the revision # every time a VLAN is added, modifed,, or deleted.
  + Will advertise the latest version of the VLAN database on trunk interfaces, and the VTP cilents will sync their VLAN databases to it.
  + Also functions as VTP clients.
  + Will sync to another VTP server with a higher revision number.
+ VTP Clients
  + Cannot add, modify, or delete VLANs.
  + Doesn't store the VLAN database in NRAM (in VTPv3 they do).
  + Will sync their VLAN database to the server with the highest revision # in their VTP domain.
  + Will advertise their VLAN database, and foward VTP advertisements to other clients over their trunk ports.
+ VTP Versions
  + v1: Doesn't support the extended VLAN range (1006-4094).
  + v2
    + Doesn't support the extended VLAN range (1006-4094).
    + Supports token ring VLANs.
    + Not much different from v1; if you're using token ring VLANs use v2, otherwise use v1.
  + v3
    + Does support the extended VLAN range (1006-4094).
    + Clients store VLAN database in NVRAM.
+ By default the domain name is null. If you want VTP to sync among devices, you'll need to configure them with the same domain name.
+ If a switch with no domain name receives a VTP advert with a VTP domain name, it'll automatically join that domain.
+ If you connect and old switch with a higher revision # to your network and the VTP domain name matches, all switches in the domain will sync their VLAN database to that switch.
+ VTP Transparent Mode
  + Doesn't participate in the VTP domain (doesn't sync its VLAN database).
  + Maintains its own VLAN database in NRAM. Can add, modify, and delete VLANs, but they won't be advertised to other switches.
  + Will forward VTP adverts that are in the same domain name as it.
+ Changing the VTP domain to and unused one or changing the VTP mode to transparent will reset the revision #.
+ Commands
  + `show vtp status` shows VTP information on a switch.
  + `vtp domain <name>` changes the VTP domain's name.
  + `vtp mode <mode` chasnges the VTP mode.
  + `vtp version <version #>` changes the VTP version.
+ Graphic: VTP Mode Functions
  ![image](https://github.com/psaumur/CCNA/assets/106411237/87dcd7ff-f3d3-4441-841c-a0506c249f03)