# Study Guide: Subnetting Process (Parts 1 and 2)

## Overview
This study guide is based on the seventh and eighth videos from the YouTube playlist on network switching, presented by Barry Smith, Program Director for Information Technology at Virginia College Online. These videos provide a step-by-step guide to subnetting, including the six-step process for subnetting (the "hard way") and the simplified approach using CIDR notation (the "easy way"). The guide emphasizes practical application and understanding for network administration and certification exams.

## Key Concepts

### 1. Importance of Subnetting
- **Subnetting Overview**: Subnetting divides a single network into smaller subnetworks (subnets) for better management, security, and performance.
- **Certification Relevance**: Subnetting is critical for certifications like Cisco’s CCNA (approximately 60% of the exam) and other networking exams (e.g., Network+, Security+).
- **Learning Curve**: Subnetting may seem complex initially, but with practice, it becomes manageable. Patterns in subnet masks and calculations simplify the process over time.

### 2. Prerequisites
- **Required Knowledge**:
  - Understanding of IP address classes (A, B, C) and their default subnet masks.
  - Ability to convert between binary and decimal numbers using a binary calculator (128, 64, 32, 16, 8, 4, 2, 1).
  - Familiarity with network and node/host IDs from previous lessons.
- **Tools**:
  - **Binary Calculator**: A chart with powers of 2 (128, 64, 32, 16, 8, 4, 2, 1) used for binary-to-decimal conversions.
  - **Excel Spreadsheet**: Available in the course’s doc sharing, titled “Subnetting Information,” to follow along with examples.
- **Practice Tip**: Write down the binary calculator (128, 64, 32, 16, 8, 4, 2, 1) during exams for quick reference.

### 3. The Six Steps of Subnetting ("Hard Way")
Subnetting involves six steps to create subnets from a given IP address and determine their ranges. These steps are applied when subnetting without CIDR notation.

- **Step 1: Identify the Class**
  - Determine the IP address class (A, B, or C) based on the first octet:
    - Class A: 1–126
    - Class B: 128–191
    - Class C: 192–223
  - Example: For 172.16.0.0, the first octet (172) is between 128–191, so it’s **Class B**.

- **Step 2: Identify Network and Node IDs**
  - Based on the class, identify which octets represent the network ID and which represent the node/host ID:
    - Class A: First octet (network), last three octets (node).
    - Class B: First two octets (network), last two octets (node).
    - Class C: First three octets (network), last octet (node).
  - Example: For 172.16.0.0 (Class B), network ID is 172.16, node ID is 0.0.

- **Step 3: Apply the Default Subnet Mask**
  - Assign the default subnet mask based on the class:
    - Class A: 255.0.0.0 (binary: 11111111.00000000.00000000.00000000)
    - Class B: 255.255.0.0 (binary: 11111111.11111111.00000000.00000000)
    - Class C: 255.255.255.0 (binary: 11111111.11111111.11111111.00000000)
  - Example: For 172.16.0.0 (Class B), default subnet mask is **255.255.0.0**.

- **Step 4: Convert Subnet Mask to Binary**
  - Convert each octet of the subnet mask to binary using the binary calculator.
  - Example: 255.255.0.0 = **11111111.11111111.00000000.00000000** (8 ones, 8 ones, 8 zeros, 8 zeros).

- **Step 5: Determine the Custom Subnet Mask**
  - Use the formula **2^n - 2** to calculate the number of subnets needed.
    - **n** is the number of bits to borrow from the node portion to create subnets.
    - The result must be ≥ the number of subnets required.
  - Example: Need 11 subnets for 172.16.0.0.
    - Calculate: 2^4 = 16, 16 - 2 = **14** (≥ 11).
    - Alternative: 2^5 = 32, 32 - 2 = **30** (also ≥ 11, allows more growth).
    - Choose n = 4 (14 subnets) for this example.
  - Borrow **n** bits from the node portion of the subnet mask, turning zeros into ones.
    - Rule: Subnet mask bits must start with continuous ones, followed by zeros.
    - For Class B (255.255.0.0), borrow 4 bits from the third octet:
      - Original: 11111111.11111111.00000000.00000000
      - Borrow 4 bits: 11111111.11111111.11110000.00000000
      - Convert to decimal: 255.255.240.0 (128 + 64 + 32 + 16 = 240).
  - Custom subnet mask: **255.255.240.0**.

- **Step 6: Determine the Least Significant Bit (LSB) and Subnet Ranges**
  - The **LSB** is the smallest bit in the modified octet that is a 1 (has value).
  - Example: In the third octet (11110000), the smallest bit with a 1 is **16** (LSB).
  - The LSB determines the **increment** for subnet ranges.
    - Subnets start at multiples of the LSB in the modified octet.
  - Example: For 172.16.0.0 with subnet mask 255.255.240.0 (LSB = 16):
    - Subnet 1: 172.16.0.0 to 172.16.15.255
    - Subnet 2: 172.16.16.0 to 172.16.31.255
    - Subnet 3: 172.16.32.0 to 172.16.47.255
    - Continue: 172.16.48.0, 172.16.64.0, etc., up to 172.16.240.0.
  - Each subnet is a “slice” of the original network, with the range defined by the LSB (e.g., every 16 numbers in the third octet).

### 4. The Easy Way: CIDR Notation
- **CIDR Notation**: Uses a slash and number (e.g., /20) to indicate the number of 1s in the subnet mask.
  - Example: 172.16.0.0/20 means the subnet mask has 20 ones.
- **Why It’s Easy**:
  - Steps 1–5 are already done; the /number provides the custom subnet mask.
  - Only Step 6 (finding the LSB and ranges) is needed.
- **Process**:
  - Convert the /number to a subnet mask:
    - Total bits = 32 (IPv4 address).
    - /20 = 20 ones, 12 zeros.
    - Divide into octets: 8 ones (255), 8 ones (255), 4 ones (240), 0 ones (0).
    - Subnet mask: **255.255.240.0**.
  - Find the LSB:
    - In the third octet (11110000), LSB = **16**.
  - Calculate ranges using the LSB, as in the “hard way.”
    - Example: 172.16.0.0/20 yields the same ranges as above (172.16.0.0–172.16.15.255, 172.16.16.0–172.16.31.255, etc.).
- **Advantage**: Skips the need to calculate the number of subnets or borrow bits manually.

### 5. Subnetting Rules and Patterns
- **Subnet Mask Rule**: Must start with continuous 1s, followed by 0s (e.g., 11110000, not 11001100).
- **Common Subnet Masks**: Recognize patterns in modified octets:
  - 11110000 = 240 (128 + 64 + 32 + 16)
  - 11100000 = 224 (128 + 64 + 32)
  - 11000000 = 192 (128 + 64)
- **LSB Values**: Common LSBs (16, 8, 32, etc.) indicate subnet increments.
- **Practice Tip**: Memorize common subnet masks (e.g., 255.255.240.0 = /20) and their LSBs to speed up calculations.

## Practice Exercises
1. **Subnetting (Hard Way)**:
   - IP: 192.168.1.0, need 5 subnets.
   - Follow the six steps to:
     - Identify the class, network/node IDs, and default subnet mask.
     - Calculate the number of bits to borrow (2^n - 2 ≥ 5).
     - Determine the custom subnet mask and LSB.
     - List the first three subnet ranges.
2. **Subnetting (Easy Way)**:
   - IP: 10.0.0.0/12
   - Convert /12 to a subnet mask.
   - Find the LSB and list the first three subnet ranges.
3. **Mixed Practice**:
   - For IP 172.20.0.0, need 8 subnets.
   - Determine the custom subnet mask and LSB.
   - Compare with 172.20.0.0/21 (CIDR notation) to verify if it meets the requirement.
4. **Pattern Recognition**:
   - Convert the following binary subnet mask octets to decimal and identify the LSB:
     - 11100000
     - 11111000
     - 11000000
5. **Real-World Scenario**:
   - A company needs 10 subnets for departments. Start with IP 172.30.0.0.
   - Calculate the subnet mask, LSB, and list all subnet ranges.
   - Assign departments (e.g., HR, IT, Sales) to specific subnets.

## Tips for Success
- **Follow All Steps**: Even when confident, mentally go through all six steps to avoid errors.
- **Memorize the Binary Calculator**: 128, 64, 32, 16, 8, 4, 2, 1 is essential for conversions.
- **Practice CIDR Notation**: Learn common /numbers (e.g., /20 = 255.255.240.0) and their LSBs.
- **Recognize Patterns**: Common subnet masks (240, 224, 192) and LSBs (16, 8, 32) repeat frequently.
- **Don’t Panic**: Subnetting takes practice; expect initial confusion but aim for 7–10 second calculations with repetition.
- **Use Resources**: Download the “Subnetting Information” Excel spreadsheet from the course to follow along.
- **Certification Focus**: Subnetting is a major component of Cisco exams; practice until it’s second nature.

## Additional Notes
- **Pizza Analogy**:
  - Original network = whole pizza.
  - Subnets = slices, created by borrowing bits to form new network IDs.
- **Why LSB Matters**: The LSB defines the increment for subnet ranges, making it the key to determining where subnets start and end.
- **Real-World Application**:
  - Network administrators choose a starting IP (e.g., 172.16.0.0) and design subnets based on organizational needs.
  - Subnetting improves security (isolating departments), organization (grouping by function), and performance (reducing traffic).
- **Future Learning**:
  - Additional videos will provide more practice examples.
  - Focus on recognizing patterns and speeding up calculations for exams.