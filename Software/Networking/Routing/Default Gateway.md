---
date: 2025-10-13
tags:
link:
---


# Default Gateway

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.


## 🔹 Default Gateway and Its MAC

1. **Default Gateway**
    
    - The **router interface** that devices in a subnet use to reach **other subnets or the internet**.
    - Example: In `192.168.0.0/24` subnet, the default gateway is usually `192.168.0.1`.
    
2. **MAC Address of the Gateway**
    
    - Every network interface (even router interfaces) has a **unique MAC address**.
    - Devices on the same subnet need the **MAC address** to send Ethernet frames.
    - When sending to an **outside subnet**, a device sends the frame to the **gateway’s MAC**, not the final destination.
    
3. **How It Works in Steps**
    
    - Device A wants to send data to Device C in a different subnet.
    - Device A checks its routing table → sees C is outside subnet → send to **default gateway**.
    - Device A uses **ARP** to find the MAC address of `192.168.0.1` (the router interface).
    - Device A sends the Ethernet frame **to the gateway’s MAC**.
    - Switch forwards the frame to the router.
    - Router then looks at IP of C and forwards it toward the next hop.