# **IP Addressing and Subnetting**

## **1. Understanding IP Addressing**
An **IP address** (Internet Protocol address) is a unique identifier assigned to each device on a network, allowing devices to communicate. There are two types of IP addresses:

### **A. IPv4 Addressing**
IPv4 uses **32-bit addressing**, divided into **4 octets** (8 bits each), written in **dotted decimal format**.

Example:  
```
192.168.1.1
```
Each octet ranges from **0 to 255** (since each is 8 bits, and 2⁸ = 256).  

### **B. IPv6 Addressing**
IPv6 uses **128-bit addressing**, written in **hexadecimal format**.

Example:
```
2001:db8::ff00:42:8329
```
IPv6 was introduced because IPv4 was running out of unique addresses.

---

## **2. IPv4 Address Classes**
IPv4 addresses are categorized into **five classes**, based on the first octet.

| **Class** | **First Octet Range** | **Subnet Mask**   | **Purpose**      |
|-----------|---------------------|----------------|----------------|
| A         | 1 - 126             | 255.0.0.0      | Large networks |
| B         | 128 - 191           | 255.255.0.0    | Medium networks |
| C         | 192 - 223           | 255.255.255.0  | Small networks |
| D         | 224 - 239           | N/A            | Multicast |
| E         | 240 - 255           | N/A            | Experimental |

👉 **Classful addressing is outdated. Today, CIDR (Classless Inter-Domain Routing) is used instead.**

---

## **3. What is Subnetting?**
### **A. Definition**
Subnetting is the process of dividing a large network into smaller, more efficient subnetworks (**subnets**).  
It helps **optimize IP address usage** and **improve network security and performance**.

### **B. Why Use Subnetting?**
- Reduces network congestion by limiting broadcast domains.
- Increases security by isolating departments.
- Efficient IP address allocation to avoid waste.

### **C. Subnet Mask**
A **subnet mask** defines which portion of an IP address represents the network and which part represents the host.

Example:

| IP Address  | 192.168.1.10 |
|------------|-------------|
| Subnet Mask | 255.255.255.0 |

- `255.255.255.0` → `/24` (`256` IPs)
- `255.255.255.128` → `/25` (`128` IPs)

**Subnet masks can be written in two ways:**
- **Dotted Decimal Notation** → `255.255.255.0`
- **CIDR Notation** → `/24` (means 24 bits are for the network)

---

## **4. Practical Scenario: Designing a Subnet for a Company**
### **Scenario**
A company has **200 employees**, each needing a unique IP. The admin has the **192.168.1.0/24** network but needs to split it into subnets.

### **Step 1: Calculate Subnet Requirements**
1. **Total Available IPs in /24**  
   - A **/24 subnet** has **256** total addresses (2⁸ = 256).
   - **Usable IPs:** 256 - 2 = **254** (excluding **network** and **broadcast** addresses).

2. **Required IPs:**
   - IT: **120 devices**
   - HR: **50 devices**
   - Sales: **30 devices**
   - Management: **10 devices**

3. **Choosing the Right Subnet Masks**
   - **IT needs 120 IPs** → `/25` (supports **126 usable** IPs)
   - **HR needs 50 IPs** → `/26` (supports **62 usable** IPs)
   - **Sales needs 30 IPs** → `/26` (supports **62 usable** IPs)
   - **Management needs 10 IPs** → `/28` (supports **14 usable** IPs)

### **Step 2: Assign Subnet Ranges**
| **Department** | **Subnet**  | **IP Range** | **Usable IPs** |
|--------------|------------|-------------|-------------|
| IT          | 192.168.1.0/25  | 192.168.1.1 - 192.168.1.126 | 126 |
| HR          | 192.168.1.128/26 | 192.168.1.129 - 192.168.1.190 | 62 |
| Sales       | 192.168.1.192/26 | 192.168.1.193 - 192.168.1.254 | 62 |
| Management  | 192.168.2.0/28 | 192.168.2.1 - 192.168.2.14 | 14 |

---

## **5. Router Configuration for Subnetting**
Each subnet needs a **router interface** (gateway). Here's how to set up interfaces on a Cisco router.

### **Step 1: Assign IPs to Router Interfaces**
```shell
Router(config)# interface FastEthernet0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.128
Router(config-if)# no shutdown
```
```shell
Router(config)# interface FastEthernet0/1
Router(config-if)# ip address 192.168.1.129 255.255.255.192
Router(config-if)# no shutdown
```
```shell
Router(config)# interface FastEthernet0/2
Router(config-if)# ip address 192.168.1.193 255.255.255.192
Router(config-if)# no shutdown
```

### **Step 2: Configure DHCP for Clients**
A **DHCP server** automatically assigns IPs to devices.

```shell
Router(config)# ip dhcp pool IT-NET
Router(dhcp-config)# network 192.168.1.0 255.255.255.128
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# exit
```

---

## **6. Verifying Network Connectivity**
### **A. Check Assigned IP**
On a client machine (Windows/Linux):
```shell
ipconfig (Windows)
ifconfig (Linux)
```
### **B. Test Connectivity**
Use the **ping** command to check communication.
```shell
ping 192.168.1.129
```
If successful, it means the network is properly configured.

---

## **7. Key Takeaways**
✅ **Subnetting improves network efficiency, security, and performance.**  
✅ **IP addressing follows CIDR (Classless Inter-Domain Routing).**  
✅ **Subnet masks determine network and host portions.**  
✅ **Routers and DHCP can be configured for dynamic IP assignment.**  

