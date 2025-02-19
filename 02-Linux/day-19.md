# IPTables Scenario Guide

## 1. Cinnamoroll Connection (Restrict to Bakery’s IP Address)
Cinnamoroll wants to allow only traffic from his bakery's IP (`192.168.1.100`) and block all other connections.

```bash
iptables -A INPUT -s 192.168.1.100 -j ACCEPT
iptables -A INPUT -j DROP
```

This ensures that only the bakery can access the network.

---

## 2. Hello Kitty's HTTP Server (Allow Only HTTP)
Hello Kitty runs an HTTP server for her online store. She needs to allow only HTTP (`port 80`) traffic and block everything else.

```bash
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -j DROP
```

This allows web traffic while rejecting all other types.

---

## 3. Keroppi's Firewall (Log Dropped Packets)
Keroppi wants to log all dropped packets in a playful way.

```bash
iptables -A INPUT -j LOG --log-prefix "Keroppi-Watch: " --log-level 4
iptables -A INPUT -j DROP
```

This logs all dropped packets with the prefix `Keroppi-Watch:`.

---

## 4. My Melody’s Birthday Party (Allow Only Friends' IPs)
My Melody wants to invite only her friends (`192.168.1.101`, `192.168.1.102`) to her birthday party.

```bash
iptables -A INPUT -s 192.168.1.101 -j ACCEPT
iptables -A INPUT -s 192.168.1.102 -j ACCEPT
iptables -A INPUT -j DROP
```

This ensures that only invited guests can access the network.

---

## 5. Kuromi’s Security (Custom Chain for Mischief Management)
Kuromi wants to create a custom chain to manage her mischievous friends.

```bash
iptables -N MISCHIEF_CONTROL
iptables -A MISCHIEF_CONTROL -s 192.168.1.200 -j REJECT
iptables -A MISCHIEF_CONTROL -s 192.168.1.201 -j ACCEPT
iptables -A INPUT -j MISCHIEF_CONTROL
```

This creates a custom chain (`MISCHIEF_CONTROL`), blocks one mischievous friend (`192.168.1.200`), allows another (`192.168.1.201`), and applies the chain to incoming traffic.

---

## Summary
These `iptables` rules help secure each character’s environment:
- **Cinnamoroll:** Only allows traffic from the bakery.
- **Hello Kitty:** Only allows HTTP traffic.
- **Keroppi:** Logs dropped packets.
- **My Melody:** Allows only friends to connect.
- **Kuromi:** Manages mischievous friends with a custom chain.

