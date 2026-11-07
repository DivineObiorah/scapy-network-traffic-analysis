# Scapy Packet Crafting Lab – Lab Notes

## 1. Lab Overview

This practical focused on exploring Scapy, a Python-based interactive packet manipulation tool used for network discovery, packet crafting, traffic sniffing and network analysis.

The exercise provided hands-on experience with inspecting network protocols, capturing traffic, constructing custom ICMP packets and transmitting TCP SYN packets.

## 2. Lab Environment

| Component | Details |
|---|---|
| Operating System | Kali Linux |
| Packet Manipulation Tool | Scapy |
| Packet Analysis Tool | Wireshark |
| Network Interface | eth0 |
| Lab Network | 172.20.10.0/24 |
| Target IP | 172.20.10.5 |


## 3. Activities Performed

### Part 1: Introduction to Scapy

Scapy was launched through its interactive shell to explore its available functionality.

The following commands were used:

- `ls()` – Displayed available protocol layers and packet formats.
- `ls(IP)` – Displayed the fields and parameters associated with the IPv4 protocol.

**Observations:**

- Scapy provides access to numerous network protocols and packet formats.
- The `ls()` command makes it possible to explore available protocol layers.
- The IPv4 inspection command displayed fields such as source address, destination address, TTL, protocol and packet length.
- These fields help explain how IP packets are structured and transmitted across networks.

### Part 2: Network Traffic Sniffing

Scapy's sniffing functionality was used to capture network traffic and inspect the packets collected.

The practical involved:

- Capturing traffic on the default network interface.
- Capturing traffic on the `eth0` interface.
- Filtering captured traffic to identify ICMP packets.
- Using `summary()` and `nsummary()` to examine captured packets.
- Inspecting individual packet layers.
- Saving captured traffic in PCAP format and opening it in Wireshark.

**Observations:**

- Scapy can capture packets travelling through a selected network interface.
- Traffic filtering helps isolate packets belonging to a particular protocol.
- Packet summaries provide a quick overview of captured network communication.
- Individual packet inspection reveals additional information about protocol layers and packet fields.
- PCAP files allow captured traffic to be saved and examined later using tools such as Wireshark.

### Part 3: Creating and Sending ICMP Packets

A custom ICMP packet was constructed and transmitted using Scapy.

The packet included:
- An IPv4 header.
- An ICMP layer.
- A custom payload containing the text `This is a test`.

The destination used in the Cisco lab was `172.20.10.5`.

**Observations:**

- Scapy allows different protocol layers to be combined to construct custom packets.
- The IP layer specifies the destination address.
- The ICMP layer identifies the packet's control-message protocol.
- A custom payload can be included in the packet.
- The transmission output and captured packet provide evidence of the packet-sending operation.

### Part 4: Creating and Sending TCP SYN Packets

A TCP SYN packet was constructed and transmitted to the lab target on destination port 445.

The packet used:
- IPv4 as the network layer.
- TCP as the transport layer.
- Destination port 445.
- The SYN (`S`) flag.

**Observations:**

- TCP packets use flags to control and manage connection establishment.
- The SYN flag is used to initiate a TCP connection.
- A SYN-ACK (`SA`) response indicates that the target acknowledged the connection request.
- The response can provide useful information about the state of a TCP port.
- Packet inspection helps identify the flags and other details contained in the response.

## 4. General Findings

The practical demonstrated several important capabilities of Scapy:

1. Protocol inspection and exploration.
2. Network traffic capture and filtering.
3. Packet-layer inspection.
4. Custom ICMP packet construction and transmission.
5. TCP SYN packet construction and response analysis.
6. Saving and analysing packet captures using Wireshark.

## 5. Challenges and Troubleshooting

Some practical activities may depend on the correct network interface, permissions and availability of traffic on the lab network.

The following considerations were important during the exercise:

- Running Scapy with appropriate privileges for packet capture and transmission.
- Selecting the correct network interface.
- Applying the correct protocol filter when sniffing traffic.
- Confirming that the target system was reachable within the isolated lab environment.
- Inspecting packet responses carefully to understand the results.

## 6. Conclusion

This practical provided hands-on experience with Scapy and demonstrated how it can be used to inspect network protocols, capture traffic, construct custom packets and analyse TCP responses.

The exercise strengthened my understanding of packet structure, network communication and basic network reconnaissance techniques.

It also demonstrated the importance of packet analysis tools such as Wireshark when investigating network traffic.