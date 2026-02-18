# IPv4 Addressing Pt. 2

## Calculating a Network's Address Space
+ Maximimum Hosts per Network = 2^n - 2
  + n = # of Host Bits
  + AKA # of usable IP addresses.
  + E.g., The # of usuable host for 192.168.1.0/24 is 2^8 - 2 = 254.
+ The first usable IP address is the network address plus 1; in binary 00000000 to 00000001.
+ The last usable IP address is the broadcast address minus 1 in binary 11111111 to 11111110.
+ Graphic: IPv4 Address Classes
![image](CCNA_COURSE_NOTES\Graphics\day08_image01.png)

## Configuring a CISCO Router with IP Addresses
+ The `show ip interface brief` command in priviledged EXEC mode shows the status of each interface on the device and their IP addresses.
  + Columns: Interface, IP-Address; OK?, legacy feature (probably not in use); Method, indicates the method in which the interface was assigned an IP address; Status, interface's Layer 1 status; Protocol, interface's Layer 2 status.
+ "administratively down" means that the interface has been disabled with the `shutdown` command.
+ A CISCO router's interfaces are administratively down by default.
+ A CISCO switch's interfaces are <mark>not</mark> administratively down by default.
+ `interface <name of interface>` in global config mode to enter interface config mode.
+ `ip address <IP address> <subnet mask in decimal notation>` to set the IP address of the interface.
+ `no shutdown` enables an interface.
+ Note: use `do show ip interface brief` in interface config mode to execute the command.
+ `show interfaces <interface>` shows Layer 1, layer 2, and Layer 3 information of the interface.
+ `show interfaces description` shows the interfaces descriptions, which are optional, but are helpful in identifying the purpose of each interface.
   + Use `description <description>` in interface config mode to set descriptions.
+ Use `end` to exit interface config mode into user EXEC mode.


CISCO CLI DEVICE CONFIGURATION

R1> enable
R1# show ip interface brief

Lists the Interfaces, IP Addresses, Method, Status, and Protocol.

Interfaces:

- What port interfaces are available/connected

IP Addresses

- Self explanatory. What IP Address is assigned.

Method

- What method was the IP address assigned?

Status (Layer 1 Status)

- Current status of interface
- 'administratively down' = Interface has been disabled with the 'shutdown' command

Administratively down is the DEFAULT status of Cisco Router interfaces.

Cisco Switch interfaces are NOT administratively down by DEFAULT.

Protocol (Layer 2 Status)

- Cannot operate if Status (Layer 1) is down
  
![image](https://github.com/psaumur/CCNA/assets/106411237/fa113ff0-a8ee-410b-ab3e-64684654cac6)


---

// configure terminal cmd

R1# conf t

// This enters interface configuration mode

R1(config)# interface gigabitethernet 0/0

This can be shortened to 'g0/0' like they are listed in physical network maps.

![image](https://github.com/psaumur/CCNA/assets/106411237/df83bf09-c391-45b7-b1b4-41db061b84f4)


// This sets the IP ADDRESS and SUBNET MASK of device

R1(config-if) #ip address 10.255.255.254 255.0.0.0

// This enables the device

R1(config-if) #no shutdown

---

Two messages should appear showing the state has changed to 'up' (Status). Second message should show line protocol is now 'up' (Protocol).

// 'do' allows you to run a Privileged EXEC command from outside the mode.

R1(config-if) #do show ip interface brief

Good to confirm that the device/interface you have configured is up and running.

---

More 'show' CLI Commands

![image](https://github.com/psaumur/CCNA/assets/106411237/bdc1152e-1946-4ddb-ae72-1e23b9c9defa)


'show interfaces <interface name>'

- Shows Layer 1 and Layer 2 information about the interface and some Layer 3.
- Shows MAC Address (or BIA address)
- IP Address
- ... and so much more

'show interfaces description'

- show description for interface.

Example:

// Configure mode for interface Gigabyte Interface 0/0

R1(config) #int g0/0

R1(config) #description ## to SW1 ##

This sets the 'Description' column to display:

Interface 				Description

Gi0/0                   ## to SW1 ##
