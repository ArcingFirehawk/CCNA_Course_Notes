# Day 09 | Switch Interfaces

![image](https://github.com/psaumur/CCNA/assets/106411237/5d0d80dc-74d1-4656-841c-fcaa2b89c760)


## CISCO Switch CLI


+ `enable` command to enter privileged EXEC mode.
+ `show ip interface brief` command in privileged EXEC mode shows the interfaces currently on the switch.
  + Has the same information structure as Cisco Routers.

![image](https://github.com/psaumur/CCNA/assets/106411237/e3947ef5-9100-426f-8d62-fd4ce5224351)

+ Router interfaces will have the `shutdown` command applied by default; thus being in the "administratively down/down" state.
+ Switch interfaces <mark>don't</mark> have the `shutdown` command applied by default; thus being in the "administratively up/up" state. Or in the "down/down" state if not connected to another device.
+ Command `show interfaces status` in privileged EXEC mode lists the following:
  + Ports
  + Name: Description.
  + Status: Connection status.
  + Vlan: Can be used to divide up LANs.
    + VLAN 1 is the default.
  + Duplex: Can the connection send/receive at same time?
    + Auto is default
  + Speed: In bps. "Auto" is default.
  + Type: What medium is being used, speed of interface.

![image](https://github.com/psaumur/CCNA/assets/106411237/e0fdc339-21d9-4313-b7d8-78303a7ba1ea)

+ `speed <speed in bps>` and `duplex <duplex type>` in interface config mode (`conf t` and `interface <interface name>`), allows you configure the speed and duplex of an interface.
---

![image](https://github.com/psaumur/CCNA/assets/106411237/12a33be7-795f-467a-87a4-42c5b218960b)

+ Normally, you'd keep auto-negotiation on.
+ Unused Interfaces can pose a security risk so it's a good idea to deactivate them.
+ `interface range <range>` in global config mode to enter intetface range config mode; this allows you to configure mutliple interfaces at once.
  + E.g., `interface range f0/5 - 12`
![image](https://github.com/psaumur/CCNA/assets/106411237/06e2e267-1e07-48a1-8c8c-8edbd5bd48ae)

## Duplex
+ **Half Duplex** The device <mark>cannot</mark> send and receive data at the same time. If it is receiving a frame, it must wait before sending a frame.
+ **Full Duplex** The device <mark>can</mark> send and receive data at the same time. It doesn't have to wait.
+ Most modern sitches support full duplex interfaces.
+ In modern networks half duplex is used almost nowhere.

## Hubs
+ An old typle of network device that's simpler than a switch.
+ A repeater; any frame it receives, it'll flood to all other devices connected to it.
+ Operate at Layer 1.
+ Used half duplex.
+ When multiple packets were received by the hub, it would flood the connections with both, causing a collision (on the interface), and hosts would not receive the frame intact.
+ All devices connected to a hub are called a collision domain.
+ Collisions are common.
+ To deal with collisions on a half duplex situation, Ethernet devices use CSMA/CD.
+ Care must be taken when configuring speed and duplex.

## CSMA/CD
+ **Carrier Sense Multiple Access with Collision Detection (CSMA/CD)** A mechanism that describes how devices avoid collisions in a half duplex situation, and how that react if collisions occur.
+ Process
  1. Before sending frames, devices "listen" to the collision domain until they detect that other devices are not sending.
  2. If a collision occurs, the device sends a jamming signal to inform the other devices that a collision happened.
  3. Each device will wait a random period of time before sending frames again.
  4. The process repeats.

## Switches
+ Switches are more sophisticated than hubs.
+ Operate on Layer 2 using Layer 2 addressing.
+ Collisions rarely occur.
+ Care isn't needed when configuring duplex, it'll always be full.

## Speed/Duplex Autonegotiation
+ Interfaces that can run at different speeds (10/100 or 10/100/1000) have a default setting of "speed auto" and "duplex auto".
- Interfaces "advertise" their capabilities to the neighbouring device, and they negotiate the best speed and duplex settings they're both capable of.
+ If autonegotiation is disabled on a device connected to the switch, duplex mismatch may occur. This will cause collisions and thus poor network performance.
  + If the speed is 10 or 100 Mbps, the switch interface will be set to half duplex. Otherwise it'll be full duplex.
+ if a switch or router

## Interface Errors
+ `show interfaces <interface name>` command in privileged EXEC mode shows statistics about an interface.
![image](https://github.com/psaumur/CCNA/assets/106411237/20d6affd-6014-427d-9ad9-c638ace358f8)
+ Runts: Counts frames that are smaller than the minimum frame size (64 bytes).
+ Giants: Counts frames that are larger than the maximum frame size (1518 bytes).
+ CRC: Counts frames that failed the CRC check (in the Ethernet FCS trailer).
+ Frame: Counts frames that have an incorrect format (due to an error).
+ Input Eerrors: Total of various counters, such as the above four
+ Output Errors: Counts frames the switch tried to send, but failed due to an error.