# TCP, UDP and Common Ports

This section covers TCP, UDP, ports, and common network services relevant to cybersecurity and pentesting.

Understanding transport protocols and ports is essential when performing network reconnaissance, service enumeration, packet analysis, and port scanning.

---

## Transport Layer

TCP and UDP operate at:

```text
OSI Layer 4 - Transport Layer
```

The Transport Layer is responsible for communication between applications running on different systems.

Two of the most important protocols at this layer are:

```text
TCP
UDP
```

---

# TCP

**TCP** stands for:

**Transmission Control Protocol**

TCP is a **connection-oriented** transport protocol.

Before application data is exchanged, TCP normally establishes a connection between two systems.

TCP provides features such as:

- Reliable data delivery
- Ordered data transmission
- Error detection
- Retransmission of lost data
- Connection management

Because of these features, TCP is commonly used by applications where reliable communication is important.

Examples include:

```text
SSH
HTTP
HTTPS
FTP
SMTP
```

---

## TCP Three-Way Handshake

TCP normally establishes a connection using the:

**Three-Way Handshake**

The process is:

```text
Client                          Server

   ─────── SYN ────────────────>

   <────── SYN/ACK ─────────────

   ─────── ACK ────────────────>
```

The three steps are:

```text
1. SYN
2. SYN/ACK
3. ACK
```

### Step 1 - SYN

The client sends a packet with the `SYN` flag.

```text
Client → Server
SYN
```

This indicates that the client wants to establish a TCP connection.

### Step 2 - SYN/ACK

The server responds with:

```text
SYN + ACK
```

This acknowledges the client's request and indicates that the server is willing to establish the connection.

### Step 3 - ACK

The client responds with:

```text
ACK
```

The connection is then established and application data can be exchanged.

---

## TCP Handshake and Pentesting

Understanding the TCP handshake is important because many port-scanning techniques interact directly with this process.

For example, when testing whether a TCP port is open, a scanner may send:

```text
SYN
```

If the target responds with:

```text
SYN/ACK
```

the port is generally considered open.

A response such as:

```text
RST
```

often indicates that the port is closed.

This behavior is the foundation of several TCP scanning techniques.

---

# UDP

**UDP** stands for:

**User Datagram Protocol**

UDP is a **connectionless** transport protocol.

Unlike TCP, UDP does not establish a connection using a three-way handshake before sending data.

Conceptually:

```text
Sender ─────── Datagram ───────> Receiver
```

UDP does not provide the same built-in reliability mechanisms as TCP.

It does not inherently guarantee:

```text
Delivery
Ordering
Retransmission
```

This makes UDP simpler and often faster for applications where low overhead or real-time communication is more important than guaranteed delivery.

Common protocols that use UDP include:

```text
DNS
DHCP
TFTP
SNMP
```

---

## TCP vs UDP

| Feature | TCP | UDP |
|---|---|---|
| Connection type | Connection-oriented | Connectionless |
| Three-way handshake | Yes | No |
| Reliable delivery | Yes | Not inherently |
| Ordered delivery | Yes | Not inherently |
| Retransmission | Yes | No built-in retransmission |
| Overhead | Higher | Lower |
| Common use | Web, SSH, email, file transfer | DNS, DHCP, streaming, discovery |

Neither protocol is always "better."

The correct protocol depends on the requirements of the application.

---

# Ports

Ports allow multiple network services and applications to communicate using the same IP address.

A port number is a **16-bit value**.

The valid range is:

```text
0 - 65535
```

This means TCP has:

```text
65,536 possible port numbers
```

and UDP independently has:

```text
65,536 possible port numbers
```

TCP and UDP have separate port spaces.

For example:

```text
TCP/53
UDP/53
```

are different transport endpoints even though they use the same port number.

---

## IP Address + Port

An IP address identifies a host or network interface.

A port helps identify a particular network service or application endpoint.

Example:

```text
192.168.1.50:22
```

can be interpreted as:

```text
IP Address → 192.168.1.50
Port       → 22
```

Port `22` is commonly associated with SSH.

Another example:

```text
192.168.1.100:443
```

commonly indicates an HTTPS service.

> A port number does not guarantee which application is actually running. Services can be configured to use non-standard ports.

---

# Port Ranges

Ports are commonly divided into three ranges.

| Range | Name |
|---|---|
| `0 - 1023` | Well-Known Ports |
| `1024 - 49151` | Registered Ports |
| `49152 - 65535` | Dynamic / Private Ports |

## Well-Known Ports

Ports from:

```text
0 - 1023
```

are commonly associated with standard network services.

Examples:

```text
21  → FTP
22  → SSH
23  → Telnet
25  → SMTP
53  → DNS
80  → HTTP
443 → HTTPS
```

These ports are especially useful to recognize during pentesting because they can quickly provide clues about the services running on a target.

---

# Common Ports and Protocols

| Port | Transport | Service | Purpose |
|---|---|---|---|
| `21` | TCP | FTP | File Transfer Protocol control connection |
| `22` | TCP | SSH | Secure remote shell |
| `23` | TCP | Telnet | Unencrypted remote shell |
| `25` | TCP | SMTP | Email transmission |
| `53` | UDP / TCP | DNS | Domain name resolution |
| `67` | UDP | DHCP Server | DHCP server traffic |
| `68` | UDP | DHCP Client | DHCP client traffic |
| `69` | UDP | TFTP | Trivial File Transfer Protocol |
| `80` | TCP | HTTP | Web traffic |
| `110` | TCP | POP3 | Email retrieval |
| `139` | TCP | NetBIOS Session Service | Legacy Windows file/network communication |
| `143` | TCP | IMAP | Email retrieval |
| `161` | UDP | SNMP | Network monitoring and management |
| `443` | TCP | HTTPS | Encrypted web traffic |
| `445` | TCP | SMB | Windows file and resource sharing |

---

## Port 21 - FTP

```text
TCP/21
```

FTP is used to transfer files between systems.

The standard FTP control connection uses TCP port 21.

From a pentesting perspective, FTP services may be checked for:

```text
Anonymous access
Weak credentials
Exposed files
Outdated FTP software
```

---

## Port 22 - SSH

```text
TCP/22
```

SSH provides encrypted remote access to systems.

It is commonly used to administer Linux and Unix-like systems.

During enumeration, SSH may reveal information such as:

```text
SSH version
Server implementation
Authentication methods
```

---

## Port 23 - Telnet

```text
TCP/23
```

Telnet provides remote terminal access.

Unlike SSH, Telnet does not provide encryption for the session.

This makes Telnet insecure for modern remote administration and particularly interesting when discovered during a security assessment.

---

## Port 25 - SMTP

```text
TCP/25
```

SMTP is used for sending and relaying email.

During pentesting, SMTP enumeration may reveal information about:

```text
Mail servers
Users
Server configuration
Mail infrastructure
```

---

## Port 53 - DNS

DNS commonly uses:

```text
UDP/53
```

but it can also use:

```text
TCP/53
```

DNS translates domain names into IP addresses and provides other information through different DNS record types.

Example:

```text
example.com → IP Address
```

DNS is especially important during reconnaissance because it can reveal information about an organization's infrastructure.

---

## Ports 67 and 68 - DHCP

DHCP uses UDP.

```text
UDP/67 → DHCP Server
UDP/68 → DHCP Client
```

DHCP allows devices to automatically obtain network configuration such as:

```text
IP Address
Subnet Mask
Default Gateway
DNS Servers
```

---

## Port 69 - TFTP

```text
UDP/69
```

TFTP stands for:

**Trivial File Transfer Protocol**

It is a simple file transfer protocol that uses UDP.

It provides significantly fewer features and security mechanisms than protocols such as SSH/SFTP.

---

## Port 80 - HTTP

```text
TCP/80
```

HTTP is commonly used for unencrypted web communication.

When discovered during enumeration, the next step is often to inspect the web application or web server running on the target.

---

## Port 110 - POP3

```text
TCP/110
```

POP3 is used by email clients to retrieve messages from mail servers.

---

## Port 139 - NetBIOS

```text
TCP/139
```

Port 139 is associated with the NetBIOS Session Service.

It can appear in older Windows networking environments and legacy SMB configurations.

Modern SMB commonly uses TCP port 445 directly.

---

## Port 143 - IMAP

```text
TCP/143
```

IMAP is used to access and manage email stored on a mail server.

---

## Port 161 - SNMP

```text
UDP/161
```

SNMP stands for:

**Simple Network Management Protocol**

It is commonly used to monitor and manage network devices.

SNMP can be especially interesting during pentesting because improperly configured services may reveal significant information about devices and network infrastructure.

---

## Port 443 - HTTPS

```text
TCP/443
```

HTTPS provides encrypted web communication using TLS.

Most modern websites and web applications use HTTPS.

> Modern HTTP/3 can use QUIC over UDP port 443, but traditional HTTPS commonly uses TCP port 443.

---

## Port 445 - SMB

```text
TCP/445
```

SMB stands for:

**Server Message Block**

It is commonly used in Windows environments for:

```text
File sharing
Printer sharing
Shared folders
Network resources
```

SMB is particularly important in internal network pentesting and Windows/Active Directory environments.

---

# Service Enumeration

Finding an open port is only the beginning.

During pentesting, the next objective is normally to determine:

```text
What service is running?
What version is running?
How is it configured?
Does it require authentication?
Is the service vulnerable?
```

For example:

```text
22/tcp open
```

suggests that a service is accepting TCP connections on port 22.

SSH is commonly associated with port 22, but the service should still be identified rather than assumed.

The general process is:

```text
Discover host
     ↓
Discover open ports
     ↓
Identify services
     ↓
Identify versions
     ↓
Enumerate configuration
     ↓
Investigate potential vulnerabilities
```

---

# Viewing Listening Ports in Linux

The `ss` command can display network sockets on Linux.

A useful command is:

```bash
ss -tuln
```

The flags mean:

```text
-t → TCP sockets
-u → UDP sockets
-l → Listening sockets
-n → Show numeric addresses and ports
```

To also display process information:

```bash
sudo ss -tulnp
```

The additional flag:

```text
-p → Show the process using the socket
```

This can help determine which applications are listening for network connections on a Linux system.

---

# TCP and UDP Scanning

Pentesting tools can scan both TCP and UDP ports.

Conceptually:

```text
TCP Scan
    ↓
Check TCP ports
    ↓
Identify responding services
```

and:

```text
UDP Scan
    ↓
Check UDP ports
    ↓
Analyze responses or lack of responses
```

UDP scanning can be more difficult and slower than TCP scanning because UDP does not use a connection handshake and many UDP services may not respond to unexpected traffic.

---

# Packet Analysis

Tools such as Wireshark can be used to inspect TCP and UDP traffic.

During a TCP connection, the three-way handshake can be observed by inspecting TCP flags:

```text
SYN
SYN, ACK
ACK
```

Wireshark may apply colors to different packets based on its configured coloring rules.

> Wireshark colors should not be memorized as fixed meanings because coloring rules can vary depending on the profile and configuration. The packet fields and TCP flags are what should be inspected.

---

# Quick Reference

| Concept | Meaning |
|---|---|
| TCP | Connection-oriented transport protocol |
| UDP | Connectionless transport protocol |
| SYN | Request to initiate a TCP connection |
| SYN/ACK | Acknowledges SYN and requests synchronization |
| ACK | Acknowledgement |
| Port | Identifies a transport-layer endpoint |
| TCP Port Range | `0 - 65535` |
| UDP Port Range | `0 - 65535` |
| `ss -tuln` | Show listening TCP/UDP sockets |

---

# Common Port Cheat Sheet

```text
21/tcp     FTP
22/tcp     SSH
23/tcp     Telnet
25/tcp     SMTP
53/udp     DNS
53/tcp     DNS
67/udp     DHCP Server
68/udp     DHCP Client
69/udp     TFTP
80/tcp     HTTP
110/tcp    POP3
139/tcp    NetBIOS Session Service
143/tcp    IMAP
161/udp    SNMP
443/tcp    HTTPS
445/tcp    SMB
```

---

## Notes

- TCP and UDP operate at OSI Layer 4.
- TCP is connection-oriented and uses a three-way handshake.
- UDP is connectionless and does not use the TCP three-way handshake.
- TCP and UDP each have their own port range from `0` to `65535`.
- A port number alone does not guarantee which service is running.
- DNS can use both UDP and TCP port 53.
- Ports 67 and 68 are used by DHCP.
- SMB commonly uses TCP port 445 on modern Windows networks.
- Understanding common ports helps prioritize service enumeration during pentesting.
- Finding an open port should normally be followed by service and version enumeration.
