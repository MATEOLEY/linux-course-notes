# IP Addressing and NAT

This section covers IP addressing concepts relevant to networking, cybersecurity, and pentesting.

Topics include IPv4, IPv6, private IP addresses, loopback addresses, default gateways, and Network Address Translation (NAT).

---

## IP Addresses

An **IP address** is a logical address used to identify and communicate with devices across IP networks.

IP operates at:

```text
OSI Layer 3 - Network Layer
```

Two versions of IP are commonly encountered:

```text
IPv4
IPv6
```

---

# IPv4

IPv4 stands for:

**Internet Protocol Version 4**

An IPv4 address contains:

```text
32 bits
```

It is divided into four 8-bit sections called **octets**.

Example:

```text
192.168.1.10
```

Each octet can contain a decimal value between:

```text
0 - 255
```

Conceptually:

```text
192      168       1        10
 ↓        ↓        ↓         ↓
8 bits   8 bits   8 bits    8 bits

8 + 8 + 8 + 8 = 32 bits
```

---

## Binary Representation

Computers internally represent IPv4 addresses using binary.

Each octet contains 8 bits.

The positional values are:

```text
128  64  32  16  8  4  2  1
```

For example:

```text
192
```

can be represented as:

```text
128 + 64 = 192
```

Therefore:

```text
192 = 11000000
```

Another example:

```text
168 = 128 + 32 + 8
```

Therefore:

```text
168 = 10101000
```

The IPv4 address:

```text
192.168.1.10
```

can therefore be represented as:

```text
11000000.10101000.00000001.00001010
```

Understanding binary becomes especially useful when working with subnet masks and CIDR notation.

---

# IPv6

IPv6 stands for:

**Internet Protocol Version 6**

IPv6 was designed in part to address the limited IPv4 address space.

While IPv4 contains 32 bits, IPv6 contains:

```text
128 bits
```

IPv6 addresses are represented using hexadecimal.

Example:

```text
2001:db8:85a3::8a2e:370:7334
```

IPv6 is actively deployed and used on modern networks and the Internet.

> IPv4 remains extremely common, so pentesters should understand both addressing systems.

This knowledge base will focus primarily on IPv4 initially because it is commonly encountered in labs, internal networks, and introductory pentesting environments.

---

# Private IPv4 Addresses

Not every IPv4 address is globally routable on the public Internet.

Specific IPv4 ranges are reserved for **private networks**.

The three private IPv4 ranges are:

| Private Range | CIDR |
|---|---|
| `10.0.0.0 - 10.255.255.255` | `10.0.0.0/8` |
| `172.16.0.0 - 172.31.255.255` | `172.16.0.0/12` |
| `192.168.0.0 - 192.168.255.255` | `192.168.0.0/16` |

These addresses are commonly used inside:

- Home networks
- Corporate networks
- Labs
- Virtual environments
- Internal infrastructure

Examples:

```text
10.0.0.25
172.16.20.15
192.168.1.100
```

Private IPv4 addresses are not directly routed across the public Internet.

---

## Important: Private Ranges vs Classful Networks

Historically, IPv4 networks were divided into classes such as:

```text
Class A
Class B
Class C
```

This terminology can still appear in courses and older documentation.

Modern networks primarily use:

**CIDR - Classless Inter-Domain Routing**

For example, the private ranges should be remembered as:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

rather than simply as Class A, B, and C networks.

CIDR will be covered in more detail in the subnetting section.

---

# Public IP Addresses

Public IP addresses are globally routable addresses that can be used for communication across the Internet.

A device inside a private network will commonly have a private IP such as:

```text
192.168.1.25
```

while the network itself may communicate with the Internet through a public IP assigned by an ISP.

A simplified example:

```text
Computer
192.168.1.25
      |
      |
   Router
Private: 192.168.1.1
Public: 203.0.113.x
      |
      |
   Internet
```

> The public IP shown above is only an example. `203.0.113.0/24` is reserved for documentation and examples.

---

# NAT

**NAT** stands for:

**Network Address Translation**

NAT allows network addresses to be translated as traffic passes through a device such as a router or firewall.

A very common use of NAT is allowing multiple devices using private IPv4 addresses to communicate with external networks through public addressing.

Example:

```text
192.168.1.10 ─┐
192.168.1.20 ─┼── Router / NAT ── Public IP ── Internet
192.168.1.30 ─┘
```

The internal devices use private addresses:

```text
192.168.1.10
192.168.1.20
192.168.1.30
```

while the router translates traffic when communicating with external networks.

---

## NAT and Pentesting

NAT is important to understand during pentesting because:

- An internal IP address may not be reachable directly from the Internet.
- Multiple internal hosts may appear behind the same public IP.
- Internal and external network perspectives can be different.
- Port forwarding can expose internal services through a router/firewall.
- Network reconnaissance results depend on where the pentester is located.

For example, discovering:

```text
192.168.1.50
```

indicates that the target is using an address from a private IPv4 range.

---

# Default Gateway

A **default gateway** is the device a host sends traffic to when the destination is outside the networks the host knows how to reach directly.

In many small networks, the default gateway is the local router.

Example:

```text
Computer
IP:      192.168.1.25
Gateway: 192.168.1.1
             |
             ↓
           Router
             |
             ↓
          Internet
```

Common home network gateway addresses include:

```text
192.168.0.1
192.168.1.1
10.0.0.1
```

However, the gateway does **not** have to end in `.1` or `.254`.

Its address depends entirely on the network configuration.

---

## Finding the Default Gateway in Linux

The routing table can be viewed using:

```bash
ip route
```

Example:

```text
default via 192.168.1.1 dev eth0
```

In this example:

```text
192.168.1.1 → Default Gateway
eth0        → Network Interface
```

Older systems may also use:

```bash
route
```

or:

```bash
route -n
```

However, on modern Linux systems:

```bash
ip route
```

is generally preferred.

---

# Loopback

The loopback interface allows a computer to communicate with itself.

The most commonly used IPv4 loopback address is:

```text
127.0.0.1
```

It is commonly associated with:

```text
localhost
```

Example:

```bash
ping 127.0.0.1
```

or:

```bash
ping localhost
```

The IPv4 loopback block is:

```text
127.0.0.0/8
```

Therefore, loopback is not limited technically to only `127.0.0.1`, although that is by far the address most commonly used.

---

## Why Loopback Matters in Pentesting

A service can be configured to listen only on the loopback interface.

For example:

```text
127.0.0.1:8080
```

This generally means the service is accessible locally but is not directly listening on an external network interface.

Compare:

```text
127.0.0.1:8080
```

with:

```text
0.0.0.0:8080
```

A service listening on:

```text
127.0.0.1
```

is bound to the local loopback interface.

A service listening on:

```text
0.0.0.0
```

is generally listening on all available IPv4 interfaces.

This distinction can become important during enumeration, exploitation, pivoting, and port forwarding.

---

# Viewing IP Information in Linux

Modern Linux systems commonly use the `ip` command.

To display IP addresses:

```bash
ip addr
```

Short version:

```bash
ip a
```

To display routing information:

```bash
ip route
```

To display network interfaces:

```bash
ip link
```

Older systems may use:

```bash
ifconfig
```

`ifconfig` can display information such as:

- IP address
- MAC address
- Network interface
- Interface status

However, `ifconfig` belongs to the older `net-tools` package.

The modern `iproute2` commands are generally preferred:

```text
ifconfig  → ip addr / ip link
route     → ip route
```

---

# Quick Reference

| Concept | Description |
|---|---|
| IPv4 | 32-bit IP addressing |
| IPv6 | 128-bit IP addressing |
| Octet | 8 bits of an IPv4 address |
| Private IP | Address reserved for private networks |
| Public IP | Globally routable IP address |
| NAT | Network Address Translation |
| Default Gateway | Device used to reach other networks |
| Loopback | Communication with the local machine |
| `127.0.0.1` | Common IPv4 localhost address |
| `ip addr` | Display interface IP information |
| `ip route` | Display routing information |
| `ip link` | Display network interfaces |

---

# Private IPv4 Cheat Sheet

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

Loopback:

```text
127.0.0.0/8
```

Common localhost address:

```text
127.0.0.1
```

---

## Notes

- IPv4 addresses contain 32 bits.
- IPv6 addresses contain 128 bits.
- Each IPv4 octet contains 8 bits and ranges from 0 to 255.
- IPv4 private ranges should be remembered using CIDR notation.
- Private IPv4 addresses are not directly routed on the public Internet.
- NAT translates network addresses and is commonly used between private networks and external networks.
- The default gateway is used to reach destinations outside directly reachable networks.
- A gateway does not necessarily end in `.1` or `.254`.
- `127.0.0.1` is the commonly used IPv4 loopback address.
- `ip addr`, `ip link`, and `ip route` are important Linux networking commands.
