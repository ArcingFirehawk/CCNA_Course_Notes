# Day 12 | Life of a Packet

+ Example Network Topology
  ![image](https://github.com/psaumur/CCNA/assets/106411237/ec16b9fd-4d90-4b73-b930-cd825ff13b00)


+ Each network device's interface has a <mark>unique</mark> MAC addresses.
+ In a TCP Header the source IP address comes before the destination IP address, while in an Ethernet Header the destination MAC address comes before the source MAC address.
+ Full Packet Sending Process
  1. PC1 broadcasts an ARP Request to find the MAC address of the default gateway. R1 sends (unicast) and ARP Reply back to PC1.
  2. PC1 sends the packet to R1 encapsulated with an Ethernet Header and R1's MAC address.
  3. R1 de-encapsulates the packet's Ethernet Header.
  4. R1 looks up the packet's destination in its routing table for the most specific route.
  5. R1 broadcasts an ARP to learn R2's MAC address. R2 sends (unicast) and ARP Reply back to R1.
  6. R1 sends the packet to R2 encapsulated with an Ethernet Header and R2's MAC address.
  7. Repeat steps 3-6 for R2 to R4.
  8. Repeat steps 3-6 for R4 to PC4.
+ ARP is only necessary if the devices don't know a MAC address.
+ In this process, switches don't modify frames. They forwareded them and learned MAC addresses.
+ When a hest sends a packet to another host, the source and destination IP doesn't change—even though routers modify Ethernet Header.

---

![image](https://github.com/psaumur/CCNA/assets/106411237/5eb94811-32f3-47f6-884e-f45a71456e84)


![image](https://github.com/psaumur/CCNA/assets/106411237/dc0d05cc-9b76-4921-895d-bfbe78ceb0a7)


![image](https://github.com/psaumur/CCNA/assets/106411237/884f7113-21a9-407f-a38e-44489ae3b47e)


![image](https://github.com/psaumur/CCNA/assets/106411237/36459aeb-e802-4347-b626-0c9cc168c624)


![image](https://github.com/psaumur/CCNA/assets/106411237/163bfaf6-15c7-4f7d-9429-4c62a28f0292)


![image](https://github.com/psaumur/CCNA/assets/106411237/1f7e5683-00e6-4ce0-b52a-ca8fdb24c87b)


![image](https://github.com/psaumur/CCNA/assets/106411237/18d04c9d-3734-44e7-995d-b53ab3aaa2a1)


![image](https://github.com/psaumur/CCNA/assets/106411237/07c44007-a208-47a2-a0e8-ca289f86be75)


![image](https://github.com/psaumur/CCNA/assets/106411237/4bcbdba0-234a-4cfa-aa25-cbc3c3c061e1)


![image](https://github.com/psaumur/CCNA/assets/106411237/81c2e8ad-be55-487c-b9da-02540f70b0d9)


![image](https://github.com/psaumur/CCNA/assets/106411237/91cfe407-28b5-48e8-b5f8-a60b324e0706)


![image](https://github.com/psaumur/CCNA/assets/106411237/4bf8c10b-1240-4e7d-8db4-85ea5f3f619f)


![image](https://github.com/psaumur/CCNA/assets/106411237/f938e440-ebdb-444c-b4c7-705d8fd2a4e9)


![image](https://github.com/psaumur/CCNA/assets/106411237/1f236bda-d2cf-4252-af3b-bdc5ec5c2aca)



