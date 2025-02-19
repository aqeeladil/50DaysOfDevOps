# Network Scenarios and Solutions

This document provides various network-related scenarios with questions and useful answers to help in troubleshooting and designing networks effectively.

## Scenarios

### **Scenario 1: IP Addressing and Subnetting**
You are tasked with setting up a small office network. The office has three departments: HR (10 devices), IT (15 devices), and Sales (20 devices). You have been given the IP address range `192.168.1.0/24`.

- **Question 1:** How would you subnet this network to ensure each department has enough IP addresses?
  - Subnetting involves dividing the `192.168.1.0/24` network into smaller subnets to accommodate each department.
  - You can use subnet masks to create:
    - HR: `192.168.1.0/27` (32 total addresses, 30 usable)
    - IT: `192.168.1.32/27` (32 total addresses, 30 usable)
    - Sales: `192.168.1.64/26` (64 total addresses, 62 usable)

- **Question 2:** What subnet mask would you assign to each department?
  - HR and IT: `255.255.255.224` (/27)
  - Sales: `255.255.255.192` (/26)

- **Question 3:** How many usable IP addresses will each subnet have?
  - /27 subnet: 30 usable IPs
  - /26 subnet: 62 usable IPs

---

### **Scenario 2: Routing and Default Gateway**
A company has two networks: `192.168.1.0/24` and `192.168.2.0/24`. These networks are connected via a router.

- **Question 1:** What is the purpose of the default gateway in this setup?
  - The default gateway allows devices in one network to communicate with devices in another network.

- **Question 2:** If a device in `192.168.1.0/24` wants to send data to a device in `192.168.2.0/24`, how does the router facilitate this communication?
  - The router receives the packet, checks its routing table, and forwards it to the appropriate interface.

- **Question 3:** What would happen if the router fails?
  - Devices in each subnet can communicate internally but will be unable to communicate with the other subnet or the internet.

---

### **Scenario 3: DNS Resolution**
A user reports that they cannot access `www.example.com` from their computer, but they can access the website using its IP address.

- **Question 1:** What could be the possible cause of this issue?
  - The issue could be due to a DNS server failure or incorrect DNS configuration.

- **Question 2:** How would you troubleshoot this problem?
  - Use `nslookup www.example.com` to check DNS resolution.
  - Check the DNS settings on the device.
  - Try changing to a public DNS server like Google (8.8.8.8).

- **Question 3:** What role does the DNS server play in this scenario?
  - The DNS server translates domain names to IP addresses for easier access.

---

### **Scenario 4: Network Protocols**
A company is setting up a file-sharing system for its employees. They want to ensure secure and efficient file transfers.

- **Question 1:** Which protocol would you recommend for secure file transfers (FTP, SFTP, or TFTP)? Why?
  - SFTP is recommended as it encrypts both data and authentication.

- **Question 2:** What is the difference between TCP and UDP, and which one would be more suitable for this use case?
  - TCP ensures reliable data transfer, while UDP is faster but less reliable. TCP is better for file transfers.

- **Question 3:** How does HTTPS ensure secure communication compared to HTTP?
  - HTTPS encrypts data using SSL/TLS, preventing interception.

---

### **Scenario 5: Network Devices**
You are setting up a network for a small business. The network includes 20 computers, a printer, and a server.

- **Question 1:** What network device would you use to connect all the computers within the same network?
  - A network switch.

- **Question 2:** If the business wants to connect to the internet, what additional device would you need?
  - A router.

- **Question 3:** What is the difference between a hub and a switch, and which one would you recommend for this setup?
  - A switch is better as it intelligently forwards packets, reducing collisions.

---

### **Scenario 6: Troubleshooting Connectivity**
A user cannot connect to the internet, but other devices on the same network can.

- **Question 1:** What steps would you take to diagnose the issue?
  - Check physical connections, IP configuration, and network settings.

- **Question 2:** How would you check if the issue is with the user's IP configuration?
  - Run `ipconfig /all` (Windows) or `ifconfig` (Linux/Mac) to verify IP settings.

- **Question 3:** What command-line tools would you use to troubleshoot this problem?
  - `ping`, `ipconfig`, `tracert`, `nslookup`.

---

### **Scenario 7: Wireless Networking**
A company is setting up a wireless network for its employees.

- **Question 1:** What security protocol would you recommend (WEP, WPA, or WPA2)? Why?
  - WPA2, as it provides the strongest encryption.

- **Question 2:** How would you prevent unauthorized devices from connecting to the network?
  - Use MAC filtering and strong passwords.

- **Question 3:** What factors affect wireless signal strength?
  - Obstacles, interference, and distance from the router.

---

### **Scenario 8: Network Address Translation (NAT)**
A small business has a single public IP address but needs to connect multiple devices to the internet.

- **Question 1:** How does NAT help in this situation?
  - NAT allows multiple devices to share one public IP.

- **Question 2:** What is the difference between static NAT and dynamic NAT?
  - Static NAT maps a private IP to a fixed public IP, while dynamic NAT assigns public IPs from a pool.

- **Question 3:** What device typically performs NAT in a home or small office network?
  - A router.

---

### **Scenario 9: VLANs**
A company wants to segment its network into VLANs for security and performance reasons.

- **Question 1:** What is the purpose of VLANs?
  - VLANs segment a network logically to improve security and efficiency.

- **Question 2:** How would you configure VLANs on a switch?
  - Use switch commands to assign ports to VLANs.

- **Question 3:** What is trunking, and why is it important?
  - Trunking allows VLAN traffic to pass between switches.

---

### **Scenario 10: Firewalls and Security**
A company wants to protect its internal network from external threats.

- **Question 1:** What is the role of a firewall?
  - It filters incoming and outgoing traffic based on security rules.

- **Question 2:** What is the difference between a stateful and stateless firewall?
  - A stateful firewall tracks session states; a stateless one checks packets individually.

- **Question 3:** How would you configure a firewall to allow only HTTP and HTTPS traffic?
  - Set rules to allow TCP ports 80 and 443.

