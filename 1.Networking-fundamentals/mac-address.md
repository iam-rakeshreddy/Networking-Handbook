# MAC Address — Quick Revision Notes

## 1. What Is a MAC Address?

A **MAC (Media Access Control) address** is a Layer 2 address used to identify a network interface within a local network.

- **OSI Layer:** Layer 2 — Data Link
- **Size:** 48 bits (6 bytes) for standard Ethernet MAC addresses
- **Format:** Hexadecimal
- **Purpose:** Deliver Ethernet frames to the correct device or group.

**Example:**
```text
00:1A:2B:3C:4D:5E
```

## 2. MAC Address Structure

A typical MAC address contains 6 bytes.

```text
00:1A:2B : 3C:4D:5E
|--------| |--------|
First 3   Last 3
bytes     bytes
```

- **First 3 bytes:** Traditionally associated with the manufacturer through an IEEE-assigned OUI.
- **Last 3 bytes:** Often assigned by the manufacturer to identify an interface.

**Remember:** Locally administered and randomized MAC addresses may not reveal the actual manufacturer.

## 3. Types of MAC Addresses

| Type | Purpose | Example |
|---|---|---|
| Unicast | One destination interface | `00:1A:2B:3C:4D:5E` |
| Multicast | A group of interfaces | `01:00:5E:00:00:01` |
| Broadcast | All devices in the Layer 2 broadcast domain | `FF:FF:FF:FF:FF:FF` |

## 4. MAC Address vs. IP Address

| MAC Address | IP Address |
|---|---|
| Layer 2 | Layer 3 |
| Used for local frame delivery | Used for addressing and routing |
| Example: `AA:BB:CC:DD:EE:FF` | Example: `192.168.1.10` |
| Used by Ethernet switches | Used by hosts and routers |
| Ethernet addresses change across routed hops | IP addresses usually remain the same across routed hops, unless translated or modified |

**Easy example:** IP identifies the network-layer destination; MAC identifies the next local Layer 2 destination.

When communicating outside the local network, a computer normally sends the Ethernet frame to its default gateway's MAC address.

## 5. How MAC Addresses Work

Example: Computer A communicates with Computer B on the same subnet.

```text
Computer A
     |
     | 1. Find destination MAC using ARP
     v
Ethernet Switch
     |
     | 2. Check destination MAC table
     v
Computer B
```

### Process

1. Computer A checks whether Computer B is on the local subnet.
2. It checks the ARP cache for Computer B's MAC address.
3. If unknown, it sends an ARP request.
4. Computer B replies with its MAC address.
5. Computer A sends an Ethernet frame to that MAC.
6. The switch forwards the frame through the appropriate port if the destination is known.

**Remember:** A switch learns from the **source MAC** and forwards using the **destination MAC**.

## 6. MAC Address Table

A switch maintains a table that maps MAC addresses to ports and VLANs.

| MAC Address | Switch Port |
|---|---|
| AA:AA:AA:AA:AA:AA | Gi0/1 |
| BB:BB:BB:BB:BB:BB | Gi0/2 |

- **Learn:** Read the source MAC of an incoming frame.
- **Forward:** Send a frame to the known destination port.
- **Flood:** Send a frame through relevant ports when its destination is unknown, or when the frame is a broadcast.
- **Age out:** Remove dynamic entries after inactivity.

## 7. What Is ARP?

**ARP (Address Resolution Protocol)** finds the MAC address associated with an IPv4 address on a local network.

Example:

```text
IP Address: 192.168.1.20
MAC Address: BB:BB:BB:BB:BB:BB
```

| ARP Message | Purpose |
|---|---|
| ARP Request | Asks which device has an IPv4 address |
| ARP Reply | Provides the corresponding MAC address |
| Gratuitous ARP | Announces or checks the sender's own IPv4 address |

**IPv6 uses NDP (Neighbor Discovery Protocol), not ARP.**

### View the ARP / Neighbor Cache

**Windows**
```powershell
arp -a
```

**Linux / Kali Linux**
```bash
ip neigh
```

## 8. How to Find Your MAC Address

### Windows
```powershell
ipconfig /all
getmac /v
```

### Linux / Kali Linux
```bash
ip link show
ip -br link
```

### macOS
```bash
ifconfig
```

Look for `Physical Address` on Windows or `link/ether` on Linux.

**Note:** One computer can have multiple MAC addresses for Wi-Fi, Ethernet, virtual machines and other network interfaces.

## 9. MAC Address and Ethernet Frames

An Ethernet frame contains:

```text
+------------------+
| Destination MAC  | 6 bytes
+------------------+
| Source MAC       | 6 bytes
+------------------+
| Type / Length    | 2 bytes
+------------------+
| Payload          | Variable
+------------------+
| FCS              | 4 bytes
+------------------+
```

- **Destination MAC:** Intended receiver or group.
- **Source MAC:** Sending interface.
- **Type/Length:** Indicates the upper-layer protocol or payload length.
- **Payload:** Carries data, such as an IP packet.
- **FCS:** Detects frame transmission errors.

## 10. MAC Address Security

| Vulnerability / Concept | Meaning | Defensive Measure |
|---|---|---|
| MAC spoofing | Changing or impersonating a MAC address | Use stronger authentication, such as 802.1X where appropriate |
| ARP spoofing | Sending forged IP-to-MAC mappings | Dynamic ARP Inspection and network monitoring |
| MAC flooding | Attempting to exhaust a switch's MAC table | Port security and MAC learning limits |
| Rogue devices | Unauthorized devices connected to a network | Network access control and asset monitoring |
| MAC randomization | Using changing MAC addresses to improve privacy | Account for randomized addresses during device inventory |

**Security takeaway:** MAC addresses can often be spoofed. MAC filtering alone is not reliable authentication.

## 11. MAC Address Analysis with Wireshark

Capture traffic on an interface you are authorized to monitor.

| Display Filter | Purpose |
|---|---|
| `arp` | Show ARP packets |
| `eth.dst == ff:ff:ff:ff:ff:ff` | Show Ethernet broadcast frames |
| `eth.src == aa:bb:cc:dd:ee:ff` | Filter by source MAC |
| `eth.dst == aa:bb:cc:dd:ee:ff` | Filter by destination MAC |
| `eth.addr == aa:bb:cc:dd:ee:ff` | Show packets involving that MAC |

Replace the example address with an address from your packet capture.

**Important:** On a switched network, you usually see traffic available to your interface, not every packet exchanged across the entire network.

## 12. Quick Revision — Interview Questions

| Question | Quick Answer |
|---|---|
| Which OSI layer uses MAC addressing? | Layer 2 |
| What is the standard Ethernet MAC size? | 48 bits |
| What is the Ethernet broadcast MAC? | `FF:FF:FF:FF:FF:FF` |
| What resolves IPv4 addresses to MAC addresses? | ARP |
| What does a switch learn from an incoming frame? | Source MAC and incoming port/VLAN |
| What is the destination MAC used for? | Local Layer 2 frame delivery |
| What happens to MAC addresses at a router? | A new Layer 2 frame is created for the next link |
| Can a MAC address be changed? | Often yes, if the OS/interface supports it |
| Can MAC filtering prevent all unauthorized access? | No |
| What does IPv6 use instead of ARP? | NDP |
| What is a MAC table? | A switch's MAC-to-port/VLAN forwarding table |

## 13. Practical Commands to Remember

```bash
# Display network interfaces and MAC addresses
ip link show

# Display neighbor cache
ip neigh

# Capture ARP traffic on a Linux interface
sudo tcpdump -i eth0 -nn arp
```

Replace `eth0` with your actual interface name.



---

### Final Takeaway

**MAC = Layer 2 | IP = Layer 3 | ARP = IPv4-to-MAC resolution | Switch = MAC-based forwarding | Router = IP-based routing**

