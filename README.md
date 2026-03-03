# 🔐 Enterprise Network Security Lab
Cybersecurity lab simulating enterprise network segmentation, traffic control, and lateral movement using Kali Linux, pfSense, and vulnerable virtual machines.

## 🚀 Overview
This project demonstrates the design and implementation of a segmented virtual network using VirtualBox and pfSense. The lab simulates an enterprise environment with isolated internal subnets, enabling safe testing of network communication, system connectivity, and lateral movement scenarios.

The environment was built to strengthen practical skills in networking, system configuration, and troubleshooting while exploring how segmentation impacts security.

## ✅ Key Outcomes
- Implemented network segmentation to isolate systems across multiple internal subnets
- Demonstrated how a dual-homed host can act as a pivot point for lateral movement
- Configured and validated firewall rules, NAT, and routing to control traffic flow
- Simulated realistic enterprise network behaviour in a controlled lab environment
- Strengthened troubleshooting skills across networking, DNS, and system connectivity

## 🛠️ Skills Demonstrated
- Network segmentation and subnetting
- Firewall configuration (pfSense)
- NAT and inter-network routing
- TCP/IP networking and DNS resolution
- Virtualisation (VirtualBox)
- Network troubleshooting and diagnostics

## 🧱 Lab Architecture
The lab consists of the following virtual machines:
- **pfSense** – Firewall/router providing network segmentation and internet access 
- **Kali Linux** – Attacker machine for security testing  
- **Windows 10** – Dual-homed system acting as a pivot between networks  
- **Metasploitable** – Vulnerable internal target machine
- **OWASP Broken Web Applications (BWA)** – Vulnerable web application environment

## 🌐 Network Design

### Internal Network 1 (intnet – 192.168.1.0/24)
- Kali Linux → `192.168.1.111`  
- Windows 10 → `192.168.1.113`  
- OWASP BWA → (same subnet)  
- pfSense LAN → `192.168.1.1`

### Internal Network 2 (intnet2 – 192.168.2.0/24)
- Windows 10 → `192.168.2.8`  
- Metasploitable → `192.168.2.2`

### WAN
- pfSense WAN connected via **NAT** to the host machine

The Windows 10 machine is dual-homed, connecting both internal networks and simulating a potential pivot point between segmented environments.

## 📊 Network Summary
| Machine        | Interface | IP Address     | Network   |
|----------------|----------|----------------|----------|
| Kali Linux     | eth0     | 192.168.1.111  | intnet   |
| Windows 10     | Eth0     | 192.168.1.113  | intnet   |
| Windows 10     | Eth1     | 192.168.2.8    | intnet2  |
| Metasploitable | eth0     | 192.168.2.2    | intnet2  |
| pfSense        | LAN      | 192.168.1.1    | intnet   |

## 🧪 Validation Tests

### Kali Linux Configuration
Verified connectivity to the internal network:
- Interface: `eth0`  
- IP Address: `192.168.1.111`

Evidence:

<img width="603" height="372" alt="kali-ifconfig" src="https://github.com/user-attachments/assets/16c891ee-e63a-4de6-88f0-bbb19ca21c56" />

### pfSense Internet Connectivity
Tested outbound connectivity and DNS resolution:
- Command: `ping www.google.com`  
- Result: Successful responses with **0% packet loss**  
- Domain resolved to: `142.251.221.68`

This confirms:
- Proper WAN configuration
- Functional NAT
- Working DNS resolution

Evidence:

<img width="717" height="207" alt="pfsense-ping" src="https://github.com/user-attachments/assets/f678ba01-d862-4ba6-9949-9c11a82ddf6f" />

### Internal Network Connectivity (intnet2)

#### Windows 10 to Metasploitable
Evidence:

<img width="448" height="228" alt="win-ping-metasploitable" src="https://github.com/user-attachments/assets/80bb5ea8-3de3-4cf8-b416-35a8764e43ee" />

#### Metasploitable to Windows 10
Evidence:

<img width="561" height="192" alt="metasploitable-ping-win" src="https://github.com/user-attachments/assets/9f010b1e-50ec-46ab-92d2-e311f6ca0ba7" />

Successful ICMP communication verifies both systems are operating within the same subnet (192.168.2.0/24), enabling internal communication and supporting lateral movement scenarios.

## 🔍 Supporting Configuration Evidence

### pfSense Interface Configuration
Evidence:

<img width="1920" height="423" alt="pfsense-interfaces" src="https://github.com/user-attachments/assets/f8b389f6-83a0-450d-97c8-86e29e9f5f97" />

### Windows 10 Configuration
Evidence:

<img width="532" height="372" alt="win-ipconfig" src="https://github.com/user-attachments/assets/13e5511a-675e-461f-ae5b-d8f795ed9c6e" />

### Metasploitable Network Configuration
Evidence:

<img width="716" height="303" alt="metasploitable-ifconfig" src="https://github.com/user-attachments/assets/5503b4dc-bfd0-4e61-9841-8f0eeff4f15a" />

## 🔐 Security Concepts Demonstrated
- Network segmentation using multiple internal networks  
- Firewall rule configuration and traffic control using pfSense
- NAT and controlled outbound connectivity
- Risks of dual-homed systems as lateral movement pivot points  
- Isolation of vulnerable systems in a controlled lab environment

## ⚠️ Security Considerations
- Vulnerable machines are not exposed directly to the internet  
- pfSense restricts and controls traffic between WAN and internal networks  
- All systems operate within an isolated virtual lab environment
