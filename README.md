# cybersecurity-home-lab
Cybersecurity lab for network segmentation, lateral movement, and exploitation using Kali Linux, pfSense, and vulnerable VMs.

## Overview
This project demonstrates the design and implementation of a segmented virtual cybersecurity lab using VirtualBox and pfSense. The environment simulates a real-world enterprise network with isolated internal segments, enabling safe testing of vulnerabilities, network communication, and lateral movement scenarios.

## Lab Architecture

The lab consists of the following virtual machines:

pfSense – Firewall/router providing network segmentation and internet access
Kali Linux – Attacker machine for security testing
Windows 10 – Dual-homed system acting as a pivot between networks
Metasploitable – Vulnerable target machine (internal network)
OWASP Broken Web Applications (BWA) – Vulnerable web applications for testing

## Network Design

### Internal Network 1 (intnet – 192.168.1.0/24)
Kali Linux - '192.168.1.111'
Windows 10 - '192.168.1.113'
OWASP BWA - (same subnet)
pfSense LAN - '192.168.1.1'

### Internal Network 2 (intnet2 – 192.168.2.0/24)
Windows 10 - '192.168.2.8'
Metasploitable - '192.168.2.2'

### WAN
pfSense WAN connected via NAT to the host machine

Windows 10 is dual-homed, connecting both networks and simulating a pivot point for lateral movement.

## Network Summary

| Machine        | Interface | IP Address     | Network   |
|----------------|----------|----------------|----------|
| Kali Linux     | eth0     | 192.168.1.111  | intnet   |
| Windows 10     | Eth0     | 192.168.1.113  | intnet   |
| Windows 10     | Eth1     | 192.168.2.8    | intnet2  |
| Metasploitable | eth0     | 192.168.2.2    | intnet2  |
| pfSense        | LAN      | 192.168.1.1    | intnet   |

## Validation Tests

### Kali Linux Configuration
Verified that Kali Linux is correctly connected to the internal network.

Interface: 'eth0'
IP Address: '192.168.1.111'

Evidence:

<img width="603" height="372" alt="kali-ifconfig" src="https://github.com/user-attachments/assets/16c891ee-e63a-4de6-88f0-bbb19ca21c56" />

### pfSense Internet Connectivity
Tested external connectivity and DNS resolution from pfSense.

Command: 'ping www.google.com'
Result: Successful responses with 0% packet loss
Domain resolved to: '142.251.221.68'

Evidence:

<img width="717" height="207" alt="pfsense-ping" src="https://github.com/user-attachments/assets/f678ba01-d862-4ba6-9949-9c11a82ddf6f" />

pfSense uses a WAN interface configured with NAT, allowing outbound internet access through the host system. Successful ping to a domain confirms both DNS resolution and internet routing are functioning correctly.

### Internal Network Connectivity (intnet2)
Validated communication between Windows 10 and Metasploitable on the isolated internal network.

#### Windows 10 to Metasploitable
Evidence:

<img width="448" height="228" alt="win-ping-metasploitable" src="https://github.com/user-attachments/assets/80bb5ea8-3de3-4cf8-b416-35a8764e43ee" />

#### Metasploitable to Windows 10
Evidence:

<img width="561" height="192" alt="metasploitable-ping-win" src="https://github.com/user-attachments/assets/9f010b1e-50ec-46ab-92d2-e311f6ca0ba7" />

Successful ICMP communication confirms both systems are correctly configured on the same subnet (192.168.2.0/24). This validates the functionality of the isolated internal network and supports realistic internal network attack scenarios such as lateral movement.

## Supporting Configuration Evidence

### Windows 10 Configuration
Evidence:

<img width="532" height="372" alt="win-ipconfig" src="https://github.com/user-attachments/assets/13e5511a-675e-461f-ae5b-d8f795ed9c6e" />

### Metasploitable Network Configuration
Evidence:

<img width="716" height="303" alt="metasploitable-ifconfig" src="https://github.com/user-attachments/assets/5503b4dc-bfd0-4e61-9841-8f0eeff4f15a" />

## Security Concepts Demonstrated
- Network segmentation using multiple internal networks  
- Firewall configuration and traffic control using pfSense  
- Dual-homed system risk (pivot point for lateral movement)  
- Isolation of vulnerable systems within a controlled lab  
- DNS resolution and outbound connectivity validation

## Security Considerations

- Vulnerable machines are not exposed directly to the internet  
- pfSense controls traffic between WAN and internal networks  
- All systems operate within an isolated virtual lab environment
