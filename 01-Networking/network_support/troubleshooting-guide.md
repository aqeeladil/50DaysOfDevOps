## Basic Networking Commands with Troubleshooting Scenarios

### 1. **ipconfig** (Windows) / **ifconfig** (Linux & Mac)
- This command provides details about your network configuration, including:
  - Your **IP address**
  - **Subnet mask**
  - **Default gateway**
  - **DNS servers**
- Example:
  ```sh
  ipconfig /all
  ```
  This will display complete network details.

#### **Troubleshooting Scenario:**
**Issue:** Unable to connect to the internet.

**Steps:**
1. Run `ipconfig /all` to check if your system has a valid IP address.
2. If the IP address is `169.254.x.x`, it means the system failed to obtain an IP from the DHCP server.
3. Run `ipconfig /release` and `ipconfig /renew` to request a new IP address.
4. If using static IP, verify the settings in **Network Adapter Properties**.

---

### 2. **nslookup**
- This command helps find the IP address of a domain name and vice versa.
- Useful for checking DNS resolution issues.
- Example:
  ```sh
  nslookup google.com
  ```
  This will return the IP address of Google’s servers.

#### **Troubleshooting Scenario:**
**Issue:** Unable to access websites while other network services work fine.

**Steps:**
1. Run `nslookup google.com` to check if the DNS server is resolving domain names correctly.
2. If the command fails, try `nslookup google.com 8.8.8.8` to query Google’s public DNS.
3. If Google's DNS works, there may be an issue with your ISP’s DNS settings.
4. Change your DNS to **8.8.8.8** (Google) or **1.1.1.1** (Cloudflare) in network settings.

---

### 3. **ping**
- Used to test the connectivity between two devices.
- Helps check if a server or website is reachable.
- Example:
  ```sh
  ping 8.8.8.8
  ```
  This will send packets to Google’s public DNS server and check the response time.

#### **Troubleshooting Scenario:**
**Issue:** Cannot browse the internet but can access local network resources.

**Steps:**
1. Run `ping 8.8.8.8` to check if the system can reach Google’s DNS.
2. If successful, DNS resolution might be the issue; use `nslookup` to verify.
3. If `ping` fails, check your router connection or contact your ISP.
4. If you receive **Request Timed Out**, your firewall might be blocking outbound traffic.

---

### 4. **tracert** (Windows) / **traceroute** (Linux & Mac)
- This command helps trace the path taken by packets from your system to a destination.
- Useful for identifying network delays and broken connections.
- Example:
  ```sh
  tracert google.com
  ```
  This will display each hop the packet takes before reaching Google.

#### **Troubleshooting Scenario:**
**Issue:** Slow internet or high latency when accessing a website.

**Steps:**
1. Run `tracert google.com` to check the route taken by your data.
2. If any hop shows a high response time, that indicates possible congestion.
3. If packets drop at a specific hop, it may indicate an issue with that network node.
4. Contact your ISP if latency is high beyond your local network.

---

### 5. **netstat**
- Displays active network connections and ports in use.
- Helps identify open connections on your system.
- Example:
  ```sh
  netstat -an
  ```
  This will list all active TCP/UDP connections along with their statuses.

#### **Troubleshooting Scenario:**
**Issue:** Suspicious network activity or high system resource usage.

**Steps:**
1. Run `netstat -an` to check for unusual active connections.
2. Look for external IPs that your system is communicating with unexpectedly.
3. If you find suspicious connections, note the **PID** and run `tasklist /FI "PID eq <PID>"` to identify the process.
4. Use a firewall to block unwanted connections or scan your system for malware.

---

### 6. **Telnet**
Telnet checks if a particular service is available on a specific port.

#### Scenario Example:
**Issue:** Users cannot connect to an internal database at `10.0.0.5` on port `3306`.

**Steps:**
1. Run:
   ```sh
   telnet 10.0.0.5 3306
   ```
2. **Response:**
   - If successful, the port is open.
   - If unsuccessful:
     - A firewall may be blocking the connection.
     - The service may not be running.

---

## The FixIt Framework for Troubleshooting
A structured 5-step approach for troubleshooting network and other IT-related issues.

### 1. Find the Problem
- Gather relevant data and define the exact issue.
- Ask clarifying questions:
  - Can the user access the service from another device?
  - Is the issue intermittent or constant?
  
#### Scenario Example:
**Issue:** A user cannot send emails.

- Ask: "Can you send emails from the webmail interface?"
- If webmail works, the issue is likely with the email client configuration.

### 2. Inspect the Symptoms
- Identify patterns or trends.
- Check logs and system messages.

#### Scenario Example:
**Issue:** Users report slow VPN connections.

- Inspect network logs for congestion.
- Monitor usage spikes during peak hours.

### 3. Exclude Possibilities
- Eliminate unlikely causes through logical deduction.

#### Scenario Example:
**Issue:** A branch office cannot access internal servers.

- Check: Is another branch experiencing the same issue?
- If only one branch is affected, the issue is local (ISP, router, or firewall).

### 4. Implement a Fixed Hypothesis
- Formulate and test a possible fix.

#### Scenario Example:
**Issue:** Users cannot access a web application.

- Hypothesis: The firewall is blocking traffic.
- Action: Temporarily disable the firewall.
- If the issue is resolved, adjust firewall rules accordingly.

### 5. Track and Document
- Monitor after applying fixes to ensure the issue is resolved.
- Maintain documentation for future reference.

---

## Three Troubleshooting Methods Using OSI Layers

### 1. Top-Down Approach
- Starts at the **Application Layer** and moves downward.

#### Scenario Example:
**Issue:** A video conferencing app is not working.

- Check application settings and configurations before inspecting network components.

### 2. Bottom-Up Approach
- Starts at the **Physical Layer** and moves upward.

#### Scenario Example:
**Issue:** A user's PC cannot connect to the network.

- Check:
  - Is the Ethernet cable properly plugged in?
  - Does switching ports on the switch resolve the issue?

### 3. Hybrid Approach
- Starts at the **Network Layer (Layer 3)** and branches outward.

#### Scenario Example:
**Issue:** Users in one subnet cannot access another subnet.

- Use:
  ```sh
  ping <destination IP>
  traceroute <destination IP>
  ```
- If traffic stops at a router, check routing tables and firewall rules.

---


