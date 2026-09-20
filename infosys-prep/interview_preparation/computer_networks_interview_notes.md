# Computer Networks Interview Notes — Infosys DSE / SP

This is the dedicated Computer Networks reference for the Infosys DSE / Specialist Programmer interview track.

Scope: networking fundamentals, OSI/TCP-IP, Ethernet and switching, IP addressing and subnetting, ARP/NDP, routing, TCP/UDP, reliability, flow/congestion control, DNS, DHCP, NAT/PAT, HTTP/HTTPS, TLS, sockets, proxies, load balancers, CORS, cookies/tokens, WebSockets, latency, packet loss, debugging, implementation drills, hidden terminology, traps, and networking-level engineering trade-offs.

Interview standard: for every major topic, be able to give the definition, explain why it exists, trace the mechanism, use a real-world analogy, identify failure modes, compare alternatives, and answer follow-up questions.

Boundary: this remains Computer Networks. The future System Design course will go deeper into architecture. Here, design discussion stays at the networking boundary: protocols, connections, latency, reliability, security, proxies, load balancing, traffic flow, and failure diagnosis.

<a id="table-of-contents"></a>

## Table of Contents

- [How to Use These Notes](#how-to-use-these-notes)
- [CN Interview Depth Model](#cn-interview-depth-model)
- [The One Mental Model That Connects Everything](#the-one-mental-model-that-connects-everything)
- [What a Network Actually Does](#what-a-network-actually-does)
- [Network Components and Their Roles](#network-components-and-their-roles)
- [OSI Model](#osi-model)
- [TCP/IP Model](#tcpip-model)
- [OSI vs TCP/IP](#osi-vs-tcpip)
- [Encapsulation and Decapsulation](#encapsulation-and-decapsulation)
- [PDU Names](#pdu-names)
- [MAC Address](#mac-address)
- [IP Address](#ip-address)
- [IPv4 Addressing](#ipv4-addressing)
- [Private and Public IP Addresses](#private-and-public-ip-addresses)
- [Loopback and Special Addresses](#loopback-and-special-addresses)
- [Subnet Mask and CIDR](#subnet-mask-and-cidr)
- [Subnetting Calculations](#subnetting-calculations)
- [Default Gateway](#default-gateway)
- [ARP](#arp)
- [IPv6 and NDP](#ipv6-and-ndp)
- [Switching](#switching)
- [Broadcast Domain and Collision Domain](#broadcast-domain-and-collision-domain)
- [Routing](#routing)
- [Routing Table](#routing-table)
- [Router vs Switch](#router-vs-switch)
- [Static vs Dynamic Routing](#static-vs-dynamic-routing)
- [Distance Vector vs Link State](#distance-vector-vs-link-state)
- [TTL and Hop Count](#ttl-and-hop-count)
- [ICMP](#icmp)
- [Ping and Traceroute](#ping-and-traceroute)
- [UDP](#udp)
- [TCP](#tcp)
- [TCP vs UDP](#tcp-vs-udp)
- [TCP Three-Way Handshake](#tcp-three-way-handshake)
- [TCP Connection Termination](#tcp-connection-termination)
- [TCP Sequence and Acknowledgement Numbers](#tcp-sequence-and-acknowledgement-numbers)
- [TCP Retransmission and Timeout](#tcp-retransmission-and-timeout)
- [TCP Flow Control](#tcp-flow-control)
- [TCP Congestion Control](#tcp-congestion-control)
- [Slow Start](#slow-start)
- [Congestion Avoidance](#congestion-avoidance)
- [Fast Retransmit and Fast Recovery](#fast-retransmit-and-fast-recovery)
- [Flow Control vs Congestion Control](#flow-control-vs-congestion-control)
- [Head-of-Line Blocking](#head-of-line-blocking)
- [MTU](#mtu)
- [MSS](#mss)
- [IP Fragmentation](#ip-fragmentation)
- [Ports and Sockets](#ports-and-sockets)
- [Socket Lifecycle](#socket-lifecycle)
- [Client-Server Connection Model](#client-server-connection-model)
- [DNS](#dns)
- [DNS Resolution](#dns-resolution)
- [DNS Record Types](#dns-record-types)
- [Recursive vs Authoritative DNS](#recursive-vs-authoritative-dns)
- [DNS Caching and TTL](#dns-caching-and-ttl)
- [What Happens When You Enter a URL](#what-happens-when-you-enter-a-url)
- [DHCP](#dhcp)
- [NAT](#nat)
- [PAT](#pat)
- [HTTP](#http)
- [HTTP Request Structure](#http-request-structure)
- [HTTP Response Structure](#http-response-structure)
- [HTTP Methods](#http-methods)
- [Safe vs Idempotent Methods](#safe-vs-idempotent-methods)
- [HTTP Status Codes](#http-status-codes)
- [HTTP Headers](#http-headers)
- [Persistent Connections and Connection Pooling](#persistent-connections-and-connection-pooling)
- [HTTP/1.1 vs HTTP/2 vs HTTP/3](#http11-vs-http2-vs-http3)
- [TLS and HTTPS](#tls-and-https)
- [TLS Handshake Mental Model](#tls-handshake-mental-model)
- [Certificates and PKI](#certificates-and-pki)
- [Symmetric vs Asymmetric Cryptography in HTTPS](#symmetric-vs-asymmetric-cryptography-in-https)
- [Forward Proxy vs Reverse Proxy](#forward-proxy-vs-reverse-proxy)
- [Load Balancer](#load-balancer)
- [CORS](#cors)
- [Cookies](#cookies)
- [Sessions vs Tokens](#sessions-vs-tokens)
- [Authentication vs Authorization](#authentication-vs-authorization)
- [WebSockets](#websockets)
- [Long Polling vs WebSockets](#long-polling-vs-websockets)
- [REST and Networking](#rest-and-networking)
- [Compression and Content Negotiation](#compression-and-content-negotiation)
- [HTTP Caching Headers](#http-caching-headers)
- [Rate Limiting at the Network Boundary](#rate-limiting-at-the-network-boundary)
- [Latency, Bandwidth, Throughput and Jitter](#latency-bandwidth-throughput-and-jitter)
- [Packet Loss and Goodput](#packet-loss-and-goodput)
- [Unicast, Multicast, Broadcast and Anycast](#unicast-multicast-broadcast-and-anycast)
- [Proxy, Gateway, Router and Load Balancer Distinctions](#proxy-gateway-router-and-load-balancer-distinctions)
- [Common Network Failure Scenarios](#common-network-failure-scenarios)
- [Network Debugging Workflow](#network-debugging-workflow)
- [General Implementation Drills](#general-implementation-drills)
- [TCP Echo Server](#tcp-echo-server)
- [UDP Echo Example](#udp-echo-example)
- [Simple HTTP Request](#simple-http-request)
- [CIDR Utility](#cidr-utility)
- [Connection Pool Reasoning](#connection-pool-reasoning)
- [Project Connections](#project-connections)
- [Likely Infosys SP/DSE Follow-Up Questions](#likely-infosys-spdse-follow-up-questions)
- [Hidden Networking Keywords](#hidden-networking-keywords)
- [Common CN Traps](#common-cn-traps)
- [30-Second Revision Sheet](#30-second-revision-sheet)
- [Final Computer Networks Interview Checklist](#final-computer-networks-interview-checklist)

---

<a id="how-to-use-these-notes"></a>

## How to Use These Notes

Use this loop for every concept:

```text
What is it?
↓
Why does it exist?
↓
Simple real-world analogy
↓
What happens technically?
↓
What identifier/device/layer is involved?
↓
What can go wrong?
↓
What trade-off does it make?
↓
What follow-up can the interviewer ask?
```

For difficult topics, keep asking:

```text
Who is sending?
↓
Who is receiving?
↓
What identifier is used at this layer?
↓
Which device handles it?
↓
How does it know the next hop?
↓
How is delivery made reliable?
↓
What happens when something is delayed or lost?
```

For request traces:

```text
Application
↓
DNS
↓
Socket
↓
Transport
↓
IP
↓
Link
↓
Intermediate devices
↓
Destination
```

Personalized rule: whenever a term feels vague, ask **“What exact problem is this layer solving?”** Do not memorize the word before you can explain the problem it solves.

[Back to Table of Contents](#table-of-contents)

---

<a id="cn-interview-depth-model"></a>

## CN Interview Depth Model

### Depth 1 — Definition

Example: “What is TCP?”

> TCP is a connection-oriented transport protocol providing ordered, reliable byte-stream delivery with flow and congestion control.

### Depth 2 — Mechanism

“How does TCP establish a connection?”

Explain SYN, SYN-ACK, ACK, sequence-number state, and why both sides need to synchronize.

### Depth 3 — Comparison

“TCP vs UDP?”

Compare delivery semantics, ordering, data model, overhead, flow control, congestion control, and typical workloads.

### Depth 4 — Trace

“What happens when you open an HTTPS URL?”

Trace DNS → route → transport → TLS → HTTP → server → response → connection reuse.

### Depth 5 — Failure reasoning

“The API became slow. What network causes could exist?”

Think DNS latency, connection setup, packet loss, retransmission, congestion, TLS, proxy queues, connection exhaustion, MTU/PMTUD, and downstream latency.

### Depth 6 — Engineering discussion

“Why HTTP/2 or HTTP/3? Why use a reverse proxy? Why keep connections alive?”

Discuss workload, latency, multiplexing, head-of-line blocking, operational complexity, failure behavior, and resource limits.

[Back to Table of Contents](#table-of-contents)

---

<a id="the-one-mental-model-that-connects-everything"></a>

## The One Mental Model That Connects Everything

Think of networking as a multi-stage courier system.

The application knows the **message**.

The transport layer handles the **conversation** between endpoints.

The network layer decides how to move toward the **destination network**.

The link layer handles the **next local hop**.

```text
Application message
    ↓
TCP/UDP segment or datagram
    ↓
IP packet
    ↓
Ethernet/Wi-Fi frame
    ↓
physical signal
```

At the receiver:

```text
signal
↓
frame
↓
packet
↓
segment/datagram
↓
application data
```

This layered wrapping is called **encapsulation** on the way down and **decapsulation** on the way up.

[Back to Table of Contents](#table-of-contents)

---

<a id="what-a-network-actually-does"></a>

## What a Network Actually Does

A network is not merely “sending bytes.” It must solve several problems:

```text
Identification
Addressing
Forwarding
Routing
Reliability
Ordering
Congestion
Flow control
Security
Name resolution
Failure handling
```

### Real-world metaphor

Sending a package to another city:

- Your home needs a local identity.
- The destination needs an address.
- Your local gateway chooses the first road.
- Intermediate routers forward the package.
- The package may be delayed or lost.
- A reliable transport may recover from loss.
- Congestion changes travel time and throughput.

### Interview line

> “Computer networking is the set of protocols and mechanisms used to move data between endpoints through addressing, forwarding, transport semantics, and failure-handling mechanisms.”

[Back to Table of Contents](#table-of-contents)

---

<a id="network-components-and-their-roles"></a>

## Network Components and Their Roles

| Component | Main job | Mental model |
|---|---|---|
| NIC | Connect host to network | Host network interface |
| Repeater | Regenerate a signal | Signal extender |
| Hub | Repeat traffic to ports | Basic shared LAN device |
| Switch | Forward frames using MAC addresses | Local traffic director |
| Router | Forward packets between IP networks | Inter-network junction |
| Access Point | Provide wireless LAN connectivity | Wi-Fi bridge/access |
| Modem | Provider-specific access/signal conversion | ISP edge device |
| Firewall | Enforce traffic/security policy | Gatekeeper |
| Proxy | Relay requests for another party | Middleman |
| Reverse proxy | Front backend servers | Server-side entry point |
| Load balancer | Distribute traffic among backends | Traffic dispatcher |

A physical appliance can perform several of these roles. In interviews, describe the function rather than assuming a one-box-one-role mapping.

[Back to Table of Contents](#table-of-contents)

---

<a id="osi-model"></a>

## OSI Model

Seven conceptual layers:

```text
7 Application
6 Presentation
5 Session
4 Transport
3 Network
2 Data Link
1 Physical
```

Think of each layer as answering a different question:

| Layer | Question | Typical examples |
|---|---|---|
| Application | What does the application protocol mean? | HTTP, DNS, SMTP |
| Presentation | How is data represented/protected? | Encoding, compression, encryption concepts |
| Session | How is a session coordinated? | Session concepts |
| Transport | How do endpoints exchange data? | TCP, UDP |
| Network | Which network/next hop? | IP, routing |
| Data Link | How does the local hop deliver a frame? | Ethernet, Wi-Fi, MAC |
| Physical | How are bits carried? | Copper, fiber, radio |

### Interview nuance

OSI is a conceptual reference model. Do not treat it as a literal implementation stack for every modern system.

[Back to Table of Contents](#table-of-contents)

---

<a id="tcp-ip-model"></a>

## TCP/IP Model

A practical teaching model is:

```text
Application
Transport
Internet
Link
```

Common mapping:

```text
OSI 7-5 → Application
OSI 4   → Transport
OSI 3   → Internet
OSI 2-1 → Link
```

### Interview line

> “OSI is a conceptual seven-layer reference model; TCP/IP is the practical protocol architecture associated with the Internet.”

[Back to Table of Contents](#table-of-contents)

---

<a id="osi-vs-tcp-ip"></a>

## OSI vs TCP/IP

| Aspect | OSI | TCP/IP |
|---|---|---|
| Main purpose | Reference model | Practical protocol architecture |
| Layers | 7 | Commonly shown as 4 |
| Session/presentation | Separate | Folded into application |
| Typical use | Teaching/conceptual classification | Real Internet protocols |

### Trap

Do not say “OSI is the protocol used by the Internet.” OSI is a reference model.

[Back to Table of Contents](#table-of-contents)

---

<a id="encapsulation-and-decapsulation"></a>

## Encapsulation and Decapsulation

Suppose the browser sends an HTTP request.

Conceptually:

```text
Application data
↓
TCP header + data
↓
IP header + TCP segment
↓
Ethernet/Wi-Fi header + IP packet
```

The receiver reverses the process:

```text
frame
↓ remove link-layer information
packet
↓ process IP
transport data
↓ process TCP/UDP
application data
```

### Metaphor

A letter goes into an envelope, then into a courier bag with routing information. The recipient unwraps it in reverse order.

[Back to Table of Contents](#table-of-contents)

---

<a id="pdu-names-you-must-know"></a>

## PDU Names You Must Know

```text
Application → message/data
Transport  → segment (TCP) / datagram (UDP)
Network    → packet
Data Link  → frame
Physical   → bits/signals
```

### Hidden interview detail

A frame carries a network-layer packet plus link-layer framing information.

[Back to Table of Contents](#table-of-contents)

---

<a id="mac-address"></a>

## MAC Address

A MAC address identifies a network interface at the data-link layer.

Think:

> “Which interface on this local network should receive this frame?”

MAC is mainly about the **local hop**.

### Why MAC and IP both exist

The IP destination can remain logically end-to-end while the Layer-2 source and destination MAC addresses are relevant to each local link.

For traffic crossing routers, the MAC addresses are not kept end-to-end.

[Back to Table of Contents](#table-of-contents)

---

<a id="ip-address"></a>

## IP Address

An IP address is a network-layer logical address used for routing and interface identification within a routing context.

```text
MAC → local-link delivery
IP  → routed logical addressing
```

A host may have multiple interfaces and addresses.

[Back to Table of Contents](#table-of-contents)

---

<a id="ipv4-addressing"></a>

## IPv4 Addressing

IPv4 uses 32-bit addresses.

Example:

```text
192.168.1.10
```

That is four 8-bit octets.

Modern networks use CIDR rather than old fixed classful assumptions.

[Back to Table of Contents](#table-of-contents)

---

<a id="private-and-public-ip-addresses"></a>

## Private and Public IP Addresses

Common private IPv4 ranges:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

Private addresses are not globally routable on the public Internet.

### Metaphor

Your home can use internal room numbers such as `192.168.x.x`, but those numbers are not globally unique addresses on the Internet. Your edge device normally provides public connectivity.

[Back to Table of Contents](#table-of-contents)

---

<a id="loopback-and-special-addresses"></a>

## Loopback and Special Addresses

Common addresses:

```text
127.0.0.1 → IPv4 loopback
0.0.0.0   → unspecified/wildcard in many contexts
255.255.255.255 → IPv4 limited broadcast
::1       → IPv6 loopback
```

### Hidden point

`0.0.0.0` is not “the Internet.” A server binding to it commonly means “listen on all suitable local IPv4 interfaces.”

[Back to Table of Contents](#table-of-contents)

---

<a id="subnet-mask-and-cidr"></a>

## Subnet Mask and CIDR

CIDR expresses the number of leading bits used as the network prefix.

Example:

```text
192.168.1.0/24
```

means:

```text
first 24 bits = network prefix
remaining 8 bits = host bits
```

A `/24` contains 256 IPv4 addresses total. For a conventional host subnet, 2 are typically reserved as network and broadcast addresses, leaving 254 usable host addresses.

### Metaphor

A `/16` can be a large apartment complex. Subnetting divides it into buildings so local traffic stays local.

[Back to Table of Contents](#table-of-contents)

---

<a id="subnetting-calculations"></a>

## Subnetting Calculations

For IPv4 `/n`:

```text
host bits = 32 - n
addresses = 2^(32-n)
```

For typical non-point-to-point subnets:

```text
usable hosts = 2^(32-n) - 2
```

Example:

```text
/26
host bits = 6
addresses = 64
usable hosts = 62
```

Useful mental table:

```text
/30 → 4 addresses → usually 2 usable hosts
/29 → 8 → 6
/28 → 16 → 14
/27 → 32 → 30
/26 → 64 → 62
/25 → 128 → 126
/24 → 256 → 254
/23 → 512 → 510
```

### Example

For `192.168.1.64/26`:

```text
range = 192.168.1.64 – 192.168.1.127
network = 192.168.1.64
broadcast = 192.168.1.127
hosts = .65 – .126
```

[Back to Table of Contents](#table-of-contents)

---

<a id="default-gateway"></a>

## Default Gateway

The default gateway is the next-hop router a host uses when the destination is outside its directly connected subnet.

### Metaphor

Inside your neighborhood you know the local streets. To leave the neighborhood, you first reach the highway entrance. That entrance is the gateway.

[Back to Table of Contents](#table-of-contents)

---

<a id="arp"></a>

## ARP

ARP resolves an IPv4 address to a MAC address on the local link.

If a host needs the MAC for `192.168.1.1`, it can broadcast a request similar to:

> “Who has 192.168.1.1?”

The owner replies with its MAC address.

### Critical interview detail

A host normally does **not** ARP for a remote Internet server. It ARPs for the local next hop, usually the default gateway.

That is because the remote packet must first reach the local router.

[Back to Table of Contents](#table-of-contents)

---

<a id="ipv6-and-ndp"></a>

## IPv6 and NDP

IPv6 uses 128-bit addresses.

Example:

```text
2001:db8::10
```

IPv6 uses Neighbor Discovery Protocol (NDP), implemented using ICMPv6, instead of ARP.

The largest motivation is the much larger address space. IPv6 also changes several protocol details and provides mechanisms for neighbor discovery and autoconfiguration.

[Back to Table of Contents](#table-of-contents)

---

<a id="switching"></a>

## Switching

A switch primarily forwards Ethernet frames inside a local network using MAC addresses.

It learns mappings such as:

```text
MAC A → port 3
MAC B → port 8
```

When a frame arrives, the switch checks its MAC address table and selects the output port.

If the destination MAC is unknown, the switch may flood the frame within the relevant VLAN.

[Back to Table of Contents](#table-of-contents)

---

<a id="broadcast-domain-and-collision-domain"></a>

## Broadcast Domain and Collision Domain

### Broadcast domain

The set of devices that receive a Layer-2 broadcast.

Routers normally separate broadcast domains. VLANs create separate logical Layer-2 broadcast domains.

### Collision domain

A segment where simultaneous transmissions can collide.

Modern switched Ethernet normally gives each switch port a separate collision domain in full-duplex operation.

### Hidden keyword: VLAN

A VLAN logically separates Layer-2 networks on shared switching infrastructure.

[Back to Table of Contents](#table-of-contents)

---

<a id="routing"></a>

## Routing

Routing is the process of selecting where to forward an IP packet toward its destination.

A router asks:

```text
Which route matches the destination?
Which matching route is most specific/preferred?
Which next hop/interface should I use?
```

### Longest prefix match

A router generally prefers the most specific matching route.

Example:

```text
10.0.0.0/8
10.20.0.0/16
10.20.30.0/24
```

For destination `10.20.30.5`, the `/24` route is more specific than `/16` and `/8`.

### Metaphor

Three signs say “any city in the country,” “any city in this state,” and “this exact neighborhood.” The most specific matching direction wins.

[Back to Table of Contents](#table-of-contents)

---

<a id="routing-table"></a>

## Routing Table

A routing table stores destination prefixes and next-hop/interface information.

| Destination | Prefix | Next hop/interface |
|---|---:|---|
| Local subnet | connected | local NIC |
| Default | `0.0.0.0/0` | gateway |
| Remote network | specific prefix | next-hop router |

`0.0.0.0/0` is the least-specific IPv4 route and commonly acts as the fallback route.

[Back to Table of Contents](#table-of-contents)

---

<a id="router-vs-switch"></a>

## Router vs Switch

| | Switch | Router |
|---|---|---|
| Main layer | Data link | Network |
| Main address | MAC | IP |
| Main job | Local frame forwarding | Inter-network packet forwarding |
| Broadcast boundary | Usually within a VLAN | Separates broadcast domains |

### Interview line

> “A switch primarily forwards Layer-2 frames inside a LAN using MAC information, while a router forwards Layer-3 packets between IP networks.”

[Back to Table of Contents](#table-of-contents)

---

<a id="static-vs-dynamic-routing"></a>

## Static vs Dynamic Routing

### Static routing

Routes are configured manually.

Advantages: predictable and simple for small, stable networks.

Disadvantages: manual maintenance and poor adaptation to topology changes.

### Dynamic routing

Routers exchange routing information and compute routes.

Examples:

```text
RIP
OSPF
BGP
```

At this interview level, know the problem each class of protocol solves and its broad behavior. Do not memorize packet formats unless specifically required.

[Back to Table of Contents](#table-of-contents)

---

<a id="distance-vector-and-link-state"></a>

## Distance Vector vs Link State

### Distance Vector

Routers learn reachability/distance information from neighbors.

Classic example: RIP.

### Link State

Routers build a topology view and calculate paths.

Classic example: OSPF.

### Mental distinction

```text
Distance vector → “my neighbor says this destination is N away”
Link state      → “I have a topology view and compute paths”
```

[Back to Table of Contents](#table-of-contents)

---

<a id="ttl-and-hop-count"></a>

## TTL and Hop Count

IPv4 packets contain TTL (Time To Live).

Each routed hop decrements TTL.

When TTL reaches zero, the packet is discarded and an ICMP Time Exceeded message may be generated.

### Why?

To stop routing loops from circulating packets forever.

### Hidden connection

Traceroute relies on TTL expiration to discover path hops.

[Back to Table of Contents](#table-of-contents)

---

<a id="icmp"></a>

## ICMP

ICMP is used for network control, diagnostics, and error reporting.

Examples:

- Echo request/reply for ping.
- Destination unreachable.
- Time exceeded.

ICMP is not a replacement for TCP or UDP.

[Back to Table of Contents](#table-of-contents)

---

<a id="ping-and-traceroute"></a>

## Ping and Traceroute

### Ping

Ping uses ICMP Echo Request and Echo Reply and measures round-trip latency.

### Traceroute

Traceroute sends probes with increasing TTL values. A router where the TTL expires can return ICMP Time Exceeded.

```text
TTL=1 → first hop expires packet → ICMP Time Exceeded
TTL=2 → second hop responds
TTL=3 → third hop responds
...
```

A successful ping does not prove HTTPS is healthy. ICMP and application traffic can be filtered independently.

[Back to Table of Contents](#table-of-contents)

---

<a id="udp"></a>

## UDP

UDP is a connectionless transport protocol with low protocol overhead.

It provides:

- Port-based multiplexing.
- Datagram delivery.
- No built-in connection handshake.
- No built-in guarantee of delivery or ordering.

### Why use it?

When datagram semantics or application-managed reliability/ordering are more appropriate.

Common examples include DNS, real-time media, gaming protocols, and QUIC transport underneath HTTP/3.

UDP itself does not automatically make something “faster”; application behavior and network conditions matter.

[Back to Table of Contents](#table-of-contents)

---

<a id="tcp"></a>

## TCP

TCP is a connection-oriented transport protocol providing a reliable, ordered byte stream.

Key properties:

```text
connection-oriented
ordered byte stream
reliable delivery
acknowledgements
retransmission
flow control
congestion control
full duplex
```

### Critical interview detail: TCP is a byte stream

Suppose an application writes:

```text
"HELLO"
"WORLD"
```

The receiver might read:

```text
"HELLOW"
"ORLD"
```

or many other chunkings.

TCP does not preserve application `send()` boundaries. It preserves byte order.

### Metaphor

TCP is a conveyor belt of bytes. The receiving side chooses how many bytes to read; it does not automatically recover the sender's original message boundaries.

[Back to Table of Contents](#table-of-contents)

---

<a id="tcp-vs-udp"></a>

## TCP vs UDP

| Property | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented | Connectionless |
| Delivery | Reliable | Best effort |
| Ordering | Yes | No |
| Retransmission | Built in | Application/protocol dependent |
| Flow control | Yes | No TCP-style flow control |
| Congestion control | Yes | No TCP-style congestion control |
| Data model | Byte stream | Datagram |
| Protocol overhead | Higher | Lower |

### Interview answer

> “Use TCP when you need a reliable ordered byte stream. Use UDP when datagram semantics or application-managed transport behavior are more appropriate.”

[Back to Table of Contents](#table-of-contents)

---

<a id="tcp-three-way-handshake"></a>

## TCP Three-Way Handshake

Classic handshake:

```text
Client                         Server

SYN ------------------------->

     <------------------- SYN-ACK

ACK -------------------------->
```

### What is being achieved?

Both sides synchronize initial sequence-number state and confirm that communication is possible in both directions.

### Why three messages?

Both sides need to communicate their sequence state and confirm receipt. Two messages are insufficient to give both directions the same confirmation semantics.

[Back to Table of Contents](#table-of-contents)

---

<a id="tcp-connection-termination"></a>

## TCP Connection Termination

Typical graceful close:

```text
FIN → ACK
...
FIN ← ACK
```

Because TCP is full duplex, each direction can close independently.

### Hidden term: TIME_WAIT

The actively closing endpoint may enter `TIME_WAIT`.

Why?

- Protect against delayed old segments being confused with a later connection.
- Give the peer a chance to receive the final ACK again if needed.

`TIME_WAIT` is part of TCP correctness, not simply a useless socket leak.

[Back to Table of Contents](#table-of-contents)

---

<a id="tcp-sequence-and-acknowledgement-numbers"></a>

## TCP Sequence and Acknowledgement Numbers

TCP sequence numbers identify byte positions in the stream.

Acknowledgement numbers normally indicate the next byte expected.

Example: if a sender begins at sequence 1000 and sends 500 bytes, the receiver can cumulatively acknowledge:

```text
ACK = 1500
```

Meaning: bytes through 1499 have been received and byte 1500 is expected next.

[Back to Table of Contents](#table-of-contents)

---

<a id="tcp-retransmission-and-timeout"></a>

## TCP Retransmission and Timeout

If TCP concludes that data has likely been lost, it retransmits.

The retransmission timeout (RTO) is derived from observed network timing; there is no universal fixed timeout that works for every network.

### Why not retransmit immediately?

Because delay is not the same as loss. Too-aggressive retransmission creates unnecessary traffic; too-slow recovery increases latency.

### Hidden keyword: RTT

Round-trip time is the time for a packet/segment and relevant response/acknowledgement to make a round trip.

[Back to Table of Contents](#table-of-contents)

---

<a id="tcp-flow-control"></a>

## TCP Flow Control

Flow control protects the **receiver**.

Metaphor: the sender is a fast conveyor belt and the receiver has a small warehouse. The receiver advertises how much more data it can accept.

That advertised capacity is represented by the receive window.

```text
sender
  ↓
must respect
receiver capacity
```

[Back to Table of Contents](#table-of-contents)

---

<a id="tcp-congestion-control"></a>

## TCP Congestion Control

Congestion control protects the **network path**.

```text
Flow control       → “my receiver is getting full”
Congestion control → “the network path is overloaded”
```

TCP uses a congestion window (`cwnd`) and congestion-control algorithms to adapt the amount of in-flight data based on feedback.

[Back to Table of Contents](#table-of-contents)

---

<a id="slow-start"></a>

## Slow Start

Despite the name, slow start can increase the congestion window rapidly during the initial phase.

The sender starts with a small congestion window and increases in-flight data as acknowledgements arrive. Textbook explanations describe roughly exponential growth per RTT during this phase until a threshold or congestion event changes the regime.

“Slow” refers to starting cautiously, not necessarily to slow growth.

[Back to Table of Contents](#table-of-contents)

---

<a id="congestion-avoidance"></a>

## Congestion Avoidance

After the initial growth phase, congestion control becomes more conservative.

A classic textbook model is:

```text
Additive increase
Multiplicative decrease
```

Exact behavior depends on the chosen TCP congestion-control algorithm.

[Back to Table of Contents](#table-of-contents)

---

<a id="fast-retransmit-and-fast-recovery"></a>

## Fast Retransmit and Fast Recovery

Three duplicate ACKs traditionally provide a strong early loss signal.

TCP can retransmit the missing segment before waiting for the retransmission timeout.

Fast recovery reduces sending aggressiveness and continues according to the congestion-control algorithm.

[Back to Table of Contents](#table-of-contents)

---

<a id="flow-control-vs-congestion-control"></a>

## Flow Control vs Congestion Control

| | Flow control | Congestion control |
|---|---|---|
| Protects | Receiver | Network |
| Main signal | Receive window | Congestion window |
| Problem | Receiver cannot consume data fast enough | Network path is overloaded |

Memorize the distinction:

> Flow control prevents the sender from overwhelming the receiver; congestion control tries to prevent the sender from overwhelming the network.

[Back to Table of Contents](#table-of-contents)

---

<a id="head-of-line-blocking"></a>

## Head-of-Line Blocking

Head-of-line (HOL) blocking happens when an earlier blocked item prevents later items from making progress.

High-value example:

- HTTP/2 multiplexes multiple streams over one TCP connection.
- If TCP loses a segment, later bytes cannot be delivered to the application until the missing bytes are recovered.
- HTTP/3 uses QUIC streams, reducing this cross-stream transport HOL problem.

[Back to Table of Contents](#table-of-contents)

---

<a id="mtu"></a>

## MTU

MTU means Maximum Transmission Unit.

It is the maximum size of a packet that a link can carry as one unit at the relevant layer.

A common Ethernet MTU is 1500 bytes for the IP packet size.

### Why it matters

A path with a smaller usable MTU can create fragmentation or PMTUD problems.

### Production symptom

Small requests work but larger payloads fail. Think MTU/PMTUD, proxy size limits, and timeouts rather than assuming the application code is wrong.

[Back to Table of Contents](#table-of-contents)

---

<a id="mss"></a>

## MSS

Maximum Segment Size is the TCP payload size a host is willing to receive in one TCP segment, excluding TCP/IP headers.

For a common IPv4 + Ethernet case:

```text
MTU = 1500
IP header = 20
TCP header = 20
MSS ≈ 1460
```

Options can change header size, so 1460 is a common example rather than a universal constant.

[Back to Table of Contents](#table-of-contents)

---

<a id="ip-fragmentation"></a>

## IP Fragmentation

Fragmentation breaks an IP packet into smaller fragments so it can cross a link with a smaller MTU.

IPv4 routers can fragment packets, although modern networks generally try to avoid it.

IPv6 routers do not fragment packets in transit; fragmentation is performed by the sending endpoint when used.

### Why fragmentation is undesirable

- Additional processing.
- Losing one fragment can prevent reassembly of the original packet.
- Troubleshooting and filtering become harder.

[Back to Table of Contents](#table-of-contents)

---

<a id="ports-and-sockets"></a>

## Ports and Sockets

An IP address identifies a network-layer endpoint/interface in a routing context.

A port identifies a transport-layer endpoint on that host.

A socket is the OS abstraction representing a communication endpoint.

### TCP connection identity

A TCP flow is commonly identified by a 4-tuple:

```text
source IP
source port
destination IP
destination port
```

This allows one server port such as TCP 443 to serve many simultaneous client connections.

### Metaphor

IP = building address.

Port = apartment/door.

Socket = communication endpoint used by the application.

[Back to Table of Contents](#table-of-contents)

---

<a id="socket-lifecycle"></a>

## Socket Lifecycle

Typical TCP server:

```text
socket()
bind()
listen()
accept()
recv()/send()
close()
```

Typical client:

```text
socket()
connect()
send()/recv()
close()
```

### Critical distinction

`listen()` creates a passive listening state.

`accept()` returns a **new connected socket** for one client. The listening socket remains available for other connections.

[Back to Table of Contents](#table-of-contents)

---

<a id="client-server-connection-model"></a>

## Client-Server Connection Model

A typical web request path:

```text
Browser
↓
DNS resolution
↓
route/next hop
↓
TCP or QUIC
↓
TLS
↓
HTTP request
↓
reverse proxy/load balancer
↓
application
```

For debugging, map failures to layers:

- DNS failure → name resolution.
- TCP connect timeout → transport/path/server issue.
- TLS certificate failure → TLS/security validation.
- HTTP 404 → application/resource-level issue.

[Back to Table of Contents](#table-of-contents)

---

<a id="dns"></a>

## DNS

DNS is a distributed naming system that maps names to records.

For example:

```text
api.example.com
```

may resolve to address records.

### Metaphor

DNS is a contact list/phonebook that turns a memorable name into information needed to communicate.

[Back to Table of Contents](#table-of-contents)

---

<a id="dns-resolution-flow"></a>

## DNS Resolution

Simplified flow:

```text
Application
↓
local/browser/OS cache
↓
recursive resolver
↓
root
↓
TLD server
↓
authoritative server
↓
answer
```

A recursive resolver may already have a cached answer and skip most of the hierarchy.

### Important distinction

The client generally asks its configured recursive resolver. The client does not normally walk from root to authoritative server itself for every lookup.

[Back to Table of Contents](#table-of-contents)

---

<a id="dns-record-types"></a>

## DNS Record Types

| Record | Purpose |
|---|---|
| A | IPv4 address |
| AAAA | IPv6 address |
| CNAME | Alias to another domain name |
| MX | Mail exchanger |
| NS | Authoritative name server |
| TXT | Text metadata, verification and policy uses |
| SOA | Zone authority metadata |

### Hidden point

A CNAME points to another DNS name. It is not itself an IPv4 address record.

[Back to Table of Contents](#table-of-contents)

---

<a id="recursive-vs-authoritative-dns"></a>

## Recursive vs Authoritative DNS

### Recursive resolver

Finds an answer on behalf of the client, possibly querying other servers and caching the result.

### Authoritative server

Provides authoritative answers for DNS zones it serves.

### Metaphor

Recursive resolver = librarian who searches for you.

Authoritative server = the official catalog source.

[Back to Table of Contents](#table-of-contents)

---

<a id="dns-caching-and-ttl"></a>

## DNS Caching and TTL

DNS answers are cacheable.

TTL indicates how long a cached answer may be treated as fresh according to DNS caching rules.

### Trade-off

Long TTL → fewer lookups and more cache reuse, but slower change propagation.

Short TTL → fresher changes, but more DNS query traffic.

### Trap

TTL does not mean every client everywhere forgets a record at exactly the same moment.

[Back to Table of Contents](#table-of-contents)

---

<a id="what-happens-when-you-enter-a-url"></a>

## What Happens When You Enter a URL

This is one of the highest-value interview questions.

Suppose you enter:

```text
https://api.example.com/users
```

### 1. Parse the URL

Identify scheme, host, optional port, and path.

### 2. DNS

Resolve the hostname to one or more addresses.

### 3. Route selection

The host uses its routing table to choose a next hop.

### 4. Transport

- HTTP/1.1 and HTTP/2 commonly use TCP.
- HTTP/3 uses QUIC over UDP.

### 5. TLS

For HTTPS, establish cryptographic keys and validate the server identity using certificates.

### 6. HTTP

Send the application request.

Example:

```http
GET /users HTTP/1.1
Host: api.example.com
```

### 7. Server-side path

The request may go through a CDN, load balancer, reverse proxy, application server, cache, or database.

### 8. Response

Receive status, headers, and body.

### 9. Connection reuse

The client may reuse the connection for later requests.

### Interview-ready summary

> “I resolve the hostname with DNS, choose a route to the destination, establish TCP or QUIC, perform TLS for HTTPS, send the HTTP request, receive the response, and potentially reuse the established connection.”

### Hidden follow-ups

- Why DNS before TCP?
- Where does ARP happen?
- Does the MAC address stay the same end-to-end?
- Where does NAT happen?
- What does TLS verify?
- Why keep-alive?
- What changes with HTTP/2?
- What changes with HTTP/3?
- Where can latency appear?

[Back to Table of Contents](#table-of-contents)

---

<a id="dhcp"></a>

## DHCP

DHCP can provide:

- IP address
- subnet mask/prefix
- default gateway
- DNS resolver information

Classic client sequence:

```text
Discover
Offer
Request
ACK
```

Often remembered as DORA.

### Metaphor

You enter an office and ask for a desk number, the exit to use, and the directory service to contact.

[Back to Table of Contents](#table-of-contents)

---

<a id="nat"></a>

## NAT

Network Address Translation rewrites addressing information as traffic crosses a translation boundary.

Typical home network:

```text
192.168.1.10
192.168.1.11
192.168.1.12
       ↓
NAT gateway
       ↓
one public IPv4 address
```

### Why?

A common deployment lets many private-addressed devices share public IPv4 connectivity.

### Trade-off

NAT changes end-to-end addressing and can complicate inbound connectivity and troubleshooting.

[Back to Table of Contents](#table-of-contents)

---

<a id="pat"></a>

## PAT

Port Address Translation is a common NAT technique where multiple internal flows share one public IP and are distinguished by transport ports.

```text
192.168.1.10:50000 → public.ip:40001
192.168.1.11:50000 → public.ip:40002
```

NAT is the broader category; PAT is a common many-to-one implementation using ports.

[Back to Table of Contents](#table-of-contents)

---

<a id="http"></a>

## HTTP

HTTP is an application-layer request/response protocol.

A request typically contains:

```text
method
target/path
headers
optional body
```

A response contains:

```text
status
headers
optional body
```

HTTP is independent of TCP as an abstract application protocol; HTTP/3 runs over QUIC.

[Back to Table of Contents](#table-of-contents)

---

<a id="http-request-structure"></a>

## HTTP Request Structure

Example:

```http
POST /users HTTP/1.1
Host: api.example.com
Content-Type: application/json
Authorization: Bearer <token>

{"name":"Sai"}
```

Understand each component:

- Method → operation semantics.
- Request target/path → resource or route target.
- `Host` → target hostname in HTTP/1.1.
- `Content-Type` → representation format of the body.
- `Authorization` → credentials/authorization material.
- Body → application data.

Headers are protocol metadata/control information; business logic is still application code.

[Back to Table of Contents](#table-of-contents)

---

<a id="http-response-structure"></a>

## HTTP Response Structure

Example:

```http
HTTP/1.1 201 Created
Content-Type: application/json
Location: /users/123

{"id":123}
```

High-value headers:

```text
Content-Type
Content-Length
Cache-Control
ETag
Location
Set-Cookie
Retry-After
Access-Control-Allow-Origin
```

[Back to Table of Contents](#table-of-contents)

---

<a id="http-methods"></a>

## HTTP Methods

Know the common methods:

- `GET` — retrieve a representation.
- `POST` — submit/process/create depending on API semantics.
- `PUT` — replace a resource representation.
- `PATCH` — partially modify a resource.
- `DELETE` — delete a resource.
- `HEAD` — retrieve headers without a response body.
- `OPTIONS` — discover supported operations/metadata; commonly used in CORS preflight.

### Trap

Do not map HTTP methods mechanically to CRUD. HTTP defines method semantics; an API maps business operations onto those semantics.

[Back to Table of Contents](#table-of-contents)

---

<a id="http-safe-and-idempotent-methods"></a>

## Safe vs Idempotent Methods

### Safe

A safe method has read-only intended semantics from the perspective of the requested resource.

Common safe methods:

```text
GET
HEAD
OPTIONS
TRACE
```

### Idempotent

Repeating the same request has the same intended effect as performing it once.

Common idempotent methods include GET, HEAD, PUT, DELETE, OPTIONS, and TRACE.

### Hidden interview question

> Is POST idempotent?

Not by HTTP method semantics in general. An API can introduce idempotency keys or other deduplication logic.

[Back to Table of Contents](#table-of-contents)

---

<a id="http-status-codes"></a>

## HTTP Status Codes

```text
1xx → informational
2xx → success
3xx → redirection
4xx → client/request issue
5xx → server-side failure
```

High-value codes:

| Code | Common meaning |
|---|---|
| 200 | OK |
| 201 | Created |
| 202 | Accepted for asynchronous processing |
| 204 | No Content |
| 301 | Permanent redirect |
| 302 | Temporary redirect; historical client behavior can vary |
| 303 | See Other |
| 304 | Not Modified |
| 307 | Temporary redirect preserving method semantics |
| 308 | Permanent redirect preserving method semantics |
| 400 | Bad Request |
| 401 | Authentication required/failed |
| 403 | Forbidden |
| 404 | Not Found |
| 405 | Method Not Allowed |
| 409 | Conflict |
| 412 | Precondition Failed |
| 413 | Content Too Large |
| 429 | Too Many Requests |
| 500 | Internal Server Error |
| 502 | Bad Gateway |
| 503 | Service Unavailable |
| 504 | Gateway Timeout |

### Classic distinction

`401` is about authentication credentials. `403` means the server understood the request but refuses it under authorization policy.

[Back to Table of Contents](#table-of-contents)

---

<a id="http-headers"></a>

## HTTP Headers

Request-side headers worth knowing:

```text
Host
Accept
Content-Type
Content-Length
Authorization
Cookie
Origin
User-Agent
If-None-Match
If-Modified-Since
```

Response-side headers worth knowing:

```text
Content-Type
Content-Length
Cache-Control
ETag
Last-Modified
Location
Set-Cookie
Retry-After
Access-Control-Allow-Origin
```

The interviewer may ask why headers exist: they carry metadata/control information for representation, authentication, caching, redirects, and policies.

[Back to Table of Contents](#table-of-contents)

---

<a id="persistent-connections-and-connection-pooling"></a>

## Persistent Connections and Connection Pooling

A persistent connection allows multiple HTTP requests/responses to reuse an underlying transport connection rather than opening a new connection for every request.

### Why?

TCP/TLS setup has cost. Reuse reduces repeated connection-establishment overhead and can lower latency.

### Connection pooling

Clients/services often keep a bounded set of reusable downstream connections.

```text
request
↓
borrow connection
↓
send request
↓
read response
↓
return connection to pool
```

### Why bound the pool?

Unlimited connections can cause:

```text
traffic spike
↓
more connections
↓
more sockets/file descriptors
↓
more memory and scheduling work
↓
more downstream load
↓
instability
```

[Back to Table of Contents](#table-of-contents)

---

<a id="http-11-vs-http-2-vs-http-3"></a>

## HTTP/1.1 vs HTTP/2 vs HTTP/3

| Feature | HTTP/1.1 | HTTP/2 | HTTP/3 |
|---|---|---|---|
| Typical transport | TCP | TCP | QUIC over UDP |
| Multiplexing | Limited | Yes | Yes |
| Header compression | Text headers | HPACK | QPACK |
| TCP transport HOL | N/A as multiplexed streams issue | Yes | Avoided across QUIC streams |
| Encryption | Optional | Commonly deployed with TLS | TLS 1.3 integrated with QUIC |
| Connection migration | No equivalent QUIC feature | No | Supported by QUIC |

### Interview line

> “HTTP/2 improves multiplexing and framing over TCP. HTTP/3 moves HTTP onto QUIC, which provides independent streams without TCP's cross-stream head-of-line blocking.”

[Back to Table of Contents](#table-of-contents)

---

<a id="tls-and-https"></a>

## TLS and HTTPS

HTTPS means HTTP carried over TLS.

TLS provides:

```text
confidentiality
integrity
server authentication
```

TLS does not automatically provide correct business logic, authorization, or a secure application.

### Metaphor

HTTP is the conversation. TLS is the locked room plus identity verification around the conversation.

[Back to Table of Contents](#table-of-contents)

---

<a id="tls-handshake-mental-model"></a>

## TLS Handshake Mental Model

Exact wire details vary by TLS version and resumption, but the interview mental model is:

```text
ClientHello
↓
ServerHello + certificate + key agreement
↓
Both derive symmetric traffic keys
↓
Encrypted application data
```

### Purposes

1. Negotiate cryptographic parameters.
2. Authenticate the server using its certificate chain.
3. Establish shared symmetric traffic keys.

### Hidden keyword: Forward secrecy

Modern TLS deployments commonly use ephemeral key exchange so compromise of long-term authentication keys does not automatically reveal previously captured session traffic.

[Back to Table of Contents](#table-of-contents)

---

<a id="certificates-and-pki"></a>

## Certificates and PKI

A server certificate binds an identity such as a DNS name to a public key and is signed through a certificate-authority chain.

The client verifies items such as:

```text
certificate validity
hostname
trust chain
signature
```

### Metaphor

A certificate is like an identity card whose authenticity can be checked through a trusted issuing authority.

[Back to Table of Contents](#table-of-contents)

---

<a id="symmetric-vs-asymmetric-cryptography-in-https"></a>

## Symmetric vs Asymmetric Cryptography in HTTPS

### Asymmetric cryptography

Useful for authentication, signatures, and key establishment.

### Symmetric cryptography

Used for bulk data encryption because it is much more efficient for large volumes of traffic.

### Interview line

> “HTTPS does not encrypt the whole session with public-key cryptography. Public-key mechanisms help authenticate and establish keys; symmetric encryption protects the bulk data.”

[Back to Table of Contents](#table-of-contents)

---

<a id="forward-proxy-vs-reverse-proxy"></a>

## Forward Proxy vs Reverse Proxy

### Forward proxy

Represents the client side:

```text
Client
↓
Forward proxy
↓
Internet
```

Use cases include policy enforcement, filtering, caching, and controlled egress.

### Reverse proxy

Fronts backend servers:

```text
Client
↓
Reverse proxy
↓
Application servers
```

It may provide TLS termination, routing, caching, compression, authentication integration, and backend protection.

### Memory trick

Forward proxy represents **clients**.

Reverse proxy fronts **servers**.

[Back to Table of Contents](#table-of-contents)

---

<a id="load-balancer"></a>

## Load Balancer

A load balancer distributes traffic across backend instances.

Common strategies:

```text
round robin
least connections
weighted routing
hash-based routing
```

### L4 vs L7

Layer 4 load balancing can make decisions from transport/flow information such as TCP/UDP endpoints.

Layer 7 load balancing can understand HTTP semantics such as host, path, method, and headers.

L7 provides richer routing but requires application-protocol awareness.

[Back to Table of Contents](#table-of-contents)

---

<a id="cors"></a>

## CORS

Cross-Origin Resource Sharing is a browser security mechanism controlling whether JavaScript from one origin can read resources from another origin.

### Origin

An origin is:

```text
scheme + host + port
```

So `http://localhost:3000` and `https://example.com` are different origins.

### Preflight

Some cross-origin requests trigger an OPTIONS preflight:

```text
Browser
↓
OPTIONS preflight
↓
Server
↓
Access-Control-Allow-* response headers
↓
Browser decides whether the JS context may read the response
```

### Critical distinction

CORS is primarily a browser enforcement mechanism.

A server-to-server Python request is not blocked by browser CORS rules.

### Hidden interview question

> Does CORS protect the API from curl/Postman?

No. CORS is not authentication or authorization.

[Back to Table of Contents](#table-of-contents)

---

<a id="cookies"></a>

## Cookies

Cookies are browser-associated state sent through HTTP headers.

Server:

```http
Set-Cookie: session_id=abc; Secure; HttpOnly; SameSite=Lax
```

Browser later:

```http
Cookie: session_id=abc
```

Important attributes:

- `Secure` → cookie is restricted to secure transport contexts.
- `HttpOnly` → JavaScript cannot access it through `document.cookie`.
- `SameSite` → controls cross-site sending behavior.

Cookies commonly participate in session authentication and CSRF/security discussions.

[Back to Table of Contents](#table-of-contents)

---

<a id="sessions-vs-tokens"></a>

## Sessions vs Tokens

### Session-based authentication

The server stores session state. The client sends a session identifier, often in a cookie.

### Token-based authentication

The client sends a credential/token with each request. Bearer tokens and JWTs are common examples.

### Trade-off

Server-side sessions make revocation and central state straightforward but require session storage/availability.

Self-contained signed tokens can reduce server lookups but complicate revocation, token lifetime, and stale authorization claims.

### Trap

“JWT is stateless” is incomplete. The token can be self-contained while the overall authentication system still has state for revocation, refresh tokens, or sessions.

[Back to Table of Contents](#table-of-contents)

---

<a id="authentication-vs-authorization"></a>

## Authentication vs Authorization

```text
Authentication → Who are you?
Authorization  → What are you allowed to do?
```

Logging in proves identity. Checking whether that user may delete `/users/123` is authorization.

Credentials can travel through cookies, Authorization headers, or other identity mechanisms.

[Back to Table of Contents](#table-of-contents)

---

<a id="websockets"></a>

## WebSockets

WebSocket provides a persistent full-duplex channel between client and server.

Useful for:

- chat
- live notifications
- collaborative editing
- real-time dashboards

A connection begins with an HTTP upgrade handshake and then uses the WebSocket protocol on the established connection.

[Back to Table of Contents](#table-of-contents)

---

<a id="long-polling-vs-websockets"></a>

## Long Polling vs WebSockets

### Long polling

The client sends an HTTP request and the server holds it until data is available or a timeout occurs.

### WebSockets

A persistent bidirectional channel remains available.

### Trade-off

Long polling can fit ordinary HTTP infrastructure but creates repeated request lifecycle overhead.

WebSockets are efficient for frequent two-way real-time traffic but require explicit connection management and scaling considerations.

[Back to Table of Contents](#table-of-contents)

---

<a id="rest-and-networking"></a>

## REST and Networking

REST is an architectural style for networked resource-oriented systems and is commonly implemented over HTTP.

Useful concepts:

```text
resource
representation
URI
HTTP methods
status codes
stateless requests
cacheability
```

### Important distinction

HTTP is a protocol.

REST is an architectural style/constraint set.

REST and HTTP are related but not synonyms.

[Back to Table of Contents](#table-of-contents)

---

<a id="compression-and-content-negotiation"></a>

## Compression and Content Negotiation

Clients can communicate preferred representations and encodings.

Example:

```http
Accept: application/json
Accept-Encoding: gzip, br
```

A server can respond with:

```http
Content-Type: application/json
Content-Encoding: br
```

### Trade-off

Compression reduces bytes transferred but consumes CPU.

It is usually more useful for sizeable text payloads than tiny or already-compressed data.

[Back to Table of Contents](#table-of-contents)

---

<a id="http-caching-headers"></a>

## HTTP Caching Headers

High-value headers:

```text
Cache-Control
ETag
If-None-Match
Last-Modified
If-Modified-Since
Expires
```

### ETag flow

A server gives a representation an ETag:

```http
ETag: "abc123"
```

The client later asks:

```http
If-None-Match: "abc123"
```

If unchanged, the server can return:

```http
304 Not Modified
```

The client can reuse its cached representation instead of downloading the full body again.

[Back to Table of Contents](#table-of-contents)

---

<a id="rate-limiting-at-the-network-boundary"></a>

## Rate Limiting at the Network Boundary

Rate limiting controls how much traffic a client, identity, IP, token, or other key can generate according to a policy.

Common algorithms:

```text
fixed window
sliding window
leaky bucket
token bucket
```

It can happen at a CDN, load balancer, reverse proxy, gateway, or application.

### Trade-off

Edge limits protect backend capacity early. Application-level limits can understand richer business semantics.

[Back to Table of Contents](#table-of-contents)

---

<a id="latency-bandwidth-throughput-and-jitter"></a>

## Latency, Bandwidth, Throughput and Jitter

### Latency

Delay experienced by a transfer or operation.

### Bandwidth

The capacity/rate a link can theoretically provide.

### Throughput

The actual rate achieved by the workload.

### Jitter

Variation in packet delay over time.

### Road metaphor

- Bandwidth = number of highway lanes.
- Throughput = cars actually moving per second.
- Latency = travel time.
- Jitter = travel time changing unpredictably.

High bandwidth does not imply low latency. A long-distance or satellite path can have high capacity and still have high propagation delay.

[Back to Table of Contents](#table-of-contents)

---

<a id="packet-loss-and-goodput"></a>

## Packet Loss and Goodput

Packets can be lost because of congestion, queue overflow, wireless interference, routing problems, interface errors, or deliberate filtering.

For TCP:

```text
loss signal
↓
retransmission
↓
possible congestion-window reduction
↓
lower throughput / higher latency
```

For UDP, the application/protocol above UDP decides how to handle loss.

### Goodput

Goodput is useful application payload delivered per unit time, excluding protocol and retransmission overhead.

[Back to Table of Contents](#table-of-contents)

---

<a id="unicast-multicast-broadcast-anycast"></a>

## Unicast, Multicast, Broadcast and Anycast

### Unicast

One sender → one destination.

### Broadcast

One sender → all hosts in a relevant broadcast domain.

### Multicast

One sender → subscribed members of a multicast group.

### Anycast

The same address is advertised from multiple locations; routing directs a client toward one reachable instance.

Examples:

```text
unicast   → API request to one server
broadcast → local network announcement
multicast → one-to-many group delivery
anycast   → request reaches one of many distributed service instances
```

[Back to Table of Contents](#table-of-contents)

---

<a id="proxy-gateway-router-and-load-balancer-distinctions"></a>

## Proxy, Gateway, Router and Load Balancer Distinctions

These terms overlap in real products, so answer by function.

| Term | Main idea |
|---|---|
| Router | Forwards packets between IP networks |
| Proxy | Makes/relays requests on behalf of another party |
| Gateway | Broad term for an entry/exit or protocol boundary |
| Load balancer | Distributes traffic among backend instances |

Do not assume every gateway is a router or every reverse proxy is a load balancer. One product can perform multiple roles.

[Back to Table of Contents](#table-of-contents)

---

<a id="common-network-failure-scenarios"></a>

## Common Network Failure Scenarios

### “The website is not opening”

Reason layer by layer:

```text
DNS
↓
route
↓
TCP/QUIC
↓
TLS
↓
HTTP
↓
application
```

### “DNS is slow”

Think local cache, resolver latency, cache misses, upstream DNS latency, loss, or resolver overload.

### “TCP connects but HTTP is slow”

Possible causes include TLS negotiation, server processing, proxy queues, connection-pool exhaustion, retransmissions, large responses, or backend latency.

### “Only large requests fail”

Think:

```text
MTU
PMTUD
fragmentation
proxy limits
server body limits
timeouts
```

### “Works in Postman but not in browser”

Think:

```text
CORS
cookies
Origin
preflight
mixed content
browser security policy
```

### “Random disconnects”

Think:

```text
timeouts
NAT mapping expiry
load balancer idle timeout
server restart
wireless loss
packet loss
connection limits
```

[Back to Table of Contents](#table-of-contents)

---

<a id="network-debugging-workflow"></a>

## Network Debugging Workflow

Do not say “the network is slow” before locating the failure.

Use a layered diagnosis:

```text
1. Is DNS working?
2. Is the destination reachable?
3. Is the route correct?
4. Can the transport connection be established?
5. Does TLS succeed?
6. Was the HTTP request sent?
7. What status code returned?
8. Is server processing slow?
9. Is response transfer slow?
10. Are there retransmissions, loss, or MTU problems?
```

### Tools worth recognizing

```text
ping
traceroute / tracert
nslookup / dig
ip / ifconfig / ip addr
ss / netstat
curl
tcpdump
Wireshark
```

| Tool | Useful for |
|---|---|
| ping | Reachability + RTT |
| traceroute | Path/hop diagnosis |
| dig | DNS inspection |
| curl | HTTP/TLS/application tracing |
| ss | Socket/connection state |
| tcpdump | Packet capture |
| Wireshark | Packet-level analysis |

### Interview line

> “I would isolate the failure by layer instead of guessing.”

[Back to Table of Contents](#table-of-contents)

---

<a id="general-implementation-drills"></a>

## General Implementation Drills

Appropriate small networking implementations:

```text
TCP server/client
UDP sender/receiver
CIDR calculator
IP range checker
simple DNS lookup
raw HTTP request
application timeout + retry
sequence-numbered UDP reliability demo
application-level acknowledgement
```

Do not try to reimplement TCP in an interview. Demonstrate that you understand the abstraction and can model a small protocol when needed.

[Back to Table of Contents](#table-of-contents)

---

<a id="tcp-echo-server"></a>

## TCP Echo Server

```python
import socket

HOST = "0.0.0.0"
PORT = 5000

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as server:
    # Bind the listening socket to a local address and port.
    server.bind((HOST, PORT))

    # Start accepting TCP connections.
    server.listen()

    while True:
        # accept() returns a NEW connected socket for this client.
        conn, addr = server.accept()

        with conn:
            print("Connected:", addr)

            while True:
                data = conn.recv(4096)

                # Empty bytes mean the peer closed its sending side.
                if not data:
                    break

                conn.sendall(data)
```

### What to say aloud

> “I create a listening socket, bind it, listen for connections, accept a client into a new connected socket, then read and write the TCP byte stream.”

### Follow-ups

- Why does `accept()` return another socket?
- How would you support many clients?
- Where does blocking happen?
- How do timeouts help?
- Why might one `recv()` not equal one `send()`?

[Back to Table of Contents](#table-of-contents)

---

<a id="udp-echo-example"></a>

## UDP Echo Example

```python
import socket

HOST = "0.0.0.0"
PORT = 5001

with socket.socket(socket.AF_INET, socket.SOCK_DGRAM) as server:
    server.bind((HOST, PORT))

    while True:
        data, addr = server.recvfrom(4096)
        print("Datagram from:", addr)
        server.sendto(data, addr)
```

The important difference is that UDP preserves **datagram boundaries**, while TCP exposes a byte stream.

[Back to Table of Contents](#table-of-contents)

---

<a id="simple-http-request"></a>

## Simple HTTP Request

```python
import socket

HOST = "example.com"
PORT = 80

request = (
    "GET / HTTP/1.1\\r\\n"
    f"Host: {HOST}\\r\\n"
    "Connection: close\\r\\n"
    "\\r\\n"
).encode()

with socket.create_connection((HOST, PORT), timeout=5) as sock:
    sock.sendall(request)

    chunks = []
    while True:
        data = sock.recv(4096)
        if not data:
            break
        chunks.append(data)

response = b"".join(chunks)
print(response.decode(errors="replace"))
```

This makes the layering concrete: HTTP data is carried by a transport connection.

[Back to Table of Contents](#table-of-contents)

---

<a id="cidr-utility"></a>

## CIDR Utility

```python
from ipaddress import ip_network, ip_address

network = ip_network("192.168.1.64/26")

print("Network:", network.network_address)
print("Broadcast:", network.broadcast_address)
print("Prefix:", network.prefixlen)
print("Total addresses:", network.num_addresses)

client_ip = ip_address("192.168.1.100")
print("Inside subnet:", client_ip in network)
```

### What to say aloud

> “A /26 leaves six host bits, so there are 64 total addresses in the subnet.”

[Back to Table of Contents](#table-of-contents)

---

<a id="connection-pool-reasoning"></a>

## Connection Pool Reasoning

Repeatedly creating TCP/TLS connections adds setup cost. A connection pool reuses established connections.

```text
request
↓
borrow connection
↓
send request
↓
read response
↓
return connection
```

The pool must be bounded. Otherwise a traffic spike can produce too many sockets, file descriptors, memory allocations, context switches, and downstream requests.

This is where Computer Networks connects naturally to Operating Systems and backend engineering.

[Back to Table of Contents](#table-of-contents)

---

<a id="project-connections"></a>

## Project Connections

Project links are secondary. First answer the generic networking concept.

### URL Shortener

Typical redirect path:

```text
Browser
↓
DNS
↓
TCP/TLS
↓
HTTP GET /short-code
↓
reverse proxy / load balancer
↓
FastAPI
↓
Redis/PostgreSQL
↓
HTTP redirect response
```

Be prepared to discuss DNS failure, connection reuse, redirect latency, 307 semantics, TLS termination, Redis failure, and what the browser does after receiving the redirect.

### SceneFlow

Typical deployed flow:

```text
React frontend
↓
HTTPS
↓
FastAPI
↓
external APIs / Gemini / image providers
↓
frontend polling or result retrieval
```

Be prepared to discuss CORS, HTTPS, connection reuse, downstream timeouts, retry behavior, duplicate requests, large payloads, and the difference between network failures and application failures.

Explain the generic networking concept first; then connect it to the project.

[Back to Table of Contents](#table-of-contents)

---

<a id="likely-infosys-sp-dse-follow-up-questions"></a>

## Likely Infosys SP/DSE Follow-Up Questions

These are preparation targets, not guaranteed interview questions.

### Models and layers

- Why do networks use layers?
- OSI vs TCP/IP?
- What is encapsulation?
- Frame vs packet vs segment?
- Which layer does a switch primarily use?
- Which layer does a router primarily use?
- Why do we need MAC and IP addresses?

### IP and LAN

- What is a MAC address?
- What is an IP address?
- Private vs public IP?
- What is a subnet mask?
- What is CIDR?
- Calculate hosts for /26, /27, /28.
- What is a default gateway?
- How does ARP work?
- Why does a host ARP for the gateway for a remote destination?
- What is a VLAN?
- What is a broadcast domain?

### Routing

- What is routing?
- What is a routing table?
- What is longest prefix match?
- Static vs dynamic routing?
- Distance vector vs link state?
- What does TTL do?
- What is ICMP?
- How does traceroute work?

### TCP/UDP

- Why is TCP reliable?
- What is the three-way handshake?
- Why not two-way?
- What is a sequence number?
- What is an ACK?
- What causes retransmission?
- What is a receive window?
- What is a congestion window?
- Flow control vs congestion control?
- What is slow start?
- What is fast retransmit?
- Why does TCP use TIME_WAIT?
- TCP vs UDP?
- Why does TCP not preserve message boundaries?

### HTTP/HTTPS

- What is HTTP?
- What is an HTTP request?
- What are common methods?
- GET vs POST?
- PUT vs PATCH?
- What is idempotency?
- 401 vs 403?
- 301 vs 302 vs 307 vs 308?
- 502 vs 503 vs 504?
- What is keep-alive?
- HTTP/1.1 vs HTTP/2 vs HTTP/3?
- Why does HTTP/3 use UDP?
- What is QUIC?
- What is head-of-line blocking?

### DNS

- Why DNS?
- What is recursive DNS?
- What is an authoritative DNS server?
- A vs AAAA?
- CNAME?
- DNS TTL?
- Why do DNS changes propagate gradually?

### Security and browser behavior

- What is HTTPS?
- What does TLS provide?
- How do certificates work?
- Symmetric vs asymmetric cryptography?
- What is forward secrecy?
- TLS termination?
- What is CORS?
- Does CORS protect an API from curl/Postman?
- Cookies vs bearer tokens?
- HttpOnly / Secure / SameSite?

### End-to-end trace

- What happens when you enter a URL?
- Where does ARP happen?
- Where does NAT happen?
- Where does TLS happen?
- Where does DNS happen?
- Where does a reverse proxy sit?
- Why can the same API be fast in one region and slow in another?
- What happens if a packet is lost?
- What happens if DNS is down?
- What if TCP connects but HTTP times out?

### Debugging / production reasoning

- Why can one endpoint have high p99 latency?
- Why do only large payloads fail?
- Why can many connections slow a server down?
- Why can a connection pool help throughput?
- Why can an oversized pool hurt a system?
- Why can retries amplify an outage?
- What does exponential backoff do?
- Why do timeouts matter?

[Back to Table of Contents](#table-of-contents)

---

<a id="hidden-networking-keywords"></a>

## Hidden Networking Keywords

| Term | Know this meaning |
|---|---|
| NIC | Network interface |
| MAC | Local-link interface address |
| IP | Network-layer logical address |
| ARP | IPv4 IP-to-MAC resolution on the local link |
| NDP | IPv6 neighbor discovery |
| CIDR | Prefix-based IP addressing |
| VLAN | Logical Layer-2 segmentation |
| Default gateway | Next hop for off-subnet traffic |
| Longest prefix match | Most-specific matching route wins |
| MTU | Maximum transmission unit |
| MSS | Maximum TCP payload per segment |
| RTT | Round-trip time |
| RTO | Retransmission timeout |
| Receive window | Receiver-side flow-control limit |
| Congestion window | Sender-side congestion-control limit |
| Slow start | Initial congestion-window growth phase |
| AIMD | Additive increase, multiplicative decrease |
| TIME_WAIT | TCP closing state helping prevent stale-segment confusion |
| Socket | OS communication endpoint abstraction |
| 4-tuple | Source/destination IP and port combination |
| DNS resolver | Recursive/caching DNS component |
| Authoritative DNS | Server authoritative for a zone |
| DNS TTL | Cache freshness lifetime guidance |
| DHCP | Automatic network configuration |
| NAT | Address translation |
| PAT | Port-based NAT multiplexing |
| ICMP | Network control/error/diagnostic protocol |
| QUIC | Secure multiplexed transport over UDP |
| HOL blocking | Earlier blocked item delays later progress |
| TLS | Secure transport protocol providing encryption/integrity/authentication |
| PKI | Public-key certificate trust infrastructure |
| SNI | TLS hostname indication extension |
| ALPN | TLS application-protocol negotiation extension |
| CORS | Browser cross-origin access-control mechanism |
| CDN | Distributed edge delivery infrastructure |
| Reverse proxy | Server-side intermediary |
| Connection pooling | Reuse of bounded established connections |
| Keep-alive | Reuse of communication connections |
| p99 latency | 99th-percentile latency |
| Goodput | Useful application payload per unit time |
| Backpressure | Slow/control producers when downstream is overloaded |
| Idempotency key | Application token for deduplicating retries |
| Anycast | Same address advertised from multiple locations |
| PMTUD | Path MTU Discovery |
| MSS clamping | Adjust TCP MSS for constrained paths |
| SYN backlog | Queue/state for pending TCP connection setup |
| SYN flood | Resource-exhaustion attack against TCP setup |
| Ephemeral port | Temporary client-side transport port |
| Socket exhaustion | Running out of usable socket/OS resources |
| Connection timeout | Failure to establish a connection within a limit |
| Idle timeout | Closing an inactive connection after a limit |
| Retry storm | Synchronized retries that amplify load |
| Exponential backoff | Increasing retry delay to reduce synchronized pressure |

### Interview trigger words

```text
browser → DNS / CORS / cookies / TLS / HTTP
slow → DNS / RTT / loss / retransmission / server / queue
connect → TCP / SYN / handshake / timeout
large payload → MTU / PMTUD / body limits / timeout
many requests → keep-alive / pooling / ephemeral ports / load balancer
multiple networks → router / IP / routing table
same LAN → switch / MAC / ARP
remote host → gateway / route / ARP for next hop
https → TLS / certificate / symmetric keys
http3 → QUIC / UDP / multiplexed streams
frontend/backend → CORS / HTTPS / cookies / headers
real-time → WebSocket / long polling
retry → timeout / idempotency / backoff
high p99 → tail latency / queueing / retransmission / overloaded dependency
```

[Back to Table of Contents](#table-of-contents)

---

<a id="common-cn-traps"></a>

## Common CN Traps

### Trap 1 — TCP is just “fast and reliable”

TCP has specific connection, sequencing, acknowledgement, retransmission, flow-control, and congestion-control semantics.

### Trap 2 — UDP is unreliable, so it is useless

UDP is intentionally minimal. Higher-level protocols can add reliability; QUIC is an important example.

### Trap 3 — MAC and IP stay the same end-to-end

The destination IP can remain logically end-to-end, while Layer-2 MAC addresses are relevant to each local hop.

### Trap 4 — ARP finds a remote server's MAC

No. ARP resolves a local IP to a local-link MAC. For remote traffic, the host typically resolves the next hop's MAC.

### Trap 5 — CORS protects an API from attackers

CORS controls browser access. It does not replace authentication, authorization, server-side validation, CSRF defenses, or rate limiting.

### Trap 6 — 401 and 403 mean the same thing

401 concerns authentication credentials. 403 means the server refuses access under its authorization policy.

### Trap 7 — HTTPS makes the application secure

HTTPS protects data in transit and authenticates the server under certificate validation. Application vulnerabilities and authorization bugs remain possible.

### Trap 8 — HTTP/2 removes all head-of-line blocking

HTTP/2 reduces HTTP-level blocking through multiplexing, but TCP loss can still block progress across streams.

### Trap 9 — More bandwidth means lower latency

Bandwidth and latency are different properties.

### Trap 10 — DNS is just a database

DNS is a distributed, delegated naming system with caching and multiple record types.

### Trap 11 — Socket and port are the same

A port is a transport identifier. A socket is an OS communication endpoint abstraction.

### Trap 12 — One TCP send equals one TCP receive

False. TCP is a byte stream.

### Trap 13 — NAT is security

NAT is an addressing/translation mechanism, not a substitute for a firewall or security policy.

### Trap 14 — Retries always improve reliability

Retries can amplify overload. Use timeouts, bounded retries, backoff, and idempotency where appropriate.

### Trap 15 — Successful ping proves the API works

No. ICMP reachability does not guarantee DNS, TLS, TCP application ports, browser policy, authentication, or the application itself.

[Back to Table of Contents](#table-of-contents)

---

<a id="30-second-revision-sheet"></a>

## 30-Second Revision Sheet

```text
OSI → conceptual 7-layer reference model
TCP/IP → practical Internet protocol architecture

MAC → local-link delivery
IP → routed logical addressing
ARP → IPv4 IP-to-MAC on local link
Router → Layer-3 forwarding
Switch → Layer-2 forwarding

TCP → ordered reliable byte stream
UDP → datagrams, minimal transport semantics

SYN → SYN-ACK → ACK
FIN → graceful close
TIME_WAIT → TCP close correctness

Flow control → protect receiver
Congestion control → protect network

DNS → names to records/addresses
DHCP → network configuration
NAT/PAT → address/port translation

HTTP → application protocol
HTTPS → HTTP over TLS
TLS → confidentiality + integrity + authentication
HTTP/2 → multiplexing over TCP
HTTP/3 → HTTP over QUIC/UDP

CORS → browser cross-origin policy
Cookie → browser state
WebSocket → persistent full-duplex channel

Latency ≠ bandwidth
Throughput ≠ theoretical bandwidth
Packet loss → retransmission/congestion effects
MTU → maximum packet size on a link
MSS → TCP payload size

URL flow:
DNS
→ route
→ TCP/QUIC
→ TLS
→ HTTP
→ reverse proxy/load balancer
→ application
→ response

Debug:
DNS
→ reachability
→ transport
→ TLS
→ HTTP
→ application
```

[Back to Table of Contents](#table-of-contents)

---

<a id="final-computer-networks-interview-checklist"></a>

## Final Computer Networks Interview Checklist

### Fundamentals

- [ ] Network purpose
- [ ] OSI
- [ ] TCP/IP
- [ ] OSI vs TCP/IP
- [ ] Encapsulation / decapsulation
- [ ] PDU names
- [ ] Hub / switch / router
- [ ] MAC vs IP
- [ ] Ports / sockets

### IP and subnetting

- [ ] IPv4
- [ ] Private/public IP
- [ ] Loopback
- [ ] `0.0.0.0`
- [ ] CIDR
- [ ] subnet mask
- [ ] host calculation
- [ ] network/broadcast addresses
- [ ] default gateway
- [ ] IPv6
- [ ] NDP

### LAN and routing

- [ ] ARP
- [ ] switching
- [ ] VLAN
- [ ] broadcast domain
- [ ] collision domain
- [ ] routing table
- [ ] longest prefix match
- [ ] static vs dynamic routing
- [ ] distance vector
- [ ] link state
- [ ] TTL
- [ ] ICMP
- [ ] ping
- [ ] traceroute

### TCP/UDP

- [ ] TCP semantics
- [ ] UDP semantics
- [ ] three-way handshake
- [ ] graceful close
- [ ] sequence numbers
- [ ] acknowledgements
- [ ] retransmission
- [ ] RTT / RTO
- [ ] flow control
- [ ] congestion control
- [ ] slow start
- [ ] congestion avoidance
- [ ] fast retransmit/recovery
- [ ] TIME_WAIT
- [ ] ephemeral ports
- [ ] byte stream vs datagram
- [ ] head-of-line blocking

### Packet behavior

- [ ] MTU
- [ ] MSS
- [ ] fragmentation
- [ ] PMTUD
- [ ] packet loss
- [ ] goodput
- [ ] jitter

### DNS and infrastructure

- [ ] DNS
- [ ] recursive resolver
- [ ] authoritative DNS
- [ ] A / AAAA / CNAME / MX / NS / TXT / SOA
- [ ] DNS caching
- [ ] TTL
- [ ] DHCP
- [ ] NAT
- [ ] PAT
- [ ] anycast
- [ ] CDN

### HTTP/HTTPS

- [ ] request / response
- [ ] methods
- [ ] safe vs idempotent
- [ ] status codes
- [ ] headers
- [ ] keep-alive
- [ ] connection pooling
- [ ] HTTP/1.1
- [ ] HTTP/2
- [ ] HTTP/3
- [ ] QUIC
- [ ] TLS
- [ ] certificates
- [ ] PKI
- [ ] symmetric/asymmetric cryptography
- [ ] forward secrecy
- [ ] SNI
- [ ] ALPN

### Browser and API networking

- [ ] CORS
- [ ] origin
- [ ] preflight
- [ ] cookies
- [ ] Secure / HttpOnly / SameSite
- [ ] sessions
- [ ] tokens
- [ ] authentication vs authorization
- [ ] WebSockets
- [ ] long polling

### Proxies and traffic handling

- [ ] forward proxy
- [ ] reverse proxy
- [ ] load balancer
- [ ] Layer 4 vs Layer 7
- [ ] caching
- [ ] rate limiting
- [ ] retries
- [ ] timeouts
- [ ] exponential backoff
- [ ] idempotency

### Debugging

- [ ] ping
- [ ] traceroute
- [ ] dig / nslookup
- [ ] curl
- [ ] ss
- [ ] tcpdump
- [ ] Wireshark
- [ ] isolate by layer
- [ ] explain latency path
- [ ] explain packet loss
- [ ] explain MTU failures

### Implementation readiness

- [ ] TCP echo server
- [ ] UDP echo example
- [ ] socket lifecycle
- [ ] CIDR utility
- [ ] raw HTTP request
- [ ] timeout + retry concept
- [ ] sequence-numbered UDP reliability concept
- [ ] connection-pool reasoning

### Interview execution

- [ ] Explain every major concept in 30–60 seconds.
- [ ] Draw a request/response flow.
- [ ] Trace an HTTPS URL end to end.
- [ ] Identify the layer responsible for a symptom.
- [ ] Calculate subnet sizes.
- [ ] Explain TCP handshake without memorized wording.
- [ ] Explain flow vs congestion control.
- [ ] Distinguish DNS / TCP / TLS / HTTP failures.
- [ ] Explain CORS precisely.
- [ ] Explain HTTP/2 vs HTTP/3.
- [ ] Discuss trade-offs instead of only definitions.
- [ ] Connect generic CN concepts to URL Shortener / SceneFlow only after the generic explanation.

[Back to Table of Contents](#table-of-contents)
