# Networking Basics

## 1. Explain the difference between static and dynamic IP addresses. In which scenarios would you prefer to use each type?

- **Static IP Address:** A fixed address manually assigned to a device, which does not change over time.
- **Dynamic IP Address:** An address assigned dynamically by a DHCP server that may change periodically.

### **Use Cases:**
- Use **static IPs** for servers, printers, and devices needing constant access.
- Use **dynamic IPs** for general client devices like laptops and mobile phones to ease management.

## 2. What potential issues can arise from using a static IP address on a large network?

- Increased administrative overhead
- Potential IP conflicts
- Lack of scalability for large networks
- Limited IP address availability

## 3. Define the purpose of Class A, B, C, D, and E IP addresses.

| Class | Address Range | Default Subnet Mask | Purpose |
|-------|--------------|---------------------|---------|
| A | 1.0.0.0 – 126.255.255.255 | 255.0.0.0 | Large networks (ISP, organizations) |
| B | 128.0.0.0 – 191.255.255.255 | 255.255.0.0 | Medium-sized networks |
| C | 192.0.0.0 – 223.255.255.255 | 255.255.255.0 | Small networks (Home, Offices) |
| D | 224.0.0.0 – 239.255.255.255 | N/A | Multicasting |
| E | 240.0.0.0 – 255.255.255.255 | N/A | Reserved for research |

## 4. Why are certain IP ranges reserved and not available for general use? Provide examples.

### **Private IP Ranges:**
- **Class A:** `10.0.0.0 – 10.255.255.255`
- **Class B:** `172.16.0.0 – 172.31.255.255`
- **Class C:** `192.168.0.0 – 192.168.255.255`

These are reserved for internal networks and cannot be routed on the internet.

## 5. Explain the role of a subnet mask in an IP address.

A subnet mask defines which portion of an IP address is the **network** and which is the **host**.

Example:
- **IP:** `192.168.1.10`
- **Subnet Mask:** `255.255.255.0`
- **Network:** `192.168.1.0`
- **Host:** `10`

## 6. What is the difference between a network address and a broadcast address in a subnet?

- **Network Address:** First address in a subnet, used to identify the network (e.g., `192.168.1.0/24`).
- **Broadcast Address:** Last address in a subnet, used to communicate with all devices (`192.168.1.255`).

## 7. How does a router determine which subnet an IP packet should be sent to?

Routers use **routing tables** to determine where to forward packets based on:
- Destination IP address
- Subnet mask
- Next-hop gateway

Example Routing Table:
```
Destination     Subnet Mask      Gateway      Interface
192.168.1.0    255.255.255.0    192.168.1.1  eth0
10.0.0.0       255.0.0.0        10.0.0.1     eth1
```

## 8. Explain the purpose of a firewall in a computer network.

A **firewall** is a security system that monitors and controls incoming/outgoing network traffic.

- **Types:**
  - **Packet Filtering:** Blocks/restricts packets based on rules.
  - **Stateful Inspection:** Tracks active connections.
  - **Application Layer Firewalls:** Inspects application data.

## 9. You are given the IP address `192.168.10.0/24`. Divide this address space into four subnets. What are the network addresses, broadcast addresses, and available host ranges for each subnet?

Using **subnet mask `/26` (255.255.255.192)` to divide `/24` into 4 subnets:

| Subnet | Network Address | Broadcast Address | Usable IP Range |
|--------|----------------|-------------------|-----------------|
| 1 | 192.168.10.0 | 192.168.10.63 | 192.168.10.1 - 192.168.10.62 |
| 2 | 192.168.10.64 | 192.168.10.127 | 192.168.10.65 - 192.168.10.126 |
| 3 | 192.168.10.128 | 192.168.10.191 | 192.168.10.129 - 192.168.10.190 |
| 4 | 192.168.10.192 | 192.168.10.255 | 192.168.10.193 - 192.168.10.254 |

## 10. Create a subnet that supports 16 host IP addresses. Provide the subnet mask and the range of usable IP addresses.

For **16 host IPs**, we need **at least 4 bits for hosts (2⁴ = 16 addresses + 2 reserved)**:

- **Subnet Mask:** `255.255.255.240` (`/28`)
- **Network Address:** `192.168.1.0`
- **Broadcast Address:** `192.168.1.15`
- **Usable IP Range:** `192.168.1.1 – 192.168.1.14`
