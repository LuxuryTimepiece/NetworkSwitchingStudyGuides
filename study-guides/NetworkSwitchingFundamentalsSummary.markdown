# Summary: Network Switching Fundamentals

This document summarizes the key topics from the YouTube playlist on network switching, presented by Barry Smith, Program Director for Information Technology at Virginia College Online. The playlist covers binary numbers, IPv4 addressing, and subnetting, providing foundational knowledge for network administration and certification exams (e.g., A+, Network+, Security+, Cisco CCNA).

## 1. Binary Numbers
- **Core Concept**: Computers operate using binary (base-2) numbers, understanding only **0** (off) and **1** (on), unlike the decimal (base-10) system (0–9).
- **Binary Calculator**: A chart (128, 64, 32, 16, 8, 4, 2, 1) used for binary-to-decimal conversions.
  - Each position represents a power of 2, doubling from right to left.
  - Common in computing (e.g., 16GB, 32GB RAM are powers of 2).
- **Conversions**:
  - **Binary to Decimal**: For a binary number (e.g., 01100110), sum the values of columns with a 1 (64 + 32 + 4 + 2 = 102).
  - **Decimal to Binary**: For a decimal number (e.g., 217), find which powers of 2 sum to the number (128 + 64 + 16 + 8 + 1 = 11011001).
- **Relevance**: Essential for understanding IP addressing and subnetting, as devices process addresses in binary.

## 2. IPv4 Addressing
- **Structure**: IPv4 addresses are 32-bit, divided into four 8-bit **octets** (e.g., 192.168.1.1), each ranging from 0–255.
- **Classes**:
  - **Class A**: 1–126 (first octet), for large networks; default subnet mask 255.0.0.0.
  - **Class B**: 128–191, for medium networks; default subnet mask 255.255.0.0.
  - **Class C**: 192–223, for small networks; default subnet mask 255.255.255.0.
  - **Class D**: 224–239, for multicasting.
  - **Class E**: 240–255, for government/research (not commonly used).
  - **Loopback**: 127.0.0.1, used for troubleshooting (pinging tests network card functionality).
- **Network and Node IDs**:
  - **Network ID**: Identifies the network (like an area code).
  - **Node/Host ID**: Identifies a device within the network (like a phone number).
  - Class A: 1st octet (network), 2nd–4th (node).
  - Class B: 1st–2nd octets (network), 3rd–4th (node).
  - Class C: 1st–3rd octets (network), 4th (node).
- **Public vs. Private IPs**:
  - **Public**: Globally unique, used on the internet.
  - **Private**: Not routable on the internet, used in internal networks (e.g., home, corporate).
    - Class A: 10.0.0.0–10.255.255.255
    - Class B: 172.16.0.0–172.31.255.255
    - Class C: 192.168.0.0–192.168.255.255
  - Private IPs access the internet via a router using Network Address Translation (NAT).
- **Subnet Masks**:
  - Identify network and node portions of an IP address.
  - 255 (11111111) indicates network bits; 0 (00000000) indicates node bits.
  - Default subnet masks align with class structure (e.g., Class C: 255.255.255.0).
  - Critical for subnetting and network configuration.

## 3. Subnetting
- **Definition**: Dividing a network into smaller subnetworks (subnets) for better management, security, and performance.
  - Analogy: Dividing a pizza into slices; each subnet is a slice of the original network.
- **Benefits**:
  - **Security**: Isolates sensitive data (e.g., HR subnet separate from Sales).
  - **Organization**: Groups devices by department/function (e.g., IT, Marketing).
  - **Performance**: Reduces network congestion by isolating traffic.
- **Router’s Role**: Connects subnets, acting as a gatekeeper to control access (single point of administration).
- **Six Steps of Subnetting ("Hard Way")**:
  1. **Identify Class**: Determine Class A, B, or C based on the first octet.
  2. **Identify Network/Node IDs**: Based on class (e.g., Class B: first two octets = network, last two = node).
  3. **Apply Default Subnet Mask**: Use class-specific mask (e.g., Class B: 255.255.0.0).
  4. **Convert to Binary**: Translate subnet mask to binary (255 = 11111111, 0 = 00000000).
  5. **Determine Custom Subnet Mask**:
     - Ascertain the number of subnets needed (use formula 2^n - 2 ≥ required subnets).
     - Borrow bits from node portion, turning zeros to ones (e.g., for 11 subnets, 2^4 - 2 = 14; borrow 4 bits).
     - Convert new binary mask to decimal (e.g., 11111111.11111111.11110000.00000000 = 255.255.240.0).
  6. **Find Least Significant Bit (LSB)**: Smallest bit with a 1 in the modified octet (e.g., 11110000 = 16).
     - LSB determines subnet range increments (e.g., 172.16.0.0–172.16.15.255, 172.16.16.0–172.16.31.255).
- **CIDR Notation ("Easy Way")**:
  - Format: IP address/number (e.g., 172.16.0.0/20).
  - Number indicates how many 1s in the subnet mask (e.g., /20 = 255.255.240.0).
  - Skips steps 1–5; directly calculate LSB and ranges.
- **Key Rule**: Subnet masks must have continuous 1s followed by 0s.
- **Practice Tip**: Memorize common subnet masks (e.g., 255.255.240.0 = /20, LSB = 16) and practice calculations to achieve speed (7–10 seconds).

## Practical Applications
- **Binary**: Converts IP addresses and subnet masks for device-level processing.
- **IPv4 Addressing**: Enables device identification and communication across networks.
- **Subnetting**: Enhances network security, organization, and performance by creating manageable subnetworks.
- **Certifications**: Binary, IP addressing, and subnetting are critical for A+, Network+, Security+, and Cisco exams.

## Practice Recommendations
- **Binary Conversions**: Convert binary to decimal (e.g., 10101010) and decimal to binary (e.g., 145).
- **Class Identification**: Identify class, network/node IDs, and default subnet masks for IPs like 10.1.2.3, 172.16.100.50.
- **Subnetting Exercises**:
  - Hard Way: Subnet 192.168.1.0 for 5 subnets, calculate custom mask and ranges.
  - Easy Way: For 10.0.0.0/12, determine subnet mask and first three subnet ranges.
- **Real-World Scenarios**: Design subnet structures for a company with departments (e.g., HR, IT), assigning IPs and enforcing access rules via routers.

## Tips for Success
- **Memorize Key Values**:
  - Binary calculator: 128, 64, 32, 16, 8, 4, 2, 1.
  - Private IP ranges and default subnet masks.
  - Common CIDR notations and LSBs (e.g., /20 = 255.255.240.0, LSB = 16).
- **Use Analogies**:
  - Network ID = area code, Node ID = phone number.
  - Subnetting = slicing a pizza for easier management.
- **Practice Regularly**: Repetition builds speed and pattern recognition for exams.
- **Resources**: Use the course’s “Subnetting Information” Excel spreadsheet for practice.
- **Avoid Mistakes**:
  - Say “dot” when reading IP addresses (e.g., 192.168.1.1).
  - Don’t skip subnetting steps to avoid errors.
  - Understand private IPs require NAT for internet access.