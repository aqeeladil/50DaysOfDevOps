# Networking Basics

## 1. Identifying Network and Broadcast Addresses

### Given IP: `172.16.0.45/16`
- **Subnet Mask**: `/16` (255.255.0.0)
- **Network Address**: `172.16.0.0`
- **Broadcast Address**: `172.16.255.255`
- **Range of Host IPs**: `172.16.0.1` to `172.16.255.254`

## 2. Subnet Communication

### Given IP: `192.168.5.100/24`
- **Subnet Mask**: `/24` (255.255.255.0)
- **Network Address**: `192.168.5.0`
- **Broadcast Address**: `192.168.5.255`
- **Host IP Range**: `192.168.5.1` to `192.168.5.254`
- **Can communicate with `192.168.6.200/24`?** No, because they belong to different subnets and require a router for communication.

## 3. Static IP Configuration

### Given IP: `10.0.0.10` with Subnet Mask `255.255.255.0`
- **Network Address**: `10.0.0.0`
- **Broadcast Address**: `10.0.0.255`
- **Range of Host IPs**: `10.0.0.1` to `10.0.0.254`

## 4. DHCP Process (DORA)
1. **Discover**: Client sends a request to find a DHCP server.
2. **Offer**: DHCP server responds with an available IP.
3. **Request**: Client requests the offered IP.
4. **Acknowledge**: DHCP server confirms the assignment.

**Device receives:**
- IP Address
- Subnet Mask
- Default Gateway
- DNS Server(s)
- Lease Duration

## 5. DNS Resolution for `www.example.com`
1. **Local Cache Check**: Device checks its cache for the IP.
2. **Recursive Resolver Query**: If not found, it queries a DNS resolver.
3. **Root Server Query**: The resolver contacts a root DNS server.
4. **TLD Server Query**: Root server directs it to the `.com` TLD server.
5. **Authoritative Server Query**: TLD server directs it to `example.com`'s DNS.
6. **Response**: The authoritative DNS server provides the IP.
7. **Connection**: Device connects using the retrieved IP.

## 6. What Happens If DNS is Unreachable?
- Device cannot resolve domain names to IPs.
- If cached, the website may still load.
- If no cache, a **DNS error** appears.
- A secondary DNS server may be used if configured.

## 7. Subnetting Plan for 6 Subnets (30 Hosts Each)

### Subnet Mask: `/27` (255.255.255.224)`
Each subnet supports **30 usable hosts**.

| Subnet | Network Address | Host Range | Broadcast Address |
|--------|----------------|------------|------------------|
| 1      | 192.168.1.0/27   | 192.168.1.1 - 192.168.1.30  | 192.168.1.31 |
| 2      | 192.168.1.32/27  | 192.168.1.33 - 192.168.1.62 | 192.168.1.63 |
| 3      | 192.168.1.64/27  | 192.168.1.65 - 192.168.1.94 | 192.168.1.95 |
| 4      | 192.168.1.96/27  | 192.168.1.97 - 192.168.1.126 | 192.168.1.127 |
| 5      | 192.168.1.128/27 | 192.168.1.129 - 192.168.1.158 | 192.168.1.159 |
| 6      | 192.168.1.160/27 | 192.168.1.161 - 192.168.1.190 | 192.168.1.191 |

## 8. Splitting `192.168.50.0/25` into Two Smaller Subnets

### Original Subnet: `/25` (255.255.255.128)
Splitting into `/26` (255.255.255.192) creates **two subnets with 62 usable hosts each**.

| Subnet | Network Address | Host Range | Broadcast Address |
|--------|----------------|------------|------------------|
| 1      | 192.168.50.0/26   | 192.168.50.1 - 192.168.50.62  | 192.168.50.63 |
| 2      | 192.168.50.64/26  | 192.168.50.65 - 192.168.50.126 | 192.168.50.127 |

---
