# Day 16 | VLANs Pt. 1

## What is a LAN?
+ **Local Area Network (LAN)** A single broadcast domain, including all devices in that domain.
+ **Broadcast Domain** The group of devices which will receive a broadcast frame (Destination MAC: FFFF.FFFF.FFFF) sent by any one of the members.
+ Lots of unnecessary broadcast traffic can reduce network performance.
+ Even within the same office, you want to limit who has access to what. You can apply security policies on a router or firewall. Because this is one LAN, PC’s can reach each other directly, without traffic passing through the router. So, even if you configure security policies, they won’t have any effect.
+ Even if a network is separated into subnets (Layer 3), they might still be on the same broadcast domain (Layer 2).


Image of LAN with FOUR BROADCAST DOMAINS (192.168.1.0 / 24)

![image](https://github.com/psaumur/CCNA/assets/106411237/de712483-e881-41f5-9525-576216186498)




![image](https://github.com/psaumur/CCNA/assets/106411237/a807fdc5-27b9-4735-8b8d-51bdc0c91a8c)


BROADCAST FRAME flooding all our subnets with unnecessary traffic.

![image](https://github.com/psaumur/CCNA/assets/106411237/fcd03904-a193-4423-8940-09be1df1bd2c)


Security :



![image](https://github.com/psaumur/CCNA/assets/106411237/7bd562fc-7dff-4692-81d7-c026b007df8f)

---

## What is a VLAN?
+ VLAN = Virtual Local Area Network
+ Networks can be logically separated through configurations on the switch.
  + Configure an interface to be a part of a specific VLAN and connect the endhost to that interface.
+ VLANs
  + Logically separate end-hosts at Layer 2.
  + Are configured on Layer 2 switches on a per-interface basis.
  + any endhosts connected to that interface will be part of that VLAN.
+ A switch <mark>won't</mark> forward traffic directly between VLANs, incuding broadcast/unknown unicast traffic.
+ Switches don't perform inter-VLAN routing. It must send the traffic through a router.
+ Purpose
  + Reduces unnecessary broadcast traffic, which helps prevent network congestion and improve network performance.
  + Limits broadcast and unknown unicast traffic; improves network security, since messages won’t be received by devices outside of the VLAN.

## VLAN Configuration on Cisco Switches
+ `show vlan brief` in global config mode displays the VLANs that exist on the switch and which interfaces are in each VLAN.
+ "default" is the VLAN all interfaces are assigned to by default.

+ Graphic: Example of `show vlan brief` Command 
  ![image](https://github.com/psaumur/CCNA/assets/106411237/13ce8382-6aea-484e-9580-d91c98189522)

+ VLANs 1 and 1002-1005 exist by default and <mark>cannot be deleted</mark>.
+ Steps
  1. Use the `interface range <interfaces>` command to select all relevant interfaces at once.
  2. Use the `switchport mode access` command to set the interface as an access port.
  3. Use the `switchport access <VLAN #>` command to assign a VLAN to a port.
    + If a VLAN doesn't exist, it'll be created automatically.
+ **Access Port** A switchport which belongs to a single VLAN, and usually connects to end hosts.
+ VLAN Config Mode
  + `vlan <VLAN #>` is used to create a VLAN or configure it.
  + `name <VLAN name>` assigns a name to the VLAN.
---

HOW TO ASSIGN INTERFACES TO A VLAN

![image](https://github.com/psaumur/CCNA/assets/106411237/ed31145d-7949-4c68-b88a-97716beaf074)


1) 

2) 

---

WHAT IS AN ACCESS PORT?

- An ACCESS PORT is 

SWITCHPORTS which carry multiple VLANs are called “TRUNK PORTS” (more info on TRUNK in next chapter)

3) 

![image](https://github.com/psaumur/CCNA/assets/106411237/b1bdb937-3707-496f-bc49-445df354d16b)


Use “#vlan <#>” to enter **Configuration Mode** for a given VLAN (this can also create a VLAN)

Use “#name <name>” to configure a NAME for your VLAN

To check your VLAN configuration, use “#show vlan brief”

![image](https://github.com/psaumur/CCNA/assets/106411237/2f7d26d8-9b2a-43a3-b213-fec4f984a309)


Testing VLAN 10

Pinging from PC1 using 255.255.255.255 (FFFF:FFFF:FFFF) floods broadcast packets to R1 and VLAN10 hosts only

![image](https://github.com/psaumur/CCNA/assets/106411237/5c64e485-f492-4436-9c1d-3a1ab20fbe05)
