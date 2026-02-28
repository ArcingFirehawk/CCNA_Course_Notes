# Day 11B | Static Routing

## Review
+ SWITCHES forward traffic WITHIN LAN's
+ ROUTERS forward traffic BETWEEN LAN's

WAN (Wide Area Network)

- Network spread over a large area





## Default Gateways
+ End hosts can send packets directly to destinations in their connected network.
+ To send packets to destinations outside their local network, they must send them to their default gateway.
+ Gateway is an old term for router.
+ Default Route
  + The default gateway config is also called the default route.
  + It's a route to 0.0.0.0/0.
  + All netmask bits are set to 0 and includes all addresses from 0.0.0.0 to 255.255.255.255.
  + Least specific route possible.
+ End hosts usually have no need for any more specific routes.
  + They just need to know: to send packets outside of my local network, send them to my default gateway.

## Static Route Configuration
+ It's possible to configure routers to:
  + Load-balance between different routes.
  + Use one route as the main and the other as the backup.
+ Routers don't need routes to all networks in the path to the destination.
+ `ip route <ip-address> <netmask> <next-hop>` command to add a static route to a router's routing table.
+ The "[1/0]" displayed in a static route means "[Administrative Distance/Metric]".
+ When  configuring static routes, you can configure the next-hop address, exit interface, or both.
  + `ip route <ip-address> <netmask> <exit-interface>`
  + `ip route <ip-address> <netmask> <exit-interface> <next-hop>`
+ Static routes in which you specify only the exit interface, relies on a feature called Proxy ARP to function.
  + This is usually not a problem, but generally you stick to "next-hop" or "exit-interface next-hop".
  + Neither is better than the other; use what you prefer.
+ Use `no ip route <ip-address> <netmask> <next-hop>` in terminal config mode to remove a route.

## Default Route
+ A default route is a route to 0.0.0.0/0.
+ If the router doesn't have any more specific routes that match a packet's destination IP address, the router will forward the packet using the default route.
+ A default route is often used to direct traffic to the Internet.
+ `ip route 0.0.0.0 0.0.0.0 <next-hop>` to configure a default route.

![image](https://github.com/psaumur/CCNA/assets/106411237/e44ac71c-91e3-4963-85da-ac07e475b248)


![image](https://github.com/psaumur/CCNA/assets/106411237/289212da-6c94-44fb-a1e3-1c066b56d79c)


![image](https://github.com/psaumur/CCNA/assets/106411237/f8f7d58b-89b7-412c-9cf6-c038338e105d)


![image](https://github.com/psaumur/CCNA/assets/106411237/63611407-719e-46d3-8331-a18533616285)

---

STATIC ROUTES:

![image](https://github.com/psaumur/CCNA/assets/106411237/10135afa-ace6-47f1-aada-1b73f243589b)

---

STATIC ROUTE CONFIGURATION:

![image](https://github.com/psaumur/CCNA/assets/106411237/d375a428-e171-4212-9698-2f2589878884)


![image](https://github.com/psaumur/CCNA/assets/106411237/012f4134-2667-421b-9b36-f449faebf423)


![image](https://github.com/psaumur/CCNA/assets/106411237/0a3ed6cb-c414-4365-aef4-754b4b82483e)


![image](https://github.com/psaumur/CCNA/assets/106411237/4379f8fb-a366-4279-a31c-ff2ba3f6fdb8)


![image](https://github.com/psaumur/CCNA/assets/106411237/6fed6489-c53c-404e-b794-b71c2e9b8e4f)

---

STATIC ROUTE CONFIGURATION with *exit-interface*

![image](https://github.com/psaumur/CCNA/assets/106411237/dc93b5f9-791c-44fc-8b88-2053491183a9)

---

DEFAULT ROUTE

![image](https://github.com/psaumur/CCNA/assets/106411237/a0eef93a-b40b-409b-8b51-6cdbace4ff45)
