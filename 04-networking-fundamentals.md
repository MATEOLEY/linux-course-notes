# Networking Fundamentals

This section contains fundamental networking concepts relevant to cybersecurity and pentesting.

The goal is not to document every networking concept, but to keep a practical reference for understanding how devices communicate and how different networking technologies relate to each other.

---

## OSI Model

The **OSI (Open Systems Interconnection) Model** is a conceptual model used to describe how network communication works.

It divides network communication into **7 layers**:

| Layer | Name | Examples / Concepts |
|---|---|---|
| 7 | Application | HTTP, HTTPS, DNS, SMTP |
| 6 | Presentation | Data encoding, encryption, compression |
| 5 | Session | Session establishment and management |
| 4 | Transport | TCP, UDP, ports |
| 3 | Network | IP addresses, routing, routers |
| 2 | Data Link | Ethernet, MAC addresses, switches |
| 1 | Physical | Cables, signals, physical transmission |

The layers are usually represented from Layer 7 to Layer 1:

```text
7 - Application
6 - Presentation
5 - Session
4 - Transport
3 - Network
2 - Data Link
1 - Physical
```

For practical networking and pentesting, some of the most important layers are:

```text
Layer 2 → MAC addresses, Ethernet, switches
Layer 3 → IP addresses, routing, routers
Layer 4 → TCP, UDP, ports
Layer 7 → Application protocols such as HTTP, DNS and SMTP
```

---

## Layer 2 - Data Link

Layer 2 is responsible for communication between devices on the same local network segment.

Important concepts at this layer include:

- Ethernet
- MAC addresses
- Network switches
- Frames

A network switch primarily operates at Layer 2.

Switches learn which MAC addresses are reachable through their ports and use this information to forward Ethernet frames toward the correct destination.

---

## MAC Address

**MAC** stands for:

**Media Access Control**

A MAC address identifies a network interface at the Data Link layer.

A traditional MAC address is **48 bits** long and is usually represented as six hexadecimal pairs.

Example:

```text
00:1A:2B:3C:4D:5E
```

It may also appear using different separators:

```text
00-1A-2B-3C-4D-5E
```

---

## MAC Address Structure

A traditional 48-bit MAC address can be viewed as two main parts:

```text
00:1A:2B | 3C:4D:5E
   OUI   | Device-specific portion
```

### OUI

The first **24 bits** traditionally identify the organization or manufacturer.

This portion is known as the:

**OUI - Organizationally Unique Identifier**

Example:

```text
00:1A:2B
```

The OUI can sometimes be searched in an OUI database to identify the manufacturer associated with a MAC address.

This can be useful during network reconnaissance because it may provide information about the type or manufacturer of a network interface.

> Identifying the manufacturer does not necessarily identify the exact device. MAC addresses can also be changed, randomized, or spoofed.

### Device-Specific Portion

The remaining 24 bits are assigned by the manufacturer as part of identifying the network interface.

Example:

```text
3C:4D:5E
```

---

## Finding a MAC Address in Linux

Network interface information can be displayed using commands such as:

```bash
ip addr
```

or:

```bash
ip link
```

A MAC address may appear as:

```text
link/ether 00:1a:2b:3c:4d:5e
```

Older Linux systems or environments may also use:

```bash
ifconfig
```

Depending on the system, the MAC address may appear under a field such as:

```text
ether
```

> `ifconfig` is considered a legacy command on many modern Linux distributions. The `ip` command from the `iproute2` suite is generally preferred.

---

## Switches and MAC Addresses

A switch uses MAC addresses to decide where Ethernet frames should be forwarded within a local network.

The switch learns MAC addresses by examining the **source MAC address** of frames arriving on its ports.

It stores this information in a **MAC address table**.

Conceptually:

```text
MAC Address         Switch Port
-----------------   -----------
00:11:22:33:44:55   Port 1
AA:BB:CC:DD:EE:FF   Port 4
```

When the switch receives a frame destined for a known MAC address, it can forward the frame through the corresponding port.

This allows switches to efficiently move traffic between devices on a LAN.

---

## Layer 3 - Network

Layer 3 is responsible for communication between different networks.

Important concepts include:

- IP addresses
- Routing
- Routers
- Packets

A router primarily operates at Layer 3 and makes forwarding decisions based on IP addresses.

```text
Layer 2 → MAC Address → Switch
Layer 3 → IP Address  → Router
```

This distinction is important when analyzing network traffic.

---

## Layer 4 - Transport

Layer 4 provides transport between applications running on networked systems.

The two protocols that will be most relevant are:

```text
TCP
UDP
```

Layer 4 also introduces the concept of **ports**, which allow network traffic to be associated with particular services or applications.

Examples include:

```text
22  → SSH
53  → DNS
80  → HTTP
443 → HTTPS
```

TCP, UDP, ports, and the TCP three-way handshake will be covered in more detail in a separate section.

---

## Data Units by Layer

Different names are commonly used for data as it moves through the network stack.

| Layer | Common Data Unit |
|---|---|
| Layer 4 - Transport | Segment (TCP) / Datagram (UDP) |
| Layer 3 - Network | Packet |
| Layer 2 - Data Link | Frame |
| Layer 1 - Physical | Bits |

A simplified representation is:

```text
Application Data
      ↓
TCP Segment / UDP Datagram
      ↓
IP Packet
      ↓
Ethernet Frame
      ↓
Bits
```

This process of adding networking information as data moves down the stack is known as **encapsulation**.

---

## Why This Matters for Pentesting

Understanding the network layers helps determine what information and protocols are involved during reconnaissance and network attacks.

For example:

```text
MAC Address → Layer 2
IP Address  → Layer 3
TCP / UDP   → Layer 4
HTTP / DNS  → Layer 7
```

When analyzing traffic in tools such as Wireshark, these protocols can be inspected at different layers.

Understanding the layers also makes it easier to understand what networking and pentesting tools are actually interacting with instead of treating them as black boxes.

---

## Quick Reference

| Concept | Layer | Purpose |
|---|---|---|
| Ethernet | Layer 2 | Local network communication |
| MAC Address | Layer 2 | Identifies a network interface at the Data Link layer |
| Switch | Primarily Layer 2 | Forwards Ethernet frames |
| IP Address | Layer 3 | Logical network addressing |
| Router | Primarily Layer 3 | Routes packets between networks |
| TCP | Layer 4 | Connection-oriented transport |
| UDP | Layer 4 | Connectionless transport |
| Ports | Layer 4 | Identify network services/applications |
| HTTP / HTTPS | Layer 7 | Web communication |
| DNS | Layer 7 | Name resolution |

---

## Notes

- The OSI model contains 7 layers.
- Switches primarily operate at Layer 2 and work with MAC addresses.
- Routers primarily operate at Layer 3 and work with IP addresses.
- TCP and UDP operate at Layer 4.
- MAC addresses are commonly 48 bits and represented in hexadecimal.
- The first 24 bits of a traditional globally assigned MAC address can contain an OUI associated with a manufacturer.
- MAC addresses should not be treated as permanent or trustworthy identifiers because they can be spoofed or randomized.
- Understanding Layers 2, 3, 4, and 7 is especially useful when analyzing network traffic during pentesting.
