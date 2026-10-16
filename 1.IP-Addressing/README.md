# IP Addressing and Subnetting — Complete Revision Notes

> **Purpose:** Learn IPv4 addressing, subnet masks, IP classes, CIDR notation, subnetting, the block size method, and practical questions with step-by-step solutions.
>
> **Use this README for:** Quick revision, networking fundamentals, CCNA preparation, Linux/network administration, and technical interviews.

---

## Table of Contents

1. [IP Address Fundamentals](#1-ip-address-fundamentals)
2. [IPv4 Address Structure](#2-ipv4-address-structure)
3. [Public and Private IP Addresses](#3-public-and-private-ip-addresses)
4. [IP Address Classes](#4-ip-address-classes)
5. [Subnet Mask](#5-subnet-mask)
6. [CIDR Notation](#6-cidr-notation)
7. [Subnetting Fundamentals](#7-subnetting-fundamentals)
8. [Subnetting Formulas](#8-subnetting-formulas)
9. [Block Size Method](#9-block-size-method)
10. [Quick CIDR Reference Table](#10-quick-cidr-reference-table)
11. [Solved Practical Questions](#11-solved-practical-questions)
12. [Practice Questions](#12-practice-questions)
13. [Common Mistakes](#13-common-mistakes)
14. [One-Minute Revision Sheet](#14-one-minute-revision-sheet)

---

# 1. IP Address Fundamentals

## What is an IP address?

An **IP (Internet Protocol) address** is a logical address assigned to a network interface to identify it and enable communication over an IP network.

Example:

`192.168.1.10`

An IPv4 address is divided into two logical parts:

- **Network portion:** Identifies the network.
- **Host portion:** Identifies an interface within that network.

The subnet mask or CIDR prefix determines where the network portion ends and the host portion begins.

### Example

IP address: `192.168.1.10/24`

- Network address: `192.168.1.0`
- Host address: `192.168.1.10`
- Broadcast address: `192.168.1.255`
- Usable host range: `192.168.1.1 – 192.168.1.254`

## IPv4 vs. IPv6

| Feature | IPv4 | IPv6 |
|---|---|---|
| Address size | 32 bits | 128 bits |
| Format | Decimal, separated by dots | Hexadecimal, separated by colons |
| Example | `192.168.1.10` | `2001:db8::10` |
| Address space | About 4.3 billion addresses | Vastly larger address space |

This README focuses on IPv4 subnetting.

---

# 2. IPv4 Address Structure

An IPv4 address contains **32 bits**, divided into four octets.

Each octet contains 8 bits.

Example:

`192.168.1.10`

| Octet | Decimal | Binary |
|---|---:|---|
| 1 | 192 | `11000000` |
| 2 | 168 | `10101000` |
| 3 | 1 | `00000001` |
| 4 | 10 | `00001010` |

Full binary address:

`11000000.10101000.00000001.00001010`

## Binary place values

Each 8-bit octet uses these place values:

| Bit position | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Value | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |

### Example: Convert binary to decimal

Binary: `11000000`

Calculation:

`128 + 64 = 192`

Therefore, `11000000 = 192`.

### Example: Convert decimal to binary

Decimal: `10`

Calculation:

`8 + 2 = 10`

Place a `1` in the 8 and 2 positions.

Binary: `00001010`

### Important range

- Minimum value of an octet: `0`
- Maximum value of an octet: `255`
- Total possible values per octet: `256`

---

# 3. Public and Private IP Addresses

## Private IPv4 ranges

Private IP addresses are intended for use inside private networks, such as home, office, and cloud networks. They are not globally routed across the public Internet.

| Private range | CIDR | Default classful range |
|---|---|---|
| `10.0.0.0 – 10.255.255.255` | `10.0.0.0/8` | Class A |
| `172.16.0.0 – 172.31.255.255` | `172.16.0.0/12` | Class B |
| `192.168.0.0 – 192.168.255.255` | `192.168.0.0/16` | Class C |

**Memory trick:** Private IPv4 starts with `10`, `172.16–172.31`, or `192.168`.

## Public IP addresses

Public IP addresses are globally routable addresses allocated through the Internet addressing system.

Examples of private addresses:

- `192.168.1.10`
- `10.1.2.3`
- `172.20.5.10`

Example of a documentation address, not a real public host:

- `203.0.113.10`

## Special IPv4 addresses

| Range/address | Purpose |
|---|---|
| `127.0.0.0/8` | Loopback |
| `169.254.0.0/16` | IPv4 link-local |
| `0.0.0.0` | Unspecified address in appropriate contexts |
| `255.255.255.255` | Limited broadcast |
| `224.0.0.0/4` | Multicast |

Note: An IP address alone does not tell you whether a host is reachable. Routing, firewall rules, interface configuration, and other factors also matter.

---

# 4. IP Address Classes

IPv4 was historically divided into five classes. This is called **classful addressing**.

Modern networks use CIDR, but classes are still useful for understanding networking fundamentals and interview questions.

| Class | First octet | Default mask | Default prefix | Original purpose |
|---|---|---|---|---|
| A | 1–126 | `255.0.0.0` | `/8` | Large networks |
| B | 128–191 | `255.255.0.0` | `/16` | Medium networks |
| C | 192–223 | `255.255.255.0` | `/24` | Smaller networks |
| D | 224–239 | Not applicable | Not applicable | Multicast |
| E | 240–255 | Not applicable | Not applicable | Reserved/experimental |

Important details:

- `0.x.x.x` has special significance and is not ordinary Class A unicast space.
- `127.x.x.x` is reserved for loopback.
- Class D and Class E are not ordinary host-address classes.
- Classful defaults do not determine the actual subnet mask of a modern CIDR network.

### How to identify a class

Example: `172.16.5.10`

The first octet is `172`.

Since `172` falls between `128` and `191`, it is historically a **Class B** address.

Its classful default mask is `255.255.0.0`, or `/16`.

However, if the address is configured as `172.16.5.10/24`, its actual subnet mask is `/24`, not `/16`.

---

# 5. Subnet Mask

## What is a subnet mask?

A subnet mask identifies which bits of an IPv4 address represent the network prefix and which bits represent the host portion.

- Network bits are `1`.
- Host bits are `0`.

Example:

IP address: `192.168.1.10`

Subnet mask: `255.255.255.0`

Binary mask:

`11111111.11111111.11111111.00000000`

The first 24 bits are network bits, so the prefix is `/24`.

## Common subnet masks

| CIDR | Subnet mask | Network bits | Host bits |
|---|---|---:|---:|
| `/8` | `255.0.0.0` | 8 | 24 |
| `/16` | `255.255.0.0` | 16 | 16 |
| `/24` | `255.255.255.0` | 24 | 8 |
| `/25` | `255.255.255.128` | 25 | 7 |
| `/26` | `255.255.255.192` | 26 | 6 |
| `/27` | `255.255.255.224` | 27 | 5 |
| `/28` | `255.255.255.240` | 28 | 4 |
| `/29` | `255.255.255.248` | 29 | 3 |
| `/30` | `255.255.255.252` | 30 | 2 |

## How to calculate the network address

Use a bitwise AND between the IP address and the subnet mask.

Example:

IP: `192.168.1.10`

Mask: `255.255.255.0`

The first three octets remain unchanged, and the last octet becomes zero.

Network address: `192.168.1.0`

For `/24`, the last octet contains only host bits.

## Why do we need subnet masks?

Subnet masks help devices determine:

- Whether a destination is on the local subnet.
- Whether traffic should be sent directly to the destination.
- Whether traffic should be forwarded through a default gateway.

---

# 6. CIDR Notation

CIDR stands for **Classless Inter-Domain Routing**.

CIDR represents the network prefix using a slash followed by a number.

Example:

`192.168.1.10/24`

Here, `/24` means:

- 24 network bits.
- 8 host bits, because `32 - 24 = 8`.
- Subnet mask: `255.255.255.0`.

## CIDR formula

For an IPv4 prefix `/n`:

- Network bits = `n`
- Host bits = `32 - n`
- Total addresses = `2^(32 - n)`

For conventional subnets with network and broadcast addresses reserved:

- Usable host addresses = `2^(32 - n) - 2`

This usable-host formula normally applies to prefixes from `/0` through `/30`. `/31` and `/32` require special treatment.

### Example: `/26`

Host bits:

`32 - 26 = 6`

Total addresses:

`2^6 = 64`

Usable hosts in a conventional subnet:

`64 - 2 = 62`

Subnet mask:

`255.255.255.192`

### CIDR to subnet mask conversion

Example: `/27`

Step 1: Put 27 ones in the mask.

`11111111.11111111.11111111.11100000`

Step 2: Convert the final octet.

`128 + 64 + 32 = 224`

Answer:

`255.255.255.224`

---

# 7. Subnetting Fundamentals

## What is subnetting?

Subnetting divides a larger IP network into smaller logical networks called subnets.

### Why subnetting is used

- Reduces unnecessary broadcast traffic.
- Organizes networks by department, location, or purpose.
- Helps use address space efficiently.
- Supports network segmentation and access control.
- Simplifies routing and network administration.

## Borrowing host bits

When you increase the prefix length, you borrow bits from the host portion.

Example: Divide `192.168.1.0/24` into `/26` subnets.

Original prefix: `/24`

New prefix: `/26`

Bits borrowed:

`26 - 24 = 2`

Number of subnets:

`2^2 = 4`

Host bits remaining:

`32 - 26 = 6`

Addresses per subnet:

`2^6 = 64`

Usable hosts per conventional subnet:

`64 - 2 = 62`

The four subnets are:

| Subnet | Network address | Usable host range | Broadcast address |
|---|---|---|---|
| 1 | `192.168.1.0` | `.1 – .62` | `192.168.1.63` |
| 2 | `192.168.1.64` | `.65 – .126` | `192.168.1.127` |
| 3 | `192.168.1.128` | `.129 – .190` | `192.168.1.191` |
| 4 | `192.168.1.192` | `.193 – .254` | `192.168.1.255` |

All four subnets use the mask `255.255.255.192`.

## Important terminology

- **Network address:** Identifies the subnet itself.
- **First usable host:** Usually network address + 1.
- **Last usable host:** Usually broadcast address − 1.
- **Broadcast address:** Identifies the subnet's directed broadcast destination in conventional IPv4 subnets.
- **Default gateway:** The router address a host uses to reach other networks; it is usually a usable address on the local subnet.

---

# 8. Subnetting Formulas

Memorize these formulas for quick calculations.

| What to calculate | Formula |
|---|---|
| Host bits | `32 - prefix length` |
| Total IPv4 addresses | `2^(host bits)` |
| Conventional usable hosts | `2^(host bits) - 2` |
| Bits borrowed | `New prefix - Original prefix` |
| Number of equal-sized subnets | `2^(bits borrowed)` |
| Block size | `256 - subnet mask value in interesting octet` |

### Example

Given: `192.168.10.0/27`

Host bits:

`32 - 27 = 5`

Total addresses:

`2^5 = 32`

Usable hosts:

`32 - 2 = 30`

Subnet mask:

`255.255.255.224`

Block size:

`256 - 224 = 32`

**Answer:** 32 addresses per subnet, with 30 conventional usable host addresses.

### Special cases

- `/31`: 2 addresses; commonly used for point-to-point links under RFC 3021, with both addresses usable as endpoints.
- `/32`: One address, representing a single IPv4 address or host route.
- Do not subtract two blindly when dealing with `/31` or `/32`.

---

# 9. Block Size Method

The block size method is one of the fastest ways to calculate subnet ranges without converting the entire IP address to binary.

## Formula

**Block size = 256 − subnet mask value in the interesting octet**

The interesting octet is the octet in the subnet mask that is neither `255` nor `0`.

For example:

Mask: `255.255.255.192`

Interesting octet: `192`

Block size:

`256 - 192 = 64`

The subnet boundaries in the fourth octet are:

`0, 64, 128, 192`

Each subnet contains 64 addresses.

## Step-by-step procedure

1. Identify the CIDR prefix.
2. Convert the prefix into a subnet mask.
3. Find the interesting octet.
4. Calculate the block size.
5. List multiples of the block size starting from zero.
6. Find the interval containing the given IP address.
7. The interval's starting address is the network address.
8. The address before the next interval is the broadcast address.
9. For conventional subnets, the usable range is network + 1 through broadcast − 1.

## Example 1: Find the subnet details

Given:

`192.168.10.77/26`

### Step 1: Find the subnet mask

`/26 = 255.255.255.192`

### Step 2: Find the block size

`256 - 192 = 64`

### Step 3: Calculate subnet boundaries

`0, 64, 128, 192`

### Step 4: Identify the range containing 77

Since `77` falls between `64` and `127`, the subnet is:

`192.168.10.64 – 192.168.10.127`

### Final answer

| Parameter | Answer |
|---|---|
| IP address | `192.168.10.77` |
| CIDR | `/26` |
| Subnet mask | `255.255.255.192` |
| Network address | `192.168.10.64` |
| First usable host | `192.168.10.65` |
| Last usable host | `192.168.10.126` |
| Broadcast address | `192.168.10.127` |
| Total addresses | 64 |
| Usable hosts | 62 |

## Example 2: Block size in the third octet

Given:

`172.16.35.123/20`

### Step 1: Calculate the mask

`/20 = 255.255.240.0`

### Step 2: Find the interesting octet

The third octet is `240`.

### Step 3: Calculate the block size

`256 - 240 = 16`

### Step 4: List third-octet boundaries

`0, 16, 32, 48, 64, 80, ...`

The third octet `35` falls in the interval `32–47`.

### Final answer

| Parameter | Answer |
|---|---|
| IP address | `172.16.35.123` |
| CIDR | `/20` |
| Subnet mask | `255.255.240.0` |
| Network address | `172.16.32.0` |
| First usable host | `172.16.32.1` |
| Last usable host | `172.16.47.254` |
| Broadcast address | `172.16.47.255` |
| Total addresses | 4,096 |
| Usable hosts | 4,094 |

### Why does the third octet matter?

A `/20` mask uses 16 bits in the first two octets and 4 bits in the third octet.

The third octet is therefore divided into blocks of 16, and the fourth octet ranges from `0` to `255` within each block.

---

# 10. Quick CIDR Reference Table

This table is especially useful for interviews and quick revisions.

| CIDR | Subnet mask | Total addresses | Usable hosts* | Block size |
|---|---|---:|---:|---:|
| `/24` | `255.255.255.0` | 256 | 254 | 256 |
| `/25` | `255.255.255.128` | 128 | 126 | 128 |
| `/26` | `255.255.255.192` | 64 | 62 | 64 |
| `/27` | `255.255.255.224` | 32 | 30 | 32 |
| `/28` | `255.255.255.240` | 16 | 14 | 16 |
| `/29` | `255.255.255.248` | 8 | 6 | 8 |
| `/30` | `255.255.255.252` | 4 | 2 | 4 |
| `/31` | `255.255.255.254` | 2 | 2 on supported point-to-point links | 2 |
| `/32` | `255.255.255.255` | 1 | Special case | 1 |

\*Usable-host figures for `/24` through `/30` use the conventional network and broadcast reservation.

### Prefixes with the interesting octet in different positions

| CIDR | Mask | Interesting octet | Block size |
|---|---|---|---:|
| `/8` | `255.0.0.0` | None in the ordinary partial-octet sense | Full second-octet range: 256 |
| `/16` | `255.255.0.0` | None in the ordinary partial-octet sense | Full third-octet range: 256 |
| `/17` | `255.255.128.0` | Third | 128 |
| `/18` | `255.255.192.0` | Third | 64 |
| `/19` | `255.255.224.0` | Third | 32 |
| `/20` | `255.255.240.0` | Third | 16 |
| `/21` | `255.255.248.0` | Third | 8 |
| `/22` | `255.255.252.0` | Third | 4 |
| `/23` | `255.255.254.0` | Third | 2 |
| `/24` | `255.255.255.0` | Full fourth-octet range | 256 |
| `/25` | `255.255.255.128` | Fourth | 128 |
| `/26` | `255.255.255.192` | Fourth | 64 |
| `/27` | `255.255.255.224` | Fourth | 32 |
| `/28` | `255.255.255.240` | Fourth | 16 |
| `/29` | `255.255.255.248` | Fourth | 8 |
| `/30` | `255.255.255.252` | Fourth | 4 |

For `/8` and `/16`, the mask changes at an octet boundary; use the host-bit formula or consider the full range in the next octet.

---

# 11. Solved Practical Questions

## Question 1: Find the network and broadcast address

Given:

`192.168.1.70/27`

**Step 1:** Mask = `255.255.255.224`

**Step 2:** Block size = `256 - 224 = 32`

**Step 3:** Boundaries = `0, 32, 64, 96, 128, 160, 192, 224`

The value `70` falls between `64` and `95`.

**Solution:**

- Network: `192.168.1.64`
- First host: `192.168.1.65`
- Last host: `192.168.1.94`
- Broadcast: `192.168.1.95`
- Usable hosts: `30`

## Question 2: How many usable hosts are in `/28`?

Host bits:

`32 - 28 = 4`

Total addresses:

`2^4 = 16`

Usable hosts:

`16 - 2 = 14`

**Answer: 14 usable hosts.**

## Question 3: How many `/26` subnets can be created from a `/24`?

Bits borrowed:

`26 - 24 = 2`

Subnets:

`2^2 = 4`

**Answer: 4 subnets**, each containing 64 addresses and 62 conventional usable host addresses.

## Question 4: Find the subnet mask for `/22`

A `/22` prefix contains:

- 8 ones in the first octet.
- 8 ones in the second octet.
- 6 ones in the third octet.

Third octet:

`128 + 64 + 32 + 16 + 8 + 4 = 252`

**Answer: `255.255.252.0`**

## Question 5: Find the network of `10.20.37.45/21`

**Step 1:** Mask = `255.255.248.0`

**Step 2:** Block size = `256 - 248 = 8`

**Step 3:** Third-octet boundaries:

`0, 8, 16, 24, 32, 40, 48, ...`

Since `37` lies between `32` and `39`:

- Network: `10.20.32.0`
- First host: `10.20.32.1`
- Last host: `10.20.39.254`
- Broadcast: `10.20.39.255`
- Total addresses: `2^(32-21) = 2048`
- Usable hosts: `2046`

## Question 6: Does `192.168.1.10/24` communicate directly with `192.168.2.20/24`?

Host A: `192.168.1.10/24`

Host B: `192.168.2.20/24`

Network A: `192.168.1.0/24`

Network B: `192.168.2.0/24`

The network addresses differ.

**Answer:** They are on different subnets. Communication between them normally requires routing through a router or Layer 3 device, along with suitable routes and firewall permissions.

## Question 7: What prefix is required for at least 50 hosts?

Try `/26`:

- Host bits: `32 - 26 = 6`
- Total addresses: `64`
- Usable hosts: `62`

A `/27` provides only 30 usable hosts, so it is insufficient.

**Answer: `/26`, with subnet mask `255.255.255.192`.**

## Question 8: Find the subnet range for `192.168.5.200/28`

Mask: `255.255.255.240`

Block size:

`256 - 240 = 16`

Relevant boundaries:

`... 160, 176, 192, 208, 224 ...`

The address `200` falls in the `192–207` block.

**Answer:**

- Network: `192.168.5.192`
- First host: `192.168.5.193`
- Last host: `192.168.5.206`
- Broadcast: `192.168.5.207`
- Usable hosts: `14`

## Question 9: Find the subnet for `172.16.100.200/23`

Mask: `255.255.254.0`

Block size in the third octet:

`256 - 254 = 2`

Third-octet blocks are `... 98–99`, `100–101`, `102–103`, etc.

Since the third octet is `100`, the network begins at `100`.

**Answer:**

- Network: `172.16.100.0`
- First host: `172.16.100.1`
- Last host: `172.16.101.254`
- Broadcast: `172.16.101.255`
- Total addresses: `512`
- Usable hosts: `510`

## Question 10: Divide `192.168.10.0/24` into eight equal subnets

**Step 1:** Eight subnets require 3 borrowed bits because `2^3 = 8`.

**Step 2:** New prefix = `/24 + 3 = /27`.

**Step 3:** Mask = `255.255.255.224`.

**Step 4:** Block size = `32`.

| Subnet | Network | Usable host range | Broadcast |
|---|---|---|---|
| 1 | `192.168.10.0` | `.1 – .30` | `.31` |
| 2 | `192.168.10.32` | `.33 – .62` | `.63` |
| 3 | `192.168.10.64` | `.65 – .94` | `.95` |
| 4 | `192.168.10.96` | `.97 – .126` | `.127` |
| 5 | `192.168.10.128` | `.129 – .158` | `.159` |
| 6 | `192.168.10.160` | `.161 – .190` | `.191` |
| 7 | `192.168.10.192` | `.193 – .222` | `.223` |
| 8 | `192.168.10.224` | `.225 – .254` | `.255` |

**Answer:** Eight `/27` subnets, each with 30 conventional usable host addresses.

---

# 12. Practice Questions

Try solving these before checking the answer key.

## Beginner level

1. How many bits are present in an IPv4 address?
2. What is the subnet mask for `/24`?
3. How many usable hosts are available in `/29`?
4. Which class historically contains `200.10.10.1`?
5. Is `192.168.10.5` a private IP address?

## Intermediate level

6. Find the network address of `192.168.1.150/26`.
7. Find the broadcast address of `192.168.1.150/26`.
8. Find the usable host range of `192.168.10.90/27`.
9. How many `/28` subnets can be created from a `/24`?
10. What is the subnet mask for `/20`?

## Advanced level

11. Find the network and broadcast addresses of `10.10.75.200/22`.
12. Find the network and broadcast addresses of `172.16.45.130/20`.
13. You need at least 100 usable hosts per subnet. Which prefix should you choose?
14. You need at least 12 equal-sized subnets from a `/24`. What is the smallest conventional fixed-length subnet size that provides enough subnets, and how many usable hosts does each have?
15. Divide `192.168.20.0/24` into four equal subnets. List their network addresses.

---

## Answer Key with Short Solutions

### 1. IPv4 address size

**Answer: 32 bits.**

### 2. Mask for `/24`

**Answer: `255.255.255.0`.**

### 3. Usable hosts in `/29`

Host bits = `3`

Total = `2^3 = 8`

Usable = `8 - 2 = 6`

**Answer: 6.**

### 4. Class of `200.10.10.1`

First octet = `200`, which is in the historical Class C range.

**Answer: Class C.**

### 5. Is `192.168.10.5` private?

Yes. It falls in `192.168.0.0/16`.

**Answer: Yes.**

### 6. Network address of `192.168.1.150/26`

Mask = `255.255.255.192`

Block size = `64`

Blocks: `0–63`, `64–127`, `128–191`, `192–255`

**Answer: `192.168.1.128`.**

### 7. Broadcast address of `192.168.1.150/26`

The subnet range is `192.168.1.128–192.168.1.191`.

**Answer: `192.168.1.191`.**

### 8. Usable range of `192.168.10.90/27`

Block size = `32`

The address falls in the `64–95` block.

- Network: `192.168.10.64`
- Broadcast: `192.168.10.95`

**Answer: `192.168.10.65–192.168.10.94`.**

### 9. `/28` subnets from `/24`

Borrowed bits = `28 - 24 = 4`

Subnets = `2^4 = 16`

**Answer: 16 subnets.**

### 10. Mask for `/20`

**Answer: `255.255.240.0`.**

### 11. `10.10.75.200/22`

Mask = `255.255.252.0`

Block size in third octet = `256 - 252 = 4`

The third-octet block containing `75` is `72–75`.

- Network: `10.10.72.0`
- Broadcast: `10.10.75.255`

### 12. `172.16.45.130/20`

Mask = `255.255.240.0`

Block size in third octet = `16`

The block containing `45` is `32–47`.

- Network: `172.16.32.0`
- Broadcast: `172.16.47.255`

### 13. At least 100 usable hosts

A `/25` has 126 usable hosts.

A `/26` has only 62.

**Answer: `/25`.**

### 14. At least 12 subnets from `/24`

Borrow 4 bits:

`2^4 = 16` subnets.

New prefix = `/28`.

Each `/28` has 16 total addresses and 14 conventional usable hosts.

**Answer: `/28`, giving 16 subnets with 14 usable hosts each.**

### 15. Four equal subnets from `192.168.20.0/24`

Borrow 2 bits:

`/24 + 2 = /26`

Block size = `64`.

**Network addresses:**

1. `192.168.20.0/26`
2. `192.168.20.64/26`
3. `192.168.20.128/26`
4. `192.168.20.192/26`

---

# 13. Common Mistakes

1. **Confusing the network address with a host address.**  
   The network address identifies the subnet; it is not normally assigned to a host.

2. **Using the classful default mask instead of the configured CIDR prefix.**  
   For example, `172.16.5.10/24` uses `/24`, even though `172` historically belongs to Class B.

3. **Subtracting 2 for every prefix.**  
   `/31` point-to-point networks and `/32` host routes are special cases.

4. **Calculating block size using the wrong octet.**  
   For `/20`, use the third octet (`240`), not the fourth.

5. **Choosing a subnet that is too small.**  
   A requirement for 50 hosts needs `/26` or a larger subnet in address-space terms, not `/27`.

6. **Assuming all private IPs start with `192.168`.**  
   `10.0.0.0/8` and `172.16.0.0/12` are private as well.

7. **Assuming different subnets cannot communicate.**  
   They can communicate through routing when the network is configured correctly.

8. **Confusing total addresses with usable host addresses.**  
   A `/26` has 64 total addresses but normally 62 usable host addresses.

---

# 14. One-Minute Revision Sheet

## Must-remember formulas

```text
IPv4 bits          = 32
Host bits          = 32 - prefix
Total addresses    = 2^(host bits)
Usable hosts       = 2^(host bits) - 2*
Borrowed bits      = new prefix - old prefix
Number of subnets  = 2^(borrowed bits)
Block size         = 256 - interesting octet value
```

`*` The conventional usable-host formula has `/31` and `/32` exceptions.

## Quick subnet mask values

```text
128 = /25
192 = /26
224 = /27
240 = /28
248 = /29
252 = /30
254 = /31
255 = /32
```

These values apply to the final partial octet, or to the relevant partial octet in a larger prefix.

## Quick block sizes

```text
128 -> blocks of 128
192 -> blocks of 64
224 -> blocks of 32
240 -> blocks of 16
248 -> blocks of 8
252 -> blocks of 4
254 -> blocks of 2
```

## Private IPv4 ranges

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

## Historical IP classes

```text
Class A = 1–126 (with special-use exceptions)
Class B = 128–191
Class C = 192–223
Class D = 224–239 (multicast)
Class E = 240–255 (reserved/experimental)
```

## Five-step subnetting shortcut

1. Find the subnet mask from CIDR.
2. Calculate the block size.
3. Find the block containing the given IP.
4. Determine the network and broadcast addresses.
5. Calculate the usable range and host count.

---

## Recommended Learning Order

- [ ] Understand IPv4 binary and decimal conversion.
- [ ] Memorize subnet masks and CIDR prefixes.
- [ ] Learn the difference between network, host, and broadcast addresses.
- [ ] Practice `/24`, `/25`, `/26`, `/27`, and `/28`.
- [ ] Practice block size calculations in the third octet.
- [ ] Solve the 15 practice questions without checking the answers.
- [ ] Revisit the one-minute revision sheet before interviews or exams.

## Final takeaway

**If you remember only three things, remember these:**

1. `Host bits = 32 - CIDR prefix`
2. `Total addresses = 2^(host bits)`
3. `Block size = 256 - subnet mask value in the interesting octet`

Master these three rules, and most basic IPv4 subnetting problems become much easier.

---

### Further Reading

- RFC 1918 — Address Allocation for Private Internets: https://www.rfc-editor.org/rfc/rfc1918
- RFC 4632 — Classless Inter-domain Routing (CIDR): https://www.rfc-editor.org/rfc/rfc4632
- RFC 3021 — Using 31-Bit Prefixes on IPv4 Point-to-Point Links: https://www.rfc-editor.org/rfc/rfc3021
- RFC 791 — Internet Protocol: https://www.rfc-editor.org/rfc/rfc791
