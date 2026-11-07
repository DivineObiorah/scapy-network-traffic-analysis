# Scapy Lab – Findings and Results

## 1. Scapy Protocol Exploration

**Commands used:**
- `ls()`
- `ls(IP)`

**Findings:**

- Successfully launched the Scapy interactive shell.
- Explored the available protocol layers and packet formats.
- Inspected the IPv4 header structure and identified fields such as source address, destination address, TTL and protocol.

## 2. Network Traffic Sniffing

**Activities performed:**
- Captured network traffic using Scapy.
- Used the `eth0` interface.
- Applied an ICMP filter.
- Inspected captured packets using `summary()` and `nsummary()`.
- Saved the capture as `capture1.pcap`.

**Findings:**

- Successfully captured network traffic.
- Successfully filtered and identified ICMP packets.
- Inspected packet details and protocol layers.
- Saved the captured traffic for further analysis.

## 3. ICMP Packet Crafting

**Destination IP:** 172.20.10.5

**Custom payload:** `This is a test`

**Findings:**

- Successfully constructed and transmitted a custom ICMP packet using Scapy.
- The custom payload was visible in the captured traffic.
- Confirmed that the packet contained the intended ICMP message and destination information.

## 4. TCP SYN Packet Crafting

**Destination IP:** 172.20.10.5

**Destination port:** 445

**TCP flags observed:** S, SA and R

**Findings:**

- Successfully constructed and transmitted a TCP SYN packet.
- Observed the SYN flag (`S`) in the transmitted packet.
- Observed SYN-ACK (`SA`) and RST (`R`) flags in TCP traffic.
- The SYN-ACK response indicated acknowledgement of a connection request.
- The RST response indicated that a connection attempt was reset or rejected.

## 5. Wireshark Analysis

**Capture file:** `capture1.pcap`

**Findings:**

- Successfully opened the saved PCAP file in Wireshark.
- Examined the captured packets using Wireshark's packet list and packet details.
- Verified packet information and protocol layers through graphical packet analysis.

## 6. Overall Results

| Practical activity | Result |
|---|---|
| Scapy protocol exploration | Completed |
| IPv4 header inspection | Completed |
| Network traffic sniffing | Completed |
| ICMP traffic filtering | Completed |
| Packet inspection | Completed |
| PCAP file creation | Completed |
| Wireshark analysis | Completed |
| Custom ICMP packet transmission | Successful |
| TCP SYN packet transmission | Successful |
| TCP response analysis | Completed |

## 7. Final Observation

The practical demonstrated how Scapy can be used to explore network protocols, capture and inspect traffic, construct custom packets and analyse TCP responses.

The exercise also demonstrated how Wireshark complements Scapy by providing a graphical environment for examining saved packet captures.