# 🌐 Network Models: OSI and TCP/IP

> Learning documentation for understanding computer networking, OSI layers, TCP/IP architecture, data flow, protocols, and practical examples.

## 📚 Table of Contents

- [1. Introduction to Network Models](#1-introduction-to-network-models)
- [2. What Is the OSI Model?](#2-what-is-the-osi-model)
- [3. OSI Model Diagram](#3-osi-model-diagram)
- [4. Explanation of the Seven OSI Layers](#4-explanation-of-the-seven-osi-layers)
- [5. How Data Flows Through OSI Layers](#5-how-data-flows-through-osi-layers)
- [6. Encapsulation and Decapsulation](#6-encapsulation-and-decapsulation)
- [7. What Is the TCPIP Model?](#7-what-is-the-tcpip-model)
- [8. OSI vs TCPIP Model](#8-osi-vs-tcpip-model)
- [9. Real-World Example: Opening a Website](#9-real-world-example-opening-a-website)
- [10. Important Protocols and Their Layers](#10-important-protocols-and-their-layers)
- [11. Quick Revision Notes](#11-quick-revision-notes)
- [12. Practice Questions with Answers](#12-practice-questions-with-answers)

---

## 1. Introduction to Network Models

### What is a network model?

A **network model** is a conceptual framework that explains how devices communicate and exchange data over a network.

It divides network communication into layers, with each layer responsible for specific tasks.

### Why do we need network models?

Imagine sending a parcel to a friend in another city. Several tasks must happen:

1. Pack the item.
2. Write the sender's and receiver's addresses.
3. Transport the parcel.
4. Deliver it to the correct destination.
5. Open the parcel and use the item.

Computer networking works similarly. Data must be prepared, addressed, transmitted, routed, delivered, and interpreted.

Network models help us understand these processes in an organized way.

### Types of network models

There are two important network models:

| Model | Number of layers | Main purpose |
|---|---:|---|
| OSI Model | 7 | Explains network communication in seven distinct layers |
| TCP/IP Model | 4 | Describes the practical architecture used for communication over the Internet |

**Remember:** The OSI model is useful for learning and troubleshooting. The TCP/IP model describes the architecture behind real-world Internet communication.

---

## 2. What Is the OSI Model?

OSI stands for **Open Systems Interconnection**.

It is a conceptual model developed by the International Organization for Standardization (ISO) to describe how data moves between networked systems.

The OSI model contains seven layers. Each layer performs a specific function and interacts with the layers above or below it.

### The seven OSI layers

From top to bottom:

1. Application
2. Presentation
3. Session
4. Transport
5. Network
6. Data Link
7. Physical

---

## 3. OSI Model Diagram

### Seven-layer architecture

```text
          SENDER                          RECEIVER
     ┌─────────────────┐             ┌─────────────────┐
 L7  │   Application   │             │   Application   │
     ├─────────────────┤             ├─────────────────┤
 L6  │  Presentation   │             │  Presentation   │
     ├─────────────────┤             ├─────────────────┤
 L5  │     Session     │             │     Session     │
     ├─────────────────┤             ├─────────────────┤
 L4  │    Transport    │             │    Transport    │
     ├─────────────────┤             ├─────────────────┤
 L3  │     Network     │             │     Network     │
     ├─────────────────┤             ├─────────────────┤
 L2  │   Data Link     │             │   Data Link     │
     ├─────────────────┤             ├─────────────────┤
 L1  │    Physical     │             │    Physical     │
     └────────┬────────┘             └────────▲────────┘
              │                               │
              ▼                               │
       Transmission over the network ─────────┘
```

The sender processes data from Layer 7 down to Layer 1. The receiver processes incoming data from Layer 1 up to Layer 7.

In practice, communication passes through network interfaces, switches, routers, and other devices as needed. Not every device processes all seven layers.

### How to understand the diagram

- **Sender:** Converts application data into a form suitable for transmission.
- **Network:** Carries the transmitted bits toward the destination.
- **Receiver:** Reconstructs and interprets the data for the receiving application.

Each layer provides services to the layer above it and uses services from the layer below it.

---

## 4. Explanation of the Seven OSI Layers

## Layer 7: Application Layer

**Main purpose:** Provides network services to applications used by people.

This is the layer closest to the user. It enables applications to access network services such as web browsing, email, and file transfers.

### Real-world example

When you open a browser and visit `https://example.com`, the browser uses application-layer protocols to communicate with the website.

### Important protocols

- HTTP — Hypertext Transfer Protocol
- HTTPS — HTTP secured using TLS
- DNS — Domain Name System
- SMTP — Sending email
- IMAP — Accessing and synchronizing email
- FTP — File Transfer Protocol

### Why is this layer important?

- Enables applications to communicate over networks.
- Provides services such as web access and email.
- Defines how applications request and exchange information.

**Easy memory trick:** Application Layer = Network services for applications.

---

## Layer 6: Presentation Layer

**Main purpose:** Handles data representation and transformation.

Different systems may represent data in different formats. The Presentation Layer describes functions that help make data usable by the receiving application.

### Main responsibilities

1. Data formatting and translation.
2. Encryption and decryption.
3. Compression and decompression.

### Real-world example

Suppose you send a photograph to another computer.

The image must be represented in a format the receiving software understands. Data may also be compressed or encrypted as part of the communication process.

### Examples

- Character encoding such as UTF-8.
- Data formats such as JPEG and PNG.
- Encryption and compression functions.

**Important clarification:** TLS encryption is commonly associated with the Presentation Layer in simplified OSI explanations, but real Internet implementations generally integrate TLS with application protocols and the TCP/IP stack. JPEG and PNG are data formats, not network protocols.

### Why is this layer important?

- Helps systems interpret data consistently.
- Supports encryption and decryption.
- Can reduce the size of data through compression.

**Easy memory trick:** Presentation Layer = Format, encrypt, compress.

---

## Layer 5: Session Layer

**Main purpose:** Manages logical conversations between applications.

A session represents an ongoing exchange of information between communicating parties.

### Main responsibilities

- Establishing a communication session.
- Maintaining and coordinating a session.
- Synchronization and recovery points in some communication systems.
- Managing the orderly ending of a session.

### Real-world example

Imagine a remote collaboration application where two participants exchange information during a meeting. The application must manage the ongoing interaction and its state.

The Session Layer provides a conceptual way to understand this kind of communication management.

### Examples

- Session management concepts in remote procedure calls.
- Dialog control and synchronization.
- Application-managed session identifiers and state.

**Important clarification:** Real-world applications often implement session management at the application layer rather than using a separate Session Layer protocol.

### Why is this layer important?

- Organizes communication between applications.
- Helps coordinate ongoing exchanges.
- Provides a useful model for understanding session management and synchronization.

**Easy memory trick:** Session Layer = Start, manage, and end conversations.

---

## Layer 4: Transport Layer

**Main purpose:** Provides communication between processes running on different hosts.

The Transport Layer handles end-to-end transport functions. Depending on the protocol, these may include reliability, segmentation, ordering, retransmission, and flow control.

### Main responsibilities

- Dividing application data into smaller units.
- Using port numbers to identify communicating processes.
- Supporting reliable delivery when the protocol provides it.
- Managing ordering and retransmission when supported.
- Multiplexing data from multiple applications.

### Important protocols

- TCP — Transmission Control Protocol
- UDP — User Datagram Protocol

### TCP vs UDP

| Feature | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented | Connectionless |
| Delivery guarantee | Reliable delivery of the byte stream | No delivery guarantee |
| Ordering | Preserves byte order | No ordering guarantee |
| Retransmission | Supported | Not provided by UDP itself |
| Common uses | Web traffic, SSH, file transfers | DNS queries, voice and video traffic, gaming |

Applications may add reliability or other features on top of UDP.

### What are port numbers?

Port numbers help a computer direct incoming transport traffic to the appropriate application or service.

Examples:

- HTTP — TCP port 80
- HTTPS — TCP port 443
- SSH — TCP port 22
- DNS — commonly UDP port 53; TCP port 53 is also used

Modern HTTP/3 uses QUIC over UDP rather than TCP.

### Why is this layer important?

- Helps deliver data to the correct application process.
- Supports reliable communication through TCP.
- Allows multiple applications to communicate simultaneously.
- Supports different transport requirements through TCP and UDP.

**Easy memory trick:** Transport Layer = Process-to-process delivery and ports.

---

## Layer 3: Network Layer

**Main purpose:** Moves packets between networks using logical addressing and routing.

The Network Layer determines how data can travel from a source network to a destination network.

### Main responsibilities

- Logical addressing using IP addresses.
- Routing packets between networks.
- Selecting paths through routing decisions.
- Forwarding packets toward their destinations.

### Important protocols

- IPv4 — Internet Protocol version 4
- IPv6 — Internet Protocol version 6
- ICMP — Internet Control Message Protocol

### What is an IP address?

An IP address identifies a network interface logically within an IP network.

Example:

```text
Source IP:      192.168.1.10
Destination IP: 203.0.113.20
```

The source and destination IP addresses help identify where the packet originates and where it is intended to go.

### What does a router do?

A router examines IP packet information and uses its routing table to decide where to forward the packet next.

For communication across different networks, routers forward packets toward the destination.

### Why is this layer important?

- Enables communication across different networks.
- Provides logical addressing.
- Supports routing and packet forwarding.
- Allows the Internet to operate as interconnected networks.

**Easy memory trick:** Network Layer = IP addresses and routing.

---

## Layer 2: Data Link Layer

**Main purpose:** Transfers frames across a local network link.

The Data Link Layer organizes data into frames and uses link-level addressing and rules to communicate over a particular network link.

### Main responsibilities

- Framing data.
- Using MAC addresses in Ethernet and Wi-Fi.
- Detecting many transmission errors using mechanisms such as frame checksums.
- Controlling access to a shared transmission medium where applicable.
- Delivering frames across a local link.

### Important technologies and protocols

- Ethernet (IEEE 802.3)
- Wi-Fi MAC (IEEE 802.11)
- VLAN tagging (IEEE 802.1Q)

### What is a MAC address?

A MAC address is a link-layer address used by network interfaces in technologies such as Ethernet and Wi-Fi.

Example:

```text
Source MAC:      00:1A:2B:3C:4D:5E
Destination MAC: 00:AA:BB:CC:DD:EE
```

MAC addresses are used for delivery over a local network link. They are not substitutes for IP addresses.

### What does a switch do?

A typical Ethernet switch learns MAC addresses and forwards Ethernet frames through the appropriate ports within a VLAN.

### Why is this layer important?

- Supports communication on local network links.
- Provides framing and link-level addressing.
- Helps switches forward frames.
- Detects certain transmission errors.

**Easy memory trick:** Data Link Layer = Frames and MAC addresses.

---

## Layer 1: Physical Layer

**Main purpose:** Transmits raw bits over a physical medium.

This layer describes how bits are represented and transmitted through electrical, optical, or radio signals.

### Main responsibilities

- Defining physical signaling characteristics.
- Specifying connectors and physical interfaces.
- Transmitting bits through copper cables, fiber-optic cables, or wireless signals.
- Defining relevant timing and transmission characteristics.

### Examples

- Ethernet physical interfaces and signaling.
- Fiber-optic transmission.
- Radio transmission used by Wi-Fi.
- Copper network cables.
- Repeaters and hubs, in traditional Ethernet contexts.

### Real-world example

When a computer sends data through an Ethernet cable, the bits are represented by physical signals that travel over the cable.

For Wi-Fi, information is carried through radio signals instead.

### Why is this layer important?

- Makes actual transmission of bits possible.
- Defines the physical medium and signaling.
- Provides the foundation on which higher networking layers operate.

**Easy memory trick:** Physical Layer = Bits, signals, and media.

---

## 5. How Data Flows Through OSI Layers

Let's understand how data travels when you send a message from one computer to another.

Suppose Computer A sends the message:

`Hello, how are you?`

### Step 1: Sender-side processing

The message starts at the Application Layer and moves downward through the layers.

| Layer | What happens |
|---|---|
| L7 — Application | The application creates the message. |
| L6 — Presentation | Data may be encoded, encrypted, or compressed. |
| L5 — Session | Communication-session functions may be managed. |
| L4 — Transport | TCP or UDP processes the data and uses port numbers. |
| L3 — Network | An IP packet is formed with source and destination IP addresses. |
| L2 — Data Link | The packet is placed inside a link-layer frame. |
| L1 — Physical | Bits are transmitted as physical signals. |

The exact functions depend on the actual protocols and applications being used.

### Step 2: Data travels across the network

The data travels through the appropriate network medium and devices.

For example:

```text
Computer A
    |
    | Ethernet / Wi-Fi
    v
Network Switch
    |
    v
Router
    |
    v
Internet
    |
    v
Destination Network
    |
    v
Computer B
```

A switch generally forwards link-layer frames. A router forwards IP packets and normally uses a new link-layer frame for the next link.

### Step 3: Receiver-side processing

At the destination, data moves upward through the layers.

| Layer | What happens |
|---|---|
| L1 — Physical | Signals are received and interpreted as bits. |
| L2 — Data Link | Frames are processed and their payload is passed upward. |
| L3 — Network | IP packet information is processed. |
| L4 — Transport | TCP or UDP delivers data to the appropriate application process. |
| L5 — Session | Relevant session functions are handled if implemented. |
| L6 — Presentation | Data is decoded, decrypted, or decompressed as needed. |
| L7 — Application | The receiving application processes the message. |

The message is now available to the receiving application.

### Remember the direction

```text
SENDER                              RECEIVER

Application  (L7)                   Application  (L7)
     |                                    ▲
Presentation (L6)                   Presentation (L6)
     |                                    ▲
Session      (L5)                   Session      (L5)
     |                                    ▲
Transport    (L4)                   Transport    (L4)
     |                                    ▲
Network      (L3)                   Network      (L3)
     |                                    ▲
Data Link    (L2)                   Data Link    (L2)
     |                                    ▲
Physical     (L1)  ─── NETWORK ───> Physical     (L1)

       Encapsulation                 Decapsulation
```

**Key point:** The sender processes data downward, while the receiver processes it upward.

---

## 6. Encapsulation and Decapsulation

These are two important concepts in networking.

### What is encapsulation?

**Encapsulation** is the process of adding protocol information to data as it moves down the network stack.

Each layer adds information needed for its communication function.

### Encapsulation diagram

```text
Application Layer
┌─────────────────────────────┐
│       Application Data      │
└─────────────────────────────┘
               |
               v
Transport Layer
┌──────────────┬──────────────┐
│ TCP/UDP Header│ Application │
│              │     Data     │
└──────────────┴──────────────┘
               |
               v
Network Layer
┌────────────┬────────────────┐
│ IP Header  │ Transport Data │
└────────────┴────────────────┘
               |
               v
Data Link Layer
┌─────────────┬───────────────┬───────────┐
│ Frame Header│   IP Packet   │ Frame FCS │
└─────────────┴───────────────┴───────────┘
               |
               v
Physical Layer
          Bits / Signals
```

This diagram is simplified. Real headers and trailers vary by protocol, and some links use different framing formats.

### Protocol Data Units (PDUs)

Each layer has a commonly used name for its data unit.

| OSI layer | Data unit |
|---|---|
| Application (L7) | Data |
| Presentation (L6) | Data |
| Session (L5) | Data |
| Transport (L4) | Segment (TCP) / Datagram (UDP) |
| Network (L3) | Packet |
| Data Link (L2) | Frame |
| Physical (L1) | Bits |

### What is decapsulation?

**Decapsulation** is the reverse process. The receiving system processes the incoming data and removes or interprets the relevant protocol information as data moves upward through the stack.

For example:

1. The Data Link Layer processes the frame.
2. The Network Layer processes the IP packet.
3. The Transport Layer processes the TCP segment or UDP datagram.
4. The application receives its data.

### Quick memory trick

- Sender = Encapsulation.
- Receiver = Decapsulation.

---

## 7. What Is the TCP/IP Model?

TCP/IP stands for **Transmission Control Protocol / Internet Protocol**.

The TCP/IP model describes the architecture used for communication across interconnected IP networks, including the Internet.

It is commonly represented using four layers.

### Four layers of the TCP/IP model

| Layer | Main responsibility | Examples |
|---|---|---|
| Application | Application-level communication and data representation | HTTP, DNS, SMTP, SSH |
| Transport | Process-to-process transport | TCP, UDP |
| Internet | IP addressing and routing | IPv4, IPv6, ICMP |
| Network Access / Link | Communication over a local link | Ethernet, Wi-Fi |

Different references use names such as **Network Access**, **Link**, or **Network Interface** for the bottom layer.

### TCP/IP model diagram

```text
┌─────────────────────────────┐
│  Application Layer          │
│  HTTP, DNS, SMTP, SSH        │
├─────────────────────────────┤
│  Transport Layer            │
│  TCP, UDP                    │
├─────────────────────────────┤
│  Internet Layer             │
│  IPv4, IPv6, ICMP            │
├─────────────────────────────┤
│  Network Access / Link      │
│  Ethernet, Wi-Fi             │
└─────────────────────────────┘
```

### How does TCP/IP work?

Suppose you open a website:

1. The application uses HTTP or HTTPS to request content.
2. The transport protocol carries the application data, commonly TCP or, for HTTP/3, QUIC over UDP.
3. IP provides addressing and routing across networks.
4. The link layer transmits data over Ethernet, Wi-Fi, or another link technology.

The receiving system processes the data through the corresponding networking stack.

**Important:** TCP/IP is not just TCP and IP. It includes a complete collection of protocols that work together to enable Internet communication.

---

## 8. OSI vs TCP/IP Model

The OSI model has seven layers, while the commonly taught TCP/IP model has four.

### Layer mapping diagram

```text
OSI MODEL                         TCP/IP MODEL

┌───────────────────┐
│ 7. Application    │
├───────────────────┤
│ 6. Presentation   │───────┐
├───────────────────┤       │
│ 5. Session        │───────┴──> ┌───────────────────┐
                                  │  Application      │
┌───────────────────┐             └───────────────────┘
│ 4. Transport      │───────────> ┌───────────────────┐
                                  │  Transport        │
┌───────────────────┐             └───────────────────┘
│ 3. Network        │───────────> ┌───────────────────┐
                                  │  Internet         │
┌───────────────────┐             └───────────────────┘
│ 2. Data Link      │───────┐
├───────────────────┤       ├────> ┌───────────────────┐
│ 1. Physical       │───────┘      │  Network Access   │
                                  └───────────────────┘
```

### Comparison table

| Feature | OSI Model | TCP/IP Model |
|---|---|---|
| Number of layers | 7 | 4 in the common model |
| Nature | Reference model | Protocol architecture and model |
| Developed by | ISO | DARPA-sponsored research; developed through Internet research and standardization |
| Main use | Learning, conceptual understanding, troubleshooting | Internet and practical network communication |
| Session layer | Separate conceptual layer | Functions generally included in the application layer or implemented by applications |
| Presentation layer | Separate conceptual layer | Functions generally included in the application layer or implemented by applications |
| Network layer equivalent | Network Layer | Internet Layer |
| Data Link and Physical | Separate layers | Usually combined into the Network Access / Link layer |

### Which model should you learn first?

Start with the OSI model because it clearly separates networking responsibilities. Then learn how those responsibilities map to TCP/IP and real-world protocols.

**Remember:** OSI explains networking in seven conceptual layers; TCP/IP describes the architecture used for practical Internet communication.

---

## 9. Real-World Example: Opening a Website

Let's understand what happens when you type:

`https://example.com`

### Step 1: Application Layer

Your browser initiates an HTTPS request.

DNS may be used to resolve the hostname to an IP address before the browser connects to the server.

### Step 2: Presentation and Session concepts

TLS provides encryption and integrity protection for HTTPS communication. Application software also handles data representation and session-related functions as required.

In real implementations, these functions are not necessarily separate OSI layers.

### Step 3: Transport Layer

For traditional HTTP/1.1 or HTTP/2 over HTTPS, the browser commonly uses TCP.

For HTTP/3, the browser uses QUIC over UDP.

Transport protocols and ports help deliver traffic to the correct service.

### Step 4: Network Layer

IP addresses identify the source and destination interfaces logically, and routers forward packets toward the destination.

### Step 5: Data Link Layer

The computer sends frames over the local Ethernet or Wi-Fi link.

If the destination is outside the local network, the frame is normally addressed to the next hop, such as the default gateway, rather than directly to the remote web server's MAC address.

### Step 6: Physical Layer

Bits are transmitted using electrical signals, optical signals, or radio waves, depending on the medium.

### Step 7: The web server responds

The server's response returns through the network. Your computer processes the received data through its networking stack, and the browser renders the page.

### End-to-end flow

```text
Browser
   |
   | HTTPS / HTTP
   v
TCP or QUIC
   |
   | IP packets
   v
Local Ethernet / Wi-Fi
   |
   v
Router / Internet
   |
   v
Web Server
   |
   v
Response returns to browser
```

This is a simplified conceptual flow. DNS lookups, connection establishment, TLS negotiation, packet forwarding, and application processing may involve additional exchanges.

---

## 10. Important Protocols and Their Layers

| Protocol / Technology | Common layer association | Purpose |
|---|---|---|
| HTTP | Application | Web communication |
| HTTPS | Application with TLS security | Secure web communication |
| DNS | Application | Resolves domain names and other DNS records |
| DHCP | Application | Automatically configures IP networking parameters |
| SMTP | Application | Sends email |
| SSH | Application | Secure remote access |
| FTP | Application | File transfer |
| TCP | Transport | Reliable, ordered byte-stream transport |
| UDP | Transport | Connectionless datagram transport |
| IPv4 | Network / Internet | IP addressing and routing |
| IPv6 | Network / Internet | IP addressing and routing using IPv6 |
| ICMP | Network / Internet | Network control and diagnostic messages |
| ARP | Between IP and link functions in IPv4 networks | Resolves IPv4 addresses to link-layer addresses on a local network |
| Ethernet | Data Link and Physical | Wired local networking |
| Wi-Fi (IEEE 802.11) | Data Link and Physical | Wireless local networking |

**Note:** ARP is specific to IPv4 networks. IPv6 uses Neighbor Discovery, which operates through ICMPv6. Layer associations can be simplified differently in different textbooks.

---

## 11. Quick Revision Notes

### OSI layers in one table

| Layer | Name | Main function | PDU / common concept |
|---:|---|---|---|
| 7 | Application | Application network services | Data |
| 6 | Presentation | Data representation, encryption, compression concepts | Data |
| 5 | Session | Session and dialog management concepts | Data |
| 4 | Transport | Process delivery, ports, transport reliability | Segment / Datagram |
| 3 | Network | Logical addressing and routing | Packet |
| 2 | Data Link | Frames and link-level addressing | Frame |
| 1 | Physical | Signals and bit transmission | Bits |

### Important differences to remember

**IP address vs MAC address**

- IP address: Logical addressing used to route packets between networks.
- MAC address: Link-layer addressing used to deliver frames over a local network link.

**Switch vs Router**

- Switch: Typically forwards Ethernet frames based on MAC addresses within a VLAN.
- Router: Forwards IP packets between networks based on routing information.

**TCP vs UDP**

- TCP: Reliable, ordered byte-stream transport.
- UDP: Connectionless datagram transport without built-in delivery or ordering guarantees.

**Packet vs Frame**

- Packet: Network-layer data unit, such as an IP packet.
- Frame: Data-link-layer unit that carries a packet over a link.

**Encapsulation vs Decapsulation**

- Encapsulation: Adding protocol information as data moves down the stack.
- Decapsulation: Processing protocol information as data moves up the stack.

### Which layer should you check during troubleshooting?

| Problem | Layers or areas to investigate |
|---|---|
| Damaged cable or no physical link | Layer 1 |
| Local Ethernet or VLAN issue | Layer 2 |
| Incorrect IP address or routing | Layer 3 |
| Port blocked or transport connection failure | Layer 4 and firewalls |
| DNS resolution failure | Application / DNS configuration |
| Website or application error | Application layer and relevant dependencies |
| TLS certificate or handshake failure | TLS and application configuration |

These are starting points rather than strict rules. Many network problems involve multiple layers.

---
