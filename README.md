# Scapy Packet Crafting Lab

A hands-on network analysis and packet crafting practical using **Python Scapy**, **Kali Linux**, and **Wireshark**.

This project documents the exploration of network protocols, live traffic sniffing, packet inspection, custom ICMP packet transmission, and TCP SYN packet analysis in an isolated Cisco lab environment.

## Project Objectives

The main objectives of this practical were to:

- Explore Scapy and its available protocol layers.
- Examine IPv4 header fields.
- Capture and filter network traffic.
- Inspect individual packets and their protocol layers.
- Construct and transmit custom ICMP packets.
- Create TCP SYN packets and analyse the responses.
- Save packet captures and examine them using Wireshark.

## Tools and Technologies

| Tool | Purpose |
|---|---|
| Kali Linux | Practical lab environment |
| Python Scapy | Packet crafting and traffic sniffing |
| Wireshark | Packet capture analysis |
| PCAP | Packet capture file format |

## Lab Environment

| Component | Details |
|---|---|
| Operating System | Kali Linux |
| Network Interface | `eth0` |
| Lab Network | `172.20.10.0/24` |
| Target IP | `172.20.10.5` |
| TCP Destination Port | `445` |


## Practical Activities

### Part 1: Scapy Basics

Explored Scapy's interactive environment and inspected available protocol layers.

Commands used:

```python
ls()
ls(IP)
```

The exercise involved identifying available packet formats and examining IPv4 header fields, including source address, destination address, TTL and protocol.

### Part 2: Network Traffic Sniffing

Used Scapy to capture and inspect network traffic.

Activities included:

- Capturing packets on network interfaces.
- Sniffing traffic on `eth0`.
- Filtering traffic using the ICMP protocol.
- Displaying packet summaries using `summary()` and `nsummary()`.
- Inspecting individual packet layers.
- Saving captured traffic into a PCAP file.
- Opening the saved capture in Wireshark.

### Part 3: Custom ICMP Packet Crafting

Constructed and transmitted a custom ICMP packet containing a text payload.

Command:

```python
send(IP(dst="172.20.10.5")/ICMP()/"This is a test")
```

**Result:** The custom ICMP packet was successfully transmitted, and its payload was visible in the captured traffic.

### Part 4: TCP SYN Packet Crafting

Constructed and transmitted a TCP SYN packet targeting port 445.

Command:

```python
send(IP(dst="172.20.10.5")/TCP(dport=445, flags="S"))
```

**Result:** TCP traffic containing SYN (`S`), SYN-ACK (`SA`) and RST (`R`) flags was observed during the exercise.

The responses demonstrated different stages and outcomes of TCP connection attempts.

## Key Findings and Learning Outcomes

Through this practical, I gained hands-on experience with:

1. Exploring network protocols using Scapy.
2. Understanding the structure of IPv4 headers.
3. Capturing and filtering network traffic.
4. Inspecting packet layers and protocol information.
5. Creating and transmitting custom ICMP packets.
6. Understanding TCP SYN, SYN-ACK and RST flags.
7. Analysing saved packet captures with Wireshark.

## Project Structure

```text
Scapy_Packet_Crafting_Lab/
│
├── README.md
├── LICENSE
├── .gitignore
├── .gitattributes
│
├── docs/
│   ├── workflow.md
│   ├── lab-notes.md
│   └── findings-template.md
│
├── evidence/
│   ├── screenshots/
│   │   ├── part-1-scapy-basics/
│   │   ├── part-2-traffic-sniffing/
│   │   ├── part-3-icmp-packet/
│   │   └── part-4-tcp-syn/
│   │
│   ├── terminal-outputs/
│   └── pcaps/
│
├── scripts/
│
└── references/
```

## Evidence and Screenshots

The following screenshots document the practical activities and their results.

### Part 1: Scapy Basics

1. [Scapy Version](evidence/screenshots/part-1-scapy-basics/01-scapy-version.png)
2. [Scapy Welcome Screen](evidence/screenshots/part-1-scapy-basics/02-scapy-welcome-screen.png)
3. [Scapy Protocol List](evidence/screenshots/part-1-scapy-basics/03-scapy-protocol-list.png)
4. [TFTP Packet Formats](evidence/screenshots/part-1-scapy-basics/04-tftp-packet-formats.png)
5. [IPv4 Header Fields](evidence/screenshots/part-1-scapy-basics/05-ipv4-header-fields.png)

### Part 2: Traffic Sniffing

6. [Default Traffic Capture](evidence/screenshots/part-2-traffic-sniffing/06-default-traffic-capture.png)
7. [Traffic Summary](evidence/screenshots/part-2-traffic-sniffing/07-traffic-summary.png)
8. [Internal Interface Sniffing](evidence/screenshots/part-2-traffic-sniffing/08-internal-interface-sniffing.png)
9. [ICMP Filtered Capture](evidence/screenshots/part-2-traffic-sniffing/09-icmp-filtered-capture.png)
10. [Packet Inspection](evidence/screenshots/part-2-traffic-sniffing/10-packet-inspection.png)
11. [PCAP and Wireshark Analysis](evidence/screenshots/part-2-traffic-sniffing/11-pcap-and-wireshark-analysis.png)

### Part 3: ICMP Packet Crafting

12. [ICMP Packet Construction](evidence/screenshots/part-3-icmp-packet/12-icmp-packet-construction.png)
13. [ICMP Transmission and Analysis](evidence/screenshots/part-3-icmp-packet/13-icmp-transmission-and-analysis.png)

### Part 4: TCP SYN Packet Crafting

14. [TCP SYN Packet](evidence/screenshots/part-4-tcp-syn/14-tcp-syn-packet.png)
15. [TCP Response Analysis](evidence/screenshots/part-4-tcp-syn/15-tcp-response-analysis.png)

## Documentation

Additional project documentation is available in the `docs/` directory:

- `lab-notes.md` – Detailed notes on the practical activities.
- `findings-template.md` – Findings and results from the exercises.
- `workflow.md` – Lab procedure and GitHub workflow.

## Security and Ethical Considerations

All packet crafting and traffic analysis activities in this project were performed within an authorised educational lab environment.

Network scanning, packet sniffing and packet transmission should only be conducted on systems and networks where appropriate permission has been granted.

## References

- [Scapy documentation – Introduction](https://scapy.readthedocs.io/en/latest/introduction.html)
- [Scapy project](https://github.com/secdev/scapy)
- [IANA ICMP Parameters](https://www.iana.org/assignments/icmp-parameters/icmp-parameters.xhtml)
- Cisco Networking Academy: *Lab – Packet Crafting with Scapy* (course material supplied for this exercise)

## Author

**Divine Obiorah**

Computer Science Student | Cybersecurity Enthusiast

GitHub: [DivineObiorah](https://github.com/DivineObiorah)

