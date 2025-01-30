# Guide: Wireshark

!!! note "Wireshark"
    A network protocol analyzer - allows you to inspect recorded network traffic.

    [Download link](https://www.wireshark.org/)

---

!!! definition "What is a PCAP file?"
    Packet capture file - `.pcap` file extension.

    Contains a copy of every byte transmitted on the network (OSI layers 2-7).

    [Endance - what is a pcap file?](https://www.endace.com/learn/what-is-a-pcap-file)

## File Structure

### File Header

<ins>_Magic numbers (4-bytes)_</ins>

- `0xA1B2C3D4`: timestamp is seconds and microseconds
- `0xA1B23C4D`: timestamp is seconds and nanoseconds

<ins>_SpanLen (4-bytes)_</ins>

- maximum number of octets captured from each packet

<ins>_LinkType (2-bytes)_</ins>

- describes the type of link the packets were captured from - assigned by [tcpdump.org](tcpdump.org)

<ins>_F (1-bit)_</ins>

- acts as a boolean indictor for the `FCS` field

<ins>_Frame Check Sequence (FCS) (3-bits)_</ins>

- if set as 'True'
- 16-bit (2 bytes) words of `FCS` that are appended to each packet
- e.g. Ethernet typically has the value 2 stored here - indicating 32-bit FCS

### Packet Records

- There will be zero or more of these.

- Each packet record reprents a single packet.

<ins>_Packet record header_</ins>

- <ins>timestamp (seconds)</ins>
    - the number of seconds that have elapsed since 1970-01-01 00:00:00 UTC (EPOCH)
- <ins>timestamp (micro/nanoseconds)</ins>
    - the number of microseconds or nanoseconds that have elapsed since the last full second
- <ins>captured packet length</ins>
    - the number of octets captured from the packet
    - if packets are truncated this value is the length of the truncated packet
- <ins>original packet length</ins>
    - 32-bits
    - the actual length of the packet when it was transmitted on the network

<ins>_Ethernet header_</ins>

<ins>_IP packet_</isn>

<ins>_Ethernet frame checksum (EFC)_</ins>

- may or may not have been captured
- **if dropped**: captured packets can still be assumed to be valid - erraneous packets may have been dropped
- **if included**: reader can check for errors in each packet

---

## Alternatives

!!! definition "File extension: `*.pcapng`"
    PCAP Next Generation

    Has a more flexible file structure.

    Includes additional packet information such as drop counters, DNS records, etc.

!!! definition "File extension: `*.erf`"
    Extensible Record Format

    Adds provenance metadata (e.g. originating system name, system status, etc.), more detailed timestamps, and in-band packet loss auditing.

---

## Viewing Network Traffic in Wireshark

[ctf101 - what is wireshark](https://ctf101.org/forensics/what-is-wireshark/)

- Shows the packets in the order in which they were captured.

- Allows you to filter by protocol, source IP address, destination IP address, length, etc.