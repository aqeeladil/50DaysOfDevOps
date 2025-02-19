# Networking Basics

### 11. Given the IP address `172.16.0.45/16`, identify the network address, broadcast address, and the range of host IPs.

- **Network Address**: `172.16.0.0`
- **Broadcast Address**: `172.16.255.255`
- **Range of Host IPs**: `172.16.0.1` to `172.16.255.254`

### 12. For the IP address `192.168.5.100/24`, identify which subnet this address belongs to and whether it can communicate directly with the IP address `192.168.6.200/24` without a router.

- **Subnet**: `192.168.5.0/24`
- **Broadcast Address**: `192.168.5.255`
- **Range of Host IPs**: `192.168.5.1` to `192.168.5.254`
- **Communication with `192.168.6.200/24`**: No, because `192.168.5.0/24` and `192.168.6.0/24` are different subnets. A router is required for communication between them.

### 13. Configure a device with a static IP address of `10.0.0.10` on a network with the subnet mask `255.255.255.0`. What will be the network address and broadcast address for this configuration?

- **Network Address**: `10.0.0.0`
- **Broadcast Address**: `10.0.0.255`
- **Range of Host IPs**: `10.0.0.1` to `10.0.0.254`

### 14. Using a dynamic IP configuration, explain how a device obtains an IP address from the DHCP server. What information does the device receive from the DHCP server?

**DHCP Process (DORA):**
1. **Discover**: The client sends a DHCP Discover packet to find a DHCP server.
2. **Offer**: The DHCP server responds with an available IP address.
3. **Request**: The client requests to lease the offered IP address.
4. **Acknowledge**: The server confirms and assigns the IP address.

The device receives:
- IP address
- Subnet mask
- Default gateway
- DNS server(s)
- Lease duration

### 15. How does DNS resolve the domain name `www.example.com` into an IP address? Describe the process step by step.

1. **Local Cache Check**: The computer checks its local cache for `www.example.com`.
2. **Query to Recursive Resolver**: If not found, it queries a recursive DNS server.
3. **Root Server Query**: The recursive server asks a root DNS server.
4. **TLD Server Query**: The root server directs it to the TLD (Top-Level Domain) server.
5. **Authoritative Server Query**: The TLD server directs it to the authoritative DNS server for `example.com`.
6. **Response**: The authoritative server responds with the IP address.
7. **Connection**: The client uses the retrieved IP address to connect to the website.

### 16. Explain what would happen if the DNS server is unreachable when trying to access a website.

- The device will be unable to resolve domain names to IP addresses.
- If the IP address is cached, the site may still load.
- If no cache exists, the browser will display a **DNS error**.
- A backup or secondary DNS server may be queried if configured.
- 
### 17. Design a subnetting plan for a company that requires 6 subnets with at least 30 hosts each. What will be the subnet mask and range of each subnet?

- **Minimum host requirement**: 30
- **Formula**: `2^n - 2 >= 30` → `n = 5` (32 addresses per subnet)
- **Subnet mask**: `255.255.255.224` (`/27`)
- **Subnets and Ranges**:

| Subnet | Network Address | Host Range | Broadcast Address |
|--------|----------------|------------|------------------|
| 1      | 192.168.1.0/27 | 192.168.1.1 - 192.168.1.30 | 192.168.1.31 |
| 2      | 192.168.1.32/27 | 192.168.1.33 - 192.168.1.62 | 192.168.1.63 |
| 3      | 192.168.1.64/27 | 192.168.1.65 - 192.168.1.94 | 192.168.1.95 |
| 4      | 192.168.1.96/27 | 192.168.1.97 - 192.168.1.126 | 192.168.1.127 |
| 5      | 192.168.1.128/27 | 192.168.1.129 - 192.168.1.158 | 192.168.1.159 |
| 6      | 192.168.1.160/27 | 192.168.1.161 - 192.168.1.190 | 192.168.1.191 |

### 18. You have been given the IP address `192.168.50.0/25`. Further divide this into two subnets. What are the new subnet masks and IP address ranges?

- **Original Subnet**: `192.168.50.0/25`
- **New Subnet Mask**: `255.255.255.192` (`/26`)
- **Divided Subnets**:

| Subnet | Network Address | Host Range | Broadcast Address |
|--------|----------------|------------|------------------|
| 1      | 192.168.50.0/26 | 192.168.50.1 - 192.168.50.62 | 192.168.50.63 |
| 2      | 192.168.50.64/26 | 192.168.50.65 - 192.168.50.126 | 192.168.50.127 |

---
