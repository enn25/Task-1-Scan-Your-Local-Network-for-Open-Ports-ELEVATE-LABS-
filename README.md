# Task-1-Scan-Your-Local-Network-for-Open-Ports-ELEVATE-LABS-
# Network Port Scanning with Nmap

[![Security](https://img.shields.io/badge/Security-Network%20Reconnaissance-red?style=flat-square)](https://github.com)
[![Tool](https://img.shields.io/badge/Tool-Nmap-blue?style=flat-square)](https://nmap.org/)
[![OS](https://img.shields.io/badge/OS-Parrot%20Linux-green?style=flat-square)](https://parrotsec.org/)

> **Internship Task 1**: Scan Your Local Network for Open Ports.

---

## Objective

Learn to discover open ports on devices in your local network to understand network exposure.

---

## Technical Environment

| Component | Details |
|-----------|---------|
| **Operating System** | Parrot OS (Security-focused Linux distribution) |
| **Virtualization** | VirtualBox with Bridged Network Mode |
| **Network Interface** | `enp0s3` |
| **IP Configuration** | `192.168.1.73/24` |
| **Scanning Tool** | Nmap v7.94SVN |

---

## Scan Execution

### Primary Command
```bash
sudo nmap -sS 192.168.1.0/24 -oN scan_results.txt
```

**Command Breakdown:**
- `-sS`: TCP SYN stealth scan (half-open scan)
- `192.168.1.0/24`: Target network range (256 addresses)
- `-oN`: Output results in normal format to file

---

## Network Discovery Results

### Router (192.168.1.1)
| Port | State | Service | Security Assessment |
|------|-------|---------|-------------------|
| **23** | Open | Telnet | **HIGH RISK** - Unencrypted remote access |
| **53** | Open | DNS | **MEDIUM RISK** - Potential for DNS attacks |
| **80** | Open | HTTP | **MEDIUM RISK** - Unencrypted web interface |
| **443** | Open | HTTPS | **LOW RISK** - Encrypted web interface |
| **22** | Filtered | SSH | **SECURE** - Properly firewalled |

### Nintendo Device (192.168.1.71)
- **Status**: All 1000 ports filtered
- **Analysis**: Device implements strict firewall policies, silently dropping scan packets
- **Security Posture**: Excellent - No exposed attack surface

### Unknown Device (192.168.1.77)
- **Status**: All 1000 ports filtered  
- **Analysis**: Likely IoT device with embedded security controls
- **Security Posture**: Good - No accessible services detected

### Unknown Device (192.168.1.85)
- **Status**: All ports closed (TCP RST responses)
- **Analysis**: Host is responsive but no services running
- **Security Posture**: Secure baseline configuration

### Scanning Host (192.168.1.73)
- **Status**: All ports closed
- **Analysis**: Parrot OS with secure default configuration
- **Security Posture**: Hardened system with no exposed services

---

## Port State Analysis

| State | Description | Security Implication |
|-------|-------------|---------------------|
| **Open** | Service actively listening | Potential attack vector |
| **Closed** | Port reachable but no service | Minimal risk |
| **Filtered** | No response received | Firewall protection active |

---

## Security Vulnerabilities Identified

### Critical Issues

#### Telnet Service (Port 23)
- **Risk Level**: HIGH
- **Issue**: Plaintext authentication and data transmission
- **Recommendation**: Disable Telnet and use SSH (Port 22) instead
- **Exploitation Potential**: Credential interception, man-in-the-middle attacks

#### HTTP Admin Interface (Port 80)
- **Risk Level**: MEDIUM
- **Issue**: Unencrypted web management interface
- **Recommendation**: Force HTTPS redirect or disable HTTP access
- **Exploitation Potential**: Session hijacking, credential theft

#### DNS Service Exposure (Port 53)
- **Risk Level**: MEDIUM
- **Issue**: Public DNS resolver accessibility
- **Recommendation**: Restrict DNS access to internal networks only
- **Exploitation Potential**: DNS amplification attacks, cache poisoning

---

## Repository Structure

```
network-scan-analysis/
├── README.md                    # This comprehensive documentation
├── scan_results.txt             # Raw Nmap output data
├── screenshots/
    ├── ip_a.png                 # Network interface configuration
    └── nmap_scan.png            # Nmap execution output

```

---

## Screenshots
#-> ip -a
<img width="834" height="666" alt="ip-a" src="https://github.com/user-attachments/assets/3b7aed74-aaa2-4164-b76a-283eaf5e1018" />

#-> Nmap Scan
<img width="1919" height="938" alt="nmap-scan" src="https://github.com/user-attachments/assets/281adcb0-47bf-496a-b858-f15f2ce6c05b" />

#-> Wireshark Scan
<img width="1919" height="761" alt="wireshark" src="https://github.com/user-attachments/assets/43e59521-b4bf-430a-adde-0d088c6cffc5" />
