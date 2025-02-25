# Linux Networking Commands
---

## 1. **ifconfig** (Interface Configuration)
### **Definition:**
Used to configure or display network interfaces (deprecated, replaced by `ip` command).

### **Syntax:**
```bash
ifconfig [interface] [options]
```

### **Example:**
```bash
ifconfig eth0
```
Displays details of the `eth0` network interface.

---

## 2. **ip** (IP Configuration)
### **Definition:**
Displays and manages IP addresses and routing.

### **Syntax:**
```bash
ip [options] [object] [command]
```

### **Example:**
```bash
ip addr show
```
Displays all network interfaces and assigned IP addresses.

---

## 3. **ping** (Packet Internet Groper)
### **Definition:**
Checks connectivity between two hosts by sending ICMP packets.

### **Syntax:**
```bash
ping [options] destination
```

### **Example:**
```bash
ping google.com
```
Sends continuous pings to `google.com`.

---

## 4. **netstat** (Network Statistics)
### **Definition:**
Displays network connections, routing tables, and statistics (deprecated, replaced by `ss`).

### **Syntax:**
```bash
netstat [options]
```

### **Example:**
```bash
netstat -tulnp
```
Displays active TCP/UDP ports and listening services.

---

## 5. **ss** (Socket Statistics)
### **Definition:**
Replaces `netstat` to display detailed socket information.

### **Syntax:**
```bash
ss [options]
```

### **Example:**
```bash
ss -tulnp
```
Displays active TCP/UDP sockets.

---

## 6. **traceroute** (Trace Route)
### **Definition:**
Shows the route packets take to a destination.

### **Syntax:**
```bash
traceroute [destination]
```

### **Example:**
```bash
traceroute google.com
```
Shows the path packets take to reach `google.com`.

---

## 7. **dig** (Domain Information Groper)
### **Definition:**
Retrieves DNS information for a domain.

### **Syntax:**
```bash
dig [domain]
```

### **Example:**
```bash
dig google.com
```
Displays DNS records for `google.com`.

---

## 8. **nslookup** (Name Server Lookup)
### **Definition:**
Queries DNS servers for domain name resolution.

### **Syntax:**
```bash
nslookup [domain]
```

### **Example:**
```bash
nslookup google.com
```
Retrieves the IP address of `google.com`.

---

## 9. **curl** (Client URL)
### **Definition:**
Transfers data from or to a server using protocols like HTTP, HTTPS, FTP.

### **Syntax:**
```bash
curl [options] [URL]
```

### **Example:**
```bash
curl https://example.com
```
Fetches the contents of `example.com`.

---

## 10. **wget** (Web Get)
### **Definition:**
Downloads files from the web using HTTP, HTTPS, and FTP.

### **Syntax:**
```bash
wget [options] [URL]
```

### **Example:**
```bash
wget https://example.com/file.zip
```
Downloads `file.zip` from `example.com`.

---

## 11. **hostname** (Display Hostname)
### **Definition:**
Shows or sets the system’s hostname.

### **Syntax:**
```bash
hostname
```

### **Example:**
```bash
hostname
```
Displays the current hostname of the system.

---

## 12. **arp** (Address Resolution Protocol)
### **Definition:**
Shows and modifies the ARP cache.

### **Syntax:**
```bash
arp [options]
```

### **Example:**
```bash
arp -a
```
Displays the ARP table.

---

## 13. **route** (Routing Table Management)
### **Definition:**
Shows and manipulates the system’s IP routing table.

### **Syntax:**
```bash
route [options]
```

### **Example:**
```bash
route -n
```
Displays the routing table.

---

## 14. **nmap** (Network Mapper)
### **Definition:**
Scans networks and detects open ports and services.

### **Syntax:**
```bash
nmap [options] [target]
```

### **Example:**
```bash
nmap 192.168.1.1
```
Scans the target IP for open ports and services.

---

## Conclusion
These commands are essential for managing and troubleshooting networks in Linux. Understanding them helps diagnose connectivity issues, configure networks, and enhance system security.

For advanced networking tasks, refer to official Linux networking documentation or the `man` pages:
```bash
man [command]
```

