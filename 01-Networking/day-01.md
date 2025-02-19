# Networking Basics

## 1. Difference Between Static and Dynamic IP Addresses

### **Static IP Address:**
- A manually assigned, **fixed** IP address that does not change over time.
- Used for devices requiring a **consistent** address.

**Example Use Cases:**
- Servers (web, database, DNS)
- Network devices (routers, firewalls, printers)
- Remote access (VPN, security cameras)

### **Dynamic IP Address:**
- Assigned **automatically** by a DHCP (Dynamic Host Configuration Protocol) server.
- Changes periodically to optimize IP address allocation.

**Example Use Cases:**
- Client devices (laptops, mobile phones, IoT devices)
- Home networks where manual management is unnecessary

---

## 2. Issues with Using Static IP Addresses in Large Networks

1. **Administrative Overhead:**
   - Requires **manual configuration** for each device.
2. **IP Conflicts:**
   - If two devices are assigned the same IP, network issues occur.
3. **Lack of Scalability:**
   - Managing hundreds of static IPs becomes **difficult and error-prone**.
4. **IP Address Exhaustion:**
   - Without careful planning, manually assigned IPs can deplete available addresses.

---

## 3. Purpose of Class A, B, C, D, and E IP Addresses

| **Class** | **Address Range** | **Default Subnet Mask** | **Purpose** |
|-----------|------------------|-------------------------|------------|
| **A** | 1.0.0.0 – 126.255.255.255 | 255.0.0.0 | Large networks (ISPs, corporations) |
| **B** | 128.0.0.0 – 191.255.255.255 | 255.255.0.0 | Medium-sized networks |
| **C** | 192.0.0.0 – 223.255.255.255 | 255.255.255.0 | Small networks (homes, offices) |
| **D** | 224.0.0.0 – 239.255.255.255 | N/A | Multicasting (e.g., video streaming) |
| **E** | 240.0.0.0 – 255.255.255.255 | N/A | Reserved for research & future use |

---

## 4. Reserved IP Ranges

Some IP address ranges are **reserved** to ensure:
✅ **Internal network communication** without interference from public networks.
✅ **Efficient use of IPs** without duplication across organizations.

### **Private IP Ranges:** (Not routable on the public internet)

| **Class** | **Private IP Range** | **Example Usage** |
|-----------|----------------------|------------------|
| **A** | 10.0.0.0 – 10.255.255.255 | Large enterprises, cloud networks |
| **B** | 172.16.0.0 – 172.31.255.255 | ISPs, VPNs, corporate networks |
| **C** | 192.168.0.0 – 192.168.255.255 | Home and office networks |

---

## 5. Role of a Subnet Mask

A **subnet mask** helps divide an IP address into:
1. **Network Portion** – Identifies the network.
2. **Host Portion** – Identifies devices within that network.

### **Example:**

| **IP Address** | **Subnet Mask** | **Network** | **Host** |
|---------------|---------------|------------|--------|
| 192.168.1.10 | 255.255.255.0 | 192.168.1.0 | .10 |

---

## 6. Network Address vs. Broadcast Address

- **Network Address:**
  - First IP in a subnet.
  - Used to **identify the subnet itself** (not assignable to devices).
  - **Example:** `192.168.1.0/24`

- **Broadcast Address:**
  - Last IP in a subnet.
  - Used to **send data to all devices** in that subnet.
  - **Example:** `192.168.1.255`

---

## 7. How a Router Determines Packet Destination

Routers use **routing tables** to make forwarding decisions.

### **Example Routing Table:**
```plaintext
Destination     Subnet Mask      Gateway      Interface
192.168.1.0    255.255.255.0    192.168.1.1  eth0
10.0.0.0       255.0.0.0        10.0.0.1     eth1
```

---

## 8. Purpose of a Firewall

A **firewall** is a security system that:
✅ **Filters incoming and outgoing traffic**
✅ **Prevents unauthorized access**
✅ **Blocks malware and cyber threats**

### **Types of Firewalls:**
1. **Packet Filtering:**
   - Blocks or allows packets based on predefined rules.
2. **Stateful Inspection:**
   - Tracks active connections and allows only related traffic.
3. **Application Layer Firewalls:**
   - Inspects application-specific data (e.g., web traffic filtering).

---

## 9. Subnetting Example: Dividing `192.168.10.0/24` into Four Subnets

To divide `/24` into 4 subnets, we use a **subnet mask of `/26` (255.255.255.192)**:

| **Subnet** | **Network Address** | **Broadcast Address** | **Usable IPs** |
|-----------|--------------------|--------------------|---------------|
| **1** | 192.168.10.0 | 192.168.10.63 | 192.168.10.1 – 192.168.10.62 |
| **2** | 192.168.10.64 | 192.168.10.127 | 192.168.10.65 – 192.168.10.126 |
| **3** | 192.168.10.128 | 192.168.10.191 | 192.168.10.129 – 192.168.10.190 |
| **4** | 192.168.10.192 | 192.168.10.255 | 192.168.10.193 – 192.168.10.254 |

---

## 10. Creating a Subnet for 16 Hosts

To support **16 hosts**, we need at least **4 bits** for hosts (`2⁴ = 16 + 2 reserved`):

| **Subnet Mask** | **Network Address** | **Broadcast Address** | **Usable IP Range** |
|---------------|--------------------|--------------------|----------------|
| 255.255.255.240 (/28) | 192.168.1.0 | 192.168.1.15 | 192.168.1.1 – 192.168.1.14 |

✅ **Reserved Addresses:**
- **Network Address:** `192.168.1.0`
- **Broadcast Address:** `192.168.1.15`

---
