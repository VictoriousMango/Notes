<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# Computer Networks: Exam-Ready Short Notes (ISRO ICRB \& GATE CSE)

This cheat sheet is **specially curated for last-minute revision** before exams (ISRO ICRB CSE \& GATE CSE) and covers **all important theory and numerical formulas** for Computer Networks. It is **compressed for efficient revision**, yet covers all key points and numericals repeatedly asked in GATE and ISRO.

***

## 1. Syllabus \& Weightage

- **GATE/ISRO Weightage:** 7–8 marks (5–6 questions, many numerical)
- **Numerical emphasis:** Sliding window, throughput, subnetting, routing, error detection/correction, protocol behaviour, OSI/TCP-IP, IP fragmentation.
- **Must-know:** OSI \& TCP-IP architecture, addressing, routing, MAC/IP/ARP/ICMP, flow/congestion/error control, protocols, wireless, subnetting.

***

## 2. OSI and TCP/IP Layer Models

| OSI Model | Main Functionality | TCP/IP Model | Example Protocols |
| :-- | :-- | :-- | :-- |
| 7. Application | User interface | Application | HTTP, FTP, SMTP, DNS |
| 6. Presentation | Syntax/semantics, encryption |  | JPEG, SSL, ASCII |
| 5. Session | Dialog control, synchronization |  | RPC, NetBIOS |
| 4. Transport | End-to-end, reliability, ports | Transport | TCP, UDP, SCTP |
| 3. Network | Routing, addressing | Internet | IP, ICMP, ARP |
| 2. Data Link | Framing, MAC, error control | Link | Ethernet, PPP, HDLC |
| 1. Physical | Bit transmission, encoding | Physical | Cables, Hubs, Modems |


***

## 3. Network Topologies

- **Mesh:** Each node connects to every other. Links = \$ \frac{n(n-1)}{2} \$
- **Star:** Central hub; robust except hub failure.
- **Bus:** Single backbone; easy to install but fault isolating is hard.
- **Ring:** Each node to two adjacent; single fault affects all.

***

## 4. Transmission Modes

- **Simplex:** One-way. Ex: keyboard, monitor.
- **Half-Duplex:** Both send/receive, not at same time. Ex: walkie-talkie.
- **Full-Duplex:** Both ways, simultaneously. Ex: telephone.

***

## 5. Switching Techniques

| Circuit Switching | Packet Switching (Datagram/Virtual Circuit) |
| :-- | :-- |
| Dedicated path, constant delay | Efficient resource use, variable path/delay |
| Call setup required | No setup (Datagram), virtual circuit setup (VC) |
| Example: Telephone | Example: Internet |


***

## 6. Multiplexing

- **FDM (Frequency):** Analog. TV/radio, old cable.
- **TDM (Time):** Digital. Used in digital telephony.
- **WDM (Wavelength):** Optical fiber (fiber channels).

***

## 7. Physical Layer Essentials

- **Transmission media:** Twisted pair (UTP, STP), coaxial, fiber optic, wireless.
- **Encoding:** NRZ, Manchester (used in Ethernet; mid-bit transition represents data), Differential Manchester (transition at start for 0 or 1).
    - **Manchester Bit Rate**: \$ Bit Rate = Baud Rate \$
- **Baud Rate:** Rate of signal changes/sec.

***

## 8. Data Link Layer

### Services

- **Framing, address, error/flow control (LLC/MAC)**
    - *Framing methods:*
        - Character/Byte-Oriented (byte stuffing)
        - Bit-Oriented (bit stuffing, flag 01111110, eg. HDLC)


### Error Detection \& Correction

| Code | Detect (max) | Correct (max) | Notes/formulas |
| :-- | :-- | :-- | :-- |
| Parity (single) | 1 | 0 | Only detects odd no. |
| 2D Parity | 3 | 1 | Detects up to 3 bits |
| Hamming | $d_{min} = 3$ | 1 | $2t+1 \leq d_{min}$, $s+1 \leq d_{min}$ |
| CRC | Depends on poly | 0 | Modulo-2 division, generator |

#### Key Numericals

- **Utilization (sliding window):**
    - \$ Utilization = \frac{W}{1 + 2a} \$, W = window size, \$a = \frac{propagation delay}{transmission time} \$
- **Stop \& Wait Efficiency:** \$ \frac{1}{1+2a} \$
- **Go-Back-N/Ack numbers/window:** ARQ minimum seq. \# = Max(window_s, window_r) (for correct unambiguous ARQ operation).

***

## 9. Media Access Control (MAC)

- **ALOHA:**
    - Pure: Throughput \$ S = G\exp(-2G) \$, max = 18.4%
    - Slotted: \$ S = G\exp(-G) \$, max = 36.8%
- **CSMA:** Sense before transmit. Types: 1-persistent, non, p-persistent.
- **CSMA/CD:** Used in Ethernet; collision detected and jam signal sent, **Min Ethernet frame** must be at least $2 \times \text{max propagation time}$.

***

## 10. Ethernet \& IEEE 802.3

- **Frame fields:** [Preamble | SFD | Dest MAC | Src MAC | Length/Type | Data | CRC]
- **MAC:** 48-bit address, globally unique.
- **Exponential Backoff:** Used by Ethernet in CSMA/CD after collision.

***

## 11. Network Layer

### IPv4 Addressing

- **Classful:** [A: 0-127], [B: 128–191], [C: 192–223], D/E: special.
- **Subnet Mask, CIDR:** Used for efficient IP management.


### Subnetting/CIDR

- **Formula:** \$ 2^{32-n} \$ = \# of hosts in /n subnet.
- **Wildcard mask**: \$ 255.255.255.255 - subnet mask \$
- First and last address = network and broadcast.


### Fragmentation

- **MTU:** Max payload at link layer (eg, 1500 bytes for Ethernet)
- **Fragment offset:** in units of 8 bytes.
- **Flag MF (More Fragments):** 1 for all but last.

***

## 12. Routing Algorithms

| Distance Vector | Link State |
| :-- | :-- |
| Bellman-Ford; slow | Dijkstra; fast converge |
| RIP (UDP 520) | OSPF (uses IP directly) |
| Split horizon, count-to-infinity | Topology sent via LSP |


***

## 13. Protocols (ICMP, ARP, DHCP)

- **ICMP:** Reports errors, notifies unreachable, time exceeded (ping uses ICMP echo).
- **ARP:** IP-to-MAC resolution.
- **DHCP:** Dynamic allocation of IP addresses.

***

## 14. Transport Layer

### Protocols

- **TCP:**
    - Reliable, connection-oriented, stream of bytes.
    - Three-way handshake (SYN, SYN-ACK, ACK)
    - 16-bit Port numbers, 32-bit Sequence/Ack \# (per byte), Window size = flow control.
    - Congestion control: Slow Start (exponential), Congestion Avoidance (linear), Fast Retransmit.
- **UDP:**
    - Connectionless, unreliable, no flow or error control.
    - Used for DNS, streaming.


### **Key TCP Formulae**

- **Throughput:** \$ \frac{wnd size}{RTT} \$
- **Wrap Around Time:** \$ \frac{2^{32}}{bandwidth in bytes/sec} \$
- **Timeout (TCP):** Van Jacobson Algorithm (Smoothed RTT)

***

## 15. Application Layer

- **HTTP:** Port 80, client-server. GET, POST methods.
- **FTP:** Separate control (21) \& data (20) ports.
- **SMTP (Mail transfer):** Push method, Port 25.
- **POP3/IMAP (Mail access):** Pull methods; 110/143.
- **DNS:** Name to IP resolution (UDP, port 53 for query; can use TCP for large xfer).

***

## 16. Security \& Cryptography

- **Symmetric Key:** \$ \frac{n(n-1)}{2} \$ keys for n users.
- **Public Key:** n key-pairs for n users.
- **RSA:** Security based on factorizing large composite numbers.

***

## 17. Wireless and Mobile

- **802.11 (WiFi):** CSMA/CA, distributed coordination, 2.4/5GHz.
- **Bluetooth:** Short-range PAN, frequency hopping.
- **Cellular:** GSM, CDMA, LTE.

***

## 18. Most Common Numerical Problem Templates

### Sliding Window/Utilization:

- \$ U = \frac{W}{1 + 2a} \$
- **Window size for 100% utilization**: \$ W = 2a + 1 \$
- **Stop\&Wait Efficiency:** \$ \frac{1}{1+2a} \$
- **Throughput in bytes/sec:** Window Size * (Bytes/RTT)


### Subnetting:

- Hosts per subnet: \$ 2^{bits in host part} - 2 \$
- Subnet mask calculation, CIDR notation (/n)


### Aloha:

- Pure: \$ S = Ge^{-2G} \$, max throughput @ \$ G=0.5 \$
- Slotted: \$ S = Ge^{-G} \$, max @ \$ G=1 \$


### CRC:

- 1. Append k zeros, where k = degree of generator.
- 2. Divide by generator, remainder = CRC bits.

***

## 19. Quick Facts \& Last-Minute Pointers

- **ICMP error for UDP port unreachable; not for TCP (connection logic).**
- **TCP seq\# per byte, ack\# = seq\# next expected byte.**
- **Window size (TCP):** min(congestion, advertised)
- **Piggybacking:** ACK+data in one segment.
- **Ethernet minimum frame size:** 64 bytes.
- **RIP max hop:** 15, 16 = unreachable.

***

## 20. Fast Revision Table: Protocol - Layer

| Protocol | Layer OSI | Layer TCP/IP | Transport | Important Port(s) |
| :--: | :--: | :--: | :--: | :--: |
| IP | 3 | Internet |  | - |
| TCP | 4 | Transport | Yes | 20, 21 (FTP), 23 (Telnet), 25 (SMTP), 110 (POP3), 143 (IMAP), 80 (HTTP), 443 (HTTPS) |
| UDP | 4 | Transport | No | 53 (DNS), 69 (TFTP), 161 (SNMP) |
| ICMP | 3 | Internet |  | - |
| ARP | 2/3 | Link/Internet |  | - |
| OSPF | 3 | Internet |  | - |


***

## 21. Important Exam Traps:

- TCP/UDP header fields (byte numbers, port numbers, flags).
- ALOHA/CSMA/CD conceptual and numerical.
- Addressing/subnet mask questions.
- Error-control: which error pattern is/n't detected.
- Fragmentation: offset, MF bit calculations with variable packet sizes.

***

## 22. Acronyms For Memory Hacks

- **OSI:** All People Seem To Need Data Processing
    - Application, Presentation, Session, Transport, Network, Data Link, Physical
- **TCP/IP:** ANTI-L (Application, Network, Transport, Internet, Link)

***

## 23. How To Use This Sheet

- Pick any area above as per your weak zone.
- For numericals: learn formula, understand template, solve at least 2 examples.
- For theory: memorize key facts, acronyms, and tables.
- During revision, just review this page for every core topic—all GATE/ISRO CN questions fit into the patterns above.

***

**You are now exam-ready for Computer Networks for the GATE/ISRO ICRB CSE Exam!**
<span style="display:none">[^1]</span>

<div align="center">⁂</div>

[^1]: CN.pdf

