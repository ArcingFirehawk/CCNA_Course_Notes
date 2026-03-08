# Day 17 | VLANs Pt. 3
+ It's best practice to set the native VLAN to an unused VLAN, because it can cause security issues.
+ Native VLAN frames are untagged, so they're more smaller and thus more efficient than tagged ones.


## Configuring VLAN on a Router
+ 2 Methods
  + Use the `encapsulation dot1q <vlan ID> native` command on the router's subinterface.
    ![image](https://github.com/psaumur/CCNA/assets/106411237/2ea65208-6b2a-4cac-a463-982a731c9e24)

  + Configure the IP address for the native VLAN on the router's physical interface (the `encapsulation dot1q <vlan ID>` command isn't necessary).
    ![image](https://github.com/psaumur/CCNA/assets/106411237/dabcc3b4-13c3-4d60-abe2-c7cbb5edd4c2)

# Layer 3 Switches
+ AKA Multilayer Switch
+ Capable of both switching and routing.
+ It's "Layer 3 aware".
+ You can assign IP Addresses to its interface, like a router.
+ You can create virtual interfaces for each VLAN, and assign IP addresses to those interfaces.
+ You can configure routes on it, just like a router.
+ It can be used for inter-VLAN routing.
+ Has a routing table.
+ Will flood a frameto all interfaces if it doesn't have a relevant MAC address in it's routing table.
+ Graphic: Network Topology Example with L3 Switch
  ![image](https://github.com/psaumur/CCNA/assets/106411237/af59481b-d0cb-41d7-9eba-7c8d47131c28)

  + SW2 Replaced with a L3 switch.
  + Multi-VLAN connections to R1 removed and replaced with a point-to-point L3 connection.

+ **Switch Virtual Interface (SVI)** The virtual interfaces you can assign IP addresses to in a multilayer switch.
+  Configure each <mark>endhost</mark> to use the SVI as their gateway address.
+ To send traffic to different subnest/VLANS, the endhosts will send traffic to the switch, and it will route the traffic.

+ Configuring a router with a L3 switch using SVI:
  1. `no interface <interface>.<sub-interface>` to delete all sub-interfaces.
  2. `default interface <interface>` to reset an interface to its default settings.
  3. `ip address <IP Address> <Subnet Mask>` to set an IP address.

+ Configuring a L3 switch to use SVI and a point-to-point connection with a router:
  1. `default interface <interface>` to reset an interface to its default settings.
  2. `ip routing` enables L3 routin on the switch.
  3. `no switchport` on an interface to change it from a L2 switchport to a L3 routing port.
  4. `ip address <IP Address> <Subnet Mask>` to set an IP address.
  5. `ip route 0.0.0.0 0.0.0.0 <Next-Hop IP Address>` to set a default route to the router.

+ SVI Configuration
  1. `interface vlan<VLAN #>` in global config mode to create a AVI for the VLAN.
  2. Assign an IP address using `ip address <IP Address> <Subnet Mask>`.
  3. `no shutdown` to enable it.

+ Graphic: SVI Config on L3 Switch
  ![image](https://github.com/psaumur/CCNA/assets/106411237/7c1710fb-40d7-44a4-8336-b037e1c2ea77)

+ SVIs are shut down by default, so remember to use `no shutdown`.

![image](https://github.com/psaumur/CCNA/assets/106411237/2b5b13c3-1364-4296-886c-0bd9b00b4167)

+ Conditions for an SVI to be "Up/Up":
  + The VLAN must exist on the switch.
  + The switch must have at least 1 access port in the VLAN in an “up/up” state and/or one trunk port that allows the VLAN that is in an “up/up” state.
  + The VLAN must not be shutdown.
  + The SVI must not be shutdown.