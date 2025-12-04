# Task-10-Write-a-Detailed-Security-Assessment-Report-for-a-Network-OIBSIP


# Report on Nmap Scan Conducted on the "Multillidea" Network
## Introduction

Nmap (Network Mapper) is an open‑source tool used for network discovery, security auditing, and vulnerability scanning. It helps identify open ports, running services, operating systems, and potential security weaknesses on a network or specific host.

This report provides an analysis of an Nmap scan conducted on the "Multillidea" network. The objective is to understand the network’s exposed services, detect vulnerabilities, and evaluate the overall security posture based on the scan results.

---

## Objectives of the Nmap Scan

1. **Identify open ports** on devices connected to the Multillidea network.
2. **Determine active services and versions** running on those ports.
3. **Fingerprint operating systems** and detect possible vulnerabilities.
4. **Highlight security concerns** related to exposed services.
5. **Offer recommendations** to strengthen network security.

---

## Methodology

The following Nmap techniques were used during the scan:

1. **Ping Scan (`-sn`)** – to identify live hosts on the network.
2. **Port Scan (`-sS`, `-sU`)** – to detect open TCP and UDP ports using SYN and UDP scanning techniques.
3. **Service Version Detection (`-sV`)** – to determine service type and version.
4. **OS Fingerprinting (`-O`)** – to estimate the operating system of each host.
5. **Vulnerability Scripts (`--script vuln`)** – optional scan for common vulnerabilities using Nmap Scripting Engine (NSE).

The scan was conducted under controlled conditions with proper authorization to avoid network disruption.

---

## Summary of Scan Results

### 1. **Live Hosts Detected**

The scan detected multiple active devices on the Multillidea network, including:

* User workstations
* A file server
* A router/gateway device
* IoT/Peripheral devices (e.g., printers)

This confirms stable internal network activity with several nodes online.

---

### 2. **Open Ports and Services**

Several ports were detected on different hosts. The most notable were:

#### **TCP Ports**

| Port              | Service | Observation                                                                    |
| ----------------- | ------- | ------------------------------------------------------------------------------ |
| **80/tcp**        | HTTP    | Several hosts running web services, some outdated versions.                    |
| **443/tcp**       | HTTPS   | Secure web service present; certificate validity unknown.                      |
| **21/tcp**        | FTP     | Found on a server; running without TLS support.                                |
| **22/tcp**        | SSH     | Enabled on multiple devices; versions varied.                                  |
| **139 & 445/tcp** | SMB     | File sharing enabled; may expose vulnerabilities (e.g., SMBv1).                |
| **3389/tcp**      | RDP     | Remote Desktop access found on one host; may be at risk if exposed externally. |

#### **UDP Ports**

| Port          | Service | Observation                               |
| ------------- | ------- | ----------------------------------------- |
| **53/udp**    | DNS     | Active DNS resolver; no DNSSEC indicated. |
| **67/68/udp** | DHCP    | Normal internal network behavior.         |

---

### 3. **Operating System Fingerprints**

Nmap OS detection suggested the following systems in use:

* **Windows Server 2016/2019** on the main file server
* **Windows 10/11** on client machines
* **Linux-based OS** (possibly Ubuntu or Debian) running on a local service host
* **Embedded OS** on network peripherals (printer, router)

While OS fingerprinting was mostly accurate, some devices returned "OS match uncertain," common when firewalls filter ICMP packets.

---

### 4. **Security Concerns Identified**

The Nmap scan revealed several potential vulnerabilities:

#### **1. Presence of Unsecured Services**

* **FTP running without encryption** allows credentials to be intercepted.
* **HTTP (port 80)** used by some internal hosts transmits data in plaintext.

#### **2. SMB Services Active**

* SMBv1 may be enabled on certain devices, potentially exposing the network to attacks similar to WannaCry or EternalBlue.

#### **3. Exposed RDP Service**

* RDP on port 3389 can be a high-risk entry point if not properly secured with strong passwords and firewalls.

#### **4. Outdated Services**

* Some servers reported older versions of Apache, OpenSSH, and FTP services, which may contain known vulnerabilities.

#### **5. Unnecessary Open Ports**

* Several devices had open services that did not appear to be in active use (e.g., unused web admin interfaces, open printer management pages).

---

## Key Findings

1. **Overall network is functional**, with expected services responding.
2. **Multiple hosts expose services unnecessarily**, increasing the attack surface.
3. **Several security risks** were identified, particularly related to unencrypted protocols and outdated service versions.
4. **OS detection shows a mixture of Windows and Linux devices**, with varying patch levels.
5. **No immediate evidence of intrusion**, but the exposed services could allow future attacks if unaddressed.

---

## Recommendations

### **1. Disable or Restrict Unnecessary Services**

* Close unused ports on client machines and servers.
* Disable SMBv1 entirely.

### **2. Migrate to Secure Protocols**

* Replace **FTP** with **SFTP or FTPS**.
* Enforce HTTPS and disable HTTP where possible.

### **3. Harden Remote Access**

* Protect RDP with MFA or VPN access only.
* Change default ports or block external access altogether.

### **4. Update and Patch All Systems**

* Apply security patches to Windows and Linux hosts regularly.
* Update web servers, SSH servers, and printer firmware.

### **5. Implement Network Segmentation**

* Separate critical servers from standard user devices.
* Use VLANs to isolate high‑risk or IoT devices.

### **6. Monitor for Vulnerabilities**

* Conduct regular Nmap and vulnerability scans.
* Implement intrusion detection systems (IDS/IPS).

---

## Conclusion

The Nmap scan on the Multillidea network reveals a generally stable environment but highlights multiple security concerns. Open ports, outdated services, and unencrypted protocols increase the risk of intrusion or exploitation. Implementing the recommended security measures will significantly improve the network’s resilience and reduce exposure to potential threats.

Regular scanning and network monitoring remain essential for maintaining ongoing security.
